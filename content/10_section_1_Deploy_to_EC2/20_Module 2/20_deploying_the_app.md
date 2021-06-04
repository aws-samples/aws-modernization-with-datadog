+++
title = "1.2.1 Deploying the Application with Terraform"
chapter = false
weight = 10
+++

In thtis section we are going to deploy our simple application with Terraform. It has a frontend service which consumes APIs from a discounts and ads service and pulls data from a database: ![ecommerce app diagram](/images/dd-ecommerce-app-diagram.png)


1.  With your Cloud9 editor open, navigate to **section 1**. 
2.  Double-click on the **variables.tf** file.
    1.  In the editor, you can see the variables that have been set. 
    2.  Most of the variables can be left as is, but notice the variable **owner**. It is currently set to datadogworkshop. Feel free to change that to your name (Note: if you do make any changes you will need to save the file.). We will see where that is set a little later. 
        ```
        variable "owner" {
            type    = string
            default = "datadogworkshop"
        }
        ```
    1.  Notice that many of the variables have a default value set. If you don't override them in the **apply** command or in environment variables, the default is what will take effect. 
    2.  Scroll down to the variable **ddapikey**. Now run `env` in the terminal below the editor. You will see **TF_VAR_ddapikey** which the terraform apply command will pick up and use for the variable **ddapikey**. 
3.  Double-click on the **network.tf** file.
    1.  Notice that most of the blocks in this file are AWS resources. The format here is **resource** followed by the type, such as **aws_subnet**. Then what you want to call that resource throughout the other parts of the configuration files. 
        ```
        resource "aws_subnet" "ecommerceapp-subnet" {
          vpc_id                  = aws_vpc.ecommerceapp-vpc.id
          cidr_block              = "10.0.1.0/24"
          map_public_ip_on_launch = "true"
          availability_zone = "${var.region}${var.az}"
          tags = {
            Name  = "ecommerceapp"
            Owner = var.owner
          }
        }
        ```
    2.  The one block that isn't part of the AWS provider is the data block at the top. This grabs your ip address and sets it as the only machine allowed to connect to it over ssh.
        ```
        data "http" "myip" {
          url = "http://ipv4.icanhazip.com"
          request_headers = {
            Accept = "application/text"
          }
        }
        ```
4.  Double-click on **main.tf**.
    1.  At the top of the file there is a **null_resource** that runs the command specified on the local machine (which is our Cloud9 instance). This just deletes some of the shell scripts that get created during the apply command in case you run it again. 
    2.  Then there are 4 **aws_instance**s that get created. They all use the resources created in the other files. There is also a **user_data** file that is created on the resources which is a script that is run when the instance is initialized. Notice that the template file is populated with the api key.
    3.  Double-click on **install_discounts_host.sh.tpl**. You can see on line 31 that the api key is populated here. 
5.  In the terminal below the editor, make sure you are in the **~/environment/section1** directory and then run `terraform init`.![terraform init run](/images/dd-terraform-init-run.png)

6.  Now apply with the command `terraform apply`.
7.  For both **var.clienttoken** and **var.rumappid**, just press enter to skip entering anything.
8.  Scroll up to see what terraform is going to add to your AWS account.
9.  Type `yes` to accept.
10. When the apply command completes you will see the results of the output.tf file, listing the id's for each instance as well as the command to run to ssh into each.
11. If the results of this scroll out of the buffer of the terminal and you can no longer see it, run `terraform output` to see the output again.
12. Each of the instances created rely on knowing how to reach the other instances, but there is no way to configure that until ip addresses have been assigned to all of them. So a local shell script was also created to update the hosts files on each instance. Unfortunately a mistake was made in the file so update it with this command: `sed -i '4s/ssh -o/ssh -i ecommerceapp -o/' ~/environment/section1/run.sh` (if the file has been fixed since writing this content, running the command won't break anything). 
13. Now run `./run.sh` to set the hosts files. If you see a series of **connection refused errors**, it just means the instances aren't fully up and running. It will take a few moments for the script to get access and complete.
14. Find the ssh command for the **frontend** instance. Remember, if the output of terraform is no longer on-screen, run `terraform output` to retrieve the values.
15. Now run the command labeled **ssh_to_frontend** in the terminal.
16. Change directories to /app: `cd /app`. If the directory is not there, the install is not quite complete. You will see some messages pop up on the screen showing you the current status of the install, and it may take a minute or so. 
17. Run this command to start the web frontend: `bundle exec puma --config config/puma.rb`

If you are using a personal AWS account, when you want to destroy the instances created, just run **terraform destroy** in this directory.
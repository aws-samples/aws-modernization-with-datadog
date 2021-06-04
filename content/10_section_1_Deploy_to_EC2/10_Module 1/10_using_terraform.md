+++
title = "1.1.1 Terraform Basics"
chapter = false
weight = 1
+++


 
## What is Terraform

A great answer to this question comes from the [Terraform website](https://www.terraform.io/intro/index.html): 

> Terraform is a tool for building, changing, and versioning infrastructure safely and efficiently. Terraform can manage existing and popular service providers as well as custom in-house solutions.

> Configuration files describe to Terraform the components needed to run a single application or your entire datacenter. Terraform generates an execution plan describing what it will do to reach the desired state, and then executes it to build the described infrastructure. As the configuration changes, Terraform is able to determine what changed and create incremental execution plans which can be applied.

Using terraform involves installing the tool which is a single executable, and then writing .tf files. These can be edited in any text editor. tf files are processed all at the same time, so there is no order of files and there is no magic naming of files required.

## Using Terraform

Terraform is already installed in the AmazonLinux2 instance that is backing Cloud9. It's a little bit older so the script you ran in the prerequisites section updated it with a **sudo yum install terraform** command.

When you build out a collection of tf files, run **terraform init** in that directory. 
This will look at all of your tf files and identify any additional providers you used. For example, in the files you will be looking at on the next page it will install the AWS provider. ![terraform init](/images/dd-terraform-init.png)

Running **terraform apply** in the directory will process all the files, build a resource graph, and then ask you for any variables that still need to be set. Then it will display the plan for what terraform will do. Type yes if you want to apply the changes and then and only then will terraform create or update the resources specified. 

If you make a change to the terraform files and run apply again, the changes will be applied where it can, or the resource will be destroyed and recreated with the new settings. 

When you are done with the resources, running **terraform destroy** will clean up everything you created. ![terraform destroy](/images/dd-terraform-destroy.png)

Spacing in a tf file doesn't matter, but it will make the file more readable to others. So running **terraform fmt** will clean up the look and feel of the files.

## Terraform Conventions

While there is no requirement to name files in any specific way or even to split out the configuration to multiple files, there are some files you will typically see in a set of terraform files. 

There is often a **variables.tf** file. This is where you might set variables that get reused in the rest of the project. 
![variable region](/images/dd-variable-region.png)

will set a variable called region. Then you can use it elsewhere like this: 
![provider aws region](/images/dd-provider-aws-region.png)

If you want to combine variables with other variables or text, wrap it in quotes (look at the line with availability_zone):
![aws subnet](/images/dd-aws-subnet.png)

You will often see different concerns broken out into separate files. So you will see one file for the main resources and another for network resources. 

Now let's move on to actually using these commands.
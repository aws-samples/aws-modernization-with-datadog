+++
title = "Datadog Setup"
chapter = false
weight = 40
+++



We recommend that you create a new Datadog organization for this workshop. While it is possible to use the organization created for your work, we think it is best to work with a fresh and clean environment so that you don't risk doing anything unexpected to resources that others rely on.

1. The quickest and easiest way to create a new account for Datadog for the use of this course is to visit https://labs.datadoghq.com. Then click the Login button. ![labs.datadoghq.com](/images/DD-labs-login.png). 
2. You will see a login prompt. Enter your email address and click submit. ![login](/images/dd-login-screen.png). 
3. Within a few seconds you will receive an email to that account with a verification code. ![email](/images/dd-email-verify.png).
4. Go back to your browser and enter that code ![verified](/images/dd-verified.png)
5. Click on the link on the section on the left for the **Snippet Labs**.![choose snippet](/images/dd-choose-snippet.png)
6. Choose any of the labs. We just want to access the account that it creates so the content doesn't matter. Click the Start Scenario button and wait for the scenario to start.
7. When the environment is started you will see something like this. Take note of the username and password. You are going to need it later. ![username password](/images/dd-usernamepassword.png).
8. In the terminal on labs.datadoghq.com, run the command: `env | sed -n '/DD_/s/.*/export &/p'`. You should see something like this: ![export api key](/images/dd-export-api-key.png)
9. Copy the output of that command and paste it into your Cloud9 terminal. 
10. Setup the workshop by running the following command in your Cloud9 terminal: `curl https://raw.githubusercontent.com/technovangelist/aws-datadog-workshop-sourcefiles/main/install.sh | bash`. This command performs the following activities:
    1.  Clones the source files from a GitHub repository then copies those files to the correct locations.
    2.  Updates and sets up Terraform for use in the first section.
    3.  Adds all the required environment variables to ~/.bashrc so you can create new terminals and still work with the cluster.
    4.  Installs kubectl for when we work with Kubernetes.
    5.  Creates some SSH keys.
    6.  Creates the Kops user, group, and policies. Kops is the tool used to create a Kubernetes cluster.
    7.  Creates and configures an S3 bucket for the Kops configuration
    8.  Configures the configuration file for the cluster based on the unique S3 bucket name. S3 bucket names have a single global namespace so no two buckets can have the same name.
    9.  Use Kops to create the cluster. This will create two t3.medium instances in the account. If you are running this in your personal account, these instances will charge against your account. 
    10. Add a secret to the cluster, update it, and add login information to ~/.bashrc.
    11. Set up the EC2 environment
11. Close the current terminal by clicking the **x** in the tab and then create a new terminal by clicking the **+** sign where the tab was. 
12. Change directory in the new terminal to ~/environment/section1, then run `terraform output`.
13. Copy the SSH commands and add them to your notes.
14. Run the command shown next to SSH to Frontend above
15. Change directory to **/app**. If the directory is not there yet, wait a few seconds and try again.
16. Run `bundle exec puma --config config/puma.rb`, then create another terminal by clicking the **+** sign again. If you get an error when running puma that says there is a missing gem, wait for the message that says 'all done' and try again.

If you are not running this with the AWS provided credentials and instead using your personal account, there is a **cleanup.sh** script under **~/sourcefiles/cleanup/this will delete everything/**. Only run this when you are done with the workshop. As the folder is titled, this script will delete everything created in the setup script.

If you just want to remove the cluster and the instances it runs on, run `kops delete cluster --name="$KOPSNAME" --state="$KOPS_STATE_STORE"`. To delete the EC2 instances you can run `terraform destroy -auto-approve` in the section1 directory.

Now you can move on to Section 1 of the workshop

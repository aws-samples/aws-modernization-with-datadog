+++
title = "1.2.2 Using the Application"
chapter = false
weight = 20
+++

1.  Leave the current terminal connected to the frontend open and open a new terminal by clicking the plus button to the right of the terminal tab then choose **New Terminal**. ![circleplus](/images/dd-circleplus.png).
2.  Change directories into the section1 directory: `cd ~/environment/section1`.
3.  Run `terraform output` to get the URL of the website. 
4.  Open the URL in your browser. 
5.  You may notice that nothing is loading in the browser. The terraform files were created assuming you would run it from your local machine. But we aren't doing that. The security group that was created is only allowing the Cloud9 instance to access it on port 3000.
6.  Open the **network.tf** file.
7.  Scroll down to line 75 and change the cidr_blocks field as shown:
    ```
    ingress {
      from_port   = 3000
      to_port     = 3000
      protocol    = "tcp"
      cidr_blocks = ["0.0.0.0/0"]
    }
    ```
8.  Run `terraform apply`, pressing enter twice to skip clienttoken and rumappid, then type **yes** to accept. 
9.  When terraform completes, refresh the browser that is open to port 3000.
10. If you get an error, refresh a few times and it should start working. If it still doesn't work, make sure you did the steps on the previous page with fixing the script and then running run.sh.
11. Look around the page. Refresh your browser and notice that the coupon code at the top left updates. This is being served by the discounts server. 
12. In the search box at the top right, enter `cup` to search for cups. Click on one of them. 
13. Open `app.datadoghq.com` and login using the credentials that noted in labs.datadoghq.com. 
14. Navigate to the **Service Map** under **APM**. If you don't see anything here, you may need to wait a few minutes for data to start to appear here. You should see each of the services of the application and how they are linked to each other.
15. Click on **Store Frontend** and choose to **View the Service Overview**. Scroll down the page and notice the different types of information available. 
16. Click on the **Spree::HomeController** endpoint. Click on one of the spans at the bottom of the page. You should see a flamegraph representing that particular request. 
17. Try the other options from the **Service Map**. Take a look at the other services on the map. 
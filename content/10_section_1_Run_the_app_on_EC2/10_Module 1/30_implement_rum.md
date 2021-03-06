+++
title = "1.1.3 Implementing Real User Monitoring"
chapter = false
weight = 30
+++
 

1.  Navigate to Real User Monitoring at this URL: https://app.datadoghq.com/rum. 
2.  Click the button to create a **New Application**.
3.  For **Application type**, choose JS.
4.  Enter **frontend** for the **Application Name**.
5.  Click the **Create New RUM Application** buttton. 
6.  Take note of the **applicationId** and **clientToken** strings.
7.  In the terminal that is running the puma app on the frontend, press control-c to quit puma.
8.  Edit ~/.profile. If you know vim, you can use that, otherwise nano is also installed. `nano ~/.profile`.
9.  The last two lines of the file set the DD_CLIENT_TOKEN and DD_APPLICATION_ID. Set the values using what you collected from the RUM UI. Then save the file.
10. Type `exit` to logout, and then ssh back into the host. 
11. Change directories to /app and run `bundle exec puma --config config/puma.rb`.
12. Visit the application website and do a search and add something to the shopping cart. 
13. Switch back to the RUM UI. Within a few seconds you should see the page verify the installation. ![reporting successfully](/images/dd-reporting-successfully.png)
14. Now you should be able to move on to see the session you just started. ![full waterfall](/images/dd-full-waterfall.png)

Real User Monitoring is great to see how your users are actually experiencing the website. Try visiting the application site and navigating around to a few different pages. Run a search. Then update the session in RUM to see the updated flow. 



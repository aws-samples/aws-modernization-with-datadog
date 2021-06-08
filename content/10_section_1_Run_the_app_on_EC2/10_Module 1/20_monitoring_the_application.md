+++
title = "1.1.2 Using the Application"
chapter = false
weight = 20
+++
![ecommerce app diagram](/images/dd-ecommerce-app-diagram.png)

1.  Open `app.datadoghq.com` and login using the credentials from labs.datadoghq.com that you copied to your notes. 
2.  Under Infrastructure take a look at the Host Map. Each hexagon represents a single host or instance in our environment. 
3.  Click on the hexagon that represents the database (db).
4.  Try clicking on the pill for postgres. Now we can see metrics for postgres on this instance.
5.  From the infrastructure menu, click **Processes**. We can now see the processes running in each of our instances.
6.  Click on any of the processes that you recognize and look around.
7.  Take a look at Network under Infrastructure. Here you can see the amount of network traffic traveling between our nodes.
8.  Finally take a look at the Network Map under Infrastructure. Now you can visualize those connections. Hover over each of the instances to see more detail.
9.  Navigate to the **Service Map** under **APM**. If you don't see anything here, you may need to wait a few minutes for data to start to appear here. You should see each of the services of the application and how they are linked to each other.
10. Click on **Store Frontend** and choose to **View the Service Overview**. Scroll down the page and notice the different types of information available. 
11. Click on the **Spree::HomeController** endpoint. Click on one of the spans at the bottom of the page. You should see a flamegraph representing that particular request. 
12. Try the other options from the **Service Map**. Take a look at the other services on the map.
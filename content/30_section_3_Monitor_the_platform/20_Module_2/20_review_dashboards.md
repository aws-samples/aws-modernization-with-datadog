+++
title = "3.2.2 Dashboards"
chapter = false
weight = 10
+++

1.  Login to your Datadog account and navigate to **Dashboards**. You should see a list of nearly 20 dashboards that have been auto-discovered. If you only see a few, navigate to **Integrations**, scroll down to the Kubernetes-related integrations and install them. Return to **Dashboards** and select the **Kubernetes - Overview** dashboard.
2.  At the top, you can see high level information about your cluster. 
3.  Below that and to the right are lots of different graphs and charts about the different resources you have been working with.
4.  Click on the **Running pods per node** widget. Notice the pop up menu that appears. ![running pods per node](/images/dd-running-pods-per-node.png) From here you can go straight to other related pages on Datadog. You can even copy the configuration for this widget and paste it into a new dashboard. 
5.  Find a widget with some sort of anomaly or bump on it. Click it and choose **Find correlated metrics**. Datadog will open a view to show all other metrics that experienced a similar bump at a similar time. 
6.  Since this is a built in dashboard, you cannot modify it. But click the **Clone Dashboard** button at the top and you can tweak it. 
7.  On your new cloned dashboard, click on the **Running pods per namespace** widget. Notice there is a **Custom Links** section of the menu. Click **Edit Widgets** at the top of the dashboard.
8.  Click the pencil icon on **Running pods per namespace**. Here you can tweak everything about this widget, including adding custom links and those links can include information from the graph in the query string. So you could create a link that searches Github or Jira for issues that happened at that time, or add notes about it to some other application. ![custom links](/images/dd-custom-links.png)





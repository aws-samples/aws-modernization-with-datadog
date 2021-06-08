+++
title = "3.2.1 Reviewing the Containers view"
chapter = false
weight = 1
+++

In the previous section we used **kubectl** to dig in to our Kubernetes cluster. In this section we will use some of the tools in Datadog to do some of the same things, and then take it a bit further.

1.  Using the login information you collected during the prerequisites section, login to Datadog at **https://app.datadoghq.com**.
2.  Navigate to the Infrastructure > Containers view. ![containers view.png](/images/dd-containers-view.png) From this page you can see memory vs CPU of all the containers across your Kubernetes clusters and Docker on all platforms.
3.  Click on one of the two containers for etcd-manager to see a small dashboard of that particular container.
4.  Next look at the logs for that container. If you don't see anything, change the time period from Live Tail, which will show logs as they come in to Past 12 Hours. We don't have APM enabled so nothing will show up there.
5.  Click the X at the top right and then change the **Resource** at the top left from **Containers** to **Pods**. Now we see a list of all the **Pods** that are being monitored right now. 
6.  Click on any of them and you will see the YAML that describes that pod. This is not the YAML file that started the pod, but rather the current representation of it.
7.  You saw the **Logs** and **Network** tab before, but now we also have **Processes** showing each of the processes running in that Pod. 
8.  Click on any process shown and you will open a page for that process. Note, this opens in a new tab so you never loose your place. Just close this tab when you are done.
9.  Notice that you can also switch to other resources: **Deployments**, **Replica Sets**, **Services**, and **Nodes**.
10. Under Infrastructure, there are also dedicated views for all processes as well as network.
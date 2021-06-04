+++
title = "4.2.1 Starting to Monitor the Kubernetes Workload"
chapter = false
weight = 1
+++

There are lots of places we can start to learn about our application. The Containers view is a wonderful source of information about all the containers in your environment, regardless of where they are running. They could be running in Docker, Kubernetes, EKS, EKC and anywhere else. 

1.  Navigate to https://app.datadoghq.com/containers?sort=container_name%2CASC. This shows us all the containers running in our cluster. Scroll through the list and see if you recognize some of the container names. 
2.  Click on one of the containers and try out the different options.
3.  Switch over to https://app.datadoghq.com/process. Here we see a similar view from the perspective of the actual processes that run across all of our containers. And if your EC2 version of the app is still running, those processes will be here too.
4.  Take a look at https://app.datadoghq.com/network/map. Its probably not very interesting right now. That's because we are looking at how the different hosts are talking to each other. At the top there is a drop-down labelled view. ![network view type](/images/dd-network-view-type.png) Change this to **pod_name**. This just became a lot more interesting: ![network by pod names](/images/dd-network-by-pod-names.png)


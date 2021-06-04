+++
title = "4.2.2 What's different about workloads on EC2 vs Kubernetes"
chapter = false
weight = 10
+++


In our quick look at some of the Datadog features, monitoring your workloads on Kubernetes is almost identical to monitoring workloads hosted in a VM. But there are some things that are unique about Kubernetes that you should pay attention to. 

With older clustering technologies, there was a hard requirement that all nodes must be equal: equal memory, storage, CPU, IO, and everything else. But with Kubernetes there is no such requirement. So in a cluster with 10 nodes, all of them may have slightly different configurations. The way the scheduler works is that it looks at the processor and memory requirements of the deployment, and finds a node that is capable of accommodating those requirements. 

As a result, paying attention to the key metrics of the Scheduler is very important. 

1.  From the Dashboards menu, open the **Kubernetes Scheduler - Overview** dashboard. 
1.  Scheduled Attempts at the top of the dashboard is a great one to watch. Let's update our frontend deployment to be partially unschedulable. In the editor, open **section4/frontend.yaml**.
2.  Line 41 defines the ports that the frontend should respond to. Update that block to:
    
        ports:
        - containerPort: 3000
          protocol: TCP
          hostPort: 12345
3.  Rather than just using a port on the container that is abstracted, you are telling the pod that it always needs to use port 12345 on the host.
4.  Apply frontend.yaml and you will see that everything works as expected. This is because there is only one copy of the pod being scheduled. 
5.  On line 9 of frontend.yaml is where the number of replicas is defined. Change the number 1 to a 3. Apply the yaml file. 
6.  Open the **Kubernetes Scheduler - Overview** dashboard and watch what happens. 
7.  We have two available nodes and thus two targets available for the scheduler to schedule a pod that needs port 12345 on the host. Those two pods will be scheduled and the third will be unschedulable. 

Perhaps this is a contrived example, but it is quite possible to have a deployment that requires a certain amount of memory and multiple replicas and that amount is only available on a few nodes. 

The **Kubernetes - Overview** is another important dashboard to review. It will give you a good complete picture of your cluster and identify the most cpu- and memory-intensive pods. As with most of the integration dashboards like these be sure to look into the template variables as well. You can choose to filter down by deployment and choose the frontend deployment. Now you can see all of the key metrics that affect just that one deployment. Try out some of the other options to see what is available.

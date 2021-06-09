+++
title = "2.2.6 Using Kubernetes"
chapter = false
weight = 60
+++

Let's take a look at some of the basic commands needed to work with resources on Kubernetes

1.  If you weren't able to complete the last section or the yaml file doesn't work, run this command to reset the advertisements.yaml file: `cp -i ~/sourcefiles/completedfiles/fa888fb620 ~/environment/section2/frontend.yaml;k apply -f .`
2.  One of the primary resources that you will work with is the pod. Deployments, at a high level, deploy pods. Services are the public endpoints to pods. Containers are in pods, but you don't really manage them directly. So let's get the list of all the pods on our system. `k get pods` ![k get pods.png](/images/dd-k-get-pods.png)
3.  Well, that’s not completely true. There are also pods that run in other namespaces. A namespace is a kind of fenced off area. Which ever namespace you are in is the namespace you have access to. If you want to see another namespace, just add **-n <namespace name>** to the command. Run `k get namespaces` to see a list of all the namespaces on this cluster.
4.  You can also use the **-A** option to show the chosen resource in all namespaces. So `k get pods -A` gets everything. And `k get pods -n kube-system` gets the pods in the namespace **kube-system**. Remember from earlier that we also added to .bashrc **alias ks=k -n kube-system**. So we can run `ks get pods` to do the same thing. 
5.  All of these pods run on different nodes. In our environment, we have a single **control-plane** node and a **worker** node. You can see these by running `k get nodes`.
6.  Sometimes you want to see a bit more information about a node that is running. **Describe** will do that for you. But you need to know the name of the resource first. So if we want to describe the frontend pod, we first get the name of that pod: `k get pods`. You can see it under the NAME column. Yours will be different than mine. 
7.  Then run `k describe pod <the name of the pod>`. ![k describe pod frontend.png](/images/dd-k-describe-pod-frontend.png). 
8.  Notice that the word pod is used everytime we deal with pods. A pod is one type of resource in Kubernetes. You will also see other resources like **deployments**, **ReplicaSets**, **Services**, and more. To see tthe list of all resources, run `k api-resources`.
9.  You can already see there are a lot of commands that you can use and we have barely started. To get an understanding of how to use each command, add `--help` to the end of the command. 





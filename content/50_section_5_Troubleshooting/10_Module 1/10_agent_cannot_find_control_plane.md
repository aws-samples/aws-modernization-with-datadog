+++
title = "5.1.1 - The Agent cannot find the Control Plane components"
chapter = false
weight = 1
+++


Kubernetes clusters have different origin stories. Different tools are used with various configurations resulting in clusters using different ports and file locations and more. When building out this training, the Datadog Agent could not see etcd. 

1.  The first step after bringing up the cluster and deploying the Datadog Agent using Helm was to show the agent status. To do this, figure out the name of the agent pod: `k get pods`. If you just deployed the agent, it can take a few seconds to start, so `k get pods -w` is helpful to show the progress of starting the different pods. 
2.  Once we have a name, run `k exec <full name of pod> agent status`. This resulted in a list of pods autodiscovered. etcd wasn't in this output, but sometimes it can take a few more seconds to show up. 
3.  When it still didn't show, get the name of the etcd pod: `k get pods -n kube-system`. This cluster was deployed using Kops. Kops uses etcd-manager and in this cluster there are two etcd pods, we want etcd-manager-main.
4.  Now describe the pod to see how it is configured: `k describe pod <name of etcd pod>`. 
5.  Right away something jumps out which should have been obvious when realizing its using etcd-manager. The name of the container used is etcd-manager. The Datadog agent will autodiscover etcd, but it won't autodiscover etcd-manager. You can see this in this file: https://github.com/DataDog/integrations-core/blob/master/etcd/datadog_checks/etcd/data/auto_conf.yaml. So we need to override the configuration.
6.  Continue review the output of describe. We can see in the command for etcd that the client-urls is set to use port 4001.
7.  Open  the values.yaml file  for our Helm chart. Update datadog.confd as follows:

        confd: 
          etcd.yaml: |-
            ad_identifiers:
              - etcd-manager
            instances:
              - prometheus_url: https://%%host%%:4001/metrics

8.  When you add ad_identifiers, it tells Datadog to treat this as an autodiscovery template. It will then replace %%host%% and %%port%% with the appropriate values for this container. Though there is a set of rules to remember about %%port%%; its not always what you would expect. Read more about it here: https://docs.datadoghq.com/agent/faq/template_variables/
9.  Run the Helm upgrade command on our agent and run the agent status command again. We are getting connection refused. We need the SSL certificates specified. 
10. I researched online to figure out the right certs to use and ended up with:
        
        etcd.yaml: |-
          ad_identifiers:
            - etcd-manager
          instances:
            - prometheus_url: https://%%host%%:4001/metrics
              ssl_verify: false
              use_preview: true
              ssl_cert: /keys/etcd-clients-ca.crt
              ssl_private_key: /keys/etcd-clients-ca.key

11. Run Helm upgrade again, and the agent was collecting metrics as expected from etcd. 
12. Another way to test that this is the right url and port is to run curl from the node running the pod. In this case the pod is running on the control-plane node. SSH into the node. This node was built by Kops using an Ubuntu AMI, so `ssh ubuntu@<ipaddress of master>`. To figure out the IP address, either look at your EC2 instances in the AWS console, or run `k get nodes` and then describe the node and find the external IP address. 
13. Then run `curl https://localhost:4001/metrics -k --cert /etc/kubernetes/pki/etcd-manager-main/etcd-clients-ca.crt --key /etc/kubernetes/pki/etcd-manager-main/etcd-clients-ca.key` on that host and you get the stream of current metrics.

This lab relied on kubectl but you have also seen the great tools available in Datadog to do the same thing. Instead of running kubectl describe, navigate to the Container page and click on Deployments or Pods. I find this to be faster and easier and more comprehensive than using kubectl directly.

A great resource for learning some troublehshooting workflows is this kubectl cheatsheet: https://kubernetes.io/docs/reference/kubectl/cheatsheet/
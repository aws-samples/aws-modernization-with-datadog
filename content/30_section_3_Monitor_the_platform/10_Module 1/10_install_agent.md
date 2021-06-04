+++
title = "3.1.1 - Install the Agent"
chapter = false
weight = 10
+++


In this section we are going to install the Datadog agent to our cluster. There are two main ways to install the agent, either using a series of Kubernetes YAML files, or as a Helm chart. Using helm is the easier away and the approach we will take. When using helm, there is nothing you need to download to manually install the agent beyond simply installing helm. Instead, you configure the helm chart by customizing a values yaml file. 

1.  In the IDE, open **section3/values.yaml**. Take a moment to scroll through this file. It is well documented and most items in the file should be fairly easy to understand. 
2.  Run the following command to install the Datadog agent: `helm install datadogagent datadog/datadog --set datadog.apiKey=$DD_API_KEY -f ./values.yaml`.
3.  Run `k get pods -w` to watch the pods as they start up. When the agent shows that it's running, run `k exec <name of agent pod>  agent status.
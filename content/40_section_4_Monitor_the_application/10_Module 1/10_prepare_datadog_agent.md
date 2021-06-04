+++
title = "4.1.1 - Prepare the Datadog Agent"
chapter = false
weight = 1
+++

1.  In the terminal and editor, change to section4. Upgrade your Datadog agent Helm chart with the following command: `helm upgrade datadogagent datadog/datadog --set datadog.apiKey=$DD_API_KEY -f ./values.yaml`, and then apply the changes for the application with this command: `k apply -f ./db.yaml;k apply -f ./discounts.yaml;k apply -f ./advertisements.yaml;k apply -f ./frontend.yaml`
2.  The values file that we used to upgrade the helm chart was specifically tweaked for our control plane node. Let's deploy again for the nodes: `helm install datadogagentnode datadog/datadog --set datadog.apiKey=$DD_API_KEY --set clusterAgent.enabled=false --set datadog.orchestratorExplorer.enabled=false`
3.  Now lets take a look at what has changed. 
    1.  Open the **advertisements.yaml** file in the editor.
    2.  Scroll down to **spec.template.spec.containers.env**. You can see a number of new environment variables here, including: DATADOG_SERVICE_NAME, DD_ENV, DD_AGENT_HOST, DD_LOGS_INJECTION, DD_ANALYTICS_ENABLED, DD_PROFILING_ENABLED. These environment variables are all that is needed to enabled different features like profiling, and more. 
    3.  Open the **discounts.yaml** file in the editor. 
    4.  You will find many of the same environment variables here. You will also find that we changed the command at spec.template.spec.containers.command. It is now ddtrace-run, with flask being moved to the first of the command line variables. ddtrace-run is a tool for auto instrumenting python-based applications. 
    5.  Finally open **frontend.yaml**. Not much has changed here beyond the environment variables, but we will update this later to enable **Real User Monitoring**.
4.  Remember what we had to do to figure out the URL to open to visit the frontend of our site? `k get services` will show any external IP addresses we can use and we need to add port 3000 to the end of the url. But the **frontend.yaml** file also specifies that an ELB should be created. And that takes a few minutes to start. To see the current state of the ELB, run this command: `aws elbv2 describe-load-balancers`. You will probably only see a single load balancer and you want the **State** to be **active**.

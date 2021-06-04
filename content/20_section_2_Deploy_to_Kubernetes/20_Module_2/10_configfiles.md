+++
title = "2.2.1 Understanding the configuration files"
chapter = false
weight = 1
+++

In this course we are going to build out and monitor a workload running on Kubernetes. Workloads and all the resources that make up the workload are defined in YAML files. Some of the components that are defined in YAML files include **Deployments**, **ReplicaSets**, **DemonSets**, **Services**, and more. In this first step we will look at most of the key parts of the YAML file so that the rest of this section makes more sense. 

1.  The first line of a YAML file in Kubernetes is the **apiVersion**. This is a key/value pair that defines what configuration version the API server should use when parsing the file. The current version we are using in this course is "apps/v1".
1.  Generally there isn't a required order of items in the YAML, but in our files, the next line is the '**kind**' of resource. Each of our application components are going to include a '**Deployment**'. So far, our config file looks like this:

    ```
    apiVersion: apps/v1
    kind: Deployment
    ```
1.  If you tried to deploy this right now, you would be warned that a name is required. The name is going to be included in the metadata key:

    ```
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: db
    ```
1.  Next we need to define **spec.selector**, **spec.template.metadata.labels**, and **spec.template.spec.containers**. It's not good enough just to provide the keys, you also have to assign values to them. Also each of the selectors and labels should match up with the labels under metadata. For the containers key, you need to provide an image and name. 

    ```
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: db
      labels:
        service: db
    spec:
      selector:
        matchLabels:
          service: db
      template:
        metadata:
          labels:
            service: db
        spec:
          containers:
          - image: postgres:11-alpine
            name: postgres
    ```

2.  We have labels and selectors set to **service: db** but there is no requirement that it has to be the word service. You could use **color: blue** or **muppet: kermit** or combinations of anything you like. But they need to match for Kubernetes to see that they are related. This is a fully working deployment and it will load as is, but you won't be able to do anything with it. 
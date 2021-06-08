

# Datadog workshop 

This workshop covers how to migrate a simple application from running on EC2 to running in a Kubernetes cluster on AWS, as well as monitoring the application using [Datadog](http://datadoghq.com/).
Topics covered include:
* Getting started with Kubernetes
* Deploying Kubernetes to AWS
* Using Helm to install the Datadog agent
* Monitoring Kubernetes with Datadog
* Monitoring a workload on Kubernetes with Datadog


## Building the Website

This page is built with Hugo, so you'll need it [installed](https://gohugo.io/getting-started/quick-start/#step-1-install-hugo)

First, clone this repo:

```bash
git clone git@github.com:aws-samples/aws-modernization-with-datadog.git 
```
Ensure you've also cloned the submodules:

```bash
git submodule init
git submodule update
```

Then server the website with hugo:

```bash
hugo server

```

### Learning Objectives
- Basics of running Kubernetes on EC2
- How to use Helm to install Datadog Agent
- Monitoring Kubernetes with Datadog 

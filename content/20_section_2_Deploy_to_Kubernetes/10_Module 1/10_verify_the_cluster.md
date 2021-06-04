+++
title = "2.1.1 - Verify the cluster is running"
chapter = false
weight = 1
+++


Hopefully by now the Kubernetes cluster has had enough time to start. Now we need to quickly test that everything is up and running.

1.  In the terminal, change to the section2 directory: `cd ~/environment/section2`. 
2.  Run `kops validate cluster`. You should see something like this.![validate cluster](/images/dd-validate-cluster.png)

3.  Run `kubectl get pods -n kube-system` and hopefully you will see something like this: 

        NAME                                        READY   STATUS    RESTARTS   AGE
        coredns-558bd4d5db-bpsnz                    1/1     Running   0          48m
        coredns-558bd4d5db-nrj6v                    1/1     Running   0          48m
        etcd-ip-172-31-60-234                       1/1     Running   0          49m
        heapster-86b8856788-f9ww5                   1/1     Running   0          48m
        kube-apiserver-ip-172-31-60-234             1/1     Running   0          49m
        kube-controller-manager-ip-172-31-60-234    1/1     Running   0          49m
        kube-proxy-rk5qw                            1/1     Running   0          48m
        kube-scheduler-ip-172-31-60-234             1/1     Running   0          49m
        kubernetes-dashboard-65ff5d4cc8-7cnj4       1/1     Running   0          47m
        local-volume-provisioner-2dl9q              1/1     Running   0          48m
        monitoring-grafana-ff99567f4-klcwx          1/1     Running   0          48m
        monitoring-influxdb-5cf7f5bf76-mqxpf        1/1     Running   0          48m
        nginx-ingress-controller-7d7545b56d-wmln8   1/1     Running   0          48m
        weave-net-rgrwj                             2/2     Running   0          48m

What you are looking for is a list of pods that have a status. Running is best, but any status shows us that the Kubernetes cluster is at least running.
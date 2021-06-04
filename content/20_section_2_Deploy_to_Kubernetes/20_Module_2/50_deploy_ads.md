+++
title = "2.2.5 Deploy the Ads Service"
chapter = false
weight = 40
+++

Let's continue rolling out our application to Kubernetes. Here we are going to enable the third service which is the advertisements server. 

1.  If you weren't able to complete the last section or the yaml file doesn't work, run this command to reset the files: `cp -i ~/sourcefiles/completedfiles/15f27d1a54 ~/environment/section2/db.yaml;cp -i ~/sourcefiles/completedfiles/ba34a9f273 ~/environment/section2/discounts.yaml;cp -i ~/sourcefiles/completedfiles/a4c32db14d ~/environment/section2/dbpassword.yaml`. 
2.  Apply the yaml files: `k apply -f .`
3.  Open the empty **advertisements yaml** file.
4.  Now add the following content to that yaml file: 
    
        apiVersion: apps/v1
        kind: Deployment
        metadata:
          labels:
            service: advertisements
            app: ecommerce
          name: advertisements 
        spec:
          replicas: 1
          selector:
            matchLabels:
              service: advertisements
              app: ecommerce
          strategy: {}
          template:
            metadata:
              creationTimestamp: null
              labels:
                service: advertisements
                app: ecommerce
            spec:
              containers:
              - image: ddtraining/advertisements-fixed:latest
                name: advertisements 
                command: ["flask"]
                args: ["run", "--port=5002", "--host=0.0.0.0"]
                env:
                  - name: FLASK_APP
                    value: "ads.py"
                  - name: FLASK_DEBUG
                    value: "1"
                  - name: POSTGRES_PASSWORD
                    valueFrom:
                      secretKeyRef:
                        key: pw
                        name: db-password
                  - name: POSTGRES_USER
                    value: "user"
                  - name: POSTGRES_HOST
                    value: "db"
                ports:
                - containerPort: 5002
                resources: {}
        ---
        apiVersion: v1
        kind: Service
        metadata:
          labels:
            service: advertisements
            app: ecommerce
          name: advertisements
        spec:
          ports:
          - port: 5002
            protocol: TCP
            targetPort: 5002
          selector:
            service: advertisements
            app: ecommerce
        status:
    
5.  This yaml file should look pretty familiar. We are using a different docker container image, but it's configured in exactly the same way. In fact, both discounts and advertisements are very similar Python Flask apps. We will be updating all of these files when we need to start monitoring the application.
6.  Remember how to apply all our files? `k apply -f .` 
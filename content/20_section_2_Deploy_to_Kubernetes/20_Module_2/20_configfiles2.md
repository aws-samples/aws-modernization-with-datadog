+++
title = "2.2.2 Continuing to work with the Configuration File"
chapter = false
weight = 10
+++


1.  Next let's expose the port that the user needs to access the postgres application. And if you look at the [image on DockerHub](https://hub.docker.com/_/postgres) you will see that a number of environment variables need to be defined. 

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
            ports:
              - containerPort: 5432
            env:
            - name: POSTGRES_PASSWORD
              value: "password"
            - name: POSTGRES_USER
              value: "user"  
            - name: PGDATA
              value: "/var/lib/postgresql/data/mydata"
    ```

1.  The postgres database also needs a folder to write it's data to. So we need to add **spec.containers.volumeMounts** and **spec.volumes**:

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
            ports:
              - containerPort: 5432
            env:
            - name: POSTGRES_PASSWORD
              value: "password"
            - name: POSTGRES_USER
              value: "user"  
            - name: PGDATA
              value: "/var/lib/postgresql/data/mydata"
            volumeMounts:
            - mountPath: /var/lib/postgresql/data
              name: postgresdb 
          volumes:
          - name: postgresdb
    ```

1.  This configuration is pretty close to complete. But as is, it's hard to access the postgres service. To make it easier, we need to create a **Service** so that other pods can access this one using the name **db**. A Service adds on to the Deployment, so it doesn't contain any containers. It does however need to specify ports and selectors:

    ```
    apiVersion: v1
    kind: Service
    metadata:
      labels:
        service: db 
      name: db
    spec:
      ports:
      - port: 5432
        protocol: TCP
        targetPort: 5432
      selector:
        service: db
    ```

1.  You can have multiple configurations in a single file as long as they are separated by a line with three dashes.
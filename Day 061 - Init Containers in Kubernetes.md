## Day 61 - Init Containers in Kubernetes

## Task Details:

There are some applications that need to be deployed on Kubernetes cluster and these apps have some pre-requisites where some configurations need to be changed before deploying the app container.
Some of these changes cannot be made inside the images so the DevOps team has come up with a solution to use init containers to perform these tasks during deployment. Below is a sample scenario that the team is going to test first.

- Create a `Deployment` named as `ic-deploy-datacenter`

- Configure `spec` as replicas should be `1`, labels `app` should be `ic-datacenter`, template's metadata lables app should be the same `ic-datacenter`.

- The `initContainers` should be named as `ic-msg-datacenter`, use image `debian` with `latest` tag and use command `'/bin/bash'`, `'-c'` and `'echo Init Done - Welcome to xFusionCorp Industries > /ic/news'`. The volume mount should be named as `ic-volume-datacenter` and mount path should be `/ic`.

- Main container should be named as `ic-main-datacenter`, use image `debian` with `latest` tag and use command `'/bin/bash'`, `'-c'` and `'while true; do cat /ic/news`; sleep 5; done'. The volume mount should be named as `ic-volume-datacenter` and mount path should be `/ic`

- Volume to be named as `ic-volume-datacenter` and it should be an `emptyDir` type.

## Steps:

1. Create the Deployment Manifest
    ```
    vi ic-deploy-datacenter.yaml
    ```

2. Paste the  following configuration:
    ```
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: ic-deploy-datacenter
      labels:
        app: ic-datacenter
    spec:
      replicas: 1
      selector:
        matchLabels:
          app: ic-datacenter
      template:
        metadata:
          labels:
            app: ic-datacenter
        spec:
          volumes:
          - name: ic-volume-datacenter
            emptyDir: {}
          
          initContainers:
          - name: ic-msg-datacenter
            image: debian:latest
            command: ["/bin/bash", "-c", "echo Init Done - Welcome to xFusionCorp Industries > /ic/news"]
            volumeMounts:
            - name: ic-volume-datacenter
              mountPath: /ic
              
          containers:
          - name: ic-main-datacenter
            image: debian:latest
            command: ["/bin/bash", "-c", "while true; do cat /ic/news; sleep 5; done"]
            volumeMounts:
            - name: ic-volume-datacenter
              mountPath: /ic
    ```

3. Apply the Configuration
    ```
    kubectl apply -f ic-deploy-datacenter.yaml
    ```

4. Verify the Deployment
    ```
    kubectl get deployments ic-deploy-datacenter
    ```

5. Check the Pod status:
    ```
    kubectl get pods
    ```

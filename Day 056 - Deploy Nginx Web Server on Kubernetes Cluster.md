## Day 56 - Deploy Nginx Web Server on Kubernetes Cluster

## Task Details:

Some of the Nautilus team developers are developing a static website and they want to deploy it on Kubernetes cluster. They want it to be highly available and scalable.
Therefore, based on the requirements, the DevOps team has decided to create a deployment for it with multiple replicas. Below you can find more details about it:

- Create a deployment using `nginx` image with `latest` tag only and remember to mention the tag i.e `nginx:latest`. Name it as `nginx-deployment`.
- The container should be named as `nginx-container`, also make sure replica counts are `3`.
- Create a NodePort type service named `nginx-service`. The nodePort should be `30011`

## Steps:

1. Create the deployment YAML file
    ```
    vi nginx-deployment.yaml
    ```

2. Paste the following configuration:
    ```
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: nginx-deployment
    spec:
      replicas: 3
      selector:
        matchLabels:
          app: nginx
      template:
        metadata:
          labels:
            app: nginx
        spec:
          containers:
            - name: nginx-container
              image: nginx:latest
    ---
    apiVersion: v1
    kind: Service
    metadata:
      name: nginx-service
    spec:
      type: NodePort
      selector:
        app: nginx
      ports:
        - port: 80
          targetPort: 80
          nodePort: 30011
    ```

3. Apply the deployment
    ```
    kubectl apply -f nginx-deployment.yaml
    ```

4. Verify the pods are running
    ```
    kubectl get pods
    ```

5. Verify the NodePort service
    ```
    kubectl get svc nginx-service
    ```

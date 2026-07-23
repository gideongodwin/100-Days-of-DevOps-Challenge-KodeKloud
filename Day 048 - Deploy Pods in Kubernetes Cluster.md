## Day 48 - Deploy Pods in Kubernetes Cluster

## Task Details:

The Nautilus DevOps team is diving into Kubernetes for application management. One team member has a task to create a pod according to the details below:

- Create a pod named `pod-nginx` using the `nginx` image with the `latest` tag. Ensure to specify the tag as `nginx:latest`

- Set the `app` label to `nginx_app`, and name the container as `nginx-container`

## Steps:

1. Create a new file calle `pod-nginx.yaml`
    ```
    vi pod-nginx.yaml
    ```

2. Paste the following:
    ```
    apiVersion: v1
    kind: Pod
    metadata:
      name: pod-nginx
      labels:
        app: nginx_app
    spec:
      containers:
        - name: nginx-container
          image: nginx:latest
    ```

3. Deploy the pod to the cluster:
    ```
    kubectl create -f pod-nginx.yaml
    ```

4. Check the pod status:
    ```
    kubectl get pods
    ```


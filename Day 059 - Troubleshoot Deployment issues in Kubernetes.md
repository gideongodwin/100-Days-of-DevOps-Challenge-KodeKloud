## Day 59 - Troubleshoot Deployment issues in Kubernetes

## Task Details:

Last week, the Nautilus DevOps team deployed a redis app on Kubernetes cluster, which was working fine so far.
This morning one of the team members was making some changes in this existing setup, but he made some mistakes and the app went down. We need to fix this as soon as possible. Please take a look.

- The deployment name is `redis-deployment`. The pods are not in running state right now, so please look into the issue and fix the same.

## Steps:

1. Identify the Pod Status
    ```
    kubectl get pods
    ```

2. Inspect the Pod Errors
    ```
    kubectl describe pod <redis-pod-name>
    ```
    > I notcied that the image is set to `redis:alpin` instead of `redis:alpine` and ConfigMap named `redis-conig` is missing the 'f'.

3. Edit the Deployment
    ```
    kubectl edit deployment redis-deployment
    ```

4. Search for and fix the following two lines in the text editor
    ```
    image: redis:alpin  >  image: redis:alpine
    name: redis-conig  >  name: redis-config
    ```

5. Check the Pod Status:
    ```
    kubectl get pods
    ```

## Day 51 - Execute Rolling Updates in Kubernetes

## Task Details:

An application currently running on the Kubernetes cluster employs the nginx web server. The Nautilus application development team has introduced some recent changes that need deployment

They've crafted an image `nginx:1.19` with the latest updates.

- Execute a rolling update for this application, integrating the `nginx:1.19` image. The deployment is named `nginx-deployment`

- Ensure all pods are operational post-update.

> The `kubectl` utility on the `jump-host` has been configured to work with the Kubernetes cluster.

## Steps:

1. Open the deployment
    ```
    kubectl edit deployment nginx-deployment
    ```

2. Look for the `image:` line and change it to `nginx:1.19`
    ```
    containers:
          image: nginx:1.19  # <--- Change this line
          name: nginx
    ```

3. Save and exit
    ```
    :wq
    ```

4. Verify the update
    ```
    kubectl get pods
    ```

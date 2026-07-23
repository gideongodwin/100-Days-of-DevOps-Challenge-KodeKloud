## Day 62 - Manage Secrets in Kubernetes

## Task Details:

The Nautilus DevOps team is working to deploy some tools in Kubernetes cluster. Some of the tools are licence based so that licence information needs to be stored securely within Kubernetes cluster.
Therefore, the team wants to utilize Kubernetes secrets to store those secrets. Below you can find more details about the requirements:

- We already have a secret key file `ecommerce.txt` under the `/opt/` directory. Create a generic secret named `ecommerce`, it should contain the password/license-number present in `ecommerce.txt` file.

- Also create a `pod` named `secret-datacenter`

- Configure pod's `spec` as container name should be `secret-container-datacenter`, image should be `ubuntu` with `latest` tag (remember to mention the tag with image). Use `sleep` command for container so that it remains in `running` state. Consume the created secret and mount it under `/opt/cluster` within the container.

To verify you can exec into the container `secret-container-datacenter`, to check the secret key under the mounted path `/opt/cluster`. Before hitting the Check button please make sure pod/pods are in running state, also validation can take some time to complete so keep patience.

## Steps:

1. Create the Kubernetes Secret
    ```
    kubectl create secret generic ecommerce --from-file=/opt/ecommerce.txt
    ```

2. Create the pod
    ```
    vi secret-datacenter.yaml
    ```

3. Paste the following configuration into the file:
    ```
    apiVersion: v1
    kind: Pod
    metadata:
      name: secret-datacenter
    spec:
      containers:
      - name: secret-container-datacenter
        image: ubuntu:latest
        command: ["/bin/bash", "-c", "sleep 3600"]
        volumeMounts:
        - name: secret-volume
          mountPath: "/opt/cluster"
          readOnly: true
      volumes:
      - name: secret-volume
        secret:
          secretName: ecommerce
    ```

4. Apply the Pod Manifest
    ```
    kubectl apply -f secret-pod.yaml
    ```

5. Verify the Deploymen
    ```
    kubectl get pods
    ```

6. Verify that the secret is mounted correctly under `/opt/cluster`
    ```
    kubectl exec -it secret-datacenter -c secret-container-datacenter -- ls /opt/cluster
    ```

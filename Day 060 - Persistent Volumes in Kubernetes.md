## Day 60 - Persistent Volumes in Kubernetes

## Task Details:

The Nautilus DevOps team is working on a Kubernetes template to deploy a web application on the cluster.

There are some requirements to create/use persistent volumes to store the application code, and the template needs to be designed accordingly. Please find more details below:

- Create a PersistentVolume named as `pv-datacenter`. Configure the `spec` as storage class should be `manual`, set capacity to `5Gi`, set access mode to `ReadWriteOnce`, volume type should be `hostPath` and set path to `/mnt/devops` (this directory is already created, you might not be able to access it directly, so you need not to worry about it).

- Create a PersistentVolumeClaim named as `pvc-datacenter`. Configure the `spec` as storage class should be `manual`, request `2Gi` of the storage, set access mode to `ReadWriteOnce`.

- Create a pod named as `pod-datacenter`, mount the persistent volume you created with claim name `pvc-datacenter` at document root of the web server, the container within the pod should be named as `container-datacenter` using image `nginx` with `latest` tag only (remember to mention the tag i.e `nginx:latest`).

- Create a node port type service named `web-datacenter` using node port `30008` to expose the web server running within the pod.

## Steps:

1. Create the PersistentVolume (PV)
    ```
    vi pv.yaml
    ```

2. Paste the following configuration:
    ```
    apiVersion: v1
    kind: PersistentVolume
    metadata:
      name: pv-datacenter
    spec:
      storageClassName: manual
      capacity:
        storage: 5Gi
      accessModes:
        - ReadWriteOnce
      hostPath:
        path: "/mnt/devops"
    ```

3. Create the PersistentVolumeClaim (PVC)
    ```
    vi pvc.yaml
    ```

4. Paste the following configuration:
    ```
    apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
      name: pvc-datacenter
    spec:
      storageClassName: manual
      accessModes:
        - ReadWriteOnce
      resources:
        requests:
          storage: 2Gi
    ```

5. Create the Pod
    ```
    vi pod.yaml
    ```

6. Paste the following configuration:
    ```
    apiVersion: v1
    kind: Pod
    metadata:
      name: pod-datacenter
      labels:
        app: web-app
    spec:
      containers:
        - name: container-datacenter
          image: nginx:latest
          volumeMounts:
            - name: storage-volume
              mountPath: "/usr/share/nginx/html"
      volumes:
        - name: storage-volume
          persistentVolumeClaim:
            claimName: pvc-datacenter
    ```

7. Create the NodePort Service
    ```
    vi service.yaml
    ```
8. Paste the following configuration:
    ```
    apiVersion: v1
    kind: Service
    metadata:
      name: web-datacenter
    spec:
      type: NodePort
      selector:
        app: web-app
      ports:
        - port: 80
          targetPort: 80
          nodePort: 30008
    ```

9. Apply the Configuration:
    ```
    kubectl apply -f pv.yaml
    kubectl apply -f pvc.yaml
    kubectl apply -f pod.yaml
    kubectl apply -f service.yaml
    ```

10. Verify the Persistent Volume (PV)
    ```
    kubectl get pv pv-datacenter
    ```

11. Verify the Persistent Volume Claim (PVC)
    ```
    kubectl get pvc pvc-datacenter
    ```

12. Verify the Pod Status
    ```
    kubectl get pods
    ```

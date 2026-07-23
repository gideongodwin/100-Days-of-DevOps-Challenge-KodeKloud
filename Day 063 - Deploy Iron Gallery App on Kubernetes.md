## Day 63 - Deploy Iron Gallery App on Kubernetes

## Task Details:

There is an iron gallery app that the Nautilus DevOps team was developing. They have recently customized the app and are going to deploy the same on the Kubernetes cluster. Below you can find more details:

- Create a namespace `iron-namespace-datacenter`

- Create a deployment `iron-gallery-deployment-datacenter` for `iron gallery` under the same namespace you created.

  - Labels `run` should be `iron-gallery`.
  
  - Replicas count should be `1`
  
  - Selector's matchLabels `run` should be `iron-gallery`.
  
  - Template labels `run` should be `iron-gallery` under metadata
  
  - The container should be named as `iron-gallery-container-datacenter`, use `kodekloud/irongallery:2.0` image ( use exact image name / tag ).
  
  - Resources limits for memory should be `100Mi` and for CPU should be `50m`
  
  - First volumeMount name should be `config`, its mountPath should be `/usr/share/nginx/html/data`.
  
  - Second volumeMount name should be `images`, its mountPath should be `/usr/share/nginx/html/uploads`.
  
  - First volume name should be `config` and give it `emptyDir` and second volume name should be `images`, also give it emptyDir.

- Create a deployment `iron-db-deployment-datacenter` for `iron db` under the same namespace.

  - Labels `db` should be `mariadb`.
  
  - Replicas count should be `1`.
  
  - Selector's matchLabels `db` should be mariadb.
  
  - Template labels `db` should be `mariadb` under metadata.
  
  - The container name should be `iron-db-container-datacenter`, use `kodekloud/irondb:2.0` image ( use exact image name / tag ).
  
  - Define environment, set `MYSQL_DATABASE` its value should be `database_host`, set `MYSQL_ROOT_PASSWORD` and `MYSQL_PASSWORD` value should be with some complex passwords for DB connections, and `MYSQL_USER` value should be any custom user ( except root ).
  
  - Volume mount name should be `db` and its mountPath should be `/var/lib/mysql`. Volume name should be db and give it an `emptyDir`.

- Create a service for `iron db` which should be named `iron-db-service-datacenter` under the same namespace. Configure spec as selector's db should be mariadb. Protocol should be `TCP`, port and targetPort should be `3306` and its type should be `ClusterIP`.

- Create a service for `iron gallery` which should be named `iron-gallery-service-datacenter` under the same namespace. Configure spec as selector's run should be iron-gallery. Protocol should be `TCP`, port and targetPort should be `80`, nodePort should be `32678` and its type should be `NodePort`.

## Steps:

1. Create the Namespace
    ```
    kubectl create namespace iron-namespace-datacenter
    ```

2. Create the Iron Gallery Deployment
    ```
    vi iron-gallery-deployment.yaml
    ```

3. Paste the following configuration:
    ```
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: iron-gallery-deployment-datacenter
      namespace: iron-namespace-datacenter
      labels:
        run: iron-gallery
    spec:
      replicas: 1
      selector:
        matchLabels:
          run: iron-gallery
      template:
        metadata:
          labels:
            run: iron-gallery
        spec:
          containers:
          - name: iron-gallery-container-datacenter
            image: kodekloud/irongallery:2.0
            resources:
              limits:
                memory: "100Mi"
                cpu: "50m"
            volumeMounts:
            - name: config
              mountPath: /usr/share/nginx/html/data
            - name: images
              mountPath: /usr/share/nginx/html/uploads
          volumes:
          - name: config
            emptyDir: {}
          - name: images
            emptyDir: {}
    ```

4. Apply the configuration:
    ```
    kubectl apply -f iron-gallery-deployment.yaml
    ```

5. Create the Iron DB Deployment
    ```
    vi iron-db-deployment.yaml
    ```

6. Paste the following configuration:
    ```
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: iron-db-deployment-datacenter
      namespace: iron-namespace-datacenter
      labels:
        db: mariadb
    spec:
      replicas: 1
      selector:
        matchLabels:
          db: mariadb
      template:
        metadata:
          labels:
            db: mariadb
        spec:
          containers:
          - name: iron-db-container-datacenter
            image: kodekloud/irondb:2.0
            env:
            - name: MYSQL_DATABASE
              value: database_host
            - name: MYSQL_ROOT_PASSWORD
              value: "dAtAbAsE_RoOt_P@ss_2026!"
            - name: MYSQL_USER
              value: "gallery_user"
            - name: MYSQL_PASSWORD
              value: "G@ll3ry_Us3r_P@ss_2026!"
            volumeMounts:
            - name: db
              mountPath: /var/lib/mysql
          volumes:
          - name: db
            emptyDir: {}
    ```

7. Apply the configuration:
    ```
    kubectl apply -f iron-db-deployment.yaml
    ```

8. Create the Iron DB Service
   ```
   vi iron-db-service.yaml
   ```

9. Paste the following configuration:
   ```
       apiVersion: v1
    kind: Service
    metadata:
      name: iron-db-service-datacenter
      namespace: iron-namespace-datacenter
    spec:
      type: ClusterIP
      selector:
        db: mariadb
      ports:
      - protocol: TCP
        port: 3306
        targetPort: 3306
   ```

10. Apply the configuration:
    ```
    kubectl apply -f iron-db-service.yaml
    ```

11. Create the Iron Gallery Service
    ```
    vi iron-gallery-service.yaml
    ```

12. Paste the following configuration:
    ```
    apiVersion: v1
    kind: Service
    metadata:
      name: iron-gallery-service-datacenter
      namespace: iron-namespace-datacenter
    spec:
      type: NodePort
      selector:
        run: iron-gallery
      ports:
      - protocol: TCP
        port: 80
        targetPort: 80
        nodePort: 32678
    ```

13. Apply the configuration:
    ```
    kubectl apply -f iron-gallery-service.yaml
    ```

14. Check the deployments:
    ```
    kubectl get pods -n iron-namespace-datacenter
    ```

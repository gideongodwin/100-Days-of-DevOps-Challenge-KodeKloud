<img width="818" height="461" alt="image" src="https://github.com/user-attachments/assets/d13d74c9-daf1-447b-b473-4225f1f96342" />## Day 64 - Fix Python App Deployed on Kubernetes Cluster

## Task Details:

One of the DevOps engineers was trying to deploy a python app on Kubernetes cluster. Unfortunately, due to some mis-configuration, the application is not coming up.

Please take a look into it and fix the issues. Application should be accessible on the specified `nodePort`.

The deployment name is `python-deployment-datacenter`, its using `poroko/flask-demo-app` image. The deployment and service of this app is already deployed.

`nodePort` should be `32345` and `targetPort` should be python flask app's default port.

## Steps:

1. Check configuration errors 
    ```
    kubectl describe deployment python-deployment-datacenter
    ```

2. Fix the configuration errors in the deployment
    ```
    kubectl edit deployment python-deployment-datacenter
    ```

3. Change the image name from `poroko/flask-app-demo` to `poroko/flask-demo-app`
    ```
        spec:
          containers:
          - image: poroko/flask-demo-app  # <--- Change this line
            imagePullPolicy: Always
            name: python-container-datacenter
            ports:
            - containerPort: 5000
              protocol: TCP
    ```

4. View the current service
    ```
    kubectl get svc
    ```

5. Edit the current service
    ```
    kubectl edit svc <your-service-name>
    ```

6. Add the following:
    ```
    spec:
      type: NodePort
      ports:
      - nodePort: 32345
        port: 5000
        targetPort: 5000
    ```

7. Verify the pod status changes to `'Running'`
    ```
    kubectl get pods -l app=python_app
    ```

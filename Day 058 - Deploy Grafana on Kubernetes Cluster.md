## Day 58 - Deploy Grafana on Kubernetes Cluster

##  Task Details:

The Nautilus DevOps teams is planning to set up a Grafana tool to collect and analyze analytics from some applications. They are planning to deploy it on Kubernetes cluster. Below you can find more details.

- Create a deployment named `grafana-deployment-nautilus` using any grafana image for Grafana app. Set other parameters as per your choice.

- Create `NodePort` type service with nodePort `32000` to expose the app.

> You do not need to make any configuration changes inside the Grafana app once deployed; just make sure you can access the Grafana login page.

## Steps: 

1. Create the `grafana.yaml` file
    ```
    vi grafana.yaml
    ```

2. Paste the following configuration into the file:
    ```
    ---
    # 1. Grafana Deployment Configuration
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: grafana-deployment-nautilus
      labels:
        app: grafana
    spec:
      replicas: 1
      selector:
        matchLabels:
          app: grafana
      template:
        metadata:
          labels:
            app: grafana
        spec:
          containers:
          - name: grafana
            image: grafana/grafana:latest
            ports:
            - containerPort: 3000 # Default Grafana port
    
    ---
    # 2. Grafana Service Configuration
    apiVersion: v1
    kind: Service
    metadata:
      name: grafana-service-nautilus
    spec:
      type: NodePort
      selector:
        app: grafana # Matches the label in the deployment
      ports:
        - port: 3000
          targetPort: 3000
          nodePort: 32000 # Required explicit NodePort
    ```

3. Apply the Configuration
    ```
    kubectl apply -f grafana.yaml
    ```

4. Verify the Deployment
    ```
    kubectl get deployments
    ```

5. Verify that the service has been created
    ```
    kubectl get service grafana-service-nautilus
    ```

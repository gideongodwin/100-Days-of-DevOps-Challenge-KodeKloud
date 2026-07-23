## Day 57 - Print Environment Variables

## Task Details:

The Nautilus DevOps team is working on to setup some pre-requisites for an application that will send the greetings to different users.
There is a sample deployment, that needs to be tested. Below is a scenario which needs to be configured on Kubernetes cluster.
Please find below more details about it.


- Create a `pod` named `print-envars-greeting`

- Configure spec as, the container name should be `print-env-container` and use `bash` image.

- Create three environment variables:

    -  `GREETING` and its value should be `Welcome to`
    
    -  `COMPANY` and its value should be `Stratos`
    
    -  `GROUP` and its value should be `Datacenter`

- Use command `["/bin/sh", "-c", 'echo "$(GREETING) $(COMPANY) $(GROUP)"']` (please use this exact command), also set its `restartPolicy` policy to `Never` to avoid crash loop back.

You can check the output using `kubectl logs -f print-envars-greeting` command.

## Steps:

1. Create the `pod.yaml` file
    ```
    vi pod.yaml
    ```

2. Paste the following configuration:
    ```
    apiVersion: v1
    kind: Pod
    metadata:
      name: print-envars-greeting
    spec:
      restartPolicy: Never
      containers:
      - name: print-env-container
        image: bash
        command: ["/bin/sh", "-c", 'echo "$(GREETING) $(COMPANY) $(GROUP)"']
        env:
        - name: GREETING
          value: "Welcome to"
        - name: COMPANY
          value: "Stratos"
        - name: GROUP
          value: "Datacenter"
    ```

3. Apply the Configuration
    ```
    kubectl apply -f pod.yaml
    ```

4.  Verify pod status
    ```
    kubectl get pods
    ```

5. Check the Output Logs
    ```
    kubectl logs -f print-envars-greeting
    ```

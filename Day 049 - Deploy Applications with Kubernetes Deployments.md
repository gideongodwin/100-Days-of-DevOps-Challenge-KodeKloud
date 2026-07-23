## Day 49: Deploy Applications with Kubernetes Deployments

## Task Details:

The Nautilus DevOps team is delving into Kubernetes for app management. One team member needs to create a deployment following these details:

- Create a deployment named `httpd` to deploy the application `httpd` using the image `httpd:latest` (ensure to specify the tag)

> The `kubectl` utility on the `jump-host` has been configured to work with the Kubernetes cluster.

## Steps:

1. Create the Deployment
    ```
    kubectl create deployment httpd --image=httpd:latest
    ```

2. Check deployment status
    ```
    kubectl get deployments
    ```

## Day 36 - Deploy Nginx Container on Application Server

## Task Details:

The Nautilus DevOps team is conducting application deployment tests on selected application servers. They require a nginx container deployment on `Application Server 3`
Complete the task with the following instructions:

- On `Application Server 3` create a container named `nginx_3` using the `nginx` image with the `alpine` tag. Ensure container is in a `running` state.

## Steps:

1. SSH into Application Server 3
    ```
    ssh banner@stapp03
    ```

2. Check if there are any existing containers
    ```
    docker ps -a
    ```

3. Deploy the Nginx Container
    ```
    docker run -d --name nginx_3 nginx:alpine
    ```

4. Verify the Deployment
    ```
    docker ps
    ```

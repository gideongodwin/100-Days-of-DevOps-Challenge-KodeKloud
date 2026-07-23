## Day 43 - Docker Ports Mapping

## Task Details:

The Nautilus DevOps team is planning to host an application on a nginx-based container. There are number of tickets already been created for similar tasks.

One of the tickets has been assigned to set up a nginx container on `Application Server 3` in `Stratos Datacenter`. Please perform the task as per details mentioned below:

- Pull `nginx:alpine-perl` docker image on `Application Server 3`

- Create a container named `blog` using the image you pulled.

- Map host port `5001` to container port `80` Please keep the container in running state.

## Steps:

1. SSH into Application Server 3
    ```
    ssh banner@stapp03
    ```

2. Pull the Docker Image
    ```
    docker pull nginx:alpine-perl
    ```

3. Run the Docker Container
    ```
    docker run -d --name blog -p 5001:80 nginx:alpine-perl
    ```

4. Verify the Deployment
    ```
    docker ps
    ```

5. Send a curl request to the host port to verify Nginx is serving traffic
    ```
    curl http://localhost:5001
    ```

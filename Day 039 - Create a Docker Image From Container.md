## Day 39 - Create a Docker Image From Container

## Task Details:

One of the Nautilus developer was working to test new changes on a container. He wants to keep a backup of his changes to the container. A new request has been raised for the DevOps team to create a new image from this container. Below are more details about it:

- Create an image `cluster:datacenter` on `Application Server 2` from a container `ubuntu_latest` that is running on same server.

## Steps:

1. Connect to Application Server 2
    ```
    ssh steve@stapp02
    ```

2. Verify the Source Container
    ```
    docker ps
    ```

3. Commit the Changes to a New Image
    ```
    docker commit ubuntu_latest cluster:datacenter
    ```

4. Confirm the New Image Exists
    ```
    docker images
    ```

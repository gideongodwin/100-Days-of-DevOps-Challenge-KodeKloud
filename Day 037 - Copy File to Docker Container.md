## Day 37 - Copy File to Docker Container

## Task Details:

The Nautilus DevOps team possesses confidential data on `App Server 1` in the `Stratos Datacenter`. A container named `ubuntu_latest` is running on the same server.

- Copy an encrypted file `/tmp/nautilus.txt.gpg` from the docker host to the `ubuntu_latest` container located at `/opt/` Ensure the file is not modified during this operation.

## Steps:

1. Access the Application Server
    ```
    ssh tony@stapp01
    ```

2. Verify that the target container
    ```
    docker ps -a
    ```

3. Locate the Source File
    ```
    ls -l /tmp/nautilus.txt.gpg
    ```

4. Copy the File to the Container
    ```
    docker cp /tmp/nautilus.txt.gpg ubuntu_latest:/opt/
    ```

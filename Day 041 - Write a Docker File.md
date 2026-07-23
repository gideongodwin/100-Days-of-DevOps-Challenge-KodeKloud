## Day 41 - Write a Docker File

## Task Details:
As per recent requirements shared by the Nautilus application development team, they need custom images created for one of their projects.
Several of the initial testing requirements are already been shared with DevOps team. Therefore, create a docker file `/opt/docker/Dockerfile` (please keep `D` capital of Dockerfile) on `App server 1` in `Stratos DC` and configure to build an image with the following requirements:

- Use `ubuntu:24.04` as the base image.

- Install `apache2` and configure it to work on `6100` port. (do not update any other Apache configuration settings like document root etc).

## Steps:

1. Log in to App Server 1
    ```
    ssh tony@stapp01
    ```

2. Go to the directory
    ```
    cd /opt/docker/
    ```

3. Create the file
    ```
    sudo vi Dockerfile
    ```

4. Add the Dockerfile Configuration
    ```
    FROM ubuntu:24.04
    
    RUN apt-get update && \
        apt-get install -y apache2
    
    RUN sed -i 's/Listen 80/Listen 6100/g' /etc/apache2/ports.conf
    
    
    EXPOSE 6100
    
    CMD ["apache2ctl", "-D", "FOREGROUND"]
    ```

5. Build the Image
    ```
    docker build . -t apache2
    ```

6. Verify
    ```
    docker run --rm apache2 cat /etc/apache2/ports.conf | grep Listen
    ```

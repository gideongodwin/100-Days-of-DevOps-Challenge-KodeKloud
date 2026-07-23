## Day 44 - Write a Docker Compose File

## Task Details:

The Nautilus application development team shared static website content that needs to be hosted on the httpd web server using a containerised platform.

The team has shared details with the DevOps team, and we need to set up an environment according to those guidelines. Below are the details:

- On `App Server 2` in `Stratos DC` create a container named `httpd` using a docker compose file `/opt/docker/docker-compose.yml` (please use the exact name for file).

- Use `httpd` (preferably `latest` tag) image for container and make sure container is named as `httpd` you can use any name for service.

- Map `80` number port of container with port 6400 of docker host.

- Map container's `/usr/local/apache2/htdocs` volume with `/opt/finance` volume of docker host which is already there. (please do not modify any data within these locations).

## Steps:

1. SSH into App Server 2
    ```
    ssh steve@stapp02
    ```

2. Go to the directory
    ```
    cd /opt/docker/
    ```

3. Open the the `docker-compose.yml` file
    ```
    sudo vi /opt/docker/docker-compose.yml
    ```

4. Paste the following configuration into the file:
    ```
    services:
      web_service:
        image: httpd:latest
        container_name: httpd
        ports:
          - "6400:80"
        volumes:
          - /opt/finance:/usr/local/apache2/htdocs
    ```

5. Deploy the container
    ```
    docker-compose up -d
    ```

6. Verify the deployment
    ```
    docker ps
    ```

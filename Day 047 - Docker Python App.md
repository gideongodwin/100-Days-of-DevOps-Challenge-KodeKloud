## Day 47 - Docker Python App

## Task Details:

A python app needed to be Dockerized, and then it needs to be deployed on `App Server 2`

We have already copied a `requirements.txt` file (having the app dependencies) under `/python_app/src/` directory on App Server 2. Further complete this task as per details mentioned below:

Create a Dockerfile under `c` directory:

Use any `python` image as the base image.

Install the dependencies using `requirements.txt` file

Expose the port `6400`

Run the `server.py` script using `CMD`

Build an image named `nautilus/python-app` using this Dockerfile

Once image is built, create a container named `pythonapp_nautilus`

Map port `6400` of the container to the host port `8092`

Once deployed, you can test the app using curl command on App Server 2 `curl http://localhost:8092/`

## Steps:

1. SSH into App Server 2
    ```
    ssh steve@stapp02
    ```

2. Go to the directory
    ```
    cd /python_app
    ```

3. Edit the Dockerfile
    ```
    sudo vi Dockerfile
    ```

4. Paste the following
    ```
    FROM python:latest
    
    WORKDIR /python_app
    
    COPY src/requirements.txt .
    
    RUN pip install --no-cache-dir -r requirements.txt
    
    COPY src/ .
    
    EXPOSE 6400
    
    CMD ["python", "server.py"]
    ```

5. Build the Docker Image
    ```
    docker build -t nautilus/python-app .
    ```

6. Run the container
    ```
    docker run -d --name pythonapp_nautilus -p 8092:6400 nautilus/python-app
    ```

7. Check that your container is running
    ```
    docker ps
    ```

8. Test that the application
    ```
    curl http://localhost:8092/
    ```

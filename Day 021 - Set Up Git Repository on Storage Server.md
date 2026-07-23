## Day 21 - Set Up Git Repository on Storage Server

## Task Details

The Nautilus development team has provided requirements to the DevOps team for a new application development project, specifically requesting the establishment of a Git repository. 
Follow the instructions below to create the Git repository on the `Storage server` in the Stratos DC:

- Utilize `yum` to install the `git` package on the Storage Server

- Create a bare repository named `/opt/official.git` (ensure exact name usage)

## Steps:

1. SSH into the Storage Server and switch to root user
    ```
    ssh natasha@ststor01
    sudo -i
    ```

2. Install Git using `yum`
    ```
    yum install git -y
    ```

3. Create a Bare Git Repository
    ```
    cd /opt/
    git init --bare official.git
    ```

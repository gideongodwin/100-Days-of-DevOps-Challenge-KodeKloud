## Day 22 - Clone Git Repository on Storage Server

## Task Details:

The DevOps team established a new Git repository last week, which remains unused at present. However, the Nautilus application development team now requires a copy of this repository on the `Storage Server` in the Stratos DC.
Follow the provided details to clone the repository:

- The repository to be cloned is located at `/opt/media.git`

- Clone this Git repository to the `/usr/src/kodekloudrepos` directory. Perform this task using the `natasha` user, and ensure that no modifications are made to the repository or existing directories, such as changing permissions or making unauthorized alterations.

## Steps: 

1. SSH into the Storage Server
    ```
    ssh natasha@ststor01
    ```

2. Navigate to the target directory
    ```
    cd /usr/src/kodekloudrepos
    ```

3. Clone the repository
    ```
    git clone /opt/media.git
    ```

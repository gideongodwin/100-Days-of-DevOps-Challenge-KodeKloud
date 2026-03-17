## Day 1 - Linux User Setup with Non-Interactive Shell

## Task Details 
Create a user named `jim` with a non-interactive shell on `App Server 1`

## Steps:

1. Log into the app server and switch to root user
    ```
    ssh tony@stapp01
    sudo -i
    ```
    > When prompted, enter the password for user `tony`
  
2. Create the user with a non-interactive shell
    ```
    useradd jim --shell /sbin/nologin
    ```
     

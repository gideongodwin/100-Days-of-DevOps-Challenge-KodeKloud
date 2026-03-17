## Day 1 - Linux User Setup with Non-Interactive Shell

### Task Details 
To accommodate the backup agent tool's specifications, the system admin team at `xFusionCorp` Industries requires the creation of a user with a non-interactive shell. Here's your task:
Create a user named `jim` with a non-interactive shell on `App Server 1`

### STEPS:
1. Log in to the app server and switch to root user
    ```
    ssh tony@stapp01
    sudo -i
    ```
    > When prompted, enter the password for user `tony`
  
2. Create the User with a Non-Interactive Shell
    ```
    useradd jim --shell /sbin/nologin
    ```
     

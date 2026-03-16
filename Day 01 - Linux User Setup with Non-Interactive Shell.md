## Day 1 - Linux User Setup with Non-Interactive Shell

#### Task Details 
To accommodate the backup agent tool's specifications, the system admin team at `xFusionCorp` Industries requires the creation of a user with a non-interactive shell. Here's your task:
Create a user named `jim` with a non-interactive shell on `App Server 1`

#### STEPS:
1. Connect to App Server
  `ssh tony@stapp01` \
- When prompted, enter the password for user `tony`
  
2. After signing in, switch to the root user:
   `sudo su -` \
- Enter the password when prompted.

3. Create the User with a Non-Interactive Shell
  `useradd jim --shell /sbin/nologin`

 

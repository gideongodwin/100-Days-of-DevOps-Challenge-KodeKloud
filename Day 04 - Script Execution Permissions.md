## Day 4 - Script Execution Permissions

## Task Details:

- Grant executable permissions to the `/tmp/xfusioncorp.sh` script on `App Server 1`

- Ensure that all users have the capability to execute it.

## Steps: 

1. SSH into the app server and switch to root user
    ```
    ssh tony@stapp01
    sudo -i
    ```
    > When prompted, enter the password for user `tony`

2. Check the existing permissions of the script
   ```
   ls -l /tmp/xfusioncorp.sh
   ```

3. Grant Execute Permission to All Users
   ```
   chmod a+rx /tmp/xfusioncorp.sh
   ```

4. Verify that the script is now executable
   ```
   ls -l /tmp/xfusioncorp.sh
   ```

5. Exit the server
   ```
   exit
   ```

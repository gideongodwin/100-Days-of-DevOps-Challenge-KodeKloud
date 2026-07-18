## Day 3 - Secure Root SSH Access

## Task Details:

- Disable direct SSH root login on all app servers within the `Stratos Datacenter`

## Steps:

1. SSH into the first app server and switch to root user
    ```
    ssh tony@stapp01
    sudo -i
    ```
    > When prompted, enter the password for user `tony`

2. Open the SSH configuration file and modify the root login setting
   ```
   vi /etc/ssh/sshd_config
   ```

3. Find the line: PermitRootLogin `yes`Change it to: PermitRootLogin `no`
  
4. Save the File
    ```
    :wq
    ```

5. Restart the SSH Service
    ```
    systemctl restart sshd
    ```
6. Exit the server `stapp01`
    ```
    exit
    ```
7. Test the Change
    ```
    ssh tony@stapp01
    ```
    > You should get: Permission denied

8. Repeat steps 1 to 7 for the remaining servers
   

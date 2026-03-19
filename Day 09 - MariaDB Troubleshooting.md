## Day 9: MariaDB Troubleshooting

## Task Details:
There is a critical issue going on with the `Nautilus` application in `Stratos DC` The production support team identified that the application is unable to connect to the database. After digging into the issue, the team found that mariadb service is down on the database server.
Look into the issue and fix the same.

## Steps:

1. SSH into the Database Server
   ```
   ssh peter@stdb01
   sudo -i
   ```

2. Verify whether the MariaDB service is running
   ```
   systemctl status mariadb
   ```

3. Inspect the MariaDB data directory
   ```
   ls -l /var/lib
   ```
   
4. Correct the Ownership of the MariaDB Data Directory
   ```
   chown -R mysql:mysql /var/lib/mysql
   ```

5. Confirm that the ownership has been corrected
   ```
   ls -l /var/lib
   ```
   
6. Start the MariaDB Service
   ```
   systemctl start mariadb
   ```

7. Verify MariaDB is Running
   ```
   systemctl status mariadb
   ```   

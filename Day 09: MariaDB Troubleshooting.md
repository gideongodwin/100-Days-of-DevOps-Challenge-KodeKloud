## Day 9: MariaDB Troubleshooting

#### TASK DETAILS:
There is a critical issue going on with the `Nautilus` application in `Stratos DC` The production support team identified that the application is unable to connect to the database. After digging into the issue, the team found that mariadb service is down on the database server.
Look into the issue and fix the same.

#### STEPS:
1. SSH into the Database Server \
   `ssh peter@stdb01`

2. Switch to root user \
  `sudo -i`

3. Verify whether the MariaDB service is running \
   `systemctl status mariadb`

4. Inspect the MariaDB data directory \
   `ls -l /var/lib`

5. Correct the Ownership of the MariaDB Data Directory \
   `chown -R mysql:mysql /var/lib/mysql`

6. Confirm that the ownership has been corrected  \
   `ls -l /var/lib`

7. Start the MariaDB Service \
  `systemctl start mariadb`

8. Verify MariaDB is Running \
  `systemctl status mariadb`
   

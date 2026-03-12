## Day 10: Linux Bash Scripts

#### Task Details:
The production support team of xFusionCorp Industries is working on developing some bash scripts to automate different day to day tasks. One is to create a bash script for taking websites backup. They have a static website running on App Server 2 in Stratos Datacenter, and they need to create a bash script named beta_backup.sh which should accomplish the following tasks. (Also remember to place the script under /scripts directory on App Server 2).
   - Create a zip archive named xfusioncorp_beta.zip of /var/www/html/beta directory.
   - Save the archive in /backup/ on App Server 2. This is a temporary storage, as backups from this location will be cleaned on a weekly basis. Therefore, we also need to save this backup archive on Nautilus Storage Server.
   - Copy the created archive to Nautilus Storage Server server in /backup/ location.
   - Please make sure script won't ask for password while copying the archive file. Additionally, the respective server user (for example, tony in case of App Server 1) must be able to run it.
- Do not use sudo inside the script.
   Note:
The zip package must be installed on given App Server before executing the script. This package is essential for creating the zip archive of the website files. Install it manually outside the script.

#### STEPS:
1. Connect to App Server 2 \
   `ssh steve@stapp02`

2. Install the zip Package outside the script \
   `sudo yum install zip -y`

3. Navigate to the `/scripts` directory and create the script file \
   `vi /scripts/beta_backup.sh`

4. Inside the file, add the following script:
   ```
   #!/bin/bash
   echo "creating the zip archive"
   zip -r xfusioncorp_beta.zip /var/www/html/beta

   mv xfusioncorp_beta.zip /backup/
   echo "copying zip archive to backup server"
   scp /backup/xfusioncorp_beta.zip clint@ststor01:/backup/
   
5. Make the Script Executable \
   `chmod +x /scripts/beta_backup.sh`

6. Configure Passwordless SSH Authentication \
   `ssh-keygen`

7.  Copy the SSH key to the Storage Server \
   `ssh-copy-id -i ~/.ssh/id_ed25519.pub clint@ststor01`

8. Execute the script to perform the backup \
   `/scripts/beta_backup.sh`

9. Verify Backup Creation \
    `ls -l /backup/`


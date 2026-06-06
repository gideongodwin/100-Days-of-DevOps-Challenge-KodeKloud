## Day 74 - Jenkins Database Backup Job

## Task Details:

There is a requirement to create a Jenkins job to automate the database backup. Below you can find more details to accomplish this task:



Click on the Jenkins button on the top bar to access the Jenkins UI. Login using username admin and password Adm!n321.


Create a Jenkins job named database-backup.


Configure it to take a database dump of the kodekloud_db01 database present on the App server (stapp01) in Stratos Datacenter, the database user is kodekloud_roy and password is asdfgdsd.


The dump should be named in db_$(date +%F).sql format, where date +%F is the current date.

Copy the db_$(date +%F).sql dump to the Storage server (ststor01) under location /home/natasha/db_backups.


Further, schedule this job to run periodically at */10 * * * * (please use this exact schedule format).

## Steps:

1. Click on the Jenkins button on the top bar to access the `Jenkins UI`

2. Enter the provided credentials

    <img width="990" height="389" alt="Screenshot 2026-06-01 155715" src="https://github.com/user-attachments/assets/319328d1-c9b0-4992-9797-8e87da5dca61" />

3. On the Jenkins dashboard, click New Item.

4. Name the job `database-backup` > select Freestyle project > click OK
    
    <img width="960" height="437" alt="Screenshot 2026-06-06 162200" src="https://github.com/user-attachments/assets/d4c25301-778c-4580-9148-1699d8cb11dc" />

5. On the Build Triggers section > Check the box labeled `Build periodically`

6. In the Schedule text box, enter the exact format required to run the job every 10 minutes:
    ```
    */10 * * * *
    ```

   <img width="906" height="435" alt="Screenshot 2026-06-06 162425" src="https://github.com/user-attachments/assets/e0395e40-7be1-47c2-8192-381c57f0851d" />

7. On to the Build Steps section > Click Add build step and select Execute shell.

   <img width="941" height="314" alt="Screenshot 2026-06-04 155400" src="https://github.com/user-attachments/assets/5157b90a-984d-4f56-a053-0e2f21cc34b1" />

8. Paste the following shell script into the Command box:
    ```
    #!/bin/bash
    
    BACKUP_FILE="db_$(date +%F).sql"
    
    sshpass -p 'Ir0nM@n' ssh -o StrictHostKeyChecking=no tony@stapp01 "mysqldump -u kodekloud_roy -pasdfgdsd kodekloud_db01" > /tmp/$BACKUP_FILE
    
    sshpass -p 'Bl@kW' scp -o StrictHostKeyChecking=no /tmp/$BACKUP_FILE natasha@ststor01:/home/natasha/db_backups/
    ```

9. On the `database-backup` job page, click Build Now.

    <img width="342" height="496" alt="Screenshot 2026-06-06 162650" src="https://github.com/user-attachments/assets/08ba732a-4348-43c3-a51a-4f6c2b8404e6" />

10. Click on the build number > Open the console output.

    
    <img width="923" height="366" alt="Screenshot 2026-06-06 162708" src="https://github.com/user-attachments/assets/8f849413-402d-48fb-9a76-0dbdd96e0013" />






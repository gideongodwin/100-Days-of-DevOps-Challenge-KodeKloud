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

5. Scroll down to the Build Triggers section.

Check the box labeled Build periodically.

In the Schedule text box that appears, enter the exact format required to run the job every 10 minutes:



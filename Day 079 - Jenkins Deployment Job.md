## Day 79 - Jenkins Deployment Job

## Task Details

The Nautilus development team had a meeting with the DevOps team where they discussed automating the deployment of one of their apps using Jenkins (the one in Stratos Datacenter). They want to auto deploy the new changes in case any developer pushes to the repository. As per the requirements mentioned below configure the required Jenkins job.

Click on the Jenkins button on the top bar to access the Jenkins UI. Login using username admin and Adm!n321 password.

Similarly, you can access the `Gitea` UI using Gitea button. Username and password for Git are `sarah` and `Sarah_pass123`. Under user sarah you will find a repository named web that is already cloned on `App Server 1` under sarah's home `(/home/sarah/web)`. sarah is a developer who is working on this repository.


1. `httpd` is already installed and configured on the app server (listening on port `8080`). Ensure the httpd service is running on App Server 1 (e.g. start it manually if needed). You can make starting/restarting httpd part of your Jenkins job if you prefer.

2. Create a Jenkins job named `datacenter-app-deployment` and configure it so that if anyone pushes any new change to the `origin` repository in `master` branch, the job should auto build and deploy the latest code on `App Server 1` under `/var/www/html` directory.

Before deployment, ensure that the ownership of the /var/www/html directory is set to user sarah, so that Jenkins can successfully deploy files to that directory.

3. SSH into App Server 1 using `sarah` user credentials mentioned above. Under sarah user's home (/home/sarah/web) you will find a cloned Git repository named `web`. Under this repository there is an `index.html` file, update its content to `Welcome to the xFusionCorp Industries`, then push the changes to the origin into master branch. This push must trigger your Jenkins job and the latest changes must be deployed on the server, also make sure it deploys the entire repository content not only index.html file.

## Steps:

1. SSH into `App Server 1` (usually hostname stapp01) using `Sarah's` credentials
    ```
    ssh sarah@stapp01
    ```

2. Change the ownership of the `web` directory so Jenkins can write to it as `sarah`
   ```
   sudo chown -R sarah:sarah /var/www/html
   ```

3. Confirm the `httpd` service is still running
    ```
    systemctl status httpd
    ```

4. Click on the Jenkins button on the top bar to access the Jenkins UI

5. Enter the provided credentials

   <img width="990" height="389" alt="Screenshot 2026-06-01 155715" src="https://github.com/user-attachments/assets/b3390900-64a4-4631-a4c4-f5447b5f88ae" />

6. Click on Manage Jenkins > Under the System Configuration section, Plugins

7. Click Available plugins, search for Git and Credentials Plugins, then install

   <img width="906" height="425" alt="Screenshot 2026-06-28 121203" src="https://github.com/user-attachments/assets/5b065f37-acec-4260-b0c7-81532e7b2c66" />

8. Go back to Manage Jenkins > Credentials > Add Credential

9. Select Username with Password > Configure the following

    <img width="561" height="685" alt="Screenshot 2026-06-28 121910" src="https://github.com/user-attachments/assets/10d9ade1-ff2d-4358-8e80-4b1c3f7e8535" />

10. Go to the Jenkins Dashboard > Click New Item

11. Enter `datacenter-app-deployment` as the item name > Select Freestyle Project > Click OK

12. Under Source Code Management > Select `Git`

13. Go to your Gitea UI tab, log in as `sarah`, navigate to the web repository, and copy the HTTP clone URL

     <img width="942" height="432" alt="Screenshot 2026-06-28 125748" src="https://github.com/user-attachments/assets/901b83c1-7c22-424a-a912-2e0a0a61e61f" />

14. Paste this URL into the Repository URL field in Jenkins.

    <img width="906" height="572" alt="Screenshot 2026-06-28 122707" src="https://github.com/user-attachments/assets/cedd5dcc-809d-46aa-8862-40f6940bb1c0" />

15. Under the Build Triggers section > Check Poll SCM and enter * * * * * in the schedule box

    <img width="911" height="332" alt="Screenshot 2026-06-28 122714" src="https://github.com/user-attachments/assets/5fdd08fa-d4d4-4726-b4b5-481fdd65b116" />

    > This checks for changes every minute

16. Under Build Steps > Add Build step > Select Execute Shell

17. Enter the following command in the command box
    ```
    sshpass -p Sarah pass123 scp -o StrictHostKeyChecking=no -r sarah@stapp01:/var/www/html
    ```

18. Click Apply / Save

19. Go back to the terminal, navigate to the cloned repository
    ```
    cd /home/sarah/web

20. Edit the `index.html` file, remove the existing content and add the following
    ```
    Welcome to the xFusionCorp Industries
    ```

21. Push the changes
    ```
    git add .
    git commit -m "updated index.html"
    git push origin master
    ```

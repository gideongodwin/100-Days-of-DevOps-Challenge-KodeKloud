## Day 80 - Jenkins Chained Builds

## Task Details:

The DevOps team was looking for a solution where they want to restart Apache service on all app servers if the deployment goes fine on these servers in Stratos Datacenter.

After having a discussion, they came up with a solution to use Jenkins chained builds so that they can use a downstream job for services which should only be triggered by the deployment job.

So as per the requirements mentioned below configure the required Jenkins jobs.

- Click on the `Jenkins` button on the top bar to access the Jenkins UI. Login using username admin and Adm!n321 password.

- Similarly you can access `Gitea UI` on port `3000` (or click the `Gitea` button) and username and password for Git is `sarah` and `Sarah_pass123` respectively. Under user `sarah` you will find a repository named `web`

- Apache is already installed and configured on the app server. The doc root `/var/www/html` on App Server 1 is a local git repository tracking the origin `web` repository.

1. Create a Jenkins job named `datacenter-app-deployment` and configure it to pull changes from the `master` branch of the `web` repository on App Server 1 under `/var/www/html` directory.

2. Create another Jenkins job named `manage-services` and make it a `downstream job` for `datacenter-app-deployment`. Things to take care about this job are:
      
      a. This job should restart `httpd` service on the app server (App Server 1).
      
      b. Trigger this job only if the `upstream job` i.e `datacenter-app-deployment` is stable.

## Steps:

1. Log into Jenkins using the provided credentials

   <img width="990" height="389" alt="Screenshot 2026-06-01 155715" src="https://github.com/user-attachments/assets/751ab595-c04a-4cfd-bec4-a616165747c8" />

2. Click on Manage Jenkins > Under the System Configuration section, Plugins

3. Click Available plugins, search for Git and Credentials Plugins, then install

    <img width="906" height="425" alt="614245583-5b065f37-acec-4260-b0c7-81532e7b2c66" src="https://github.com/user-attachments/assets/96e66429-4ff2-4279-9cef-d2833b58557c" />

4.  Go to the terminal, ssh into App Server 1 as `Sarah`
    ```
    ssh sarah@stapp01
    ```

5. Confirms the `web` repo URL 
   ```
   git remote -v
   ```

6. Go back to Manage Jenkins > Credentials > Add Credential

7. Select Username with Password > Configure the following

   <img width="542" height="675" alt="Screenshot 2026-06-30 102044" src="https://github.com/user-attachments/assets/47b6f4a7-1bbd-4b05-b754-870d6a2167c8" />

8. Go to the Jenkins Dashboard > Click New Item

9.  Create the `downstream job` named `manage-services` 

    <img width="927" height="437" alt="Screenshot 2026-06-30 102358" src="https://github.com/user-attachments/assets/6e2d2fae-3e46-47d1-8d2e-50597011d770" />

10. Under Build Steps > Add Build step > Select Execute Shell

11. Enter the following command in the command box
    ```
    sshpass -p 'Sarah_pass123' ssh -o StrictHostKeyChecking=no sarah@stapp01 "echo 'Sarah_pass123' | sudo -S systemctl restart httpd"
    ```

12. Save/Apply

13.  Go to the Jenkins Dashboard > Click New Item

14.  Create the `upstream job` named `datacenter-app-deployment`

       <img width="923" height="446" alt="Screenshot 2026-06-30 102122" src="https://github.com/user-attachments/assets/04d2b163-8165-4253-9058-07ad18ef8c8c" />

15. Under Source Code Management > Select Git

16. Paste the URL (from the terminal) into the Repository URL field in Jenkins.

    <img width="907" height="744" alt="Screenshot 2026-06-30 103259" src="https://github.com/user-attachments/assets/5480d5ca-2cf4-4f81-b2e3-ef1eb0e49972" />

17. Under the Build Triggers section > Check Poll SCM and enter * * * * * in the schedule box

    <img width="911" height="332" alt="image" src="https://github.com/user-attachments/assets/99d44239-cd96-4e9e-afd7-dfe902f93fb4" />

18. Under Build Steps > Add Build step > Select Execute Shell

19. Enter the following command in the command box
    ```
    sshpass -p 'Sarah_pass123' scp -o StrictHostKeyChecking=no -r * sarah@stapp01:/var/www/html
    ```

20. Under Post-build actions > Add > Build other projects

    <img width="918" height="496" alt="Screenshot 2026-06-30 103434" src="https://github.com/user-attachments/assets/d1a6442d-a286-4131-a7d7-7e12ae1ef3de" />

21. Save / Apply

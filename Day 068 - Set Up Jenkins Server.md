## Day 68 - Set Up Jenkins Server

## Task Details:

The DevOps team at xFusionCorp Industries is initiating the setup of CI/CD pipelines and has decided to utilize Jenkins as their server. Execute the task according to the provided requirements:



1. Install `Jenkins` on the jenkins server using the `apt` utility only, and start it using the `service` command.

If you face a timeout issue while starting the Jenkins service, first check the service status with `service jenkins status`
Then review the logs in `/var/log/jenkins/jenkins.log` to identify the cause.

2. Jenkin's admin user name should be `theadmin`, password should be `Adm!n321`, full name should be `Jim` and email should be `jim@jenkins.stratos.xfusioncorp.com`


Note:

1. To access the `jenkins` server, connect from the jump host using the `root` user with the password `S3curePass`

2. After Jenkins server installation, click the Jenkins button on the top bar to access the Jenkins UI and follow on-screen instructions to create an admin user.

## Steps:

1. Connect to the Jenkins Server
    ```
    ssh root@jenkins
    ```

2. Install Java
    ```
    apt update
    apt install openjdk-21-jre -y
    ```

3. Install Jenkins
    ```
    apt install jenkins -y
    ```

4. Start Jenkins using the service command
    ```
    service jenkins start
    ```

5. Verify that the service is running successfully
   ```
   service jenkins status
   ```

6. Retrieve the initial admin password
    ```
    cat /var/lib/jenkins/secrets/initialAdminPassword
    ```

7. In the "Unlock Jenkins" page, paste the initialAdminPassword

   <img width="989" height="408" alt="Screenshot 2026-05-30 221710" src="https://github.com/user-attachments/assets/3d291ea5-527d-45c9-ab5d-590768cb26df" />

8. Click on Install suggested plugins

   <img width="990" height="453" alt="Screenshot 2026-05-31 123247" src="https://github.com/user-attachments/assets/cadaa0d9-fb0b-40c2-a7b2-1c020f8ec17f" />

   <img width="990" height="767" alt="Screenshot 2026-05-31 123325" src="https://github.com/user-attachments/assets/2380394a-0509-42eb-a17f-e21b6b1c992f" />


9. On the "Create First Admin User" page. Fill in the exact details provided:

     <img width="988" height="639" alt="Screenshot 2026-05-31 123508" src="https://github.com/user-attachments/assets/0d3566fa-17eb-492a-8829-3821e00f6987" />

10. On the Instance Configuration page, leave the Jenkins URL as default and click Save and Finish.
  
    <img width="987" height="361" alt="Screenshot 2026-05-31 123615" src="https://github.com/user-attachments/assets/c9c67eaa-8c90-4d90-9cbd-b0d6049b8ac8" />

11. Start using Jenkins

    <img width="988" height="282" alt="Screenshot 2026-05-31 123629" src="https://github.com/user-attachments/assets/8f550eda-6482-4b9b-8bbe-6d92f5745ce6" />



    

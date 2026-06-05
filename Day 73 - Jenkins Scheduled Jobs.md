## Day 73 - Jenkins Scheduled Jobs

## Task Details:

The devops team of xFusionCorp Industries is working on to setup centralised logging management system to maintain and analyse server logs easily.

Since it will take some time to implement, they wanted to gather some server logs on a regular basis. At least one of the app servers is having issues with the Apache server.

The team needs Apache logs so that they can identify and troubleshoot the issues easily if they arise. So they decided to create a Jenkins job to collect logs from the server. Please create/configure a Jenkins job as per details mentioned below:

Click on the `Jenkins` button on the top bar to access the Jenkins UI. Login using username `admin` and password `Adm!n321`

1. Create a Jenkins jobs named copy-logs`.

2. Configure it to periodically build `every 6 minutes` to copy the Apache logs (both `access_log` and `error_log`) from App Server 2 (stapp02) from the default logs location to location `/usr/src/itadmin` on the Storage Server.


3. Build the job at least once so that the logs are copied and can be verified.

## Steps:

1. Click on the Jenkins button on the top bar to access the `Jenkins UI`

2. Enter the provided credentials

   <img width="990" height="389" alt="Screenshot 2026-06-01 155715" src="https://github.com/user-attachments/assets/1d9ab709-90ab-466b-a374-915c0257d23c" />

3. On the Jenkins dashboard, click New Item.

4. Name the job `copy-logs` > select Freestyle project > click OK

   <img width="918" height="436" alt="Screenshot 2026-06-05 041259" src="https://github.com/user-attachments/assets/fd0c8538-4594-4782-8548-3b12d620b1f1" />

5. On the Build Triggers section > Check the box for Build periodically.

6. In the Schedule text box, enter the following cron expression to run the job every 6 minutes:
   ```
   */6 * * * *
   ```

   <img width="909" height="443" alt="Screenshot 2026-06-05 041431" src="https://github.com/user-attachments/assets/60524632-d087-4408-877a-2c81fa40eba0" />

7. On to the Build Steps section > Click Add build step and select Execute shell.

    <img width="910" height="364" alt="Screenshot 2026-06-05 041624" src="https://github.com/user-attachments/assets/47566c90-d802-487f-9e2d-b1ecb2a45044" />

8. Paste the following shell script into the Command box:
    ```
    sshpass -p 'Am3ric@' ssh -o StrictHostKeyChecking=no steve@stapp02 'sudo cp /var/log/httpd/access_log /var/log/httpd/error_log /tmp/ && sudo chmod 777 /tmp/access_log /tmp/error_log'
    sshpass -p 'Am3ric@' scp -o StrictHostKeyChecking=no steve@stapp02:/tmp/access_log /tmp/
    sshpass -p 'Am3ric@' scp -o StrictHostKeyChecking=no steve@stapp02:/tmp/error_log /tmp/
    sshpass -p 'Bl@kW' scp -o StrictHostKeyChecking=no /tmp/access_log /tmp/error_log natasha@ststor01:/tmp/
    sshpass -p 'Bl@kW' ssh -o StrictHostKeyChecking=no natasha@ststor01 'sudo mkdir -p /usr/src/itadmin/ && sudo cp /tmp/access_log /tmp/error_log /usr/src/itadmin/'
    ```

9. On the `copy-logs` job page, click Build Now.

    <img width="338" height="372" alt="Screenshot 2026-06-05 043056" src="https://github.com/user-attachments/assets/88711c7b-debb-4104-a1db-acad67f6f668" />

10. Click on the build number > Open the console output.

    <img width="922" height="571" alt="Screenshot 2026-06-05 043109" src="https://github.com/user-attachments/assets/76e83afb-72a3-4e26-a359-1d052086dc52" />




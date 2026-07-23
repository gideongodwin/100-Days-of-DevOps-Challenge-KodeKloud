## Day 75 - Jenkins Slave Nodes 

## Task Details:

The Nautilus DevOps team has installed and configured new Jenkins server in Stratos DC which they will use for CI/CD and for some automation tasks. There is a requirement to add all app servers as slave nodes in Jenkins so that they can perform tasks on these servers using Jenkins.

Find below more details and accomplish the task accordingly.

Click on the `Jenkins` button on the top bar to access the Jenkins UI. Login using username `admin` and password `Adm!n321`

1. Add all app servers as SSH build agent/slave nodes in Jenkins. Slave node name for `app server 1`, `app server 2` and `app server 3` must be `App_server_1`, `App_server_2`, `App_server_3` respectively.

2. Add labels as below:

    - App_server_1 : `stapp01`
    
    - App_server_2 : `stapp02`
    
    - App_server_3 : `stapp03`

3. Remote root directory for `App_server_1` must be `/home/tony/jenkins`, for `App_server_2` must be `/home/steve/jenkins` and for `App_server_3` must be `/home/banner/jenkins`

4. Make sure slave nodes are online and working properly.

## Steps:

1. Click on the Jenkins button on the top bar to access the `Jenkins UI`

2. Enter the provided credentials

    <img width="990" height="389" alt="Screenshot 2026-06-01 155715" src="https://github.com/user-attachments/assets/3edce5d5-0538-4b85-a8af-824fa68f5650" />

3. Go to Manage Jenkins > Under the System Configuration section > Click on Plugins

4. Click Available plugins, search for `SSH Build Agents`, then install

    <img width="955" height="296" alt="Screenshot 2026-06-08 173856" src="https://github.com/user-attachments/assets/3cf02281-71a0-40ec-b6d4-3971f8c4d3ea" />

5. Go to Manage Jenkins > Under the System Configuration section > Click on Nodes

   <img width="941" height="255" alt="Screenshot 2026-06-01 160009" src="https://github.com/user-attachments/assets/9c862ea7-6fe5-4ee8-a880-336622e01533" />

6. Click on New Node

   <img width="959" height="332" alt="Screenshot 2026-06-08 173334" src="https://github.com/user-attachments/assets/bb1d8537-e524-4ef7-93a2-1459fdcb130d" />

7.  Name it `App_server_1` > Select Permanent Agent and click Create

    <img width="961" height="415" alt="Screenshot 2026-06-08 173356" src="https://github.com/user-attachments/assets/e9a6e4d6-f7fb-4a3d-a24d-67013af7a758" />

8. Fill in the configuration details:

    <img width="938" height="684" alt="Screenshot 2026-06-08 174251" src="https://github.com/user-attachments/assets/7b1087e6-d59f-4544-9ec5-82739fff3ba6" />

    > Launch method: Select Launch agents via SSH

    > Click Add > Configure the following
    
    <img width="938" height="309" alt="Screenshot 2026-06-08 174310" src="https://github.com/user-attachments/assets/2e6f2061-af3f-49f1-82b4-9c87bea027f8" />
    
    <img width="940" height="438" alt="Screenshot 2026-06-08 174322" src="https://github.com/user-attachments/assets/5bbac354-01b4-4e8b-bb1c-a8c7a1b5916e" />

    <img width="939" height="674" alt="Screenshot 2026-06-08 174400" src="https://github.com/user-attachments/assets/849943f3-1392-4716-a1ab-40a269cc05ba" />

9. Then Save

   <img width="937" height="426" alt="Screenshot 2026-06-08 174558" src="https://github.com/user-attachments/assets/a82af95c-6018-4607-ac55-00716673813b" />

10. Repeat the same for creating App_server_2 : `stapp02` and App_server_3 : `stapp03`

11. Go back to Manage Jenkins > Nodes

12. Click on the App_server_1 > Log

    <img width="382" height="434" alt="Screenshot 2026-06-08 175813" src="https://github.com/user-attachments/assets/3a20f888-fdce-4bd8-8584-18f3f6a84069" />

13. Verify the Nodes are Online > Should show  "Agent successfully connected and online"

    <img width="552" height="280" alt="Screenshot 2026-06-08 175822" src="https://github.com/user-attachments/assets/b6fbdab9-dc8a-4d4f-8f2a-a43f9fbd0d2d" />

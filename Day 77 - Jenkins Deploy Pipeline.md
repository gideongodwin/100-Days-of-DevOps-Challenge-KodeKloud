## Day 77 - Jenkins Deploy Pipeline

## Task Details:

The development team of xFusionCorp Industries is working on to develop a new static website and they are planning to deploy the same on Nautilus App Server using Jenkins pipeline. They have shared their requirements with the DevOps team and accordingly we need to create a Jenkins pipeline job. Please find below more details about the task:

- Click on the `Jenkins` button on the top bar to access the Jenkins UI. Login using `username` admin and password `Adm!n321`

- Similarly, click on the `Gitea` button on the top bar to access the Gitea UI. Login using username `sarah` and password `Sarah_pass123`. There under user sarah you will find a repository named `web_app` that is already cloned on `App Server 1` under `/var/www/html`. sarah is a developer who is working on this repository.

- Add a slave node named `App Server 1`. It should be labeled as `stapp01` and its remote root directory should be `/home/sarah/jenkins_agent` (the repository is cloned under `/var/www/html`; the agent uses a separate directory so it does not pollute the repo).

   > We have already cloned repository on `App Server 1` under `/var/www/html`
   
   > `Apache` is already installed on the app server and is running on port `8080`

- Create a Jenkins `pipeline job` named `datacenter-webapp-job` (it must not be a `Multibranch pipeline`) and configure it to:

- Deploy the code from `web_app` repository under `/var/www/html` on `App Server 1`, as this is the document root of the app server. The pipeline should have a single stage named Deploy ( which is case sensitive ) to accomplish the deployment.

- `LB server` is already configured. You should be able to see the latest changes you made by clicking on the App button. Please make sure the required content is loading on the main URL `https://<LBR-URL>` i.e there should not be a sub-directory like `https://<LBR-URL>/web_app` etc.

## Steps:

1. Click on the `Jenkins` button on the top bar to access the Jenkins UI

2. Enter the provided credentials

   <img width="990" height="389" alt="Screenshot 2026-06-01 155715" src="https://github.com/user-attachments/assets/8142c6ee-791e-4643-b6fd-9e620ed8defd" />

3. Click on Manage Jenkins > Under the System Configuration section, Plugins

4. Click Available plugins, search for `SSH Build Agent`, `Git`,  `Pipleline` Plugins, then install

   <img width="923" height="328" alt="Screenshot 2026-06-10 075030" src="https://github.com/user-attachments/assets/bf2945f6-b6a1-4ab5-b50a-5963f24374f6" />

   <img width="911" height="277" alt="Screenshot 2026-06-10 075249" src="https://github.com/user-attachments/assets/7cdb10fb-a920-4a0f-85cc-f62d0d58c287" />

   <img width="907" height="386" alt="Screenshot 2026-06-10 075125" src="https://github.com/user-attachments/assets/9a914b63-ed07-4fe1-a2c1-73522096e8c6" />

5. Go back to Manage Jenkins > Click on Credentials

   <img width="907" height="328" alt="Screenshot 2026-06-10 075509" src="https://github.com/user-attachments/assets/35d730c7-a072-46fd-87ff-0a4cf1eb0550" />

6. Select `Global` > Add Credentials.

   <img width="926" height="451" alt="Screenshot 2026-06-10 075531" src="https://github.com/user-attachments/assets/01e3c27b-e869-4bd9-924c-a51e4e891bfe" />

   <img width="930" height="365" alt="Screenshot 2026-06-10 075544" src="https://github.com/user-attachments/assets/30441fb4-108b-4713-a8a4-b6cea9a51711" />

7. Choose Username with password as the Kind.

    <img width="930" height="264" alt="Screenshot 2026-06-10 075900" src="https://github.com/user-attachments/assets/67aea7b9-e529-48e9-bd16-656ea74ceeb4" />
  
8. Enter the Username `sarah` and Password `Sarah_pass123`, `gitea-creds` in the ID field and click Create.

    <img width="550" height="675" alt="Screenshot 2026-06-10 080203" src="https://github.com/user-attachments/assets/bea5dc7f-a205-4610-88c9-64b24dcf67ff" />

9. Go back to Manage Jenkins > System Configuration > Nodes > New Node

   <img width="940" height="340" alt="Screenshot 2026-06-10 080259" src="https://github.com/user-attachments/assets/db207ae9-5d5d-483f-8c32-9e7ae7244b45" />

    <img width="927" height="168" alt="Screenshot 2026-06-10 080314" src="https://github.com/user-attachments/assets/d9a7368f-2aa8-4c85-85b1-de984533608c" />

10. Enter App Server 1 as the Node Name, select Permanent Agent, and click Create.

    <img width="923" height="483" alt="Screenshot 2026-06-10 080329" src="https://github.com/user-attachments/assets/cf27b189-b07e-4a7e-a343-afd08ef463db" />

11. Configure the following

      <img width="908" height="161" alt="Screenshot 2026-06-10 080446" src="https://github.com/user-attachments/assets/11b26959-fb51-4d2e-9840-4926df1710cc" />

      <img width="914" height="415" alt="Screenshot 2026-06-10 081622" src="https://github.com/user-attachments/assets/57cfcf54-5ce1-437f-92c6-954392b1a837" />

    > Select the sarah credentials (gitea-creds) from the Credentials dropdown, then Save
    
       <img width="909" height="615" alt="Screenshot 2026-06-10 080456" src="https://github.com/user-attachments/assets/c37879da-bcf4-4408-a0a9-a3729e599c8d" />

12. Launch the Agent

    <img width="905" height="270" alt="Screenshot 2026-06-10 080529" src="https://github.com/user-attachments/assets/afe177ed-dd71-42a3-bcad-f7f40a539ddd" />

    <img width="911" height="182" alt="Screenshot 2026-06-10 080744" src="https://github.com/user-attachments/assets/f010d051-b667-4fad-8536-5d5f485197d3" />


      > Incase you run into a Java version mismatch error while trying to launch the agent
      
      > Install Java 17 on `App Server 1` using the following command `sudo yum install -y java-17-openjdk`
      
      > The logs should now show a successful connection
      
13. Log in to the `Gitea UI` using `sarah` credentials:

    <img width="926" height="440" alt="Screenshot 2026-06-10 074207" src="https://github.com/user-attachments/assets/3df505a2-6a52-4fcd-a83b-3e6b0bd5695d" />

14. Copy the repository's HTTP clone URL

     <img width="928" height="306" alt="Screenshot 2026-06-10 074311" src="https://github.com/user-attachments/assets/48f338a8-0c52-4ecd-8adf-6cc39a30182a" />

      > Swap out the external domain for internal domain in the URL.
      
      > Log into `App Server 1` and run `cat /etc/hosts`
      
      > Now the URL should be `http://gitea.stratos.xfusioncorp.com:3000/sarah/web_app.git`

15. Go to the Jenkins Dashboard > Click New Item

16. Enter `datacenter-webapp-job` as the item name > Select Pipeline > Click OK.

       <img width="910" height="800" alt="Screenshot 2026-06-10 080841" src="https://github.com/user-attachments/assets/75738a5f-e2a6-4ec0-afad-6b57f3de3130" />

17. On the Pipeline configuration section > Paste the following script
      ```
      pipeline {
          agent { 
              label 'stapp01' 
          }
          stages {
              stage('Deploy') {
                  steps {
                      git branch: 'master', 
                          credentialsId: 'gitea-creds', 
                          url: 'http://gitea.stratos.xfusioncorp.com:3000/sarah/web_app.git'
                      
                      sh '''
                          sudo cp -rf * /var/www/html/
                      '''
                  }
              }
          }
      }
      ```

       <img width="895" height="772" alt="Screenshot 2026-06-10 082011" src="https://github.com/user-attachments/assets/3f6783ed-1b61-4ed8-af3c-fc38ba86e956" />

18. Click Build Now

    <img width="337" height="370" alt="Screenshot 2026-06-10 082656" src="https://github.com/user-attachments/assets/182a7193-0b83-497d-ad99-fd2045dd4089" />

19. Click on the build number > Open the console output.

    <img width="539" height="201" alt="Screenshot 2026-06-10 082713" src="https://github.com/user-attachments/assets/56b6c033-b702-427c-b4e2-e81582dc0803" />


    






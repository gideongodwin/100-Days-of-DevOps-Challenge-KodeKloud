## Day 78 - Jenkins Conditional Pipeline

## Task Details:

The development team of xFusionCorp Industries is working on to develop a new static website and they are planning to deploy the same on Nautilus App Server using Jenkins pipeline. They have shared their requirements with the DevOps team and accordingly we need to create a Jenkins pipeline job. Please find below more details about the task:

Click on the `Jenkins` button on the top bar to access the Jenkins UI. Login using username `admin` and password `Adm!n321`


Similarly, click on the `Gitea` button on the top bar to access the Gitea UI. Login using username `sarah` and password `Sarah_pass123`. There under user `sarah` you will find a repository named `web_app` that is already cloned on App Server 1 under `/var/www/html`. sarah is a developer who is working on this repository.


Add a slave node named `App Server 1`. It should be labeled as `stapp01` and its remote root directory should be `/home/sarah/jenkins_agent` (the repository is cloned under `/var/www/html`).


We have already cloned repository on App Server 1 under `/var/www/html`.


Apache is already installed on the app server and is running on port `8080`.


Create a Jenkins pipeline job named `devops-webapp-job` (it must not be a `Multibranch pipeline`) and configure it to:


Add a string parameter named `BRANCH`.

It should conditionally deploy the code from `web_app` repository under `/var/www/html` on App Server 1, as this is the document root of the app server. The pipeline should have a single stage named Deploy ( which is case sensitive ) to accomplish the deployment.

The pipeline should be conditional, if the value `master` is passed to the `BRANCH` parameter then it must deploy the `master` branch, on the other hand if the value `feature` is passed to the `BRANCH` parameter then it must deploy the `feature` branch.

## Steps:

1. Click on the `Jenkins` button on the top bar to access the Jenkins UI

2. Enter the provided credentials

    <img width="990" height="389" alt="Screenshot 2026-06-01 155715" src="https://github.com/user-attachments/assets/db2de9f1-28b7-433b-845d-aa516e81651f" />

3. Click on Manage Jenkins > Under the System Configuration section, Plugins

4. Click Available plugins, search for `SSH Build Agent`, `Git`,  `Pipleline` Plugins, then install

     <img width="907" height="386" alt="Screenshot 2026-06-10 075125" src="https://github.com/user-attachments/assets/447d3683-438f-4f97-8b34-27edab00c195" />
    <img width="911" height="277" alt="Screenshot 2026-06-10 075249" src="https://github.com/user-attachments/assets/5b4d6891-857d-4a29-96be-398b349887a6" />

    <img width="923" height="328" alt="Screenshot 2026-06-10 075030" src="https://github.com/user-attachments/assets/239f9c63-a04c-4c0d-9c1d-a5f5cccb6be5" />

5. Go back to Manage Jenkins > System Configuration > Nodes > New Node

   <img width="929" height="163" alt="Screenshot 2026-06-11 012901" src="https://github.com/user-attachments/assets/1d0893d9-60d8-4745-b095-09bd5b1b4b87" />

6. Enter App Server 1 as the Node Name, select Permanent Agent, and click Create.

    <img width="924" height="487" alt="Screenshot 2026-06-11 012912" src="https://github.com/user-attachments/assets/8d7bc1fc-140f-4c2b-8e22-9dbec0160250" />

7. Configure the following

   <img width="909" height="757" alt="Screenshot 2026-06-11 013055" src="https://github.com/user-attachments/assets/1dfe8878-6c9c-4322-9653-5566dea8002e" />


    > Credentials: Click Add > Jenkins. Add a new Username with password credential:


    <img width="550" height="678" alt="Screenshot 2026-06-11 013032" src="https://github.com/user-attachments/assets/bc7be3ff-6c78-4e2e-925d-73a6e8eb903d" />

    <img width="909" height="619" alt="Screenshot 2026-06-11 013108" src="https://github.com/user-attachments/assets/7f1d006a-1c93-413f-ad52-f935d833c4dc" />

8. Click Save, then launch the Agent

    <img width="912" height="270" alt="Screenshot 2026-06-11 013312" src="https://github.com/user-attachments/assets/e6be38da-4c2d-4082-b7e5-ce24aa7a26a7" />

    <img width="929" height="182" alt="Screenshot 2026-06-11 013332" src="https://github.com/user-attachments/assets/9b5f396f-9ec7-4815-88ab-44e410bdc88c" />

      > Incase you run into a Java version mismatch error while trying to launch the agent
      
      > Install Java 17 on `App Server 1` using the following command `sudo yum install -y java-17-openjdk`
      
      > The logs should now show a successful connection

9. Go to the Jenkins Dashboard > Click New Item

10.  Enter `devops-webapp-job` as the item name > Select Pipeline > Click OK.

      <img width="904" height="779" alt="Screenshot 2026-06-11 013406" src="https://github.com/user-attachments/assets/0592cb46-d3a3-412e-a73d-23879210681c" />

11. In the General configuration tab, check the box for This project is parameterized.

12. Click Add Parameter and select String Parameter > Name: `BRANCH`, Default Value: `master` 
   
    <img width="905" height="439" alt="Screenshot 2026-06-11 013720" src="https://github.com/user-attachments/assets/e1d533da-1340-4045-9b81-c2bec3395ade" />

13. On the Pipeline configuration tab > Paste the following script
      ```
      pipeline {
          agent { 
              label 'stapp01' 
          }
          
          stages {
              stage('Deploy') {
                  steps {
                      script {
                          if (params.BRANCH == 'master') {
                              sh '''
                              cd /var/www/html
                              git fetch origin
                              git checkout master
                              git pull origin master
                              '''
                          } else if (params.BRANCH == 'feature') {
                              sh '''
                              cd /var/www/html
                              git fetch origin
                              git checkout feature
                              git pull origin feature
                              '''
                          } else {
                              error "Invalid branch specified. Please use 'master' or 'feature'."
                          }
                      }
                  }
              }
          }
      }
      ```

      <img width="904" height="842" alt="Screenshot 2026-06-11 013729" src="https://github.com/user-attachments/assets/379ff271-d1aa-460e-86e2-dc454d24ced0" />


15. Click Save

16. Click Build with Parameters > Click Build (leave the `BRANCH` parameter as `master`)

    <img width="920" height="366" alt="Screenshot 2026-06-11 013804" src="https://github.com/user-attachments/assets/2de36f46-7814-4098-8276-6da9d76a6533" />

17. Click on the build number > Open the console output.

18. Run the build again, but change the `BRANCH` parameter to `feature`

    <img width="916" height="350" alt="Screenshot 2026-06-11 013917" src="https://github.com/user-attachments/assets/45f564d1-3786-4c29-b88a-fa9ec31f5335" />

19. Click on the build number > Open the console output.

    <img width="899" height="784" alt="Screenshot 2026-06-11 013936" src="https://github.com/user-attachments/assets/34a4ec90-495c-4d2f-b7ad-a4af3ca6df3b" />


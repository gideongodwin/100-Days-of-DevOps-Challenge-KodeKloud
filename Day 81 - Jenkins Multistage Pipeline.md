## Day 81 - Jenkins Multistage Pipeline

## Task Details:

The development team of xFusionCorp Industries is working on to develop a new static website and they are planning to deploy the same on Nautilus App Server using Jenkins pipeline.

They have shared their requirements with the DevOps team and accordingly we need to create a Jenkins pipeline job. Please find below more details about the task:

- Click on the `Jenkins` button on the top bar to access the Jenkins UI. Login using username `admin` and password `Adm!n321`

- Similarly, click on the `Gitea` button on the top bar to access the Gitea UI. Login using username `sarah` and password `Sarah_pass123`

There is a repository named `sarah/web` in Gitea that is already cloned on App Server 1 under `/var/www/html` directory.

  - Update the content of the file `index.html` under the same repository to `Welcome to xFusionCorp Industries` and push the changes to the origin into the `master` branch.

Apache is already installed on the app server and is running on port `8080`.

- Add App Server 1 as a Jenkins agent (slave) node: name `App Server 1`, label `stapp01`, remote root directory `/home/sarah/jenkins_agent`, launch via SSH with host `stapp01` and credentials for user `sarah`. Install `java-17-openjdk` on App Server 1 if needed.

Create a Jenkins pipeline job named `deploy-job` (it must not be a `Multibranch pipeline` job) and pipeline should have two stages `Deploy` and `Test` ( names are case sensitive ). Configure these stages as per details mentioned below.

  a. The `Deploy` stage should deploy the code from `web` repository under `/var/www/html` on App Server 1, as this is the document root of the app server.
  
  b. The pipeline should run on the App Server 1 node (e.g. use label stapp01).
  
  c. The `Test` stage should just test if the app is working fine and website is accessible. Its up to you how you design this stage to test it out, you can simply add a `curl` command as well to run a curl against the LBR URL (`http://stlb01:8091`) to see if the website is working or not. Make sure this stage fails in case the website/app is not working or if the `Deploy` stage fails.

## Steps:

1. SSH into App Server 1 as Sarah
    ```
    ssh sarah@stapp01
    ```
2. Navigate to the web directory
    ```
    cd /var/www/html
    ```

3. Update the index.html file
    ```
    vi index.html
    ```
    > Change it to "Welcome to xFusionCorp Industries"

4. Push these changes
    ```
    git add inedex.html
    git commit -m "updated index.html"
    git push origin master
    ```

5. Install `java-17-openjdk`
    ```
    sudo yum install -y java-17-openjdk
    ```

6. Log into Jenkins using the provided credentials

    <img width="990" height="389" alt="Screenshot 2026-06-01 155715" src="https://github.com/user-attachments/assets/383043f0-1ddf-4715-a430-fdc490a9ad1c" />

7. Click on Manage Jenkins > Under the System Configuration section, Plugins

8. Click Available plugins, search for Git, Pipeline, SSH Build Agents and Credentials Plugins, then install

    <img width="995" height="573" alt="Screenshot 2026-07-02 025705" src="https://github.com/user-attachments/assets/4f1ca88c-8cf9-4b76-b836-954f7ee789a1" />

9. Go to Manage Jenkins > Credentials > Add Credential

10. Select Username with Password > Configure the following

    <img width="542" height="675" alt="image" src="https://github.com/user-attachments/assets/618ea0f7-e7dc-41ad-873a-dcdfdb79948d" />

11. Go to Manage Jenkins > Nodes > Create node named `App Server 1`

    <img width="935" height="458" alt="Screenshot 2026-07-02 030818" src="https://github.com/user-attachments/assets/51ae8b5f-26a1-4343-aa53-f88456deac49" />

12. Configure the following

    <img width="927" height="685" alt="Screenshot 2026-07-02 031103" src="https://github.com/user-attachments/assets/ba33480f-ea8d-4853-80e2-3b59b3054a43" />

    <img width="918" height="758" alt="Screenshot 2026-07-02 031116" src="https://github.com/user-attachments/assets/28f3ee3d-267c-439d-b93e-f27fabd3492a" />

13. Save

14. Go to Jenkins dashboard > Click New Item

15. Name it `deploy-job` > Select Pipeline

      <img width="933" height="389" alt="Screenshot 2026-07-02 031407" src="https://github.com/user-attachments/assets/26462fb5-54ec-4220-9d58-d077cad8bd34" />

16. On the Pipeline section > Paste the following Groovy script
      ```
      pipeline {
          agent {
              label 'stapp01'
          }
      
          stages {
              stage('Deploy') {
                  steps {
       
                      sh '''
                      cd /var/www/html
                      git fetch origin
                      git reset --hard origin/master
                      '''
                  }
              }
              
              stage('Test') {
                  steps {
                      sh '''
                      curl -f http://stlb01:8091
                      '''
                  }
              }
          }
      }
      ```

    <img width="908" height="776" alt="Screenshot 2026-07-02 034815" src="https://github.com/user-attachments/assets/b088d8e2-9b32-4075-8d0b-f9faa3a32e68" />

17. On the `deploy-job` dashboard > click Build Now

    <img width="345" height="365" alt="Screenshot 2026-07-02 035114" src="https://github.com/user-attachments/assets/ef999c6d-08e3-4065-9809-8b6a18e1366a" />

18. Select Console Output to verify both the Deploy and Test stages executed successfully without errors.






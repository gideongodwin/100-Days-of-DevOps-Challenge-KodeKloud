## Day 71 - Configure Jenkins Job for Package Installation

## Task Details:

Some new requirements have come up to install and configure some packages on the Nautilus infrastructure under Stratos Datacenter. The Nautilus DevOps team installed and configured a new Jenkins server so they wanted to create a Jenkins job to automate this task. Find below more details and complete the task accordingly:

- Access the Jenkins UI by clicking on the `Jenkins` button in the top bar. Log in using the credentials: username `admin` and password `Adm!n321`

- Create a new Jenkins job named `install-packages` and configure it with the following specifications:

- Add a string parameter named `PACKAGE`

- Configure the job to install a package specified in the `$PACKAGE` parameter on the `storage server` (Stratos Datacenter).

- Build the job at least once (e.g. with parameter `PACKAGE=vim-enhanced`) so the package is installed on the Storage server and can be verified

## Steps:

1. Click on the Jenkins button on the top bar to access the `Jenkins UI`

2. Enter the provided credentials

   <img width="990" height="389" alt="Screenshot 2026-06-01 155715" src="https://github.com/user-attachments/assets/24abde66-3e76-43e6-a301-5b850a2f32d1" />

3. Under the System Configuration section, click on Plugins

4. Click Available plugins, search for `Publish over SSH`, then install

   <img width="956" height="287" alt="Screenshot 2026-06-03 090611" src="https://github.com/user-attachments/assets/239edd0b-5e34-4f41-bd10-6b8e2c67e4a7" />

5. Restart Jenkins when installation is complete

6. Go to Manage Jenkins > System

7. Under the Publish over SSH Section > Add SSH Server

8. Enter the following details:

   <img width="936" height="840" alt="Screenshot 2026-06-03 091655" src="https://github.com/user-attachments/assets/7e73433d-7e86-4607-9546-cae2b5254774" />

9. Click the Test Configuration button > SUCCESS

10. Go to the Jenkins dashboard, click New Item

    <img width="949" height="170" alt="Screenshot 2026-06-03 091730" src="https://github.com/user-attachments/assets/4e4762d3-4bf2-4020-b06a-93aed589e1bc" />

11. Name the job `install-packages` > select Freestyle project > click OK.

    <img width="952" height="441" alt="Screenshot 2026-06-03 091807" src="https://github.com/user-attachments/assets/691dff57-d815-4bf6-9394-58c0aed4e3a7" />

12. In the General tab, check the box for `This project is parameterized`.

13. Click Add Parameter > String Parameter and set it up:
    ```
    Name: PACKAGE
    Default Value: vim-enhanced
    ```

14. Under Build Steps section > Add build step > Select send files or execute commands over ssh

     <img width="933" height="695" alt="Screenshot 2026-06-03 092245" src="https://github.com/user-attachments/assets/71365661-5768-4725-af83-4b8f2bc514b9" />

15. Configure the following

    <img width="936" height="859" alt="Screenshot 2026-06-03 092605" src="https://github.com/user-attachments/assets/1cbf5ea7-1b16-4192-8142-422f3f89b4c1" />

16. Click on Save / Apply

17. On the `install-packages` job page, click Build with Parameters.

18. Ensure the `PACKAGE` parameter displays `vim-enhanced` (or type it in).

19. Click Build

    <img width="955" height="338" alt="Screenshot 2026-06-03 092727" src="https://github.com/user-attachments/assets/dbfbdc7b-32e3-4374-99b1-78960d9d0eae" />

20. Click on the build number > Open the console output.
     
    <img width="318" height="522" alt="Screenshot 2026-06-03 092819" src="https://github.com/user-attachments/assets/6da41ab0-10a6-438a-a7fc-57def3a02017" />

21. Scroll to the bottom to verify the logs show a SUCCESS status

    <img width="955" height="384" alt="Screenshot 2026-06-03 092828" src="https://github.com/user-attachments/assets/bc487350-b4c5-489e-ad28-1caed7371a73" />




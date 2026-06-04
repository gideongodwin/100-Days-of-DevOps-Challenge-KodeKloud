## Day 72 - Jenkins Parameterized Builds

## Task Details:

A new DevOps Engineer has joined the team and he will be assigned some Jenkins related tasks. Before that, the team wanted to test a simple parameterized job to understand basic functionality of parameterized builds.

He is given a simple parameterized job to build in Jenkins. Please find more details below:

Click on the `Jenkins` button on the top bar to access the Jenkins UI. Login using username `admin` and password `Adm!n321`


1. Create a `parameterized` job which should be named as `parameterized-job`


2. Add a `string` parameter named `Stage`; its default value should be `Build`


3. Add a `choice` parameter named `env`; its choices should be `Development`, `Staging` and `Production`

4. Configure job to execute a shell command, which should echo both parameter values (you are passing in the job).


5. Build the Jenkins job at least once with choice parameter value `Development` to make sure it passes.

## Steps:

1. Click on the Jenkins button on the top bar to access the `Jenkins UI`

2. Enter the provided credentials

   <img width="990" height="389" alt="Screenshot 2026-06-01 155715" src="https://github.com/user-attachments/assets/3d979ee3-ffc4-49af-a464-1d6f7954176c" />

3. Go to the Jenkins dashboard, click New Item

  <img width="949" height="170" alt="Screenshot 2026-06-03 091730" src="https://github.com/user-attachments/assets/f5081b0f-8ec6-42d0-9306-473731d46211" />

4. Name the job `parameterized-job` > select Freestyle project > click OK.

  <img width="956" height="431" alt="Screenshot 2026-06-04 154943" src="https://github.com/user-attachments/assets/0e9051ea-237a-47bb-b3d5-fd062e8022b5" />

5. In the General tab, check the box for `This project is parameterized`.

6. Click Add Parameter > String Parameter and set it up:
    ```
    Name: Stage
    Default Value: Build
    ```

   <img width="941" height="341" alt="Screenshot 2026-06-04 155226" src="https://github.com/user-attachments/assets/d531b366-5b45-4a01-afaf-ae2d14fedb60" />


7. Click Add Parameter > Choice Parameter and set it up:
    ```
    Name: env
    Choices:  Development
              Staging
              Production
    ```

    <img width="941" height="376" alt="Screenshot 2026-06-04 155334" src="https://github.com/user-attachments/assets/286e12ab-c7f1-43b6-9ff3-5493ff170138" />

8. Scroll down to the Build Steps section > Click the Add build step dropdown.

   <img width="941" height="314" alt="Screenshot 2026-06-04 155400" src="https://github.com/user-attachments/assets/8e05fbf0-4246-48e6-981c-a886d8d393de" />

9. In the Command text box, configure the following:
    ```
    echo "The Stage parameter is: $Stage"
    echo "The Environment parameter is: $env
    ```
    
    <img width="941" height="441" alt="Screenshot 2026-06-04 155613" src="https://github.com/user-attachments/assets/ab4ed584-9c65-4100-8823-e883a8488d1b" />

10. Click Save / Apply

11. On the `parameterized-job` job page, click Build with Parameters.

    <img width="959" height="424" alt="Screenshot 2026-06-04 155726" src="https://github.com/user-attachments/assets/780fb965-2f9d-4521-a145-6d7ce5bbd239" />

12. Click on the build number > Open the console output.

13. Scroll to the bottom to verify the logs show a SUCCESS status

    <img width="956" height="393" alt="Screenshot 2026-06-04 155749" src="https://github.com/user-attachments/assets/af28ffa3-a67a-4616-8195-48184e149c5e" />







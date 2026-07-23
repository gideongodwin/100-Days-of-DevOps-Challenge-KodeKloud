## Day 76 - Jenkins Project Security

## Task Details:

The xFusionCorp Industries has recruited some new developers. There are already some existing jobs on Jenkins and two of these new developers need permissions to access those jobs. The development team has already shared those requirements with the DevOps team, so as per details mentioned below grant required permissions to the developers.


Click on the Jenkins button on the top bar to access the Jenkins UI. Login using username admin and password Adm!n321.

There is an existing Jenkins job named `Packages`, there are also two existing Jenkins users named `sam` with password `sam@pass12345` and `rohan` with password `rohan@pass12345`.

Grant permissions to these users to access `Packages` job as per details mentioned below:

a.) Make sure to select `Inherit permissions from parent ACL` under inheritance strategy for granting permissions to these users.

b.) Grant mentioned permissions to sam user : `build`, `configure` and `read`

c.) Grant mentioned permissions to rohan user : `build`, `cancel`, `configure`, `read`, `update` and `tag`
## Steps:

1. Click on the Jenkins button on the top bar to access the Jenkins UI

2. Enter the provided credentials

   <img width="990" height="389" alt="Screenshot 2026-06-01 155715" src="https://github.com/user-attachments/assets/9f83a360-8d46-46c8-912b-e3ce2d8ee683" />

3. Go to Manage Jenkins > System Configuration Section > Click on Plugins

4. Click Available plugins, search for `Matrix Authorization Strategy`, then install

   <img width="956" height="330" alt="Screenshot 2026-06-09 135917" src="https://github.com/user-attachments/assets/2d15d5fd-b7b1-4980-a3bb-0a2042b18132" />

5. Go to Manage Jenkins > Security

6. Scroll down to the Authorization section > Enable `Project-Based Matrix Authorization Strategy`

    <img width="939" height="422" alt="Screenshot 2026-06-09 140605" src="https://github.com/user-attachments/assets/4fc57623-a760-4689-b138-0928fccdd259" />

7. On the Jenkins dashboard, click the `Packages` job.

   <img width="952" height="314" alt="Screenshot 2026-06-09 140430" src="https://github.com/user-attachments/assets/cad39d4e-a530-4d1f-bb57-a531f648d4c4" />

8. Click on Configure

   <img width="337" height="368" alt="Screenshot 2026-06-09 140440" src="https://github.com/user-attachments/assets/c8ca0e2e-17c2-43f2-8614-1dce2920c895" />

9. On to the General section > Enable project-based security

10. Click the Add user > Add `sam` with permissions: `build`, `configure` and `read`

11. Add user `rohan` with permissions: `build`, `cancel`, `configure`, `read`, `update` and `tag`

12. Then Save

     <img width="940" height="865" alt="Screenshot 2026-06-09 140855" src="https://github.com/user-attachments/assets/354afa2c-afbe-4b9d-902e-ba063132b696" />



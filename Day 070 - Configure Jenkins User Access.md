## Day 70 - Configure Jenkins User Access

## Task Details:

The Nautilus team is integrating Jenkins into their CI/CD pipelines. After setting up a new Jenkins server, they're now configuring user access for the development team, Follow these steps:

- Click on the `Jenkins` button on the top bar to access the Jenkins UI. Login with username `admin` and password `Adm!n321`

- Create a jenkins user named `anita` with the password `dCV3szSGNA` Their full name should match `Anita`

- Utilize the `Project-based Matrix Authorization Strategy` to assign overall `read` permission to the `anita` user.

- Remove all permissions for `Anonymous` users (if any) ensuring that the `admin` user retains overall `Administer` permissions.

- For the existing job, grant `anita` user only read permissions, disregarding other permissions such as Agent, SCM etc.

## Steps:

1. Click on the Jenkins button on the top bar to access the `Jenkins UI`

2. Enter the provided credentials

   <img width="990" height="389" alt="Screenshot 2026-06-01 155715" src="https://github.com/user-attachments/assets/ce5b8911-c96d-4a9c-a901-9a61c157e85d" />

3. Click on Manage Jenkins

    <img width="956" height="129" alt="Screenshot 2026-06-01 155904" src="https://github.com/user-attachments/assets/8af9a912-4f8e-4f39-b5a2-8d3e9e48669b" />

4. Under Security section >  Manage Users

   <img width="940" height="171" alt="Screenshot 2026-06-02 175016" src="https://github.com/user-attachments/assets/7103b90c-cb3c-4b57-ad6a-66fd37b9c0c5" />

5. Create the the user `anita`

   <img width="962" height="573" alt="Screenshot 2026-06-02 173943" src="https://github.com/user-attachments/assets/93aed09c-2395-45d3-91d8-02ac8f9f76e5" />

6. Under the System Configuration section, click on Plugins

7.  Click Available plugins, search for `Project-based Matrix Authorization Strategy`, then install

     <img width="955" height="326" alt="Screenshot 2026-06-02 174156" src="https://github.com/user-attachments/assets/d6310085-2149-40fc-abcf-e518e2a35cef" />

8. Go back to Manage Jenkins > Security 

    <img width="940" height="171" alt="Screenshot 2026-06-02 175016" src="https://github.com/user-attachments/assets/5c2e98fd-8390-4e2d-93c7-b3d1374e3a2f" />

9. Scroll down to the Authorization section > Select the `Project-based Matrix Authorization Strategy` option

10. Click the Add User to add `anita` 

11. Ensure `Anita` has `read` permissions and `admin` still has `Administer` permissions > Then Apply / Save

    <img width="936" height="544" alt="Screenshot 2026-06-02 175405" src="https://github.com/user-attachments/assets/aedbf1bf-f0df-4dd3-8461-b02723e3cc75" />

12. Return to the main Jenkins Dashboard

13. Click on the existing job displayed on the screen

    <img width="949" height="348" alt="Screenshot 2026-06-02 175453" src="https://github.com/user-attachments/assets/eb11f7bd-b862-4964-ac5e-b29cd639ce73" />

14. Click Configure

    <img width="947" height="360" alt="Screenshot 2026-06-02 175508" src="https://github.com/user-attachments/assets/710afa4c-7436-48ef-9a3b-56160d679c22" />

15. In the General configuration section > check the box for `Enable project-based security`

16. Click the Add User to add `anita`

17. Ensure `Anita` has `read` permissions

    <img width="940" height="721" alt="Screenshot 2026-06-02 175625" src="https://github.com/user-attachments/assets/21d70141-4639-4d7b-aa82-7d27f59ce8e1" />





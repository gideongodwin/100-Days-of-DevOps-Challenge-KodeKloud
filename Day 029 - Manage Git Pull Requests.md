## Day 29 - Manage Git Pull Requests

## Task Details: 
`Max` want to push some new changes to one of the repositories but we don't want people to push directly to master branch, since that would be the final version of the code. 
It should always only have content that has been reviewed and approved. We cannot just allow everyone to directly push to the master branch. So, let's do it the right way as discussed below:

1. SSH into storage server using user `max`, password `Max_pass123` . There you can find an already cloned repo under Max user's home.

Max has written his story about The 🦊 Fox and Grapes 🍇

Max has already pushed his story to remote git repository hosted on Gitea branch `story/fox-and-grapes`

- Check the contents of the cloned repository. Confirm that you can see Sarah's story and history of commits by running `git log` and validate author info, commit message etc.

- Max has pushed his story, but his story is still not in the `master` branch. Let's create a Pull Request(PR) to merge Max's `story/fox-and-grapes` branch into the master branch


2. Click on the Gitea UI button on the top bar. You should be able to access the Gitea page.

    UI login info:
    
    - Username: `max`
    
    - Password: `Max_pass123`
    
    PR title : `Added fox-and-grapes story`
    
    PR pull from branch: `story/fox-and-grapes (source)`
    
    PR merge into branch: `master (destination)`


3. Before we can add our story to the master branch, it has to be reviewed. So, let's ask `tom` to review our PR by assigning him as a `reviewer`

      - Add `tom` as reviewer through the Git Portal UI
      
      - Go to the newly created PR
      
      - Click on Reviewers on the right
      
      - Add `tom` as a reviewer to the PR


4. Now let's review and approve the PR as user Tom

      - Login to the portal with the user tom
      
      - Logout of Git Portal UI if logged in as max
      
      UI login info:
      
      - Username: `tom`
      
      - Password: `Tom_pass123`
      
      PR title : `Added fox-and-grapes story`
      
      - Review and merge it.


## Steps:

1. SSH into the storage server using Max's credentials:
    ```
    ssh max@ststor01
    ```

2. Locate and enter the repository:
    ```
    ls
    cd story-blog
    ```

3. Verify the commit history
    ```
    git log
    ```

4. Open Gitea UI and log in with Max's credentials

    <img width="927" height="459" alt="Screenshot 2026-04-04 153138" src="https://github.com/user-attachments/assets/327fe946-f8d1-4b89-b8ca-ff3b0aa1ceb9" />

5. Go to the repository

    <img width="924" height="327" alt="Screenshot 2026-04-04 153205" src="https://github.com/user-attachments/assets/c2b06005-f269-40a6-bd9b-623b0276a12b" />

6. Click on the New Pull Request button.

    <img width="924" height="443" alt="Screenshot 2026-04-04 153332" src="https://github.com/user-attachments/assets/afa0e65c-418d-4a4d-95f8-23f4498ae0fe" />

7. Configure the branches for the PR:
    ```
    Merge into (destination): master
    Pull from (source): story/fox-and-grapes
    ```

8. Then Click Create Pull Request

    <img width="901" height="765" alt="Screenshot 2026-04-04 153504" src="https://github.com/user-attachments/assets/90d976b4-6a2c-4476-8a01-1b525cb06662" />

9. Locate the Reviewers section on right-hand sidebar

10. Search for Tom, and click to assign him to the PR.

    <img width="903" height="449" alt="Screenshot 2026-04-04 153558" src="https://github.com/user-attachments/assets/53c7338a-01bd-4fe1-8bf9-f20a026ec1ee" />

11. Log back into the Gitea UI with Tom's credentials:

    <img width="925" height="435" alt="Screenshot 2026-04-04 153637" src="https://github.com/user-attachments/assets/c27dd61c-a06f-47fd-a5bc-861adc4fd55c" />

12. Navigate back to the same repository

    <img width="918" height="351" alt="Screenshot 2026-04-04 153702" src="https://github.com/user-attachments/assets/08c98e9f-be05-4d57-b947-8d1ab32def77" />

13. Go to the Pull Requests tab and click on the `Added fox-and-grapes story` PR.

14. Review the PR, then click on the Create merge commit button

    <img width="902" height="684" alt="Screenshot 2026-04-04 153858" src="https://github.com/user-attachments/assets/9d553ce2-68e7-4ce3-8767-15a8928b859d" />

15. Click Create merge commit to finalize the action.

    <img width="901" height="380" alt="Screenshot 2026-04-04 153906" src="https://github.com/user-attachments/assets/84fb511c-90df-4bf7-a5f5-8a67a63c2fd7" />







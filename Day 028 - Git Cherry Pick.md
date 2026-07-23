## Day 28 - Git Cherry Pick

## Task Details:

The Nautilus application development team has been working on a project repository `/opt/ecommerce.git` This repo is cloned at `/usr/src/kodekloudrepos` on storage server in Stratos DC.
They recently shared the following requirements with the DevOps team:

There are two branches in this repository, master and feature.
One of the developers is working on the feature branch and their work is still in progress, however they want to merge one of the commits from the `feature` branch to the `master` branch, the message for the commit that needs to be merged into master is ` Update info.txt.`
Accomplish this task for them, also remember to push your changes eventually.

## Steps:

1. SSH into the Storage Server and switch to root user
    ```
    ssh natasha@ststor01
    sudo -i
    ```

2. Navigate to the target directory
    ```
    cd /usr/src/kodekloudrepos/ecommerce/
    ```

3. Verify 
    ```
    git status
    ```

4. Find the commits on the `feature` branch.
    ```
    git log feature --oneline
    ```
    > Look for the one titled `Update info.txt`

5. Move to the destination branch where we apply these changes
    ```
    git checkout master
    ```

6. Cherry-pick the commit
    ```
    git cherry-pick <commit-hash> 
    ```
    > 7-character hash found in step 4

7. Push the changes to the remote repository `/opt/ecommerce.git`
    ```
    git push origin master
    ```

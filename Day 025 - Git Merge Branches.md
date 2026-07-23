## Day 25 - Git Merge Branches

## Task Details:

The Nautilus application development team has been working on a project repository `/opt/apps.git` This repo is cloned at `/usr/src/kodekloudrepos` on storage server in Stratos DC. 
They recently shared the following requirements with DevOps team:

- Create a new branch xfusion in `/usr/src/kodekloudrepos/apps` repo from master and copy the `/tmp/index.html` file (present on storage server itself) into the repo.

- Further, add/commit this file in the new branch and merge back that branch into master branch. Finally, push the changes to the origin for both of the branches.

## Steps:

1. SSH into the storage server and switch to root user:
    ```
    ssh natasha@ststr01
    sudo -i
    ```

2. Go to the repository
    ```
    cd /usr/src/kodekloudrepos/apps
    ```

3. Ensure you're on master branch
    ```
    git checkout master
    ```

4. Create and switch to new branch `xfusion`
    ```
    git checkout -b xfusion
    ```

5. Copy the file into the repo
    ```
    cp /tmp/index.html .
    ```

6. Add and commit the file
    ```
    git add index.html
    git commit -m "Added index.html"
    ```

7. Switch back to master
    ```
    git checkout master
    ```

8. Merge `xfusion` into master
    ```
    git merge xfusion
    ```

9. Push both branches to origin
    ```
    git push origin master
    git push origin xfusion
    ```

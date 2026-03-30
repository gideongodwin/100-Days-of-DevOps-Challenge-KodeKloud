## Day 24: Git Create Branches

## Task Details:

Nautilus developers are actively working on one of the project repositories, `/usr/src/kodekloudrepos/official`
Recently, they decided to implement some new features in the application, and they want to maintain those new changes in a separate branch.
Below are the requirements that have been shared with the DevOps team:

  - On Storage server in Stratos DC create a new branch `xfusioncorp_official` from master branch in `/usr/src/kodekloudrepos/official` git repo.
  
  > Please do not try to make any changes in the code.

## Steps:

1. SSH into the storage server and switch to root user.
    ```
    ssh natasha@ststor01
    ```

2. Go to the repository directory
    ```
    cd /usr/src/kodekloudrepos/apps
    ```

3. Check existing branches
    ```
    git branch -a
    ```

4. Switch to master branch
    ```
    git checkout master
    ```

5. Create the new branch `xfusioncorp_official`
    ```
    git branch xfusioncorp_apps
    ```

6. Verify the branch
    ```
    git branch -a
    ```

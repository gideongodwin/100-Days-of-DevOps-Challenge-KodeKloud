## Day 31 - Git Stash

## Task Details:

The Nautilus application development team was working on a git repository `/usr/src/kodekloudrepos/beta` present on `Storage server` in Stratos DC. 
One of the developers stashed some in-progress changes in this repository, but now they want to restore some of the stashed changes. Find below more details to accomplish this task:

- Look for the stashed changes under `/usr/src/kodekloudrepos/beta` git repository, and restore the stash with `stash@{1}` identifier. Further, commit and push your changes to the origin.

## Steps:

1. SSH into the Storage Server and switch to root user
    ```
    ssh natasha@ststor01
    sudo -i
    ```

2. Navigate to the target directory
    ```
    cd /usr/src/kodekloudrepos/beta/
    ```

3.  Verify the stash list
    ```
    git stash
    ```

4. Restore the specific stash 
    ```
    git stash pop stash@{1}
    ```
    > this applies the changes and removes it from the stash list

5. Commit the restored changes
    ```
    git commit -m "unstashed some changes"
    ```

6. Push the changes
    ```
    git push
    ```

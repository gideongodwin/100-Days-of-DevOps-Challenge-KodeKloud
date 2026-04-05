## Day 30 - Git hard reset

## Task Details:

The Nautilus application development team was working on a git repository `/usr/src/kodekloudrepos/beta` present on `Storage server` in Stratos DC. 
This was just a test repository and one of the developers just pushed a couple of changes for testing, but now they want to clean this repository along with the commit history/work tree, so they want to point back the HEAD and the branch itself to a commit with message  `add data.txt file`
Find below more details:

- In `/usr/src/kodekloudrepos/beta` git repository, reset the git commit history so that there are only two commits in the commit history i.e initial commit and `add data.txt file`


Also make sure to push your changes.

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

3. Identify the Commit Hash with the message "add data.txt file"
    ```
    git log --oneline
    ```
    > Copy the hash (e.g., e4f5g6h) located right next to the "add data.txt file" message.

4. Hard Reset the Repository
    ```
    git reset --hard <commit-hash>
    ```

5. Verify the Commit History
    ```
    git log --oneline
    ```

6. Push the Changes
    ```
    git push -f
    ```

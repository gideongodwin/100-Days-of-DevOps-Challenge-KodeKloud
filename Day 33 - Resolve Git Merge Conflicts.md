## Day 33 - Resolve Git Merge Conflicts

## Task Details:
`Sarah` and `Max` were working on writting some stories which they have pushed to the repository.

Max has recently added some new changes and is trying to push them to the repository but he is facing some issues. Below you can find more details:

- SSH into `storage server` using user `max` and password `Max_pass123` Under `/home/max` you will find the `story-blog` repository.

- Try to push the changes to the origin repo and fix the issues. The `story-index.txt` must have titles for all `4 stories` Additionally, there is a typo in `The Lion and the Mooose` line where Mooose should be `Mouse`

- Click on the Gitea UI button on the top bar. You should be able to access the Gitea page. You can login to Gitea server from UI using username `sarah` and password `Sarah_pass123` or username `max` and password `Max_pass123`.

## Steps:

1. SSH into the Storage Server
    ```
    ssh max@ststor01
    ```

2. Navigate to the target directory
    ```
    cd /home/max/story-blog
    ```

3. Pull the Latest Changes
    ```
    git pull origin master
    ```
    > This triggers the conflict

4. Open the file
    ```
    vi story-index.txt
    ```
    > Ensure the list is clean and correctly spelled

4. Stage the resolved file
    ```
    git add story-index.txt
    ```

5. Commit the changes
    ```
    git commit -m "Fixed merge conflict and corrected Mouse typo"
    ```

6. Push changes
```
git push origin master
```
> When prompted Username: `Sarah`, Password: `Sarah_pass123`

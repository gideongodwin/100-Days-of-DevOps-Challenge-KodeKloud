## Day 26- Git Manage Remotes

## Task Details:
The xFusionCorp development team added updates to the project that is maintained under `/opt/cluster.git` repo and cloned under `/usr/src/kodekloudrepos/cluster` 
Recently some changes were made on Git server that is hosted on Storage server in `Stratos DC` 
The DevOps team added some new Git remotes, so we need to update remote on `/usr/src/kodekloudrepos/cluster` repository as per details mentioned below:

- In `/usr/src/kodekloudrepos/cluster` repo add a new remote `dev_cluster` and point it to `/opt/xfusioncorp_cluster.git` repository.

- There is a file `/tmp/index.html` on same server; copy this file to the repo and add/commit to master branch.

- Finally push master branch to this new remote origin.

## Steps:

1. SSH into the storage server
    ```
    ssh natasha@ststor01
    sudo -i 
    ```

2. Go to the repository
    ```
    cd /usr/src/kodekloudrepos/cluster
    ```

3. Add the new remote
    ```
    git remote add dev_cluster /opt/xfusioncorp_cluster.git
    ```

4. Copy the file into the repo
    ```
    cp /tmp/index.html .
    ```

5. Add and commit the file
    ```
    git add index.html
    git commit -m "Added index.html file"
    ```

6. Push master branch to the new remote
    ```
    git push dev_cluster master
    ```

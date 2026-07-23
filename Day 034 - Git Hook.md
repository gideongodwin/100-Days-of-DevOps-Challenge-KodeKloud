## Day 34: Git Hook

## Task Details:

The Nautilus application development team was working on a git repository `/opt/ecommerce.git` which is cloned under `/usr/src/kodekloudrepos` directory present on Storage server in Stratos DC. 

The team want to setup a hook on this repository, please find below more details:

- Merge the `feature` branch into the `master` branch, but before pushing your changes complete below point.

- Create a `post-update` hook in this git repository so that whenever any changes are pushed to the master branch, it creates a `release` tag with name `release-2023-06-15`, where `2023-06-15` is supposed to be the current date. For example if today is 20th June, 2023 then the release tag must be release-2023-06-20. Make sure you test the hook at least once and create a release tag for today's release.

- Finally remember to `push` your changes.

## Steps:

1. SSH into the Storage Server
    ```
    ssh natasha@ststor01
    ```

2. Navigate to the clone repo
    ```
    cd /usr/src/kodekloudrepos/ecommerce/
    ```

3. Switch to master
    ```
    git checkout master
    ```

4. Merge feature
    ```
    git merge feature
    ```

5. Create the hook file:
    ```
    vi /opt/ecommerce.git/hooks/post-update
    ```

6. Add the following script:
    ```
    #!/bin/bash
    cd /opt/ecommerce.git
    tag=release-$(date "+%Y-%m-%d")
    git tag $tag
    ```

7. Make the hook executable
    ```
    chmod +x /opt/ecommerce.git/hooks/post-update
    ```

8. Push the merged changes:
    ```
    git push
    ```


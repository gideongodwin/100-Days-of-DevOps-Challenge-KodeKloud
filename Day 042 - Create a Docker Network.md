## Day 42 - Create a Docker Network

## Task Details:

The Nautilus DevOps team needs to set up several docker environments for different applications.
One of the team members has been assigned a ticket where he has been asked to create some docker networks to be used later. Complete the task based on the following ticket description:

- Create a docker network named as `official` on App Server `3` in `Stratos DC`

- Configure it to use `macvlan` drivers.

- Set it to use subnet `10.10.1.0/24` and iprange `10.10.1.0/24`

## Steps:

1. SSH into App Server 3
      ```
      ssh banner@stapp03
      ```

  2. Create the Macvlan Network
      ```
      docker network create -d macvlan --subnet=10.10.1.0/24 --ip-range=10.10.1.0/24 official
      ```

3. Verify the Configuration
    ```
    docker network ls
    ```

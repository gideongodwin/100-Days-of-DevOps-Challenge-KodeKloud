## Day 2: Temporary User Setup with Expiry

## Task Details:
Create a user named `siva` on `App Server 1` in Stratos Datacenter. Set the expiry date to `2026-12-07` ensuring the user is created in lowercase as per standard protocol.

## Steps:

1. Log into the app server 
    ```
    ssh tony@stapp01` 
    ```
    > When prompted, enter the password for user `tony`

2. Create the User with the expiry date `2026-12-07`
    ```
    sudo adduser -e 2026-12-07 siva
    ```

## Day 7: Linux SSH Authentication

## Task Details:
The system admins team of xFusionCorp Industries has set up some scripts on jump host that run on regular intervals and perform operations on all app servers in Stratos Datacenter. To make these scripts work properly we need to make sure the thor user on jump host has password-less SSH access to all app servers through their respective sudo users (i.e tony for app server 1). Based on the requirements, perform the following:

Set up a password-less authentication from user thor on jump host to all app servers through their respective sudo users.

## STEPS:

1. Generate an SSH key \
  ```
  ssh-keygen -t rsa
  ```

2. Copy the public key to each App Server \
  ```
  ssh-copy-id -i .ssh/id_rsa.pub tony@stapp01
  ```

3.Test Password-less Login \
  ```
  ssh tony@stapp01
  ```
  > Note: You should not be asked for a password

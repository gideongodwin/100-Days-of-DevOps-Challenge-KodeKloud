## Day 86 - Ansible Ping Module Usage

## Task Details:

The Nautilus DevOps team is planning to test several Ansible playbooks on different app servers in Stratos DC. Before that, some pre-requisites must be met. 

Essentially, the team needs to set up a password-less SSH connection between Ansible controller and Ansible managed nodes. One of the tickets is assigned to you; please complete the task as per details mentioned below:

  a. `Jump host` is our Ansible controller, and we are going to run Ansible playbooks through `thor` user from `jump host`
  
  b. There is an inventory file `/home/thor/ansible/inventory` on `jump host`. Using that inventory file test `Ansible ping` from `jump host` to `App Server 2`, make sure ping works.

## Steps:

1. Generate an SSH key pair for the `thor` user.
    ```
    ssh-keygen -t rsa
    ```

2. Copy the SSH Public Key to App Server 2
    ```
    ssh-copy-id steve@stapp02
    ```

3. Verify the Passwordless Connection and exit
    ```
    ssh steve@stapp02
    ```
    ```
    exit
    ```
4. Navigate to the ansible directory
    ```
    cd ansible
    ```

5. Edit the inventory file, add the ansible username for app server 2
    ```
    vi inventory
    ```
    ```
    stapp02 ansible_user=steve
    ```

6. Test the Ansible Ping Module
    ```
    ansible -i /home/thor/ansible/inventory stapp01 -m ping
    ```

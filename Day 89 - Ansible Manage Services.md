## Day 89 - Ansible Manage Services

## Task Details:

Developers are looking for dependencies to be installed and run on Nautilus app servers in Stratos DC. They have shared some requirements with the DevOps team.

Because we are now managing packages installation and services management using Ansible, some playbooks need to be created and tested. As per details mentioned below please complete the task:

- On jump host create an Ansible playbook `/home/thor/ansible/playbook.yml` and configure it to install `vsftpd` on all app servers.

- After installation make sure to start and enable `vsftpd` service on all app servers.

- The inventory `/home/thor/ansible/inventory` is already there on jump host.

- Make sure user `thor` should be able to run the playbook on `jump host`.

  > Validation will try to run playbook using command ansible-playbook -i inventory playbook.yml so please make sure playbook works this way, without passing any extra arguments. 

## Steps:

1. Go to the Ansible directory
    ```
    cd ansible
    ```

2. Create the Playbook file and add the following configurations
    ```
    vi playbook.yml
    ```
    ```
    ---
    - name: Install and configure vsftpd
      hosts: all
      become: yes
      tasks:
        - name: Install vsftpd package
          package:
            name: vsftpd
            state: present
    
        - name: Start and enable vsftpd service
          service:
            name: vsftpd
            state: started
            enabled: yes
    ```

3. Run the playbook
    ```
    ansible-playbook -i inventory playbook.yml
    ```

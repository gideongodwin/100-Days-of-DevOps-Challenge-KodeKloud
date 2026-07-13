## Day 91 - Ansible Lineinfile Module

## Task Details:

The Nautilus DevOps team want to install and set up a simple `httpd` web server on all app servers in Stratos DC.
They also want to deploy a sample web page using Ansible. Therefore, write the required playbook to complete this task as per details mentioned below.
We already have an inventory file under /home/thor/ansible directory on jump host. Write a playbook playbook.yml under /home/thor/ansible directory on jump host itself. Using the playbook perform below given tasks:

- Install `httpd` web server on all app servers, and make sure its service is up and running.

- Create a file `/var/www/html/index.html` with content:
  
      This is a Nautilus sample file, created using Ansible!
      
- Using `lineinfile` Ansible module add some more content in `/var/www/html/index.html` file. Below is the content:

      Welcome to xFusionCorp Industries!

  Also make sure this new line is added at the top of the file.

- The `/var/www/html/index.html` file's user and group `owner` should be `apache` on all app servers.

- The `/var/www/html/index.html` file's permissions should be `0744` on all app servers.

    > Validation will try to run the playbook using command `ansible-playbook -i inventory playbook.yml` so please make sure the playbook works this way without passing any extra arguments.

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
    - name: Setup httpd and deploy sample web page
      hosts: all
      become: yes
      tasks:
        - name: Install httpd web server
          yum:
            name: httpd
            state: present
    
        - name: Ensure httpd is up and running
          service:
            name: httpd
            state: started
            enabled: yes
    
        - name: Create index.html with initial content
          copy:
            content: "This is a Nautilus sample file, created using Ansible!\n"
            dest: /var/www/html/index.html
    
        - name: Add welcome line to the top of the file
          lineinfile:
            path: /var/www/html/index.html
            line: "Welcome to xFusionCorp Industries!"
            insertbefore: BOF
    
        - name: Set correct ownership and permissions
          file:
            path: /var/www/html/index.html
            owner: apache
            group: apache
            mode: '0744'
      ```

3. Run the playbook
    ```
    ansible-playbook -i inventory playbook.yml
    ```

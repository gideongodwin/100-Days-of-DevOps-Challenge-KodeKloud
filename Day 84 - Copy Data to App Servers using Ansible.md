## Day 84 - Copy Data to App Servers using Ansible

## Task Details:

The Nautilus DevOps team needs to copy data from the jump host to all application servers in Stratos DC using Ansible. Execute the task with the following details:

  a. Create an inventory file `/home/thor/ansible/inventory` on `jump_host` and add all `application servers` as managed nodes.
  
  b. Create a playbook `/home/thor/ansible/playbook.yml` on the jump host to copy the `/usr/src/finance/index.html` file to all application servers, placing it at `/opt/finance`.
  
  > Validation will run the playbook using the command `ansible-playbook -i inventory playbook.yml`. Ensure the playbook functions properly without any extra arguments

## Steps:

1. Navigate to the ansible directory
    ```
    cd ansible
    ```

2. Create the Inventory file and add the following configurations
    ```
    vi inventory
    ```
    ```
    [app_servers]
    stapp01 ansible_user=tony ansible_ssh_pass=Ir0nM@n
    stapp02 ansible_user=steve ansible_ssh_pass=Am3ric@
    stapp03 ansible_user=banner ansible_ssh_pass=BigGr33n
    
    [all:vars]
    ansible_connection=ssh
    ansible_ssh_common_args='-o StrictHostKeyChecking=no'
    ```

3. Create the Playbook file and add the following configurations
    ```
    vi playbook.yml
    ```
    ```
    ---
    - name: Copy index.html to all application servers
      hosts: app_servers
      become: yes
      tasks:
        - name: Ensure the destination directory exists
          file:
            path: /opt/finance
            state: directory
            mode: '0755'
    
        - name: Copy finance index file
          copy:
            src: /usr/src/finance/index.html
            dest: /opt/finance/
    ```


4. Run and Validate the Playbook
    ```
    ansible-playbook -i inventory playbook.yml
    ```

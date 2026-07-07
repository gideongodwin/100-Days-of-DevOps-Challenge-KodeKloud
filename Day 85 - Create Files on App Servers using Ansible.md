## Day 85 - Create Files on App Servers using Ansible

## Task Details:

The Nautilus DevOps team is testing various Ansible modules on servers in Stratos DC. They're currently focusing on file creation on remote hosts using Ansible. Here are the details:

  a. Create an inventory file `~/playbook/inventory` on jump host and include all app servers.
  
  b. Create a playbook `~/playbook/playbook.yml` to create a blank file `/opt/opt.txt` on all app servers.
  
  c. Set the permissions of the `/opt/opt.txt` file to `0777`.
  
  d. Ensure the `user/group` owner of the `/opt/opt.txt` file is `tony` on `app server 1`, `steve` on `app server 2` and `banner` on `app server 3`
  
  > Validation will execute the playbook using the command ansible-playbook -i inventory playbook.yml, so ensure the playbook functions correctly without any additional arguments.

## Steps

1. Navigate to the playbook directory
    ```
    cd playboook
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
    - name: Create blank file and configure permissions
      hosts: app_servers
      become: yes
      tasks:
        - name: Create /opt/opt.txt with specific permissions and ownership
          file:
            path: /opt/opt.txt
            state: touch
            mode: '0777'
            owner: "{{ ansible_user }}"
            group: "{{ ansible_user }}"
    ```

4. Run and Validate the Playbook
    ```
    ansible-playbook -i inventory playbook.yml
    ```

## Day 87 - Ansible Install Package

## Task Details:
The Nautilus Application development team wanted to test some applications on app servers in `Stratos Datacenter`. They shared some pre-requisites with the DevOps team, and packages need to be installed on app servers.
Since we are already using Ansible for automating such tasks, please perform this task using Ansible as per details mentioned below:

- Create an inventory file `/home/thor/playbook/inventory` on `jump host` and add all app servers in it.

- Create an Ansible playbook `/home/thor/playbook/playbook.yml` to install `httpd` package on `all app servers` using Ansible `yum` module.

- Make sure user `thor` should be able to run the playbook on `jump host`.

> Validation will try to run playbook using command `ansible-playbook -i inventory playbook.yml` so please make sure playbook works this way, without passing any extra arguments.

## Steps:

1. Navigate to the playbook directory
    ```
    cd playbook
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
    ansible_ssh_common_args='-o StrictHostKeyChecking=no'
    ```

3. Create the Playbook file and add the following configurations
   ```
   vi playbook.yml
   ```
    ```
    ---
    - name: Install httpd on app servers
      hosts: all
      become: yes
      tasks:
        - name: Install httpd package using yum
          yum:
            name: httpd
            state: present
    ```

4. Run and Validate the Playbook
    ```
    ansible-playbook -i inventory playbook.yml
    ```

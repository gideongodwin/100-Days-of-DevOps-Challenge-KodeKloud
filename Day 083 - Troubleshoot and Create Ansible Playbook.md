## Day 83 - Troubleshoot and Create Ansible Playbook

## Task Details:

An Ansible playbook needs completion on the jump host, where a team member left off. Below are the details:

  - The inventory file `/home/thor/ansible/inventory` requires adjustments. The playbook must run on `App Server 1` in `Stratos DC`. Update the inventory accordingly.
  
  - Create a playbook `/home/thor/ansible/playbook.yml`. Include a task to create an empty file `/tmp/file.txt` on `App Server 1`.
  
  > Validation will run the playbook using the command `ansible-playbook -i inventory playbook.yml`. Ensure the playbook works without any additional arguments.

## Steps:

1. Navigate to the Ansible directory
    ```
    cd /home/thor/ansible/
    ```

2. Edit the inventory file
    ```
    stapp01 ansible_user=tony ansible_ssh_pass=$pwd ansible_ssh_common_args='-o StrictHostKeyChecking=no'
    ```
    > Change the `$pwd` to the actual password

3. Create the playbook file
    ```
    vi playbook.yml
    ```

4.  Add the following yml configuration
    ```
    ---
    - name: Create an empty file on App Server 1
      hosts: stapp01
      tasks:
        - name: Create an empty file /tmp/file.tx
          file:
            path: /tmp/file.txt
            state: touch
    ```

5. Run and Validate the Playbook
    ```
    ansible-playbook -i inventory playbook.yml
    ```

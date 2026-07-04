## Day 82 - Create Ansible Inventory for App Server Testing

## Task Details:

The Nautilus DevOps team is testing Ansible playbooks on various servers within their stack.

They've placed some playbooks under `/home/thor/playbook/` directory on the `jump host` and now intend to test them on `app server 1` in `Stratos DC`. However, an inventory file needs creation for Ansible to connect to the respective app. Here are the requirements:

  a. Create an ini type Ansible inventory file `/home/thor/playbook/inventory` on `jump host`.
  
  b. Include `App Server 1` in this inventory along with necessary variables for proper functionality.
  
  c. Ensure the inventory hostname corresponds to the `server name` as per the wiki, for example `stapp01` for `app server 1` in `Stratos DC`.

## Steps:

1. Navigate to the playbook directory
    ```
    cd /home/thor/playbook/
    ```

2. Create and open the inventory file
    ```
    vi inventory
    ```

3. Add the server `App Server 1`
    ```
    stapp01 ansible_host=stapp01 ansible_user=tony ansible_password='App Server 1 Password'
    ```

4. Test the connection
    ```
    ansible -i inventory stapp01 -m ping
    ```

5. Run the `playbook.yml` for validation
    ```
    ansible-playbook -i inventory playbook.yml
    ```

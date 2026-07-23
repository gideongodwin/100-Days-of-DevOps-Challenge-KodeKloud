## Day 93 - Using Ansible Conditionals

## Task Details:

The Nautilus DevOps team had a discussion about, how they can train different team members to use Ansible for different automation tasks.

There are numerous ways to perform a particular task using Ansible, but we want to utilize each aspect that Ansible offers. The team wants to utilise Ansible's conditionals to perform the following task:

An `inventory` file is already placed under `/home/thor/ansible` directory on `jump host`, with all the `Stratos DC app servers` included.

- Create a playbook `/home/thor/ansible/playbook.yml` and make sure to use Ansible's `when` conditionals statements to perform the below given tasks.

- Copy `blog.txt` file present under `/usr/src/dba` directory on `jump host` to `App Server 1` under `/opt/dba` directory. Its user and group owner must be user `tony` and its permissions must be `0655`

- Copy `story.txt` file present under `/usr/src/dba` directory on `jump host` to `App Server 2` under `/opt/dba` directory. Its user and group owner must be user `steve` and its permissions must be `0655`

- Copy `media.txt` file present under `/usr/src/dba` directory on `jump host` to `App Server 3` under `/opt/dba` directory. Its user and group owner must be user `banner` and its permissions must be `0655`

    > You can use `ansible_nodename` variable from gathered facts with `when` condition. Additionally, please make sure you are running the play for all hosts i.e use `- hosts: all`
    
    > Validation will try to run the playbook using command `ansible-playbook -i inventory playbook.yml`, so please make sure the playbook works this way without passing any extra arguments.

## Steps:

1. Go to the ansible directory
    ```
    cd ansible
    ```

2. Verify the hostnames
    ```
    cat inventory
    ```

3. Create the Playbook file and add the following configurations
    ```
    vi playbook.yml
    ```
    ```
    ---
    - name: Conditional File Copy to Stratos App Servers
      hosts: all
      become: yes
      tasks:
        - name: Copy blog.txt to App Server 1 
          ansible.builtin.copy:
            src: /usr/src/dba/blog.txt
            dest: /opt/dba/blog.txt
            owner: tony
            group: tony
            mode: '0655'
          when: ansible_nodename == "stapp01"
    
        - name: Copy story.txt to App Server 2 
          ansible.builtin.copy:
            src: /usr/src/dba/story.txt
            dest: /opt/dba/story.txt
            owner: steve
            group: steve
            mode: '0655'
          when: ansible_nodename == "stapp02"
    
        - name: Copy media.txt to App Server 3
          ansible.builtin.copy:
            src: /usr/src/dba/media.txt
            dest: /opt/dba/media.txt
            owner: banner
            group: banner
            mode: '0655'
          when: ansible_nodename == "stapp03"
    ```

4. Save and exit.
    ```
    :wq
    ```
5. Run the Playbook
    ```
    ansible-playbook -i inventory playbook.yml
    ```

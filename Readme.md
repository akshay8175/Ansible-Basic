# Ansible basic Projects
--------------
### Project 1: Install and start the nginx service

```yml
---
- name: Install and Start nginx
  hosts: hosts

  tasks:
    - name: Install nginx
      apt:
        name: nginx
        state: present
    - name: Start nginx
      service:
        name: nginx
        state: started
```
----------------
### project 2: Check groups in linux machine
```yml
---
- name: Check users and groups
  hosts: all
  tasks:
    - name: List all users
      ansible.builtin.command: cat /etc/passwd
      register: users_list

    - name: Print users list
      debug:
        var: users_list.stdout

    - name: List all groups
      ansible.builtin.command: cat /etc/group
      register: groups_list

    - name: Print groups list
      debug:
        var: groups_list.stdout
```
-----------------
### project 3: Create user and assign to group
```yml
---
- name: Create a user and assign to group
  hosts: hosts
  tasks:
    - name: Create a user and assign to group
      ansible.builtin.user:
        name: devuser
        group: devgroup
        state: present
        shell: /bin/bash
        home: /home/devuser
        create_home: yes
```
--------------------------------
### Project 4: Manage users and groups
```yml
---
- name: Manage users and groups
  hosts: all
  tasks:
    - name: Create a group
      ansible.builtin.group:
        name: devgroup
        state: present

    - name: Create a user and assign to group
      ansible.builtin.user:
        name: devuser
        group: devgroup
        state: present
        shell: /bin/bash
        home: /home/devuser
        create_home: yes

    - name: Set a password for the user
      ansible.builtin.user:
        name: devuser
        password: "{{ 'asd' | password_hash('sha512') }}"

```
--------------------------------
### Project 5. Create dynamic directory
```yml
---
- name: Create dynamic directory
  hosts: all
  vars:
    folder_name: autocreated_dir
  tasks:
    - name: create a dir automatically
      ansible.builtin.file:
        path: "{{ folder_name }}"
        state: directory
        mode: '0755'
```
-----------------------------
### Project 6: Create files in target machine using ansible playbook
```yml
---
- name: Create files with specific extensions
  hosts: all
  tasks:
    - name: Create an empty file with .txt extension
      ansible.builtin.file:
        path: /path/to/yourfile.txt
        state: touch  # Ensures the file exists
        mode: '0644'  # File permissions

    - name: Create an empty file with .log extension
      ansible.builtin.file:
        path: /path/to/yourfile.log
        state: touch
        mode: '0644'

```















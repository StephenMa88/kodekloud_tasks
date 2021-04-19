# Problem
The Nautilus DevOps team wants to install and set up a simple httpd web server on all app servers in Stratos DC. Additionally, they want to deploy a sample web page for now using Ansible only. Therefore, prepare the required playbook to complete this task. Find more details about the task below.


	1. We already have an inventory file under /home/thor/ansible on jump host. Create a playbook.yml under /home/thor/ansible on jump host itself.
	2. Using the playbook, install httpd web server on all app servers. Additionally, make sure its service should up and running.
	3. Using blockinfile Ansible module add some content in /var/www/html/index.html file. Below is the content:
	```
	Welcome to XfusionCorp!
	
	This is Nautilus sample file, created using Ansible!
	
	Please do not modify this file manually!
	```
	4. The /var/www/html/index.html file's user and group owner should be apache on all app servers.
	5. The /var/www/html/index.html file's permissions should be 0655 on all app servers.

Note:
i. Validation will try to run playbook using command
```
ansible-playbook -i inventory playbook.yml 
```
so please make sure playbook works this way, without passing any extra arguments.

ii. Do not use any custom or empty marker for blockinfile module.

# Solution

## Task 1
```
cd /home/thor/ansible && vi playbook.yml
```

## Task 2 - 5
Inside the file, type this content in.
```
---
- hosts: all
  become_method: sudo
  become: yes

  tasks:

  - name: ensure apache is at the latest version
    yum: name=httpd state=present

  - name: ensure it is up and running
    ansible.builtin.service:
      name: httpd
      state: started
  
  - name: Creating an empty file index.html
    file:
      path: /var/www/html/index.html
      state: touch

  - name: Use blockin to modify index.html
    blockinfile:
      path: /var/www/html/index.html
      block: |
        Welcome to XfusionCorp!
        This is Nautilus sample file, created using Ansible!
        Please do not modify this file manually!

  - name: change user and group owner to apache  and permission for index.html
    ansible.builtin.file:
      path: /var/www/html/index.html
      owner: apache
      group: apache
      mode: '0655'
```

## To check
Run command to run the playbook
```
ansible-playbook -i inventory playbook.yml
```
Check the app servers
for x in 1 2 3; do curl stapp0$x:80; echo ""; done


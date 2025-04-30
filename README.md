# Scenario 2: Bulk Package Installation & Removal
Scenario:
Install git, vim, wget, curl and remove telnet, ftp using an Ansible Role.

Question:
You are asked to install git, vim, wget, and curl on all servers, and remove telnet and ftp packages.
How would you design an Ansible Role and Playbook to automate this task?

Answer:
Create a role packagemgmt.
In vars/main.yml, list the packages to install and remove.
In tasks/main.yml, create tasks for installing and removing packages using package module.

Write a playbook that includes the role and calls the tasks.

## Detailed Explanation:
Create Role:

ansible-galaxy init packagemgmt
Define Variables:
roles/packagemgmt/vars/main.yml
```
install_packages:
  - git
  - vim
  - wget
  - curl

remove_packages:
  - telnet
  - ftp
```  
Write Tasks:
roles/packagemgmt/tasks/main.yml

```
---
- name: Install Required Packages
  package:
    name: "{{ item }}"
    state: present
  with_items: "{{ install_packages }}"

- name: Remove Unwanted Packages
  package:
    name: "{{ item }}"
    state: absent
  with_items: "{{ remove_packages }}"
Write Playbook:
packages.yml
```
```
---
- name: Install and Remove Packages
  hosts: all
  roles:
    - packagemgmt
```  
Run the Playbook:

```
ansible-playbook packages.yml
```

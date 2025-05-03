# Bulk Package Installation & Removal

Install git, vim, wget, curl and remove telnet, ftp using an Ansible Role.


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

# project-Node.js 

# Part 1 – Deployment automation #


#---
- hosts: all
  gather_facts: yes
  become: yes
  vars:
    NODEJS_VERSION: "8"
    ansible_distribution_release: "xenial" #trusty
  tasks:
    - name: Install the gpg key for nodejs LTS
      apt_key:
        url: "https://deb.nodesource.com/gpgkey/nodesource.gpg.key"
        state: present

    - name: Install the nodejs LTS repos
      apt_repository:
        repo: "deb https://deb.nodesource.com/node_{{ NODEJS_VERSION }}.x {{ ansible_distribution_release }} main"
        state: present
        update_cache: yes

    - name: Install the nodejs
      apt:
        name: nodejs
        state: present

    - name: Install git
      apt:
        name: git
        state: present
        update_cache: yes

    - name: Clone demo-webapp
      git:
        repo: https://github.com/gbh-tech/demo-webapp
        dest: /home/abygonz/demo-application-gbh/demo-webapp
        clone: yes
        update: yes

    - name: Clone a demo-api
      git:
        repo: https://github.com/gbh-tech/demo-api
        dest: /home/abygonz/demo-application-gbh/demo-api
        clone: yes
        update: yes
...#

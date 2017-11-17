users
=========

This role is used for managing users on Linux (Centos/Ubuntu).

Requirements
------------

Generate your ssh public private key pair
ssh-keygen

Copy your public key to the roles/files folder and save it as user1.key

Role Variables
--------------
Replace the value for usernames in defaults/main.yml or group_vars/all.yml

ssh_users:
  - username: user1
    shell: /bin/bash
  - username: user2
    shell: /bin/bash

sudo_users:
  - user1
  - user2

removed_users:
  - user99

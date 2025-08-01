
# Deploying Apache Web Server and Static Application with Ansible Galaxy Role

This project involves automating the deployment of an Apache web server on target Ubuntu servers and hosting a static HTML application using an Ansible role. The role leverages built-in Ansible modules for reliability and portability, and the project is published to Ansible Galaxy for community sharing and reuse.


## Prerequisite

- AWS Account
- Set up control node and target servers
- Install ansible and python on control node
- Install python on the target servers
- Sign up ansible galaxy account

## Project Structure

```bash
 aws-ansible-project/
├── inventory.ini
├── playbook.yml
├── roles/
│   └── httpd/
│       ├── tasks/
│       │   └── main.yml
│       └── handlers/
│           └── main.yml
└── files/
    └── index.html
```
## Setup Passwordless Authentication

```bash
 ssh-copy-id -f "-o IdentityFile <PATH TO PEM FILE>" ubuntu@<INSTANCE-PUBLIC-IP>
```
- ssh-copy-id: This is the command used to copy your public key to a remote machine.
- -f: This flag forces the copying of keys, which can be useful if you have keys already set up and want to overwrite them.
- "-o IdentityFile ": This option specifies the identity file (private key) to use for the connection. The -o flag passes this option to the underlying ssh command.
- ubuntu@: This is the username (ubuntu) and the IP address of the remote server you want to access.

## Setup inventory

```bash
 # Create inventory.ini in your project directory

[webservers]
ubuntu@<target_server_ip>
ubuntu@<target_server_ip>
ubuntu@<target_server_ip>
```
## Setup Ansible Galaxy Role

```bash
 ansible-galaxy role init httpd
```
- Write the tasks in the ansible role tasks folder main.yml
- Write the static html application in the ansible role files folder
## Setup Ansible Playbook

```bash
 # Create apche-server-playbook.yaml in your project directory
---
- name: Install Apache and deploy static HTML using custom role
  hosts: webserver
  become: yes
  roles:
    - httpd
```
## Push the role to your github account

```bash
 # cd httpd
git init
git add .
git commit -m "your commit message"
git branch -M main
git remote add origin <address>
git push origin main
```
## Publish the project to ansible galaxy hub

```bash
 # Go to your ansible galaxy account, click on collection, create your api token 
 
ansible-galaxy import <github username> <github repo name> --token <ansible galaxy api token>
```

   

Install LAMP Stack on Ubuntu / Debian / Redhat with Ansible

In this Task i am going to setup multiple client servers quickly with LAMP . The client servers are like  CentOS 7, Amazon Linux, Ubunt . For setting up LAMP i have used ansible roles. Main goal is to setup LAMP in both servers with latest versions of available tools. Ansible-Playbook is made as such it is easily customizable and deployable on mutiple clients(Cent OS 7 ,  Amazon Linux, Ubuntu) with task specific to each client will be executed using import_tasks module and when condition. 

## Pre-requisites

- Used Ansible Master server as Amazon Linux 2 and Client servers on Cent OS 7 and Amazon Linux.
- Ansible Master server is installed with Ansible2.

## Resources Used

- Amazon Linux 2 
- Cent OS 7 
- Ubuntu
- Apache (webserver)
- Mariadb
- PHP
- Ansible2

## Ansible Modules Used

- [Inventory](https://docs.ansible.com/ansible/2.3/intro_inventory.html)
- [File](https://docs.ansible.com/ansible/2.3/list_of_files_modules.html)
- [Template](https://docs.ansible.com/ansible/2.5/modules/template_module.html)
- [Copy](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/copy_module.html)
- [Service](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/service_module.html)
- [mysql_user](https://docs.ansible.com/ansible/latest/collections/community/mysql/mysql_user_module.html)
- [mysql_db](https://docs.ansible.com/ansible/latest/collections/community/mysql/mysql_db_module.html)
- [get_url](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/get_url_module.html)
- [Yum](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/yum_module.html)
- [Shell](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/shell_module.html)
- [Import_tasks](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/import_tasks_module.html)

## Included roles

- LAMP - Setup lamp on all  client systems.

## Actions Performed

- Install REMI & EPEL Repo for Cent OS 7
- Installs Apache, PHP, MariaDB
- Starts and enables httpd, mariadb 
- Setup virtualhost in both client systems
- Copies test file content to documentroot
- Handler used to notify and restart httpd service

## Role Variables

- Variables declared in vars folder  which include Port No, Documentroot, Httpd_user.
- You can customise these variables as per your requirements

## How to use?

To begin with this project, first ensure that ansible is installed on your server.

First create your Inventory file. You can work entirely in this repository. Name your Inventory file and setup all required connections there.

Example Inventory file:
```
[example-host]
xxx.xxx.xxx.xxx   ansible_ssh_user="user"    ansible_port=22    ansible_ssh_private_key_file="KEY_FILE.pem"

[example-host]
xxx.xxx.xxx.xxx   ansible_ssh_user="user"    ansible_port=22    ansible_ssh_private_key_file="KEY_FILE.pem"
```

Next setup your playbook. Here i have setup my playbook main-role.yml and included roles for LAMP  on both the clients. For the execution of the playbook, first check the connection status to your client servser via:

```sh
ansible  -m ping [server]
```
Once you have established the connection then check for any syntax error in the playbook:

```sh
ansible-playbook  YOUR_PLAYBOOK_FILE.yml --syntax-check
```

if all checks have pass then you are good to execute the ansible-playbook:

```sh
ansible-playbook  YOUR_PLAYBOOK_FILE.yml
```
After Ansible deployment, login to the client servers and check if everything is as good as it was planned.

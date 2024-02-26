# Introduction

This role allows to install a Laravel project in a new Ubuntu server.

# Installing

- Clone this repository

      git clone https://github.com/pniaps/laravel-ansible.git

- Install Ansible

      https://docs.ansible.com/ansible/latest/installation_guide/installation_distros.html#installing-ansible-on-ubuntu

- Install this role requirements

      ansible-galaxy install -r requirements.yml

# Create inventory

Create new `hosts` file with the following content (replace 192.168.5.5 with your IP or host):

```
[webserver]
192.168.5.5
```

# Create playbook file

Create a new playbook file `playbook.yml` **on your local machine** with the following contents:

```yaml
- hosts: webserver
  roles:
    - pniaps.laravel
  vars:
    laravel_domain: laravelapp.com
    laravel_repo: https://github.com/laravel/laravel.git
```

# Run the playboook

Exec the next command **from your local machine** changing ``<user>`` with the name of the remote user used to access the remote server
. ``--become`` is needed to execute tasks with root privileges and ``-K`` is used to ask for the privilege escalation password.

You can remove `-k`, `--become` and `-K` if your public SSH key is installed on the server.

````shell
ansible-playbook -i hosts setup.yml -u <user> -k --become
````

When the playbook is done running, if you got no errors you can go to http://laravelapp.com

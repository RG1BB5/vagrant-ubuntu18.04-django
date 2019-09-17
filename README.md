# vagrant-ubuntu18.04-django
A Vagrant template for running a Django project in development on Ubuntu 18.04

## Overview
A Vagrant development setup with ansible provisioning to create and run a django app using different webservers and databases.

## Features
- Vagrantfile
- Ansible playbook
  - Python installation
  - Apache installation
  - Nginx installation
  - Postgresql installation
- Django project initialisation


## Install requirements
- Vagrant - [https://www.vagrantup.com/docs/installation/](https://www.vagrantup.com/docs/installation/)
- Vagrant box file (if you decide to use a different one)

## Setup
    git clone https://github.com/RG1BB5/vagrant-ubuntu18.04-django.git
    chmod +x scripts/bash/vagrant_full_cleanup.sh

Rename the folder to your project name  
Edit the ansible.extra_vars in Vagrantfile (these will be used for configuring your project)

    vagrant up

## Features to add
- [ ] Update uwsgi to use socket file instead of ports
- [ ] Add MySQL installation
- [ ] Add gunicorn setup
- [ ] Add Redis
- [ ] Add Celery

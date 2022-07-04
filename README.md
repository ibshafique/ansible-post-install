# ANSIBLE POST INSTALL
#### _Automating The Boring Linux Machine Post Installation Tasks With Ansible_

## Contents
- [About the Project](#about-the-project)
- [Requirements](#requirements)
- [Installing Ansible On Node Machine](#installing-ansible-on-node-machine)
- [Installing OpenSSH On Both Machines](#installing-ansible-on-both-machines)
- [How To Run The Playbook](#how-to-run-the-playbook)
- [Running Issues](#running-issues)


## About the Project
The aim of this project is to automate the post installation tasks for Linux machines:
- Saves time and energy.
- Ansible being idempotent means change commands are not run unless needed.
- Just start the playbook and grab a cup of coffee!! :D


## Requirements
- Ansible [core 2.12.2] installed on node machine.
- OpenSSH server and client installed on both machines.
- Python3.8 or newer installed on both machines.


## Installing Ansible On Node Machine
Ansible can be installed and set to run at startups using the following commands:

```sh
$ sudo apt update
$ sudo apt install software-properties-common
$ sudo add-apt-repository --yes --update ppa:ansible/ansible
$ sudo apt install ansible
```


Check whether ansible has been successfully installed in the machine with:


```sh
ishraque@ansimac:~$ ansible --version
  ansible [core 2.12.2]
  config file = /etc/ansible/ansible.cfg
  configured module search path = ['/home/ishraque/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python3/dist-packages/ansible
  ansible collection location = /home/ishraque/.ansible/collections:/usr/share/ansible/collections
  executable location = /usr/bin/ansible
  python version = 3.8.10 (default, Nov 26 2021, 20:14:08) [GCC 9.3.0]
  jinja version = 3.0.3
  libyaml = True
```


## Installing OpenSSH On Both Machines
OpenSSH client and server can be installed with:

```sh
sudo apt install openssh-client openssh-server
```

## How To Run The Playbook
The following needs to be made sure before the playbook is run:
1. OpenSSH server is installed in the target machine.
3. The node machine can successfully ping and ssh into the target machine.


Changes are need to be done to the ```inventory.yml``` file before the playbook can be run successfully:
1. Add new hosts to the ```inventory.yml```file as required.

```sh
---
all:
  children:
    user_hosts:
      hosts:
        192.168.X.X:
            ansible_user: user1
            username: user1
        192.168.X.Y:
            ansible_user: user2
            username: user2
```

Finally the playbook can be run with the following command:

```sh
$ ansible-playbook -v playbook.yml --extra-vars "@password_secret.yml"
```

## Running Issues
- Currently no running issues. :)
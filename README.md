# How to use this repo

## Prerequisites 

Install: 

* VirtualBox: https://www.virtualbox.org/wiki/Downloads
* Vagrant: https://www.vagrantup.com/downloads
* Ansible: https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html

## Sping up the servers

Once you have necessary tools installed execute the following command in the directory where `Vagrantfile` resides.
```
vagrant up
```
This will download ISO images for both ubuntu and centos so it may take longer for this command to be executed on the first run.

Once its all don run:

```
vboxmanage list runningvms
```

to see the running vms. The output should look like the following:

```
"ubuntuvm1" {8b30231b-2b93-4924-a607-a2972cce32cf}
"ubuntuvm2" {0009c306-fdd1-478d-8201-68484c692786}
"centosvm01" {b7a0b722-65b4-4733-9ffe-e14a1c3f25e6}
"centosvm02" {9yy3b722-65b4-4733-9ffe-e14a1c3cd7e1}
```

## Connect to servers

We are able to connect to any servers at this point by using the vagrant password. Give it a try.

```console
ssh vagrant@172.16.16.101
ssh vagrant@172.16.16.102
ssh vagrant@172.16.16.111
ssh vagrant@172.16.16.112
```
Password: vagrant

We get prompted to enter the user password though. We would like ansible to connect to these machines without being have to enter user password.

Either use your existing ssh key or create a new one for ansible. I will assume that you have one public key called ansible.pub.

Copy your ansible public keys inside all the servers. We are able to connect any server by running:

```console
ssh-copy-id -i ~/.ssh/ansible.pub vagrant@172.16.16.101
ssh-copy-id -i ~/.ssh/ansible.pub vagrant@172.16.16.102
ssh-copy-id -i ~/.ssh/ansible.pub vagrant@172.16.16.111
ssh-copy-id -i ~/.ssh/ansible.pub vagrant@172.16.16.112
```

Try using your ssh key this time by running:
```console
ssh -i ~/.ssh/ansible vagrant@172.16.16.101
```

you should be able ssh into the machines without entering the user password.

## Connect servers via Ansible

* Ping hosts
```console
ansible all --key-file ~/.ssh/ansible -i inventory -m ping
```

Note: If you defined defaults in your ansible.cfg file, you can omit `--key-file ~/.ssh/ansible -i inventory`.

* List hosts

```console
ansible all --list-hosts
```

* Gather informations about hosts

```console
ansible all -m gather_facts
```

## Run the palybook

```console
ansible-playbook --ask-become-pass site.yml
```
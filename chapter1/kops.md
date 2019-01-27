# Getting Started - Kops

We will setup kubernetes on AWS using Kops, which stands for **Kubernetes Operations**.

This tool allows you to do production grade installations, upgrades and management of clusters but only works on sensible operating systems \(Mac and Linux\).

## Vagrant

Grab vagrant and install locally. Create a local working folder and then spin up an ubuntu box.

```
mkdir -p ~/k8s/ubuntu
cd ~/k8s/ubuntu
vagrant init ubuntu/bionic64
vagrant up --provider=virtualbox  # modify as approproate
```

At the end of the spinning up process you'll see something along the lines of `default: /vagrant => /Users/jamesveitch/k8s/ubuntu` which shows that the folder on the guest has been mapped to the root directory of the `Vagrantfile`.

Running `vagrant ssh-config` shows the details to connect.

```
Host default
  HostName 127.0.0.1
  User vagrant
  Port 2222
  UserKnownHostsFile /dev/null
  StrictHostKeyChecking no
  PasswordAuthentication no
  IdentityFile /Users/jamesveitch/k8s/ubuntu/.vagrant/machines/default/virtualbox/private_key
  IdentitiesOnly yes
  LogLevel FATAL
```

To connect to the box just run `vagrant ssh`.

## Setting up on AWS




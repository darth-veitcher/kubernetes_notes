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

```
Welcome to Ubuntu 18.04.1 LTS (GNU/Linux 4.15.0-43-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Sun Jan 27 16:26:10 UTC 2019

  System load:  0.0              Processes:             99
  Usage of /:   9.8% of 9.63GB   Users logged in:       0
  Memory usage: 13%              IP address for enp0s3: 10.0.2.15
  Swap usage:   0%


  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.


vagrant@ubuntu-bionic:~$ 
```

## Setting up on AWS




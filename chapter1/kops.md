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

## Setting up on AWS




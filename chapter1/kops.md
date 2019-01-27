# Getting Started - Kops

We will setup kubernetes on AWS using Kops, which stands for **Kubernetes Operations**.

This tool allows you to do production grade installations, upgrades and management of clusters but only works on sensible operating systems \(Mac and Linux\).



Vagrant

Grab vagrant and install locally. Create a local working folder and then spin up an ubuntu box.

```
mkdir -p ~/k8s/ubuntu
cd ~/k8s/ubuntu
vagrant init ubuntu/bionic64
vagrant up --provider=virtualbox  # modify as approproate
```

## Setting up on AWS






# Getting Started - Kops

We will setup kubernetes on AWS using Kops, which stands for **Kubernetes Operations**.

This tool allows you to do production grade installations, upgrades and management of clusters but only works on sensible operating systems \(Mac and Linux\).

## Vagrant

Use [Vagrant](https://www.vagrantup.com) if you need access to a Linux box \(and don't necessarily want to use a container\).

[Download vagrant](https://www.vagrantup.com/downloads.html) and install locally. Create a local working folder and then spin up an ubuntu box. If you don't have already you will need to install [Virtualbox](https://www.virtualbox.org) first.

```
mkdir -p ~/k8s/ubuntu
cd ~/k8s/ubuntu
vagrant init ubuntu/bionic64
vagrant up --provider=virtualbox  # modify as appropriate
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

Navigate to [http://github.com/kubernetes/kops](http://github.com/kubernetes/kops) and download the latest release. We will be doing this on our linux box.

```
curl -LO https://github.com/kubernetes/kops/releases/download/$(curl -s https://api.github.com/repos/kubernetes/kops/releases/latest | grep tag_name | cut -d '"' -f 4)/kops-linux-amd64
chmod +x kops-linux-amd64
sudo mv kops-linux-amd64 /usr/local/bin/kops
```

Now let's get the AWS toolsets we'll need. Again, still in the linux box.

```
sudo apt-get install -y python-pip
sudo pip install --upgrade pip awscli
```

Wider usage of the AWS CLI tool and setup of an initial AWS account are out of scope for this. In order to use the tool for our purposes we need to configure some files which can be found in a new folder `~/.aws` in your home directory.

* **config** - use this to set a sane default for `region` . I use `eu-west-2` which corresponds to London.
* **credentials** - contains an `access key` and a `secret access key` that you generate from the aws console.




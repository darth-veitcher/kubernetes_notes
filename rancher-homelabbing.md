# Using Rancher + RancherOS for Homelabbing

Sources:

* [Rancher](https://rancher.com)
* [RancherOS](https://rancher.com/rancher-os/)
* [Rancher Kubernetes Engine \(RKE\)](https://rancher.com/docs/rke/v0.1.x/en/)

## Notes

Some useful articles:

* [An Introduction to Rancher Kubernetes Engine \(RKE\)](https://rancher.com/an-introduction-to-rke/)
* [High Availability \(HA\) Install](https://rancher.com/docs/rancher/v2.x/en/installation/ha/)
* [RancherOS Quick Start](https://rancher.com/docs/os/v1.x/en/quick-start-guide/)
* [Installing RancherOS on Bare Metal](https://tzrlk.aetheric.co.nz/tech/devops/2017/06/12/installing-rancheros-on-bare-metal.html)
* [Installing RancherOS to Disk \(official\)](https://rancher.com/docs/os/v1.2/en/running-rancheros/server/install-to-disk/)
* [Configuring Network Interfaces](https://rancher.com/docs/os/v1.x/en/installation/networking/interfaces/)
* [Using ZFS \(official\)](https://rancher.com/docs/os/v1.x/en/installation/storage/using-zfs/)
* [Changing Docker Versions](https://rancher.com/docs/os/v1.1/en/configuration/switching-docker-versions/)
* [kubectl cheatsheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet)

You need to downgrade the Docker engine on RancherOS in order for Kubernetes to work \(ships with 18 at time of writing and k8s only supports 17\).

As per the official docs you can run `sudo ros engine list` to display all of the available docker runtimes and then `ros enging switch` to [change docker engine after rancheros has started](https://rancher.com/docs/os/v1.1/en/configuration/switching-docker-versions/#changing-docker-engines-after-rancheros-has-started). Going forwards this can also be incorporated into your `cloud-config.yml` too.

For a bare metal install, write the iso to a usb and then, on boot, run `ros install` pointing it at a relevant `cloud-config.yml` as needed. **Easiest thing to do is have this YAML file written already and then copy across via ssh into the machine**. The trick is to switch to the `root` user and then set password for the `rancher` user so that ssh remotely works whilst still in the live USB **before installing**.

```
sudo -s  # switches to root
passwd rancher  # sets the password
```

Here's my example `cloud-config.yml` with a couple of key things added for my setup:

* I've got bonded ethernet with LACP
* I've specified the docker engine I want
* I've added my SSH public key so that, after install, I can still login with the `rancher` user

    # See https://rancher.com/docs/os/v1.x/en/installation/configuration/
    # Stored /var/lib/rancher/conf/cloud-config.yml

    # Setup SSH keys
    ssh_authorized_keys:
      - ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDZsCEU/2uFV4YpBjoOsSIY1yRta3mGdd81TyvZFGzVsXEn7BbkJXPI6I3r8vXQaRgQvr//yj/Q3whuGlcBuH8PuCAUlHg2oJIMJ+NsIW/E300nzu0j8lltDvLg4Sl1Ncag4Hy5JtjeWyoouHCUajxN8jRKqXW1pS3hZO2+UCN2t6ZNl7n01cZZviVWcoPe2tUpy2O52iWW6Wt7cgWFSBVPCmnD3p5Vwnz2d5SrSgzQ+9Qq/jrU0ZGF32wLt/c3OzHMBRLYNJviMaEZfonIjTmpqOxUQxXzO25K3/A0QHeEtBInKpNr7TUJ/U0rtpNrw2Th6wsc4pjLLM9R9U6EbH9D james@jamesveitch.com

    # Configure hostname
    hostname: node1

    # RANCHER
    rancher:
      # Console
      # default (busybox), alpine, centos, debian, fedora, ubuntu
      console: default
      # Docker version
      # Kubernetes only supports certain versions
      # [1.11.x 1.12.x 1.13.x 17.03.x] 
      # can find what's installed with `sudo ros engine list`
      docker:
        engine: docker-17.03.2-ce
      # Bonded network interfaces
      # https://rancher.com/docs/os/v1.1/en/networking/interfaces/
      network:
        interfaces:
          bond0:
            dhcp: true
            bond_opts:
              miimon: "100"
              mode: "4"  # 802.3ad
          # eth0-eth3 in the bond
          mac=B8:AC:6F:84:AE:10:
            bond: bond0
          mac=B8:AC:6F:84:AE:12:
            bond: bond0
          mac=B8:AC:6F:84:AE:14:
            bond: bond0
          mac=B8:AC:6F:84:AE:16:
            bond: bond0




# Using Rancher + RancherOS for Homelabbing

Sources:

* [Rancher](https://rancher.com)
* [RancherOS](https://rancher.com/rancher-os/)
* [Rancher Kubernetes Engine \(RKE\)](https://rancher.com/docs/rke/v0.1.x/en/)

## Notes

You need to downgrade the Docker engine on RancherOS in order for Kubernetes to work \(ships with 18 at time of writing and k8s only supports 17\).

For a bare metal install, write the iso to a usb and then, on boot, run `ros install` pointing it at a relevant `cloud-config.yml` as needed. Easiest thing to do is have this written already and then ssh into the machine before installing. The trick is to switch to the `root` user and then set password for the `rancher` user so that ssh remotely works.

```
sudo -s  # switches to root
passwd rancher  # sets the password
```




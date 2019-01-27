# Getting started

Locally setup a kubernetes cluster using the `minikube` application which can be found on \[GitHub\]\([https://github.com/kubernetes/minikube/releases\](https://github.com/kubernetes/minikube/releases%29\).

Start the local kubernetes cluster using `minikube start`

One started this will have create a local `~/.kube/config` file which allows you to connect to the newly created VM with `kubectl` command.

```
cat ~/.kube/config
...

apiVersion: v1
clusters:
- cluster:
    certificate-authority: /Users/jamesveitch/.minikube/ca.crt
    server: https://172.16.23.174:8443
  name: minikube
contexts:
- context:
    cluster: minikube
    user: minikube
  name: minikube
current-context: minikube
kind: Config
preferences: {}
users:
- name: minikube
  user:
    client-certificate: /Users/jamesveitch/.minikube/client.crt
    client-key: /Users/jamesveitch/.minikube/client.key
```

## Kubectl

Some commands to run in order to test the cluster is all working fine.



## MacOS with VMWare Fusion

For users with VMWare Fusion installed and not wanting to download VirtualBox in addition to it you can ask minikube to launch the VM using this application instead using the `--vm-driver=vmwarefusion` switch in the command.

```
minikube start --vm-driver=vmwarefusion
```

See [https://github.com/kubernetes/minikube/blob/master/docs/drivers.md\#vmware-unified-driver](https://github.com/kubernetes/minikube/blob/master/docs/drivers.md#vmware-unified-driver) for details on the deprecation of the vmwarefusion method in future releases for a unified driver instead.


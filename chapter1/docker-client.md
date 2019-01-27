# Getting Started - Docker Client

You can also enable a local docker install to run as a Kubernetes cluster

![](/assets/Screenshot 2019-01-27 at 14.47.50.png)

Clicking to `Enable Kubernetes` will result in the following

![](/assets/Screenshot 2019-01-27 at 14.49.16.png)

To check this has been deployed properly run a `get nodes` command from `kubectl`

```
asteroid-m:~ jamesveitch$ kubectl get nodes

NAME                 STATUS    ROLES     AGE       VERSION
docker-for-desktop   Ready     master    4m        v1.10.11
```




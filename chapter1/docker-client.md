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

To check the given context under which `kubectl` is executing you can run `kubectl get-contexts`. In the below we are using `minikube` as opposed to `docker`.

```
asteroid-m:~ jamesveitch$ kubectl config get-contexts

CURRENT   NAME                 CLUSTER                      AUTHINFO             NAMESPACE
          docker-for-desktop   docker-for-desktop-cluster   docker-for-desktop   
*         minikube             minikube                     minikube
```

We can switch this to docker with a `use-context` command:

```
asteroid-m:~ jamesveitch$ kubectl config get-contexts

CURRENT   NAME                 CLUSTER                      AUTHINFO             NAMESPACE
*         docker-for-desktop   docker-for-desktop-cluster   docker-for-desktop   
          minikube             minikube                     minikube
```




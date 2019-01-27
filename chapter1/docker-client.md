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

Interestingly you can see the difference in runtimes between these two contexts when running a `get nodes` against each.

```
asteroid-m:~ jamesveitch$ kubectl config get-contexts

CURRENT   NAME                 CLUSTER                      AUTHINFO             NAMESPACE
*         docker-for-desktop   docker-for-desktop-cluster   docker-for-desktop   
          minikube             minikube                     minikube             

asteroid-m:~ jamesveitch$ kubectl get nodes

NAME                 STATUS    ROLES     AGE       VERSION
docker-for-desktop   Ready     master    11m       v1.10.11

asteroid-m:~ jamesveitch$ kubectl config use-context minikube
Switched to context "minikube".

asteroid-m:~ jamesveitch$ kubectl get nodes

NAME       STATUS    ROLES     AGE       VERSION
minikube   Ready     master    45m       v1.13.2
```

## Deploying a container

Similar to minikube we first create a deployment and then expose it.

```
kubectl run hello-kubernetes --image=gcr.io/google_containers/echoserver:1.4 --port=8080
kubectl expose deployment hello-kubernetes --type=NodePort
```

We now can show details by connecting to the service

```
asteroid-m:~ jamesveitch$ kubectl get service hello-kubernetes

NAME               TYPE       CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
hello-kubernetes   NodePort   10.107.181.111   <none>        8080:30003/TCP   2m
```

In the `PORT(S)` section the second element represents the host port mapping, so `localhost:30003` will take you to the `8080` on the container we've exposed.

```
asteroid-m:~ jamesveitch$ curl localhost:30003

CLIENT VALUES:
client_address=192.168.65.3
command=GET
real path=/
query=nil
request_version=1.1
request_uri=http://localhost:8080/

SERVER VALUES:
server_version=nginx: 1.10.0 - lua: 10001

HEADERS RECEIVED:
accept=*/*
host=localhost:30003
user-agent=curl/7.54.0
BODY:
-no body in request-
```




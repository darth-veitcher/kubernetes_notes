# Getting started - Minikube

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

```
kubectl run hello-minikube --image=gcr.io/google_containers/echoserver:1.4 --port=8080
```

The above command does the following:

* `run` - tells the cluster to run a specific image
* `hello-minikube` - names the image
* `--image=` - the particular image we want to run \(in this case the `echoserver`\)
* `--port=8080` - listen on port 8080

A response `deployment.apps "hello-minikube" created` is received from the cluster and we then need to run another command to expose it to our host machine.

```
kubectl expose deployment hello-minikube --type=NodePort
```

A response `service "hello-minikube" exposed` is received. Now the service is exposed we then need to obtain the necessary url to connect to it.

```
minikube service hello-minikube --url
```

This may take some time \(as it downloads the image\) but will finally return a url that you can visit to see the detailed response from the `echoserver`.

You can test this without needing to use a browser with `curl`

```
asteroid-m:~ jamesveitch$ minikube service hello-minikube --url

http://172.16.23.174:30268
...

asteroid-m:~ jamesveitch$ curl http://172.16.23.174:30268

CLIENT VALUES:
client_address=172.17.0.1
command=GET
real path=/
query=nil
request_version=1.1
request_uri=http://172.16.23.174:8080/

SERVER VALUES:
server_version=nginx: 1.10.0 - lua: 10001

HEADERS RECEIVED:
accept=*/*
host=172.16.23.174:30268
user-agent=curl/7.54.0
BODY:
-no body in request-
```

Finally, shut everything down with a `minikube stop`

## MacOS with VMWare Fusion

For users with VMWare Fusion installed and not wanting to download VirtualBox in addition to it you can ask minikube to launch the VM using this application instead using the `--vm-driver=vmwarefusion` switch in the command.

```
minikube start --vm-driver=vmwarefusion
```

See [https://github.com/kubernetes/minikube/blob/master/docs/drivers.md\#vmware-unified-driver](https://github.com/kubernetes/minikube/blob/master/docs/drivers.md#vmware-unified-driver) for details on the deprecation of the vmwarefusion method in future releases for a unified driver instead.


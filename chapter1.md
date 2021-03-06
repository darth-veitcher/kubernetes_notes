# Tools Available

To deploy a Kubernetes cluster there are multiple tools available:

* Minikube \(local install\)
* Docker Client \(local install\)

Minikube and Docker spin up single node clusters only for development and testing. You would not want these for a production setup.

* Kops \(best for AWS\)
* Kubeadm

Either Kops or Kubeadm can be used for production clusters \(use only one, you don't need both\). With both of these solutions you need to maintain the `master` nodes \(versus a managed solution like EKS\).

Kops is the preferred approach due to it's integrations with AWS but Kubeadm is an alternative and a more generic application which might make sense in other scenarios, especially in **bare metal** setups.


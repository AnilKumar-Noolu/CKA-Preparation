## Static Pods:
These are the pods that are created by Kubelet on its own without the intervention of API Server (or) rest of the components of K8 Cluster.

Here, a single Pod will be there without any Master Node. We can place our yaml definition files at the location /etc/kubernetes/manifests folder.

Kubelet checks it periodically and applies updates to that and creates pod/deployments based on yaml files.

Static Pods can also be used to deploy Control Plane Components (apiserver, scheduler, controller,..) as pods on the node.
In Kubelet.service, the pod manifest file location should be shared: --pod-manifest-path=/etc/kubernetes/manifests
(or) we can make use of kubeConfig file to share the location of static pods.

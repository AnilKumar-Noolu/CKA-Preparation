## Static Pods:
These are the pods that are created by Kubelet on its own without the intervention of API Server (or) rest of the components of K8 Cluster.

Here, a single Pod will be there without any Master Node. We can place our yaml definition files at the location /etc/kubernetes/manifests folder.

Kubelet checks it periodically and applies updates to that and creates pod/deployments based on yaml files.

Static Pods can also be used to deploy Control Plane Components (apiserver, scheduler, controller,..) as pods on the node.

In Kubelet.service, the pod manifest file location should be shared: --pod-manifest-path=/etc/kubernetes/manifests
(or) we can make use of kubeConfig file to share the location of static pods.

### commands:
1. kubectl get pods --all-namespaces  //Look for the pods with namespaces appended at last.
2. ssh nodename   //ssh into that pod and look for running process to find location of kubeconfig file.
3. 3. ps -ef | grep config (or) grep /var/lib/kubelet    //In this way, you can find location of Config file from where you can find the location of Static pods.
  
## Kubernetes Monitoring:
We can monitor the pods and Nodes of Kubernetes Cluster by using top command. Top command will be used to get the CPU and Memory Utilization of that particular pods or Nodes.

### Commands:
1. kubectl top node   //To get CPU and Memory Utilization of Nodes
2. kubectl top pod    //To get CPU and Memory Utilization of pods
3. kubectl top pod --sort-by='cpu' | head -5    //Gives list of Top 5 pods occupying more CPU.
4. kubectl top pod --sort-by='memory' | head -5    //Gives list of Top 5 pods occupying more memory.


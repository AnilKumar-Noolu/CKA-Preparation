## Service Networking
- ClusterIP: Service is accessible within a cluster.
- NodePort: To make the application on pod accessible outside cluster.

Services are cluster-wide resources, there will be no process/Namespace for services.

Pod and service IP's should not overlap with each other.

`cat /etc/kubernetes/manifests/kube-api-server         //You can find ranges of clusterIP and other services`

## DNS in Kubernetes
Kubernetes automatically deploys a built-in DNS server when you setup cluster.

If you want to access web Pod to DB pod in different Nodes, you create a service db-service to access DataBase from Web.

If both pods are in same Namespace, then you can access them by: `curl http://db-service`

If both Pods are in different Namespace named web and db, then you can access them by:  `curl http://db-service.db  //db is Namespace name here`

All the services are grouped together into another subdomain i.e., svc, so you can reach your application with the name --> db-service.db.svc

Finally, all the services and pods are grouped together into a routedomain for cluster which is set to `cluster.local` by default/ --> db-service.db.svc.cluster.local

Similarly for pods, K8 generates a name by replacing dots in IP with dashes --> ` curl http://10-244-23-56:web.pod.cluster.local

## CoreDNS in K8
Prior v1.12, DNS server in Kubernetes was kube-dns and from v1.12, it was changed to coreDNS which will be deployed as 2 pods in kube-system Namespace.

CoreDNS requires configuration files which are present at --> /etc/coredns/corefile

DNS Configuration on pods were done automatically by kubelet.

`cat /var/lib/kubelet/config.yaml  // You can see IP of DNS server and domain in this`

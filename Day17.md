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

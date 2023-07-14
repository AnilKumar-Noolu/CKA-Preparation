## ClusterRole and ClusterRoleBindings
Normally roles and roleBindings are name-spaced i.e., cluster-scoped Resources such as nodes, persistentVolumes doesn't fall under this.

So for Cluster-scoped resources such as Nodes, PV, namespaces, CertificateSigningRequest, we will be using ClusterRole and ClusterRoleBinding.

If you have a doubt over resources which are Namespaces and which are cluster-based resources, you can find them using the below command:

` kubectl api-resources --namespaced=false       //Gives Cluster-based resources `

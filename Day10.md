## ClusterRole and ClusterRoleBindings
Normally roles and roleBindings are name-spaced i.e., cluster-scoped Resources such as nodes, persistentVolumes doesn't fall under this.

So for Cluster-scoped resources such as Nodes, PV, namespaces, CertificateSigningRequest, we will be using ClusterRole and ClusterRoleBinding.

If you have a doubt over resources which are Namespaces and which are cluster-based resources, you can find them using the below command:

` kubectl api-resources --namespaced=false       //Gives Cluster-based resources `
` kubectl api-resources --namespaced=true      //Gives Namespaced resources `

With ClusterRoles, If you created a role to access Pods, then the user gets access to all the Pods irrespective of all namespaces in that cluster.

### Commands
We can also create role, rolebindings, clusterrole, clusterrolebindings using imperative way:

kubectl create clusterrole <clusterrole_name> --resource=pods,deployments --verbs=list,create,get,watch

kubectl create clusterrolebinding <clusterrolebinding-name> --user=<user-name> --clusterrole=<clusterrole-name>

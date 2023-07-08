## Cluster Maintenance
If there are maintenance activities on Kubernetes Cluster, then there are chances that the application deployed on that clustrer might face some downtime. Lets see how Kubernetes handles this:
## OS Upgrades:
If part of any upgrade/maintenance, if any of the Nodes were done, you will face some downtime while accessing applications on that pod in that Node.

So What Kubernetes does is , it will wait for 5 minutes to get that Node UP, if Node is not Up after those 5 minutes then Pods are terminated from that Node and if Pods are part of ReplicaSet, then it creates them on other Nodes.

If Pods are not part of ReplicaSet, then we forcefully drain it, that pods are lost forever.

### Pod eviction Timeout: 
The time the Node waits for the Pods to come back online. It will be set on the Controller manager with default time pof 5 Min utes.

### Commands:
kubectl drain node01    //This command will purposefully drain node01 and moves pod to another Nodes, The pos will be terminated and recreated.

kubectl cordon node01   //This command will not drain node01 but makes sure no new ppods will be scheduled on that Node.

kubectl uncordon node01   //Now the pods can be scheduled on that particular node node01 again.


I




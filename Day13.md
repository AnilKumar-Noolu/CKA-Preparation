## Networking Policy
Network Policy is another object in Kubernetes namespace just like Pods, Replica Sets, service, deployments..

Networking is used to link Network to one/more pods, we can define rules like:
1. Allow Ingress traffic from only one pod on port 3306
2. Once the above policy is created, it blocks all other traffic to Pod.

Networking.yaml file
```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: db-policy
spec:
  podSelector:
    matchLabels:                    // Selects Pods only matching this label.
      role: db
  policyTypes:
  - Ingress:                       // It isolates the ingress traffic only, No effect on egress traffic.
    - from:
      - podSelector:               // Solutions that support N/w policies are kube-router, calico, romana, weave-net..
          matchLabels:
            name: api-pod

        namespaceSelector:       //If there are multiple Namespaces with matchLabels of api-pod, then u need to add this label for Namespace.
          matchlabels:
            name: prod

      ports:
      - protocol: TCP
        port: 3306
      - ipBlock:
          cidr: 192.168.5.10/32     //To allow traffic from Ip addresses which are not prt of K8 Cluster.

      egress:                        //Traffic flowing from DB pod to outside.
      - to:
        - ipBlock:
            cidr:
```

## Node Selectors:
      If you want to deploy pod only on a particular Node, then we can label the nodes with a key-value pair and we can apply nodeSelector to the Pod so that the pod will deploy only on that particular Node.

 # Commands:

 i) kubectl label nodes <node_name> <label_key>=<label_value>

ii) kubectl label nodes node01 size=large

In Pod yaml definition: (under spec.containers)
```
spec:
  nodeSelector:
    size: large
```
In this way only the pods with NodeSelector of sixe=large will be place on that labelled Node.

## Taints and Tolerations:
    Taints and tolerations are also used to manage pods on only particular nodes. Taints will be applied on Node and tolerations will be applied to Pods.

# Commands:

i)kubectl taint nodes <node_name> key=value:Effect
 kubectl taint nodes node01 app=blue:NoSchedule

There are 3 types of Effects:
a) Noschedule: It instructs the pod not to be scheduled on the particular Node which has tainted with this effect.

b) PreferNoSchedule: It also tries not to schedule pod on this Node but if there are no Nodes availbe to schedule, it will schedule on thsi Node.

c) NoExecute: It will strictly not place the pod on this Nodeand even if there are any existing pods on that Node, it will evict them also.

Tolerations applied on Pod:
```
spec:
  tolerations:
  - key: "app"
    operator: "Equal"
    value: "blue"
    effect: "NoSchedule"
```

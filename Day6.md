## Resource Requirements and Limits:
If a Pod consumes more memory than its limits, then the menory is exhausted in that particular Namespace or node. So the pod will be terminated with reason OOM(Out Of Memory)

If a Pod consumes more CPU, then the Pod will throttle down.
```
spec:
  resources:
    requests:
      memory: 512GB
      cpu: 1
    limits:
      memory: 1024GB
      cpu: 2
```
If requests/limits were not set, a Pod can consume any amount of resources on that particular Node and can suffocate other pods.

Based on the Pods condition, set the requests and limits such that No Pod will consume over limit and No pod will be short of resources,

## Limit Ranges
Limit ranges helps you define default values to be set for containers in Pod. It sets the deafult values that sets the Pods tpo consume that resources and also sets max value that Pods can access.
```
spec:
  limits:
    default:
      cpu: 1
    max:
      cpu: 2
```

## 
      
:

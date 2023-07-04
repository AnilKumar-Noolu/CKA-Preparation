## ConfigMaps: 
    When we want to pass any key-value pair to an application, we will use configMaps.
We can create configmaps in 2 ways:
1) Imperative way:
a) kubectl create configmap app-config --from-literal=<key_name>=<value>
b) kubectl create configmap app-config --from-file=<file_name>

2)Declarative Way: Creating a configMap using yaml file
```
apiVersion: v1
kind: configMap
metadata:
  name: config-app
data:
  color: blue
  env: prod
```
## Configuring configMaps with Pod:

```
spec:
  envFrom:
    - configMapRef:
        name: config-app

(OR)
env:
  - name: color
    valueFrom:
      configMapKeyRef:
        name: config-app
        key: color
```

## Secrets:
  When we want to pass any sensitive information to any application, we willbe using Secrets instaed of passing that information directly in aPod or deployment.
  

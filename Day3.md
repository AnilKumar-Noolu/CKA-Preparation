## ConfigMaps: 
  When we want to pass any key-value pair to an application, we will use configMaps instaed of directly oassing it to pods or deployment.
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
  When we want to pass any sensitive information to any application, we willbe using Secrets instaed of passing that information directly in a Pod or deployment.
  Secrets are not encrypted, only encoded.
  Secrets are not encrypted in ETCD.
  Anyone able to create pods/deployment in same Namespace can access Secrets.
  
We can create secrets in 2 ways:
1) Imperative way:
a) kubectl create secret generic app-secret --from-literal=<key_name>=<value>
b) kubectl create secret generic app-secret --from-file=<file_name>

2)Declarative Way: Creating a secret using yaml file
```
apiVersion: v1
kind: Secret
metadata:
  name: app-secret
data:
  DB_HOST: mysql
  DB_USER: user
  DB_password: password
```
## Configuring secret with Pod:

```
spec:
  envFrom:
    - secretRef:
        name: app-secret

(OR)
env:
  - name: DB_HOST
    valueFrom:
      secretKeyRef:
        name: app-secret
        key: DB_HOST
```

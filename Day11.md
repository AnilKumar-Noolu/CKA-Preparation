## Service Accounts
There are two types of accounts: 1) Users and 2)Service

Service is nothing but an account used by application to interact with Kubernetes Cluster like
1. Prometheus uses Service Account to monitor metrics,
2. Jenkins uses Service Account to deploy applications on Kubernetes.

For these requests to reach kube-apiserver, they must be authenticated. For that we must use Service Accounts.

#### Commands
kubectl create serviceaccount dashboard

kubectl get serviceaccount

kubectl describe serviceaccount dashboard

- Whenever SA is created, a token will be created. This token must be used by external application while authenticating with Kubernetes API.
- Tokens are stored as a secret object, U can usethis command while using curl command.
- If we have dashboard (or) prometheus deployed on Kubernetes itself as a Pod, then we configure them by mounting the serviceaccount token secret as a volume inside pod hosting 3-party application.

Whenever a pod is created, the default SA and its token are automatically mounted on that pod as a volume mount.

Token will be stored at /var/run/secrets/kubernetes.io/serviceaccount

You cannot edit the SA of existing pod, you must delete and recreate that pod.

From V1.22 onwards, TokenRequest API was introduced with the aim of introducing time bound, audience bound and onbject bound for the tokens created.

From v1.24 onwards, reduction of secret-based SA tokens.
- It will not create secret/token default.
- You must run kubectl command to create a token.
- kubectl create sa sa1
- kubectl create token token1

To create a non-expiring secret object, create secret yaml file and add the below annotation line in metadta section:
```
metadata:
  name:
  annotatations:
     kubernetes.io/service-account-name:sa1
```
 

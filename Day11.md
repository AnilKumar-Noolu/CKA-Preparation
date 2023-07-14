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

-Whenever SA is created, a token will be created. This token must be used by external application while authenticating with Kubernetes API.
-Tokens are stored as a secret object, U can usethis command while using curl command.
-If we have dashboard (or) prometheus deployed on Kubernetes itself as a Pod, then we configure them by mounting the serviceaccount token secret as a volume inside pod hosting 3-party application.

 

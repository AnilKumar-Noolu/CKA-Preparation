## Kubernetes Security Primitives
If there is a host that forms the cluster, then All access to these hosts must be secured.
1. Root access disabled.
2. Password based authentication disabled.
3. SSH-based authentication only should be available.

## CA Certificates
These are a pair of key and certificate files which we have generated.

Whoever have access to these pair of files can access any certificate for Kubernetes env.

If there are 1/2 users, we can sign requests manually, but as users increases and team grows, we need an better automated way for signing requests, as well as to rotate certificates when they expire. K8 has an built-in certificates API which can do this.

### Steps:
- Whenever admin receives a new CertificateSigingRequest
- - Admin instead of logging into Master Node, he creates:
  - CertificateSigningRequest Object
  - Review Requests
  - Approve Requests
  - Share certificates to Users.

All certificate related activities will be carried out by Controller Manager.

## KubeConfig:
A Kubeconfig is a YAML file with all the Kubernetes cluster details, certificates, and secret token to authenticate the cluster.
KubeConfig willbe stored default at $HOME/.kube/ location.

Whenever you want to query a cluster, you should write a command with name of cluster, key, certificates..... This is a tedious task.

So u move all this necessary information to a config file called kubeConfig file
` kubectl get pods --kubeConfig config`

KubeConfig file mainly consists of 3 sections i.e., Clusters, Contexts and Users
- You will be using existing users with existing Privileges
- Which user is going to access which cluster.

```
apiVersion: v1
clusters:
- cluster:
    certificate-authority-data: <ca-data-here>
    server: https://your-k8s-cluster.com
  name: <cluster-name>
contexts:
- context:
    cluster:  <cluster-name>
    user:  <cluster-name-user>
  name:  <cluster-name>
current-context:  <cluster-name>
kind: Config
preferences: {}
users:
- name:  <cluster-name-user>
  user:
    token: <secret-token-here>
```
In Cluster Section, you can mention the name of the cluster like dev, prod environments and certificate-authority-data and server specifications will be going to this Section.

In Context section, you will mention the user who are configured with the what cluster.

In Users Section, you will mention the users along with their client-certificate, client-keys or Tokens.

### Commands
kubectl config view   //Viewds current cluster and all details

kubectl config view --kubeconfig=my-custom-config   //Now, instead of default kubeConfig file, it will use my-custom-config specifed in command.

kubectl config use-context user1@Prod-env      // Now, it will override the current-context mentioned in kubeconfig file and will use context given in command line.

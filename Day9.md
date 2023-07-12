## Authorization
We want people to get only minimum level of access not full access to modify objects in Kubernetes Cluster.

There are various Authorization methods in Kubernetes such as Node Authoriser, Webhook, Always Allow, Always Deny, ABAC(Attribute based access control), RBAC(Role Based Access Control)

Generally in kube-apiserver, authorization mode will be mentioned like --authorization-mode=RBAC. If nothing is mentioned, it takes alwaysAllow by default.

## ABAC:
We need to provide users a Policy to create/view/delet Pods and pass them to the Kube-apiserver.

If there are multiple users, we need to create multiple policies. So it will be difficult and tedious to mange many users for any complex application deployed on Kubernetes Cluster.

## RBAC:
Instead of directly associating a user/group with a set of permissions, we define roles with set of permissions and associate them with the users.

In Kube-apiserver, we will mention the following command --authorization-mode=RBAC

Before knowing about role and rolebindings, we need to know about apiGroups, resources, Verbs.

apigroups in the sense api's are grouped into multiple groups such as /apps, /extensions,.networking.k8s.io, /certificates.k8s.io,...

Resources will be under apiGroups such as /pods, /deployments, /replicasets,...

Verbs are the actions which we will perform on the resources in apiGroups such as list, get, watch, create, delete, update...

## Roles
An RBAC Role contains rules that represent a set of permissions. Permissions are purely additive, only allow rules will be there.

A Role always sets permissions within a particular namespace; when you create a Role, you have to specify the namespace it belongs in.
```
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: default
  name: pod-reader
rules:
- apiGroups: [""] # "" indicates the core API group
  resources: ["pods"]
  verbs: ["get", "watch", "list"]
```
## RoleBindings
A role binding grants the permissions defined in a role to a user or set of users. It holds a list of subjects (users, groups, or service accounts), and a reference to the role being granted. 
A RoleBinding grants permissions within a specific namespace.
```
apiVersion: rbac.authorization.k8s.io/v1
# This role binding allows "jane" to read pods in the "default" namespace.
# You need to already have a Role named "pod-reader" in that namespace.
kind: RoleBinding
metadata:
  name: read-pods
  namespace: default
subjects:              # You can specify more than one "subject"
- kind: User
  name: jane           # "name" is case sensitive
  apiGroup: rbac.authorization.k8s.io
roleRef:               # "roleRef" specifies the binding to a Role / ClusterRole
  kind: Role           #this must be Role or ClusterRole
  name: pod-reader     # this must match the name of the Role or ClusterRole you wish to bind to
  apiGroup: rbac.authorization.k8s.io
```


### Commands
kubectl create -f role.yaml

kubectl create -f rolebinding.yaml

kubectl get role

kubectl get rolebinding

#### Check Access:
kubectl auth can-i create deploy     //If the output is yes, you have an access to craete deployments

kubectl auth can-i delete pods

kubectl 

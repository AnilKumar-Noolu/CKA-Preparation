## Persistent Volumes
If you have large environment with lot of users deploying lot of pods, users would have to configure storage everytime for each pod. 

So instead of that manual activity, you would like to manage storage more centrally.

A Persistent Volume is a cluster-wide pool of storage volumes configured by an administrator to be used by users deploying applications on clusters.
Then the users can selecet storage from this pool using Persistent Volume Claims(PVC).
```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-vol
spec:
  accessModes:
    - ReadWriteOnce
  capacity:
    storage: 1Gi
  hostpath:
    path: /data
    type: Directory
```

## Persistent Volume Claim
We will create PVC to make storage available to Pod.

Administrator creates set of PV and users will create PVC to use Storage.
```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 500Mi
```
There are 3 types of reclaim policies in PVC: `persistentVolumeReclaimPolicy: Retain | Delete | Recycle`
1. If policy seleceted is retain, then even if PVC is deleted the PV will still remain but it will not be available.
2. If policy selected is Recycle, then data in datavolume will be scrubbed before making it available to pther users.
3. You can also update Pod to use PVC as its storage.
```
spec:
  containers:
  volumes:
    - name: data
      persistentVolumeClaim:
        claimName: pvc
```

## Storage Class(SC)
When Pv uses aws-ebs or gcp, first we need to create that Disk in AWS before creating PV.

With SC, you can define a provisioner such as Google Storage that can automatically provision storage on Google storage and allocates to Pod when a claim is made.

With SC, u dont need to create PV manually, it will be created automatically by SC.
```
apiVersion: storage.k8s.io/v1
kind: Storage Class
metadata:
  name: google-storage
provisioner: kubernetes.io/gce-pd
```

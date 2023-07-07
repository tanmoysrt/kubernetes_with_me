We first need to create PV and then create a PVC and then can bind that with any POD. 

#### Persistent Volume [PV]

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: block-pv
spec:
  capacity:
    storage: 10Gi
  accessModes:
    - ReadWriteOnce
  volumeMode: Filesystem
  persistentVolumeReclaimPolicy: Retain
  hostPath:
    path: "/tmp/data1"
```

Allowed `accessModes` 
- ReadWriteOnce
- ReadWriteMany
- ReadOnlyMany

`persistentVolumeReclaimPolicy` can be either `Retain` or `Recycle` or `Delete`. in case of retain after pod detached it will be still there but can be use for new pods. in delete it will be deleted after used.

#### Persistent Volume Claim [PVC]

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: block-pv-claim
spec:
  accessModes:
    - ReadWriteOnce
  volumeMode: Filesystem
  resources:
    requests:
      storage: 8Gi
  storageClassName: ""
  selector:
    matchLabels:
      name: "block-pv"
    matchExpressions:
      - {key: environment, operator: In, values: [dev]}
```
`accessModes`, `storageClassName`, `volumeMode` need to be same as PV to provision storage.

#### Attach to POD
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: mypod
spec:
  containers:
    - name: myfrontend
      image: nginx
      volumeMounts:
      - mountPath: "/var/www/html"
        name: mypd
  volumes:
    - name: mypd
      persistentVolumeClaim:
        claimName: block-pv-claim
```

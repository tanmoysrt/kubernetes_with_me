#### We can get all events of a namespace
```bash
kubectl get events -n my-namespace
```

#### We can fetch a pods event also
```bash
kubectl get events -n my-namespace <pod_name>
```


> Can't fetch event of high level stuff

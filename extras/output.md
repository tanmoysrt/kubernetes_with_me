#### Custom columns
```bash
kubectl get pods  -o "custom-columns=NAME:.metadata.name,containers:.spec.containers[*].image"
```
> first out put json and then write this, same as jsonpath query

**We can also sort `--sort-by`**
```bash
kubectl get pods  -o "custom-columns=NAME:.metadata.name,containers:.spec.containers[*].image" --sort-by .metadata.name
```

#### Json path
```bash
kubectl get pods  -o jsonpath='{.items[*].spec.containers[*].image}'
```


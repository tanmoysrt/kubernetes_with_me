### Role vs ClusterRtole
- Role can be created for a single namespace only
- ClusterRole has no namespace, it's clusterwide access

---

### For Service Account

1. Create service account
   ```bash
   kubectl create serviceaccount svc-acc
   ```
2. Create Cluster Role
   ```bash
   kubectl create role pod-reader --verb=get,list,watch --resource=pods
   ```
3. Create Cluster Role Binding
   ```bash
   kubectl create svc-acc-binding --clusterrole=pod-reader --serviceaccount=svc-acc
   ```
   > If the serviceaccount in `acme` namespace we can write `--serviceaccount=acme:svc-acc`
   
   > We can use `--user`,`--group` and `--serviceaccount`
  
4. Verify access
   ```bash
   kubectl auth can-i create pods --as system:serviceaccount:<name>:<namespace>
   ```
   
---

### For normal user

- The process is same use `--user` . That's all
- To verify access
   ```bash
   kubectl auth can-i create pods --as <new_user>
   ```
---

### Register new user

1. Generate a private key
   ```bash
   openssl genrsa -out john.key 2048
   ```
2. Generate CSR 
   ```bash
   openssl req -new -key john.key -subj "/CN=john" -out john.csr
   ```
3. Generate base64 string
   ```bash
   cat ./john.csr | base64
   ```
3. Create Request
   ```yaml
   apiVersion: certificates.k8s.io/v1
   kind: CertificateSigningRequest
   metadata:
     name: john
   spec:
    groups:
     - system:authenticated
    usages:
     - digital signature
     - key encipherment
     - server auth
    request: <BASE64_CSR>
   ```
4. On creating the CSR, admin can either deny or approve the request

---

### CSR Manage
- View CSR
  ```bash
  kubectl get csr
  ```
- Approve CSR
  ```bash
  kubectl certificate approve john
  ```
- Deny CSR
  ```bash
  kubectl certificate deny john
  ```

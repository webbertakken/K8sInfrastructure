# cert-manager
#### Prereqs
- Helm should be installed locally
- Tiller should be installed and correctly configured on the cluster.

#### Install
```bash
$ helm install stable/cert-manager --name cert-manager --namespace kube-system
```

#### Certificate Authority Account Secret
Create secrets for `letsencrypt-prod`.
```bash
$ kubectl create secret generic letsencrypt-prod --namespace=default
```

#### ClusterIssuer
Deploy the ClusterIssuer
```bash
$ kubectl apply -f letsencrypt-prod.yml
```

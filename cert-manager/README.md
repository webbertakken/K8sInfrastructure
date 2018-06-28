# cert-manager
#### Prereqs
- Helm should be installed locally
- Tiller should be installed and correctly configured on the cluster.

#### Install
```bash
helm install stable/cert-manager --name cert-manager --namespace kube-system
```

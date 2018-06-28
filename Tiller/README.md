# Tiller
This readme assumes you have installed Helm (client for Tiller)

#### Security Context
Make sure you [know your security context](https://docs.helm.sh/using_helm/#understand-your-security-context) and act on it.
 
This is imperative for production-grade environments.

#### Install Tiller
Make sure you are connected to the desired cluster
```bash
kubectl config current-context
```
Then install Tiller on your cluster
```
helm init
```

#### Access control
Create service account
```bash
kubectl create serviceaccount tiller --namespace kube-system
```

Create cluster-role-binding for that service account
```bash
kubectl apply -f ./clusterrolebinding.yml
```

Use the service account
```
helm init --service-account tiller --upgrade
```


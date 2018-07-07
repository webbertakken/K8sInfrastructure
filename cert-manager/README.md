# cert-manager

## Prereqs
- Helm should be installed locally
- Tiller should be installed and correctly configured on the cluster.

## Install
```bash
$ helm install stable/cert-manager --name=cert-manager --namespace=cert-manager
```

## Usage
In order to begin issuing certificates, you will need to set up a ClusterIssuer
or Issuer resource (for example, by creating a 'letsencrypt-staging' issuer).

More information on the different types of issuers and how to configure them
can be found in our documentation:

https://cert-manager.readthedocs.io/en/latest/reference/issuers.html

For information on how to configure cert-manager to automatically provision
Certificates for Ingress resources, take a look at the `ingress-shim`
documentation:

https://cert-manager.readthedocs.io/en/latest/reference/ingress-shim.html

## Example
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

## Delete
```bash
$ helm delete --purge cert-manager
```


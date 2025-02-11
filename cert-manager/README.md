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

## Example usage
#### Certificate Authority Account Secret
Create secrets for `letsencrypt-prod`.

This will store the account once created by cert-manager.
```bash
$ kubectl create secret generic letsencrypt-prod --namespace=default
```

#### ClusterIssuer
Deploy the ClusterIssuer

___Note:__ change the email address in `letsencrypt-prod.yml`._ 
```bash
$ kubectl apply -f letsencrypt-prod.yml
```
___Note 2:__ i'm still looking for a way to make this yaml-file generic, without putting email address in a secret, since it masks the value._

## Delete
```bash
$ helm delete --purge cert-manager
```


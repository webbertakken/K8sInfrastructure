# nginx-ingress

## Install
Install nginx-ingress in it's own namespace.
```
helm install --name=prod-ingress --namespace=nginx-ingress stable/nginx-ingress
```

## Usage
An example Ingress that makes use of the controller:
```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  annotations:
    kubernetes.io/ingress.class: nginx
  name: example
  namespace: foo
spec:
  rules:
    - host: www.example.com
      http:
        paths:
          - backend:
              serviceName: exampleService
              servicePort: 80
            path: /

  # This section is only required if TLS is to be enabled for the Ingress
  tls:
      - hosts:
          - www.example.com
        secretName: example-tls
```

If TLS is enabled for the Ingress, a Secret containing the certificate and key must also be provided:

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: example-tls
  namespace: foo
data:
  tls.crt: <base64 encoded cert>
  tls.key: <base64 encoded key>
type: kubernetes.io/tls
```

When using cert-manager this secret can be created using a Certificate:
```yaml
apiVersion: certmanager.k8s.io/v1alpha1
kind: Certificate
metadata:
  name: example-certificate
spec:
  secretName: example-tls
  dnsNames:
  - foo.example.com
  - bar.example.com
  acme:
    config:
    - ingressClass: nginx
      domains:
      - foo.example.com
      - bar.example.com
  issuerRef:
    name: letsencrypt-prod
    # The default value is Issuer (i.e. a locally namespaced Issuer)
    # A ClusterIssuer can be used across all cluster namespaces.
    kind: ClusterIssuer
```



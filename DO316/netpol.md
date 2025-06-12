```
kind: NetworkPolicy
apiVersion: networking.k8s.io/v1
metadata:
  name: netpol-http
  namespace: banana
spec:
  podSelector:
    matchLabels:
      env: production
  ingress:
    - ports:
        - protocol: TCP
          port: 443
        - protocol: TCP
          port: 80
      from:
        - podSelector: {}
          namespaceSelector:
            matchLabels:
              name: client-ns
    - {}
  policyTypes:
    - Ingress
```

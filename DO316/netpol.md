```
kind: NetworkPolicy
apiVersion: networking.k8s.io/v1
metadata:
  name: netpol-http
  namespace: banana
  uid: f89b440c-ea46-444d-ba90-bf7e7d2b3df1
  resourceVersion: '934199'
  generation: 1
  creationTimestamp: '2025-06-12T11:39:15Z'
  managedFields:
    - manager: Mozilla
      operation: Update
      apiVersion: networking.k8s.io/v1
      time: '2025-06-12T11:39:15Z'
      fieldsType: FieldsV1
      fieldsV1:
        'f:spec':
          'f:ingress': {}
          'f:podSelector': {}
          'f:policyTypes': {}
spec:
  podSelector:
    matchLabels:
      app: myvm-lan1
  ingress:
    - ports:
        - protocol: TCP
          port: 80
        - protocol: TCP
          port: 443
      from:
        - podSelector: {}
          namespaceSelector:
            matchLabels:
              name: client-ns
  policyTypes:
    - Ingress
```

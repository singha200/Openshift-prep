# Create secret with named `ex280-secret` in `cloud` project. The key name should be `environment` and the value of key should be `production`
```
oc project cloud
```
```
oc create  secret generic ex280-secret --from-literal=environment=production
```

```
oc describe secret ex280-secret
```

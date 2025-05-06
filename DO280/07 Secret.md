# Create secret with named `ex280-secret` in `cloud` project. The key name should be `MYSQL_ROOT_PASSWORD` and the value of key should be `redhat`
```
oc project cloud
```
```
oc create  secret generic ex280-secret --from-literal=MYSQL_ROOT_PASSWORD=redhat
```

```
oc describe secret ex280-secret
```

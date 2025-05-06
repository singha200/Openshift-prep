# Question: Create Resources Quota with below information for project `beta`
- Quota Name is `ex280-quota`
- Maximum  Pods `7` and Service ip `6` and Replication Controller `5` 
- Memory `1G` and cpu core is `1`
--- 
## Solution:

### Go to the project first.
```
oc project beta
```
### Check the quota.
```
oc get quota
```
### Now, create the quota.
```
oc create quota ex280-quota  --hard=memory=1Gi,cpu=1,pods=7,services=6,replicationcontrollers=5
```

### Post Check for quota.
```
oc get quota
```

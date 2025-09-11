## Prepare the lab.
```

```


# Question: You need to give ReadOnly access of your OPC cluster to `punit` user so that we can monitor all the resources.
For this, you need to create a client certificate that allows the `punit` user to examine everything in the cluster but does not allow the `punit` user to make any changes.
 
- A client certificate exists with the username: `punit`
- A group exists with the name: `cluster-monitoring-app`
- Members of this group have access to the cluster role: `cluster-reader`
- The client certificate you can download from below link.
- The client certificate must not be able to create or delete projects
- The client certificate must be able to view all pods in the cluster
---



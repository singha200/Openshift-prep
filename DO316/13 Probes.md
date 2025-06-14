# Configure a liveness probe
- Configure a liveness probe for the `mariadb-server` VM in the `apple` project and make sure following conditions are true:
- The liveness probe tests the database server at TCP Port 3306
- The time (in seconds) after the VM instance starts before the liveness probe is initiated is 100
- The delay in seconds between performing probes is 5
- download the yum.repo file to `mariadb-server` VM from "sudo curl -o /etc/yum.repos.d/yum.repo-file.repo https://raw.githubusercontent.com/anishrana2001/Openshift/refs/heads/main/DO316/yum.repo-file.repo"
---

## Solution.
# How to add Liveness Probe
## First, we can create a dummy deploy/test. Where the pods will be created or not, no worries.
```
oc create deployment test --image=nginx
oc set probe --help | grep url
```

### Now, you can search the parameters of probe command.
```
oc set probe  --help | grep tcp
oc set probe deployment test --liveness --open-tcp=3306 --initial-delay-seconds=100 --period-seconds=5
```

### Get the details of probe from deployment.
```
oc get deployment test -o  yaml | grep -iA 10 liveness
```

        livenessProbe:
          failureThreshold: 3
          initialDelaySeconds: 100
          periodSeconds: 5
          successThreshold: 1
          tcpSocket:
            port: 3306
          timeoutSeconds: 1


### Now, you need to edit these details on the VM `mariadb-server`
```
oc edit vm mariadb-server
```
## Make sure the indentation is correct. architecture, livenessProbe and domain should be on same Indentation. See the below
![image](https://github.com/user-attachments/assets/65f04432-92cf-4448-8230-199e12d5eb00)



### Or you can use this command, if you have this file. 
```
[student@workstation ~]$ cat /tmp/liveness.yaml
spec:
  template:
    spec:
        livenessProbe:
          failureThreshold: 3
          initialDelaySeconds: 100
          periodSeconds: 5
          successThreshold: 1
          tcpSocket:
            port: 3306
          timeoutSeconds: 1
```

```
oc patch vm/mariadb-server --type=merge /tmp/liveness.yaml
```	


### Need to restart the VM.
```
virtctl restart mariadb-server
oc get vmi mariadb-server
```

### Once vm up, go to the console.
```
virtctl console mariadb-server
```
### Enter the credentials.

```
Credentials : root/redhat

systemctl stop mysql
```
### Logout.
## mariadb-server VM should be restarted due to liveness probe


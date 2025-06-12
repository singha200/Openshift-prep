## Preppare the lab for this question.

```
lab start accessing-guicreate
oc login -u admin -p redhatocp https://api.ocp4.example.com:6443
sudo ssh-keygen -t rsa -q -f "/home/devops/.ssh/id_rsa" -N ""
oc create secret generic ssh-key --from-file=public-key=/tmp/devops-id_rsa.pub -n banana
```

# Create a VirtualMachine in the `banana` project with below requirements. 
- Create a VirtualMachine called `myvm-lan1` from template "Red Hat Enterprise Linux 9 VM"
- Use PVC URL, `http://utility.lab.example.com:8080/openshift4/images/rhel9-helloworld.qcow2`
-  The StorageClassName is `ocs-external-storagecluster-ceph-rbd-virtualization`
-  The PVC size should be 30GiB
-  The Volume mode should be Block.
-  The workload type is the VirtualMachine is `server`
-  The flavor type of the VirtualMachine is `small`
-  The network interface name is `default`
-  The user raja with password "anishrana2001" exists in the cloud-init definition
-  The ssh Key "/home/devops/.ssh/id_rsa.pub" from user devops at workstation has been added as an authorized ssh key via the cloud-init definition

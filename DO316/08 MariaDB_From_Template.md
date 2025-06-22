# Create a VirtualMachine Template
  - Create a project `kiwi` and a VirtualMachine template according to the following requirements
  - The Template name is `tmprhl9small` in the `kiwi` project
  - The Template is clone of the build-in rhel9-server-small template
  - Flavor small, with 1 CPU and 2Gi RAM
  - Storage space is 10Gi
  - Disk source rhel-9.2-x86_64-kvm.qcow2 provided at  http://utility.lab.example.com:8080/openshift4/images/mariadb-server.qcow2
  - storageCLassName: `ocs-external-storagecluster-ceph-rbd-virtualization`
  - The user `rahul` can login to these VirtualMachines on the console with password `anishrana2001`
  - The user `vinod` can login to these vitual machines via SSH without a password by using /home/opsdam/.ssh/id_rsa_ex316.pub key on workbench.example.com
  - When instantiated, these vitual machine will install the `httpd` RPM which is available from https://raw.githubusercontent.com/anishrana2001/Openshift/refs/heads/main/DO316/yum.repo-file.repo
  ---

  ### Solution:

```
oc new-project kiwi
```


```
sudo yum install httpd --allowerasing
```

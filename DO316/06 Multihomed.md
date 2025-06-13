# Deploy a Multihomed VirtualMachine
- Create a VM called `mariadb-server` from template `RedHat Linux 9.2 VirtualMachine` with 2 Network interfaces in `apple` project.
- The Workload type of the VirtualMachine is `server` and flavor is `small`.
- The user suraj creates the VirtualMachine `mariadb-server`
- The user suraj with password "anishrana2001" should exists in the cloud-init definition.
- The ssh Key /home/opsadm/.ssh/id_rsa_ex316.pub from user opsadm at workbench.lab.example.com has been added as an authorized ssh key via the cloud-init definition

## Storage Configuration
- The Image used to Create the Persistemt volume claim for the VirtualMachine boot source is http://utility.lab.example.com:8080/openshift4/images/rhel9-helloworld.qcow2
- The StorageClassName is `ocs-external-storagecluster-ceph-rbd-virtualization`
- The PVC size is 10Gi

## The first Network Interface configuration:
	- The first Network interface name is default
	- The First Network ineterface is attached to the pod networking (default) network
	- The first network interface type is masquerade
	- The model for the first network interface is virtio

## The Second Network Interface Configuration:
	- The second network interface name is `nic-0`
	- The second network interface is attached to the `apple/database-network` network
	- The second network interface type is `bridge`
	- The IP address of the second network interface is provided by OpenShift
	- The model for the second network interface is virto


### Solution:
### As per question, we need to add the 2nd interface, it means that first, we need to install the operator ""
### Suraj user must able to create the VM "mariadb-server", In Question 3, we have already gave the rights to this user.
### Switch to `suraj` user on console and create a VM from "RHEL 9.2, server, small" template with using mentioned PVC URL.



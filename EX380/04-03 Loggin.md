### You need to Install the OpenShift Logging operator and configure log forwarding to the syslog server according to the following specifications:

  - The log collector type must be 'vector'
  - Application and infrastructure logs must be forwarded to the syslog server on host 'tcp://utility.lab.example.com:514'
  - Audit logs must be forwarded to the syslog server on host 'tcp://utility.lab.example.com:514'


  - Application logs are tagged with procID: app
  - Infrastructure logs are tagged with msgID: app

  - Infrastructure logs are tagged with procID: infra
  - Infrastructure logs are tagged with msgID: infra

  - Audit logs are tagged with procID: audit
  - Audit logs are tagged with msgID: audit

  - All logs are tagged with appName: ocp-lab
  - All logs are tagged with msgID: audit

  - Deploy the Event Router component to capture Kubernetes events.

The syslog servers have already been fully configured for you to receive logging messages and filter them using the 'msgID' attribute to the following files:

  - /var/log/app.log
  - /var/log/infra.log
  - /var/log/audit.log

You may verify that the audit logs from the cluster nodes are forwarded to the syslog server by login into the 'utility' server with 'root' username.  

You can login Other to one master01 node to check the logs. 
'ssh core@master01.ocp4.example.com'

---

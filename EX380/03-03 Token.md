## Prepare the lab.
```
oc create sa sa-monitoring-user
```


# Question: You need to give ReadOnly access of your OPC cluster to `punit` user so that we can monitor all the resources.
For this, you need to create a client certificate that allows the `punit` user to examine everything in the cluster but does not allow the `punit` user to make any changes.
 
- A client certificate exists with the username: `mon-punit`
- A group exists with the name: `cluster-monitoring-app`
- Members of this group have access to the cluster role: `cluster-reader`
- The client certificate you can download from below link.
- The client certificate must not be able to create or delete projects
- The client certificate must be able to view all pods in the cluster


## You can download the dummy csr file from below link.
https://raw.githubusercontent.com/anishrana2001/Openshift/refs/heads/main/EX380/dummy-csr-0303-token.yaml
---
## Solution:

```
[student@workstation ~]$ oc adm groups new cluster-monitoring-app
group.user.openshift.io/cluster-monitoring-app created

[student@workstation ~]$ oc adm groups add-users cluster-monitoring-app  mon-punit
group.user.openshift.io/cluster-monitoring-app added: "mon-punit"


[student@workstation ~]$ oc get clusterrole cluster-reader
NAME             CREATED AT
cluster-reader   2024-03-05T20:06:28Z


[student@workstation ~]$ oc adm policy add-cluster-role-to-group cluster-reader cluster-monitoring-app
clusterrole.rbac.authorization.k8s.io/cluster-reader added: "cluster-monitoring-app"

[student@workstation ~]$ mkdir test
[student@workstation ~]$ cd test/


[student@workstation test]$ openssl req -newkey rsa:4096 -nodes  -keyout monitoing.key -subj "/O=cluster-monitoring-app/CN=mon-punit"  -out mon-csr....+......+...+.....+..........+.....+......+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++*.+..+...+....+........+.+.....+..........+..+...+.......+..............+.+............+...+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++*....+.........+....+.....+.+...........+.............+.....+.......+...+..+....+......+.........+..+...+....+..+...+...+.........+.........+......+....+..+.........+...+......................+.....+...+.+.....+.......+........+......+...+................+...............+.........+...........+....+...............+......+......+....................+.+.....+.......+........+............+.+.........+...........+.......+.....+...+.+...+............+.........+..+....+...............+.........+..............+..............................+.......+......+.........+.....+......+...+...............+......+.+........+....+.....+..........+............+...............+........+.+...........+...+..........+........+....+.........+..+.......+...+.....+....+...+..+..................+...+....+.....+.........+.......+..+.+......+......+........+.+...+...............+..+.+..................+......+.........+...........+....+...........+...+...+....+...+........+....+.........+.....+.........+.......+...+......+.....+.........+.+..+...+......+.........+.+.....+...+.+....................+.+...+..................+..+.+..+.............+.....+....+........+.......+..+..........+.....+.........+....+...+.........+..................+..+.+.....+.......+..+....+.....+....+.....+..........+...........................+...+........+...+.+...+...........+......+...+.+.................+..................+.+.....+...+.............+...+......+...+........+...+...................+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
....+......+.+............+..+...+...+....+.....+....+..............+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++*................+.+...+......+.....+.+......+........+......+...+...+..........+...............+..+.+..+....+...+........+....+........+.+..+.......+...+...+......+.....+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++*.........................+..+.............+.....+.........+.+............+...............+...+.....+.......+.....+....+...+.....+...+....+..............+......+.+..............+.+.....+....+...+...+.....+...+......+......+.......+............+...+..................+..+.+......+...+...+..+.+............+.........+...+.....+......+......+.............+.....+.+.........+........+...+.+......+........+.+........................+.........+...+.....+...+..........+..............+.......+........+...+.......+.....+......+....+..+.........+.+.........+......+...+............+.........+............+..+.......+.....+....+.....+............+.......+......+...........+....+.....+......+.............+...........+.........+.+......+..................+............+......+..+.......+........+...+...+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
-----
[student@workstation test]$ 

[student@workstation test]$ cat mon-csr 
-----BEGIN CERTIFICATE REQUEST-----
MIIEejCCAmICAQAwNTEfMB0GA1UECgwWY2x1c3Rlci1tb25pdG9yaW5nLWFwcDES
MBAGA1UEAwwJbW9uLXB1bml0MIICIjANBgkqhkiG9w0BAQEFAAOCAg8AMIICCgKC
AgEAqZfIKcpJjlF3QKjuFrBp8RwGpPLP4BoPm0eDiQsGvl1HrVhR6Hd9+JBeWbua
5rbvv16kk0l/rBa6LxZqO7Yf/9eQCGk1JZDtJI8Ag93B0/G8Ps3c4g4CKPZnQ5Aa
fpowvZPPe1cXTyM1Fn0cT0tnbAuLXCTGCujVU3pMX4OzaYTpuuVxMYZpGV/4k2Q1
b3aQoKZqDWwHWFuY+FETPuniESsRM6HCKdxWt+V5rO89BBygeFv3SEs5VZp4PlJE
CDGLzmbFkGaSppqgQ3jfYhZFIAxU6KASRf5aVNcHQlYLDDDkB8682ffkDWAWfQIo
6a9UU+6vk9XMhTubggHsRPqpWP5j79cA2ij+gzQ03zgAdIgxy6tQpGFag6+L6l68
y9Az39eO41qJo3s91Z5M5o9b3mYFKx0KCZQPf+uoLRXTPXewdOwEXbEvX8c+Zmkx
Ra+7nzO/l4VFrBuUpjvRAQ1u+foOkBwtxvp/lsNfHRVHeZYbvkbHfrHrlsf9ZErC
wpOEddx+T/PrP9K4wyC2WydTevhjgGYvDR29y3Eba6+ATr/Pw49szt6SUPZ/oQmn
Tf+kA1Jd6m9vyUmzK5E62d7h5hBHfxcbRaJhUZvTJsuwFv7Znc+ETYrrdKVkon91
TUcrRVcoaCX5yoOgxZ9ozpvY+btetO+kJjcez1g/x4ziFTcCAwEAAaAAMA0GCSqG
SIb3DQEBCwUAA4ICAQA68HtksMEVrrUw2BmtfLCM1wIInmX7toEBqZ6Cg8P6Neh+
/Hdm+PJrIt3u92ttxDVXz/+NQCc2j9EcJVJQMlYNlr5ZRlCQyTdyD0C1K/QNz98d
3X9NF/fPymq7gKmiDtzqfcv1YskdPE6IyVt1tUmZQDIr70jNuKUccYURuEbyVCMm
zRs4Q+aRfygI+wS2nLzUHorr/1qpTwcAr80bZ7UVu1scNl45VYMMq9125yO+o1AM
QHsR+k2s/jqX+7XA5p1sWAGtZ32znD6LvtlKn6ecUwXPlrfRwGCURQN3Ma7tmvri
xQGnRw5tHfpKGpT7TTEpUiWKThrtWXtZhDOlksXfIzQ2skVm4DaKfpj4irHGA9el
4/bS6IUStWnktFkKx4vP65RK7D9E4m1eOIP8iUPAq5h4cIZ9wQMLr9eaLgDlp2z6
y6LsVyf3xKs08yuADcNPZ0Vrnux67GqMIBnI9EkH1MnRV9o1WrEM2Gw5WAJrFG+T
gbB1qkAG/TO8H4QBN6M5G27vj6/gbYqskQanC3XEGTCVmN4EKMF+4uVEGB2KLBrr
ppKPaYkQlAG9/ohB5zKvg8vrksEh/abvRy575J5oeyr5hs8/+Df1u4UsR5LSXWKp
ROoQV+Q7FAi/hvGdlufghZ+bcfLKJjmmhjZnOkd0b0QbEP/wSu4IWLUMwsjmwA==
-----END CERTIFICATE REQUEST-----


[student@workstation test]$ base64 -w0 mon-csr ; echo 
LS0tLS1CRUdJTiBDRVJUSUZJQ0FURSBSRVFVRVNULS0tLS0KTUlJRWVqQ0NBbUlDQVFBd05URWZNQjBHQTFVRUNnd1dZMngxYzNSbGNpMXRiMjVwZEc5eWFXNW5MV0Z3Y0RFUwpNQkFHQTFVRUF3d0piVzl1TFhCMWJtbDBNSUlDSWpBTkJna3Foa2lHOXcwQkFRRUZBQU9DQWc4QU1JSUNDZ0tDCkFnRUFxWmZJS2NwSmpsRjNRS2p1RnJCcDhSd0dwUExQNEJvUG0wZURpUXNHdmwxSHJWaFI2SGQ5K0pCZVdidWEKNXJidnYxNmtrMGwvckJhNkx4WnFPN1lmLzllUUNHazFKWkR0Skk4QWc5M0IwL0c4UHMzYzRnNENLUFpuUTVBYQpmcG93dlpQUGUxY1hUeU0xRm4wY1QwdG5iQXVMWENUR0N1alZVM3BNWDRPemFZVHB1dVZ4TVlacEdWLzRrMlExCmIzYVFvS1pxRFd3SFdGdVkrRkVUUHVuaUVTc1JNNkhDS2R4V3QrVjVyTzg5QkJ5Z2VGdjNTRXM1VlpwNFBsSkUKQ0RHTHptYkZrR2FTcHBxZ1EzamZZaFpGSUF4VTZLQVNSZjVhVk5jSFFsWUxERERrQjg2ODJmZmtEV0FXZlFJbwo2YTlVVSs2dms5WE1oVHViZ2dIc1JQcXBXUDVqNzljQTJpaitnelEwM3pnQWRJZ3h5NnRRcEdGYWc2K0w2bDY4Cnk5QXozOWVPNDFxSm8zczkxWjVNNW85YjNtWUZLeDBLQ1pRUGYrdW9MUlhUUFhld2RPd0VYYkV2WDhjK1pta3gKUmErN256Ty9sNFZGckJ1VXBqdlJBUTF1K2ZvT2tCd3R4dnAvbHNOZkhSVkhlWllidmtiSGZySHJsc2Y5WkVyQwp3cE9FZGR4K1QvUHJQOUs0d3lDMld5ZFRldmhqZ0dZdkRSMjl5M0ViYTYrQVRyL1B3NDlzenQ2U1VQWi9vUW1uClRmK2tBMUpkNm05dnlVbXpLNUU2MmQ3aDVoQkhmeGNiUmFKaFVadlRKc3V3RnY3Wm5jK0VUWXJyZEtWa29uOTEKVFVjclJWY29hQ1g1eW9PZ3haOW96cHZZK2J0ZXRPK2tKamNlejFnL3g0emlGVGNDQXdFQUFhQUFNQTBHQ1NxRwpTSWIzRFFFQkN3VUFBNElDQVFBNjhIdGtzTUVWcnJVdzJCbXRmTENNMXdJSW5tWDd0b0VCcVo2Q2c4UDZOZWgrCi9IZG0rUEpySXQzdTkydHR4RFZYei8rTlFDYzJqOUVjSlZKUU1sWU5scjVaUmxDUXlUZHlEMEMxSy9RTno5OGQKM1g5TkYvZlB5bXE3Z0ttaUR0enFmY3YxWXNrZFBFNkl5VnQxdFVtWlFESXI3MGpOdUtVY2NZVVJ1RWJ5VkNNbQp6UnM0USthUmZ5Z0krd1Mybkx6VUhvcnIvMXFwVHdjQXI4MGJaN1VWdTFzY05sNDVWWU1NcTkxMjV5TytvMUFNClFIc1IrazJzL2pxWCs3WEE1cDFzV0FHdFozMnpuRDZMdnRsS242ZWNVd1hQbHJmUndHQ1VSUU4zTWE3dG12cmkKeFFHblJ3NXRIZnBLR3BUN1RURXBVaVdLVGhydFdYdFpoRE9sa3NYZkl6UTJza1ZtNERhS2ZwajRpckhHQTllbAo0L2JTNklVU3RXbmt0RmtLeDR2UDY1Uks3RDlFNG0xZU9JUDhpVVBBcTVoNGNJWjl3UU1McjllYUxnRGxwMno2Cnk2THNWeWYzeEtzMDh5dUFEY05QWjBWcm51eDY3R3FNSUJuSTlFa0gxTW5SVjlvMVdyRU0yR3c1V0FKckZHK1QKZ2JCMXFrQUcvVE84SDRRQk42TTVHMjd2ajYvZ2JZcXNrUWFuQzNYRUdUQ1ZtTjRFS01GKzR1VkVHQjJLTEJycgpwcEtQYVlrUWxBRzkvb2hCNXpLdmc4dnJrc0VoL2FidlJ5NTc1SjVvZXlyNWhzOC8rRGYxdTRVc1I1TFNYV0twClJPb1FWK1E3RkFpL2h2R2RsdWZnaForYmNmTEtKam1taGpabk9rZDBiMFFiRVAvd1N1NElXTFVNd3NqbXdBPT0KLS0tLS1FTkQgQ0VSVElGSUNBVEUgUkVRVUVTVC0tLS0tCg==
[student@workstation test]$ 

[student@workstation test]$ cat dummy-csr.yaml 
apiVersion: certificates.k8s.io/v1
kind: CertificateSigningRequest
metadata:
  name: @
spec:
  signerName: kubernetes.io/kube-apiserver-client
  expirationSeconds: 604800  # one week
  request: @
  usages:
  - client auth
[student@workstation test]$ 

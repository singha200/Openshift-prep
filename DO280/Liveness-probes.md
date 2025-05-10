## Creation of lab.
```
oc new-project tuesday
```


# Start a Probe 
- Create a `Liveliness` Health Probe in project `tuesday` which has 1 pod running
- With port `8443`
- Initial delay of `3 sec`
- Time out for the probe is `10 sec`
- Probe must survive atleast `3` crash

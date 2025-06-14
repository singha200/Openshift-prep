### Prepare the lab for this question.
```
oc label nodes worker01 datacenter=paris
oc label nodes worker02 datacenter=paris
```

# Configure VirtualMachine migration
- Configure the VirtualMachine migration so that the following condition are true:
- The VirtualMachine `mariadb-server` in the project `apple` is able to migrate between the nodes with label `datacenter: paris`
- The VirtualMachine `mariadb-server` in the Project `apple` is not able to migrate to any other nodes
---

### Solution:

### 

![image](https://github.com/user-attachments/assets/8f2890fd-1430-4cc2-b4e3-5c47dff7902c)

## In the key and value, use the label given in the question.
![image](https://github.com/user-attachments/assets/fa0dfeef-58cb-4d86-8a4a-87fe5197b3b6)

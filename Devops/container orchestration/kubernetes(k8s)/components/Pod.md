---
date updated: '2021-08-28T20:37:00+07:00'

---

# Pod

- Pod can contains multiple containers

## Example

```yml
apiVersion: v1  
kind: Pod  
metadata:  
name: chef-server  
spec:  
containers:  
 - name: chef-server  
 image: chef/chefdk  
 command: ["/bin/sh"]  
 args: ["-c", "echo Hello from the Ubuntu container; sleep 1000"]
```

## Command

- Get all pods

```shell
kubectl get pods
```

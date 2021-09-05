---
date updated: '2021-08-28T20:37:00+07:00'

---

# Pod

- Pod can contains single or multiple containers.
- Pods should be labeled (for e.g: `app: nginx`)

## Example

```yml
apiVersion: v1  
kind: Pod  
metadata:  
	name: chef-server
	label:
		env: dev
spec:  
	containers:  
	 - name: chef-server  
		 image: chef/chefdk  
		 command: ["/bin/sh"]  
		 args: ["-c", "echo Hello from the Ubuntu container; sleep 1000"]
```

## Interacting with pod

- Get all pods

```shell
kubectl get pods
```

- Describe a pod

```shell
kubectl describe pod <pod-name> -o yaml
```

- Executing pod
```
kubectl exec -it <pod-name> /bin/sh
```

- Getting follow-up log of pod

```shell
kubectl logs -f <pod-name>
```

- Delete pod

```
kubectl delete <pod-name>
```



## Managing resource 

1 core = 1000 milicore


## Probe

### Liveness probe

- check if a container is still alive
- **restart if failed**
- map to column `RESTART`
-  Type of readiness probe:
	-  An Exec probe, where a process is executed. The container’s status is deter- mined by the process’ exit status code.
	- An HTTP GET probe, which sends an HTTP GET request to the container and the HTTP status code of the response determines whether the container is alive or not.
	- A TCP Socket probe, which opens a TCP connection to a specified port of the container. If the connection is established, the container is considered alive.
- Example:
```yaml
apiVersion: v1
kind: Pod
metadata:
  labels:
    test: liveness
  name: liveness-http
spec:
  containers:
  - name: liveness
    image: k8s.gcr.io/liveness
    args:
    - /server
    livenessProbe:
      httpGet:
        path: /healthz
        port: 8080
        httpHeaders:
        - name: Custom-Header
          value: Awesome
      initialDelaySeconds: 3
      periodSeconds: 3
```

- Tips: 
	- `initialDelaySeconds` should be set because when container starts, it takes a time to boot up
	-  the liveness probe should only bec check status of service & internal component like database, cache. It should be light


### Readiness probe
-  Invoked periodically(every 10 seconds by default) and determines whether the specific pod should receive client requests or not.** When a container’s readiness probe returns success, it’s signaling that the container is ready to accept requests. Otherwise, it will be remove if it belongs to service**
-  status is mapped to column `READY`
- Type of readiness probe:
	-  An Exec probe, where a process is executed. The container’s status is deter- mined by the process’ exit status code.
	- An HTTP GET probe, which sends an HTTP GET request to the container and the HTTP status code of the response determines whether the container is ready or not.
	- A TCP Socket probe, which opens a TCP connection to a specified port of the container. If the connection is established, the container is considered ready.
- UNDERSTANDING THE OPERATION OF READINESS PROBES: When a container is started, Kubernetes can be configured to wait for a configurable amount of time to pass before performing the first readiness check. After that, it invokes the probe periodically and acts based on the result of the readiness probe. If a pod reports that it’s not ready, it’s removed from the service. If the pod then becomes ready again, it’s re-added.
- Example
```yml
	apiVersion: v1
	kind: Pod
	metadata:
		name: goproxy
		labels:
			app: goproxy
	spec:
		containers:
		- name: goproxy
			image: k8s.gcr.io/goproxy:0.1
			ports:
			- containerPort: 8080
				readinessProbe:
					tcpSocket:
						port: 8080
					initialDelaySeconds: 5
					periodSeconds: 10
```
- Tips: 
	- `initialDelaySeconds` should be set because when container starts, it takes a time to boot up

# Kubernetes cheatsheet


## Pod
- Container one or mutiple containers
-  Example

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

### Resource

### Liveness and Readiness Probe

#### Liveness

- To determine the application is healthy or not to decide restart the pod

- Can be `http`, `command` or `tcp`
- Example

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

#### Readiness

- To determine the application ready to accept the traffic ( = ready)
- Can be `http`, `command` or `tcp`
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
    livenessProbe:
      tcpSocket:
        port: 8080
      initialDelaySeconds: 15
      periodSeconds: 20
```
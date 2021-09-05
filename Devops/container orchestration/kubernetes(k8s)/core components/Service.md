---
date updated: '2021-08-28T20:37:10+07:00'

---

# Service

A Kubernetes Service is a resource you create to make a single, constant point of entry to a group of pods providing the same service. Each service has an IP address and port that never change while the service exists. Clients can open connections to that IP and port, and those connections are then routed to one of the pods backing that service

## Example

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  selector:
    app: MyApp
  ports:
    - protocol: TCP
      port: 80
      targetPort: 9376
```

The above example will gather all pod whose  label `app: MyApp` and proxy all `TCP 80` (of service) to `TCP 9376` of pod (through `targetPort`)

A service can expose multiple ports

## Discovering Service

### Environment variable

From all pod in the same namespace, you can use the environment varialble to discovering service.

For example, the Service `redis-master` which exposes TCP port 6379 and has been allocated cluster IP address 10.0.0.11, produces the following environment variables:

```shell
REDIS_MASTER_SERVICE_HOST=10.0.0.11
REDIS_MASTER_SERVICE_PORT=6379
REDIS_MASTER_PORT=tcp://10.0.0.11:6379
REDIS_MASTER_PORT_6379_TCP=tcp://10.0.0.11:6379
REDIS_MASTER_PORT_6379_TCP_PROTO=tcp
REDIS_MASTER_PORT_6379_TCP_PORT=6379
REDIS_MASTER_PORT_6379_TCP_ADDR=10.0.0.11
```

### Service Endpoint

You can access the endpoint throgh the following FQDN endpoint (which has been resolved by kube-dns)

    <servie-name>.<namespace>.svc.cluster.local

For example: `my-service.default.svc.cluster.local`.

Even you can emit `svc.cluster.local`, then the endpoint now `<service-name>.<namespace>`

## Service Type

- `ClusterIP`: Exposes the Service on a cluster-internal IP. Choosing this value makes the Service only reachable from within the cluster. This is the default `ServiceType`.
- `NodePort`: Exposes the Service on each Node's IP at a static port (the `NodePort`). A `ClusterIP` Service, to which the `NodePort` Service routes, is automatically created. You'll be able to contact the `NodePort` Service, from outside the cluster, by requesting `<NodeIP>:<NodePort>`.
- `LoadBalancer` Exposes the Service externally using a cloud provider's load balancer. `NodePort` and `ClusterIP` Services, to which the external load balancer routes, are automatically created.

### ClusterIp

Default Service Type of Service. Only reach in your K8s cluster

### NodePort

- To expose your service to outsite with specified port

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  type: NodePort
  selector:
    app: MyApp
  ports:
      # By default and for convenience, the `targetPort` is set to the same value as the `port` field.
    - port: 80
      targetPort: 80
      # Optional field
      # By default and for convenience, the Kubernetes control plane will allocate a port from a range (default: 30000-32767)
      nodePort: 30007
```

### LoadBalancer

- To support load balancer in cloud (like AWS ALB)

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  selector:
    app: MyApp
  ports:
    - protocol: TCP
      port: 80
      targetPort: 9376
  clusterIP: 10.0.171.239
  type: LoadBalancer
status:
  loadBalancer:
    ingress:
    - ip: 192.0.2.127
```

## Session Affinity

To makes the service proxy redirect all requests originating from the same client IP to the same pod, you can set the service’s sessionAffinity property to **ClientIP** (instead of None, which is the default)

```yaml
apiVersion: v1
kind: Service
spec:
  sessionAffinity: ClientIP
```

Kubernetes supports only two types of service session affinity: None and ClientIP.

---
date updated: '2021-08-23T21:47:26+07:00'

---

# Circuit Breaker

```yml
apiVersion: networking.istio.io/v1alpha3
kind: DestinationRule
metadata:
  name: serviceC
spec:
  host: serviceC
  subsets:
    - name: serviceC-v1
      labels:
        version: v1
    - name: serviceC-v2
      labels:
        version: v2
      trafficPolicy:
        connectionPool:
          http:
            http1MaxPendingRequests: 10
            maxRequestsPerConnection: 1
          tcp:
            maxConnections: 1
        outlierDetection:
            baseEjectionTime: 20s
            consecutiveErrors: 1
            interval: 10s
            maxEjectionPercent: 100
```

Quick explantion for these fields:

| Field                                                                       |                                            Descroption                                           |
| --------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------: |
| `spec.subsets[].trafficPolicy.connectionPool.http.http1MaxPendingRequests`  | The maximum number of pending requests to a backend. Any excess pending requests will be denied. |
| `spec.subsets[].trafficPolicy.connectionPool.http.maxRequestsPerConnection` |                   The maximum number of requests in a cluster at any given time                  |
| `spec.subsets[].trafficPolicy.connectionPool.tcp.maxConnections`            | The maximum number of connections to a backend. Any excess connection will be pending in a queue |

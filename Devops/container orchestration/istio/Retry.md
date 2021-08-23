---
date updated: '2021-08-23T21:47:32+07:00'

---

## HTTP Retry

Describes the retry policy to use when a HTTP request fails. For example, the following rule sets the maximum number of retries to 3 when calling `ratings:v1` service, with a 2s timeout per retry attempt.

```yaml
apiVersion: networking.istio.io/v1alpha3
kind: VirtualService
metadata:
  name: ratings-route
spec:
  hosts:
  - ratings.prod.svc.cluster.local
  http:
  - route:
    - destination:
        host: ratings.prod.svc.cluster.local
        subset: v1
    retries:
      attempts: 3
      perTryTimeout: 2s
      retryOn: gateway-error,connect-failure,refused-stream
```

---
date updated: '2021-08-23T21:47:39+07:00'

---

# Virtual Service

```yml
apiVersion: networking.istio.io/v1alpha3
kind: VirtualService
metadata:
  name: productpage
spec:
  hosts:
  - productpage
  http:
  - route:
    - destination:
        host: productpage
        subset: v1
```

Quick Explanation

| Field   |                              Descroption                              |
| ------- | :-------------------------------------------------------------------: |
| `hosts` | The address used by a client when attempting to connect to a service. |

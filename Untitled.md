

ORDER BY IF((name ~ '^[\]!@`˜#$%^&*()_+\-={}[]'), 1, 0) ASC, IF((name ~ '^[0-9]'), 1, 0) ASC, name


```yaml
apiVersion: config.istio.io/v1alpha2
kind: rule
metadata: 
	name: auth-headers 
spec:
	request_header_operations: 
	- name: X-User-Id
	  values: - request.auth.claims["org_human_identifier"]

```

```yaml
apiVersion: security.istio.io/v1beta1 kind: RequestAuthentication metadata: name: httpbin namespace: foo spec: selector: matchLabels: app: httpbin jwtRules: - issuer: "issuer-foo" jwksUri: https://example.com/.well-known/jwks.json outputPayloadToHeader: "my-jwt-header"
```
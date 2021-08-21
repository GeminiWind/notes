# Deployment

- Use to ensure the number of specified pods (by `replica`)

## Example

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80

```

You can specifiy `.spec.selector` to select the exsting pods. In the above example, the deployment will select all pod whose label `app=nginx`. Another way you can do is specifying the image for deployoment  by `.spec.template`


## Commands

- Apply the deployment

```shell
kubectl apply -f <path-to-deployment-yaml>
```

- Get all depyment

```shell
kubectl get deployments
```

- Update the deployment

```shell
kubectl set image deployment/nginx-deployment nginx=nginx:1.16.1 --record
```

- Rolling back the deployment

```shell
kubectl rollout undo deployment.v1.apps/nginx-deployment
```
- Ad-hoc scaling deployment

```shell
kubectl scale deployment.v1.apps/nginx-deployment --replicas=10
```
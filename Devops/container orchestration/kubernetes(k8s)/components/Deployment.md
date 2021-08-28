---
date updated: '2021-08-28T15:00:05+07:00'

---

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

## Interacting with deployment

### Apply

- Apply the deployment

```shell
kubectl apply -f <path-to-deployment-yaml>
```

### Get

- Get specfied deployment:

```shell
kubectl get image deployment/nginx-deployment -o yaml
```

- Get all depoyment

```shell
kubectl get deployments
```

### Delete

```shell
kubectl delete -f  <path-to-deployment-yaml>
```

### Updating

#### Updating the image

```shell
kubectl set image deployment/nginx-deployment nginx=nginx:1.16.1 --record
```

option `--record` will write the update into history to use later

#### Updating the desire instances

```shell
kubectl scale deployment.v1.apps/nginx-deployment --replicas=10
```

### Rollout, rolllback

#### Get rollout status

```shell
kubectl rollout status deployment/nginx-deployment
```

The output will be similar

    Waiting for rollout to finish: 1 out of 3 new replicas have been updated...

#### Get history of roll out

```shell
kubectl rollout history deployment.v1.apps/nginx-deployment
```

The output will be similar

```shell
deployments "nginx-deployment"
REVISION    CHANGE-CAUSE
1           kubectl apply --filename=https://k8s.io/examples/controllers/nginx-deployment.yaml --record=true
2           kubectl set image deployment.v1.apps/nginx-deployment nginx=nginx:1.16.1 --record=true
3           kubectl set image deployment.v1.apps/nginx-deployment nginx=nginx:1.161 --record=true
```

#### Rollback deployment

```shell
kubectl rollout undo deployment.v1.apps/nginx-deployment --to-revision=2
```

#### maxUnavailable, maxSurge

## Auto-scaling

### Horizontal Pod AutoScaling

#### Based on CPU

After creating the Deployment, to enable horizontal autoscaling of its pods, you need to create a HorizontalPodAutoscaler (HPA) object and point it to the Deploy- ment. You could prepare and post the YAML manifest for the HPA, but an easier way exists—using the kubectl autoscale command:

```kubectl
kubectl autoscale deployment kubia --cpu-percent=30 --min=1 --max=5
```

This creates the HPA object for you and sets the Deployment called kubia as the scal- ing target. You’re setting the target CPU utilization of the pods to 30% and specifying the minimum and maximum number of replicas. The Autoscaler will constantly keep adjusting the number of replicas to keep their CPU utilization around 30%, but it will never scale down to less than one or scale up to more than five replicas.

### Based on memory 


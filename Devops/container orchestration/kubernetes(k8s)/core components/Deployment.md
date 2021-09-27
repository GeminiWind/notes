---
date updated: '2021-08-28T15:00:05+07:00'

---

# Deployment

      

A Deployment is a higher-level resource meant for deploying applications and updating them declaratively

![[k8s-deplyoment-arch.png]]
      
When using a Deployment, the actual pods are created and managed by the Deployment’s ReplicaSets, not by the Deployment directly

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

option `--record` will write the update the CHANGE-CAUSE in revision history

#### Updating the desire instances

```shell
kubectl scale deployment.v1.apps/nginx-deployment --replicas=10
```

### Rollout & rolllback

#### Get rollout status

```shell
kubectl rollout status deployment nginx-deployment
```

The output will be similar
```shell
Waiting for rollout to finish: 1 out of 3 new replicas have been updated...
```

#### Undo the roll out

```shell
kubectl rollout undo deployment nginx-deployment
```

The ouput will be similar like this

```shell
deplpoyment "nginx-deplooyment" rolled back
```

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

#### Controlling the rate of the rollout

Two properties affect how many pods are replaced at once during a Deployment’s roll- ing update. They are *maxSurge* and *maxUnavailable*

```yml
spec:
	strategy:
		rollingUpdate:
			maxSurge: 1
			maxUnavailable: 0
		type: RollingUpdate
```

Below is the explanation of *maxSurge* and *maxUnavailable*

|Props| Explnation|
|:--:|:--:|
| *maxSurge*| Determines how many pod instances you allow to exist above the desired replica count configured on the Deployment. It defaults to 25%, so there can be at most 25% more pod instances than the desired count. If the desired replica count is set to four, there will never be more than five pod instances running at the same time during an update. When converting a percentage to an absolute number, the number is rounded up. Instead of a percentage, the value can also be an absolute value (for example, one or two additional pods can be allowed).|
| *maxUnavailable* | Determines how many pod instances can be unavailable relative to the desired replica count during the update. It also defaults to 25%, so the number of avail- able pod instances must never fall below 75% of the desired replica count. Here, when converting a percentage to an absolute number, the number is rounded down. If the desired replica count is set to four and the percentage is 25%, only one pod can be unavailable. There will always be at least three pod instances available to serve requests during the whole rollout. As with maxSurge, you can also specify an absolute value instead of a percentage.|

![[k8s-deployment-rolling-update.png]]
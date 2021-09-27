# Horizontal Pod AutoScaler (HPA)

Horizontal pod autoscaling is the automatic scaling of the number of pod replicas man- aged by a controller. It’s performed by the Horizontal controller, which is enabled and configured by creating a HorizontalPodAutoscaler (HPA) resource. The controller periodically checks pod metrics, calculates the number of replicas required to meet the target metric value configured in the HorizontalPodAutoscaler resource, and adjusts the replicas field on the target resource (Deployment, ReplicaSet, Replication- Controller, or StatefulSet).

## Architecture
 ![[k8s- hpa-arch.png.png]]

The arrows leading from the pods to the cAdvisors, which continue on to Heapster and finally to the Horizontal Pod Autoscaler, indicate the direction of the flow of met- rics data. It’s important to be aware that each component gets the metrics from the other components periodically (that is, cAdvisor gets the metrics from the pods in a continuous loop; the same is also true for Heapster and for the HPA controller). The end effect is that it takes quite a while for the metrics data to be propagated and a res- caling action to be performed. It isn’t immediate. Keep this in mind when you observe the Autoscaler in action next.

### Calculating the number of required pods
- Single metric:  summing up the metrics values of all the pods, dividing that by the target value set on the HorizontalPodAutoscaler resource, and then rounding it up to the next-larger integer. Example of calucting number of required pods for 50 % CPU utilization 
	![[k8s-hpa-single-metric.png]]
	
- Muiple metric: calculates the replica count for each metric individually and then takes the highest value (for example, if four pods are required to achieve the target CPU usage, and three pods are required to achieve the target QPS, the Autoscaler will scale to four pods)
	 ![[k8s-hpa-multiple-metric.png]]
## Example

1. Create Deployment

```yml
apiVersion: apps/v1
kind: Deployment
metadata:
	name: php-apache
spec:
	selector:
		matchLabels:
			run: php-apache
	replicas: 1
	template:
		metadata:
			labels:
				run: php-apache
		spec:
			containers:
			- name: php-apache
			image: vamsijakkula/php-hpa
			ports:
			- containerPort: 80
			  resources:
			  limits:
				  cpu: 500m
				  memory: 1Gi
			  requests:
				  cpu: 200m
				  memory: 0.5Gi
```


2. Create HPA
	1. Based on CPU utilization
		- By YAML file
		```yml
		apiVersion: autoscaling/v1
		kind: HorizontalPodAutoscaler
		metadata:
			name: php-apache
		spec:
			scaleTargetRef:
				apiVersion: apps/v1
				kind: Deployment
				name: php-apache
			minReplicas: 1
			maxReplicas: 10
			targetCPUUtilizationPercentage: 50
		```
		- By command
		```shell
		kubectl autoscale deployment php-apache --cpu-percent=50 --min=1 --max=10
		```
	2. Based on memory usage
	```yml
	apiVersion: autoscaling/v2beta2 
	kind: HorizontalPodAutoscaler
	metadata:
	  name: php-memory-scale 
	spec:
	  scaleTargetRef:
		apiVersion: apps/v1 
		kind: Deployment 
		name: php-apache 
	  minReplicas: 1 
	  maxReplicas: 10 
	  metrics: 
	  - type: Resource
		resource:
		  name: memory 
		  target:
			type: Utilization 
			averageValue: 10Mi
	```





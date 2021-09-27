# Architecture

![[k8s-arch.png]]

## etcd
- store informattion of K8s object like Pod, Deployment, Service...
- Why etcd:
	- distributed
	- high availalbility
	- fast, better perfomance
- HOW DATA IS WRITE:  not directly, through API server
- Tips:
	-  ENSURING CONSISTENCY WHEN ETCD IS CLUSTERED: For ensuring high availability, you’ll usually run more than a single instance of etcd. Multiple etcd instances will need to remain consistent
	-  The number of etcd instance should be an odd number: to support process of leader electing be easy

## API server
- Functions:
	- provides a CRUD (Create, Read, Update, Delete) interface for querying and modifying the cluster state over a RESTful API. It stores that state in etcd.
	- performs validation of those objects
	-  handles optimistic locking, so changes to an object are never overridden by other clients in the event of concurrent updates.
- How it works
![[api-server.png]]

## Controller Manager
- Functions
	- observe the current state of sytem, then do call API server to ensure the desired state
	- each type of object has seperated controller
		- Replication Manager
		- ReplicaSet, DeamonSet, Job Controller
		- Deployment Controller
		- StatefulSet Controlller
		- Node Controller
		- Service Controller
		- Endpoint Controller
		- Namespace Controller
		- Persistent Volume Controller
		- Others
- How it works:  watch the API server for changes to resources (Deployments, Services, and so on) and perform operations for each change, whether it’s a creation of a new object or an update or deletion of an existing object.
- How it works:
		- reconciliation loop: run a reconciliation loop, which reconciles the actual state with the desired state (specified in the resource’s spec section) and writes the new actual state to the resource’s status section
		- watch mechanism

## Scheduler

- Functions:
	- run scheduling algorithm to find out the Node for Pod, then update the Pod Definition through API servier
- How it works:
		1.  Filtering the list of all nodes to obtain a list of acceptable nodes the pod can be scheduled to (out of resource, node selectior ...). 
		2. Prioritizing the acceptable nodes and choosing the best one. If multiple nodes have the highest score, round-robin is used to ensure pods are deployed across all of them evenly.
![[k8s- scheduler.png]]

## Kubelet
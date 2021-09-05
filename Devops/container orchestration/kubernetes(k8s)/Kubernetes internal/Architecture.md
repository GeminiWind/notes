# Architecture

![[Pasted image 20210905110653.png]]

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
![[Pasted image 20210905112145.png]]

## Controller Manager

## Scheduler

- Functions:
	- run scheduling algorithm to find out the Node for Pod, then update the Pod Definition through API servier
- How it works:
		1.  Filtering the list of all nodes to obtain a list of acceptable nodes the pod can be scheduled to (out of resource, node selectior ...). 
		2. Prioritizing the acceptable nodes and choosing the best one. If multiple nodes have the highest score, round-robin is used to ensure pods are deployed across all of them evenly.
![[Pasted image 20210905112817.png]]
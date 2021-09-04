# Namespace

## Purpose

To isolo your workspace. For example: for `dev`, `staging` & `prod`

## Interacting with namespace

- Create a namespace

```shell
kubectl create namespace <namespace>
```

- Get all namespace

```shell
kubectl get namespances
```

- Get resource in specified namespace

```shell
kubectl get pods -n <namespace>
```

- Specify namespace in YAML file

```yml
api:
kind:
namespace: 'dev'
```
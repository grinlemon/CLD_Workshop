# Presentation

## Introduction

- Swiss cloud
- Kubernetes
- Openstack

## Demo

Connection to the infomaniak console to show the infrastructure deployed.

Get all (services, pod, nodes)

```shell
kubectl get all
```
Delete pod frontend

```shell
kubectl delete pod id_pod
```
We can see a new pod is immediately created

Load test

```shell
echo "GET http://195.15.197.137" | vegeta attack -duration=1m -rate=200 | vegeta report --type=text
```
Get all :

```shell
kubectl get all
```

Get the events of the autoscaler

```shell
horizontalpodautoscaler.autoscaling/frontend-autoscale 
```

The final result :

http://195.15.197.137/all

## Conclusion

Speak about the issues encountered.


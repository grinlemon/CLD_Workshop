# Presentation

## Introduction

Explication théorique du sujet -> reprendre le readme et expliquer notre infra (schema)

- Swiss cloud
- Openstack
- Kubernetes / Kops
- Cost

## Demo and POC

Expliquer le groupe et comment accer au service cloud depuis Infomaniak et comment y acceder depuis un cli.   
(openstack -> connection au cloud infomaniak avec un cli, kops -> creation/reglage du cluster, kubectl -> init des pods et autosacling)

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
Get all

```shell
kubectl get all
```

Get the events of the autoscaler

```shell
kubectl describe horizontalpodautoscaler.autoscaling/frontend-autoscale 
```

The final result :

http://195.15.197.137/all

Grafana :

http://195.15.196.13:3000/

## Conclusion

Speak about the issues encountered.

Interesting and realistic project.

## Références et liens 



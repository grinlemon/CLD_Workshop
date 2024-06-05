# Presentation

## Introduction

- Swiss cloud
- 

## Demo

get all (services, pod, nodes)
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
get all :

```shell
kubectl get all
```

## Conclusion

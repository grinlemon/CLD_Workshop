# Prepare the environment
To prepare the environment we followed this [documentation](https://docs.infomaniak.cloud/documentation/00.getting-started/02.Connect_project/#__tabbed_1_1) written by Infomaniak.

To validate the **STEP 01** we first need to be able to access the cluster through CLI commands.

# Create cluster
## Connect to OpenStack
Duplicate and edit the [PCP-Example-openrc.sh](PCP-Example-openrc.sh) file to put your user details : 
- 16 `export OS_PROJECT_ID="Project ID"`
- 17 `export OS_PROJECT_NAME="Project Name"`
- 27 `export OS_USERNAME="Username"`

Execute the following command to activate the connection.

```shell
source PCP-PROJET_ID-openrc.sh
```

## Create kops bucket
```shell
openstack container create kops
```

## Create container config file
```shell
kops create cluster \
  --cloud openstack \
  --name cld-workshop.k8s.local \
  --state swift://kops \
  --zones dc3-a-04,dc3-a-09,dc3-a-10 \
  --network-cidr 10.0.0.0/24 \
  --image "Debian 11 bullseye" \
  --control-plane-count 3 \
  --node-count 1 \
  --node-size a2-ram4-disk20-perf1 \
  --control-plane-size a4-ram8-disk50-perf1 \
  --etcd-storage-type CEPH_1_perf1 \
  --api-loadbalancer-type public \
  --topology private \
  --ssh-public-key ~/.ssh/id_rsa.pub \
  --networking calico \
  --os-ext-net ext-floating1 \
  --os-octavia=true \
  --os-octavia-provider octavia \
  --os-kubelet-ignore-az=true \
  --os-dns-servers=83.166.143.51,83.166.143.52
```

## Edit cluster config file
```shell
kops edit cluster cld-workshop.k8s.local --state swift://kops
```

Then add the following value `nodePortAccess` right after `networkCIDR` with the same value. In this case it's `10.0.0.0/24`

```yaml
  networkCIDR: 10.0.0.0/24
  nodePortAccess:
  - 10.0.0.0/24
```

## Apply config file
```bash
kops update cluster --name cld-workshop.k8s.local --yes --admin --state swift://kops
```

## Export contect for kubectl
```shell
kops export kubeconfig --admin --name cld-workshop.k8s.local --state swift://kops
```

Then you can test to be sure that you have access to the cluster with kubectl.

```shell
kubectl config get-contexts
```

You should have the following response

```shell
CURRENT   NAME                     CLUSTER                  AUTHINFO                 NAMESPACE
*         cld-workshop.k8s.local   cld-workshop.k8s.local   cld-workshop.k8s.local   
```

Once there you will be able to access `kubectl` commands for the newly created cluster!

You have now finish the **STEP 01**, congratulations!

## Create the pods and services (no resilience) 

```shell
kubectl create -f frontend-svc.yaml
kubectl create -f frontend-pod.yaml

kubectl create -f redis-svc.yaml
kubectl create -f redis-pod.yaml

kubectl create -f api-svc.yaml
kubectl create -f api-pod.yaml
```
after these commands you can check that the app is correctly running.
Currently there is no support for resilience. So let's add it.

## Add the support for resilience

First you have to delete all pods you have created before.

```shell
kubectl delete pod api

kubectl delete pod redis

kubectl delete pod frontend
```

Secondly, you have to update the yaml you used before for the pods and make a deployement version of them, then create them.

```shell
kubectl create -f redis-deployment.yaml
(1 replica, using only one Redis server instance ensures simplicity, consistency, and easier management. It avoids the complexity of synchronization.)

kubectl create -f frontend-deployment.yaml
(4 replicas)

kubectl create -f api-deployment.yaml
(4 replicas)
```

Now if you run `kubectl get all` you should have this output :

![img](https://github.com/grinlemon/CLD_Workshop/blob/main/img/getAll1.png)

## Put autoscaling in place

To put autoscalling in place you will have to run these two commandes that will create an hpa autoscalling :
(HPA: Adjusts the number of pod replicas based on metrics like CPU or memory usage)

```shell
kubectl apply -f frontend-autoscale.yaml
```

Now if you run `kubectl get all` you should have this output with the hpa autoscalling :

![img](https://github.com/grinlemon/CLD_Workshop/blob/main/img/getAll2.png)

## Load-Testing using vegeta

run this commande to load test the app using vegeta

```shell
echo "GET http://195.15.197.137" | vegeta attack -duration=1m -rate=200 | vegeta report --type=text
```
and you should have this output who shows that your autoscalling is working :

![img](https://github.com/grinlemon/CLD_Workshop/blob/main/img/vegeta.png)

## Usefull commandes

Have a look at the nodes, pods and services

```shell
kubectl get nodes

kubectl get services

kubectl get pods
```
or  

```shell
kubectl get all
```


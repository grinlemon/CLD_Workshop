# Prepare your environment
To prepare our environment we follow this [documentation](https://docs.infomaniak.cloud/documentation/00.getting-started/02.Connect_project/#__tabbed_1_1) written by Infomaniak.

To validate the **STEP 01** we first need to be able to access the cluster through CLI commands. Moreover you need to be able to 


# Create cluster

## Export KOPS STATE
```shell
export KOPS_STATE_STORE=swift://kops
```

## Create kops container
```shell
openstack container list
openstack container create kops
```

## Create container
```shell
kops create cluster \
  --cloud openstack \
  --name cld-workshop.k8s.local \
  --state "${KOPS_STATE_STORE}" \
  --zones nova \
  --network-cidr 10.0.0.0/24 \
  --image "Debian-11-bullseye" \
  --control-plane-count 3 \
  --node-count 1 \
  --node-size a2_ram4_disk20_perf1 \
  --control-plane-size a4_ram8_disk50_perf1 \
  --etcd-storage-type CEPH_1_perf1 \
  --api-loadbalancer-type public \
  --topology private \
  --bastion \
  --ssh-public-key ~/.ssh/id_rsa.pub \
  --networking calico \
  --os-ext-net ext-floating1
```
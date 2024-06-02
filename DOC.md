# Prepare the environment
To prepare the environment we followed this [documentation](https://docs.infomaniak.cloud/documentation/00.getting-started/02.Connect_project/#__tabbed_1_1) written by Infomaniak.

To validate the **STEP 01** we first need to be able to access the cluster through CLI commands.

# Create cluster
## Connect to OpenStack
Duplicate and edit the [PCP-Example-openrc.sh](PCP-Example-openrc.sh) file to put your user details.

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
  --os-kubelet-ignore-az=true
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
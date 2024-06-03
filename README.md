# Kubernetes cluster on Infomaniak Public Cloud

## Group members (group 4)
- Gwendal Piemontesi
- Dario Vasques
- Ewan Mariaux
- Guillaume Trüeb

## POC objectives

Validate the possible use of the Public Cloud of Infomaniak in the context of a startup which needs to deploy containers on the web using Kubernetes.

## Infra architecture

On the Kubernetes documentation, we can find a cluster architecture diagram which will present how it works.

![](img/image.png)

In our case we want to deploy the content of the CLD lab 5 (Kubernetes on Google Cloud) but on a swiss cloud which is way better concerning data protection and security. As we want a complete control of the cloud plateform to install Kubernetes we will use a **IaaS** and not a CaaS.

Through our analysis we found that Infomaniak offer a Jelastic Cloud which is considered as a PaaS (Plateform as a Service). They also offer the possibility to install our own servers directly in their datacenter. It could be a good option if you already have hardware but don't have the capacity to store them in your office.

![](img/image%20copy.png)

## Scenario

Describe step-by-step the scenario. Write it using this format (BDD style).

### STEP 01
```
given -> we don't have any cloud platform to host our containers

when -> we want to create a project using Infomaniak IaaS services (Public Cloud)

then -> create a project on the cloud platform
```

### STEP 02
```
given -> we have access to a project on Infomaniak 

when -> we create OpenStack accounts and share them with our team

then -> our OpenStack platform is accessible to our team
```

### STEP 03
```
given -> we have access to our OpenStack with Horizon or CLI

when -> we document ourselves to prepare the commands to create the cluster

then -> we have created the cluster on our OpenStack platform
```

### STEP 04
```
given -> we have a running Kubernetes cluster

when -> we want to ensure that the cluster can do auto-scaling on pods

then -> the cluster can start pods automatically
```

### STEP 05
```
given -> we have a running Kubernetes cluster capable of auto-scaling pods

when -> we want to perform a load test on the cluster to ensure it can handle many connections at the same time

then -> the tests validate that the cluster handles multiple connections correctly at the same time
```
## Cost
### Estimation
Based on a estimation we made with Infomaniak Price Calculator ([here](https://infomaniak.cloud/calculator?uuid=098009b5-bad3-45d6-a9c6-bfce2b6e844f)) we will turn around 12.68.-/month. 

## Return of experience

<take a position on the poc that has been produced.>

<Did it validate the announced objectives?>
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

In our case we want to deploy the content of the CLD lab 5 (Kubernetes on Google Cloud) but on a swiss cloud which is way better concerning data protection and security. As we want a complete control of the cloud plateform we need to use a IaaS and not a CaaS.

## Scenario

Describe step-by-step the scenario. Write it using this format (BDD style).

### STEP 01
```
Given a newly provisioned Infomaniak Public Cloud instance with available resources.

When we deploy Kubernetes on our public cloud instance using the Infomaniak dashboard or API.

Then Kubernetes is successfully deployed and running on our Infomaniak Public Cloud, providing us with a scalable and manageable container orchestration platform.
```

### STEP 02
```
Given access to our Infomaniak Public Cloud account and available resources.

When we navigate to the Infomaniak dashboard and select the option to provision a new cloud instance.

Then we specify our desired configuration, such as CPU, RAM, and storage capacity, and proceed to deploy the instance.
```

### STEP 03
```
Given that our Infomaniak Public Cloud instance is successfully provisioned.

When we log in to the instance via SSH or other remote access methods.

Then we verify that the instance is operational and accessible.
```

### STEP 04
```
Given an operational Infomaniak Public Cloud instance.

When we ensure that the necessary dependencies, such as Docker and kubectl, are installed on the instance.

Then we are ready to proceed with deploying Kubernetes.
```

### STEP 05
```
Given that Kubernetes deployment is initiated.

When we monitor the deployment process for any errors or issues.

Then we troubleshoot and resolve any encountered problems to ensure a successful deployment.
```

### STEP 06
```
Given a successfully deployed Kubernetes cluster.

When we verify the status of the cluster using kubectl commands.

Then we ensure that all nodes are in a ready state and that the control plane components are functioning properly.
```

### STEP 07
```
Given deployed applications within our Kubernetes cluster.

When we monitor the cluster's performance and resource utilization.

Then we ensure optimal operation of our applications on the Infomaniak Public Cloud Kubernetes cluster.
```

## Cost

<analysis of load-related costs.>

<option to reduce or adapt costs (practices, subscription)>

## Return of experience

<take a position on the poc that has been produced.>

<Did it validate the announced objectives?>
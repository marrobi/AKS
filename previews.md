# AKS Preview Features and Related Projects

At any given time, there can be multiple early stage features available in AKS behind a *feature flag*, along with a set of related projects available elsewhere on GitHub that you may wish deploy manually on the service. 

In most cases, these features and associated projects will eventually make their way into AKS, or at least be supported as 1st class extensions. But before they get there, we need sufficient usage from early adopters to validate their usefulness and quality.

The purpose of this page is to capture these features and associated projects in a single place.

## Preview features

### Kubernetes Audit Log

The [Kubernetes audit log](https://kubernetes.io/docs/tasks/debug-application-cluster/audit/) provides a detailed account of security-relevant events that have occurred in the cluster. You can enable it for your subscription by turning on the **AKSAuditLog** feature flag.

First, register the feature flag:

```
az feature register --name AKSAuditLog --namespace Microsoft.ContainerService
```

Then refresh your registration of the AKS resource provider:

```
az provider register -n Microsoft.ContainerService
```

Once you've done this, you will see a new **kube-audit** log source in the diagnostic settings for your cluster, as described in [this doc](https://docs.microsoft.com/azure/aks/view-master-logs).

**Please note:** AKS will only capture audit logs for clusters which are created or upgraded after the feature flag is enabled.

## Associated projects

Please note that while the following projects have been validated to work with recent AKS clusters, they are not yet officially supported by Azure CSS. If you run into issues, please file them in the corresponding GitHub repo.

### AAD Pod Identity

The AAD Pod Identity project enables you to provide Azure identities to pods running in your Kubernetes cluster. This allows individual applications running in Kubernetes to have their own rights to interact with Azure resources and to easily authentication tokens representing those rights, avoiding the need to share a single identity across the cluster or inject applications with service principals.

http://github.com/azure/aad-pod-identity. 

### KeyVault FlexVol

The KeyVault FlexVol project enables Kubernetes pods to mount Azure KeyVault stores as flex volumes, providing access to application-specific secrets, keys, and certs natively within Kubernetes. 

https://github.com/Azure/kubernetes-keyvault-flexvol 

### Azure Application Gateway Ingress Controller

The App Gateway ingress controller enables the use of the [Azure Application Gateway service](https://azure.microsoft.com/services/application-gateway/) as a layer 7 load balancer in front of Kubernetes services, providing a fully managed alternative to running something like Nginx directly inside the cluster.

https://github.com/Azure/application-gateway-kubernetes-ingress
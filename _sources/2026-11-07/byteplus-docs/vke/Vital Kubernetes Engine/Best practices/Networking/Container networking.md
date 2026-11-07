---
title: "Container networking"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using-the-Container-Network-Interface-correctly"
---

This topic describes considerations, configuration recommendations, and best practices for using Container Network Interface (CNI) in VKE.

<span id=".6YG_5YWN5ZyoLXZwYy1jbmkt572R57uc546v5aKD5Lit5L2_55SoLWhvc3Rwb3J0"></span>
## Avoid using HostPort in VPC\-CNI network environments

HostPort is a default network feature provided by Kubernetes that allows a pod to expose a service via a specific host port. Although HostPort can facilitate the implementation of network plugins for nodes and pods across different network planes, it may introduce conflicts with the source ports of the node, resulting in occasional network issues. For clusters using the VPC\-CNI network model in container services, both pods and nodes are elements on the VPC network plane, and the difference between the network paths for accessing a node and a pod is minimal, making HostPort no longer an optimal choice. To quickly access a container, you can bind an independent EIP to the pod of the container.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features">[Beta \- Apply for Trial]</a>: Binding an independent EIP to a pod is currently in the <strong>beta</strong> stage. To use this feature, submit an application.</div>


<span id=".6YG_5YWN5L-u5pS5LW5vZGVwb3J0LeeahOm7mOiupOerr-WPo-iMg-WbtA=="></span>
## Avoiding modifying the default port range for NodePort

The default NodePort ports in VKE are offset from the system\-configured `net.ipv4.ip_local_port_range`, ensuring that the ports used by NodePort do not conflict with ports of processes running on the node. In addition, ports of system components are kept separate from NodePort ports. Unnecessary modification of the NodePort port range may cause network issues due to port conflicts and therefore should be avoided.

<span id=".6YG_5YWN5ZyoLXZwYy1jbmkt572R57uc546v5aKD5Lit5Li66IqC54K56YWN572u6aKd5aSW55qE5by55oCn572R5Y2h"></span>
## Avoiding configuring additional ENIs for nodes in VPC\-CNI network environments

Configuring additional ENIs for nodes consumes the ENI quota of nodes in clusters that use the VPC\-CNI network model. This leads to reduced pod density on the node and potential failures in creating new pods. Exercise caution when you perform this operation. For information about how to calculate the density of pods on a node, see [Calculation of pod scheduling density per node](https://docs.byteplus.com/en/docs/vke/Pod-scheduling-density-calculation-for-nodes#.dnBjLWNuaS3pm4bnvqQ=).

<span id=".5YWz5rOoLXZwYy3nm7jlhbPotYTmupDnmoTphY3pop3lkozlj6_nlKjmlbDph48="></span>
## Monitoring the quota and available quantity of VPC\-related resources

The VPC\-CNI network model uses VPC resources for Kubernetes cluster networking. The quota of VPC resources directly affects the upper limit of the Kubernetes cluster scale. When creating a cluster, plan the required VPC resources to avoid business impact caused by insufficient VPC resources as the cluster grows in the future.

We recommend continuously monitoring VPC\-related resource usage for your clusters. Expand resources promptly to avoid pod networking failures caused by exhausted resource quotas. For details on VPC resource expansion, see [VPC limits](https://docs.byteplus.com/en/docs/vpc/Limits).

<span id=".6YG_5YWN5pON5L2cLXZwYy1jbmkt572R57uc5qih5Z6L5L2_55So55qE5by55oCn572R5Y2h"></span>
## Avoiding operations on ENIs used by the VPC\-CNI network model

The VPC\-CNI network model uses VPC ENIs on nodes to create networks for pods. The lifecycle and configuration of these ENIs are managed by the VPC\-CNI network add\-on. Do not perform any operations on them, including but not limited to:


* Configuring private IP addresses for ENIs managed by the VPC\-CNI network add\-on either manually or via automatic DHCP (commonly found in NetworkManager).

   Using custom private IP addresses will cause pod network failures. For related failures or further questions, [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000210) to obtain technical support.

* Deleting these ENIs.

   This operation will cause network failures for pods that use the deleted ENIs.


<span id=".6LCo5oWO5a-5LWt1YmVybmV0ZXMt6LWE5rqQ6L-b6KGM5by65Yi25Yig6Zmk5pON5L2c"></span>
## Exercising caution when forcibly deleting Kubernetes resources

Forcibly deleting Kubernetes resources (such as CRDs, pods, and other resources automatically created during add\-on installation) may cause abnormal resource status and consequent issues such as resource conflicts and invalidation. To forcibly delete Kubernetes resources, [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000210) to obtain technical support. Do not attempt this operation yourself.

<span id=".6K-35Yu_55u05o6l5L-u5pS5LXZwYy1jbmkt57uE5Lu26YWN572u"></span>
## Avoiding direct modifications to the vpc\-cni component configuration

The vpc\-cni is a critical component in clusters that use the VPC\-CNI network model. The component configuration is managed by VKE. Therefore, do not change the component configuration by directly modifying the vpc\-cni configuration file (ConfigMap). If necessary, [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000210) to obtain technical support.

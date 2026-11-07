---
title: "LoadBalancer Service overview"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/LoadBalancer_service_overview"
---

A Service of the LoadBalancer type uses an external Load Balancer instance to smoothly distribute traffic to multiple pods in a cluster. This topic describes the common concepts and technical principles of the Service of the LoadBalancer type.

<span id=".5Z-65pys5Y6f55CG"></span>
## Basic principles

When a LoadBalancer Service is created, the system creates or reuses an external Load Balancer instance to expose the service to the public or internal network. The Load Balancer instance can forward traffic to a Service of the NodePort type and containers in the VPC\-CNI network mode. The following figure shows the basic principle of forwarding traffic to a Service of the NodePort type.

<span id=".5aSW6YOo5rWB6YeP562W55Wl"></span>
## External traffic policy

When the Service type is LoadBalancer or NodePort, you can configure an external traffic policy for the Service to route traffic from the external network to the Service. Available parameters include `Local` and `Cluster`. The forwarding behavior of the external traffic policy slightly differs in the LB\-to\-pod direct connection mode and the LB\-to\-pod non\-direct connection mode.

<span id=".6Z2eLXBvZC3nm7TpgJo="></span>
### LB\-to\-pod non\-direct connection mode

In the LB\-to\-pod non\-direct connection mode, traffic is forwarded to pods through the NodePort of the node. In this case, the main differences between different external traffic policies are as follows:


* Local: Nodes where pods are located are added to CLB/NLB instances as backend servers, and external traffic is forwarded only to nodes where pods are located. The traffic distributed to a node is forwarded only to pods on the node, which means that traffic is forwarded only among pods on the same node.

* Cluster: All nodes in the cluster are added to CLB/NLB instances as backend servers, and external traffic may be forwarded to any node. The traffic distributed to a node will be forwarded to pods on different nodes.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Any VCI pods will be added to CLB/NLB instances as backend servers.</div>


The following table describes the main differences of external traffic policies in the LB\-to\-pod non\-direct connection mode.


|Item |Local |Cluster |
|---|---|---|
|Backend servers |Only nodes where pods are located are added to CLB/NLB instances as backend servers. |All nodes in the cluster will be added to CLB/NLB instances as backend servers. |
|Backend servers resource quota |This option consumes a small amount of backend server quota. For more details, refer to [CLB constraints](https://docs.byteplus.com/en/docs/clb/Product-Overview-07) and [NLB constraints](https://docs.byteplus.com/en/docs/clb/NLB-Constraints). |All nodes in the cluster are added to CLB instances as backend servers, which consume a large amount of CLB resources. For more details, refer to [CLB constraints](https://docs.byteplus.com/en/docs/clb/Product-Overview-07) and [NLB constraints](https://docs.byteplus.com/en/docs/clb/NLB-Constraints). |
|Access to the IP address of an LB instance |Requests can only be forwarded to the node where the target pod is located. |Requests are forwarded to all nodes. |
|Load balancing among pods |Load balancing among pods is disabled by default. |Load balancing among pods is enabled by default. |
|Source IP address retention |Supported. |Not supported. |
|Session persistence |Supported. |Not supported. |
|Application scenario |Applies to applications that need the original IP addresses of clients to be retained, such as logging applications based on the original IP address. |Applies to applications that require high service availability and are insensitive to source IP address retention, such as large web application clusters. |


<span id=".cG9kLeebtOmAmg=="></span>
### LB\-to\-pod direct connection mode

In the LB\-to\-pod direct connection mode, pods are directly added to CLB/NLB instances as backend servers. External requests are directly forwarded to the pods without being forwarded through nodes. The LB\-to\-pod direct connection mode is suitable for scenarios where high network performance is required.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The LB\-to\-pod direct access mode can be configured and takes effect only for clusters in the VPC\-CNI network mode.</div>


* <div data-tips="true" data-tips-type="tip">Any VCI pods will be added to CLB/NLB instances as backend servers.</div>



The following table describes the main differences between external traffic policies in the LB\-to\-pod direct access mode.


|Item |Local |Cluster |
|---|---|---|
|Backend servers |Pods are directly mounted to the backend of the CLB/NLB instance. |Pods are directly mounted to the backend of the CLB/NLB instance. |
|Backend servers resource quota |Only business pods are added to CLB instances as backend servers, which consume a small amount of CLB resources. For more details, refer to [CLB Constraints](https://docs.byteplus.com/en/docs/clb/Product-Overview-07), [NLB Constraints](https://docs.byteplus.com/en/docs/clb/NLB-Constraints). |Only business pods are added to CLB instances as backend servers, which consume a small amount of CLB resources. For more details, refer to [CLB Constraints](https://docs.byteplus.com/en/docs/clb/Product-Overview-07), [NLB Constraints](https://docs.byteplus.com/en/docs/clb/NLB-Constraints). |
|Access to the IP address of an LB instance |Requests are forwarded directly to pods. |Requests are forwarded directly to pods. |
|Load balancing among pods |Load balancing among pods is enabled by default. |Load balancing among pods is enabled by default. |
|Source IP address retention |Supported. |Supported. |
|Session persistence |Supported. |Supported. |

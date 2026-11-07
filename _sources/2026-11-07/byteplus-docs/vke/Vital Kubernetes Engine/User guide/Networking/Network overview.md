---
title: "Network overview"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Container-networks"
---

The cluster network is the foundation for ensuring internal add\-on communication, container interconnectivity, service exposure, and external access. According to Kubernetes guidelines, the cluster network must be flat and require no NAT translation between Pods. This topic mainly describes the categories and basic concepts of container networks in VKE clusters.

<span id="AEDYJkKI"></span>
## Cluster network components


* **Node network**: As the underlying network of the cluster, it is used for communication among all nodes. It ensures two\-way communication among all nodes in the cluster (including control plane nodes and worker nodes) and provides a stable underlying transmission carrier for the container network and service network.

* **Container network**: Adopting the Kubernetes flat network model, it is used for communication among all Pods within the cluster. It ensures that each Pod has an independent and routable IP address, which allows Pods to directly communicate via IP addresses without NAT translation. This reduces communication latencies and improves forwarding efficiency.

* **Service network**: Applicable to service communication within the cluster, it provides a fixed virtual IP address (ClusterIP) for each group of Pods with the same feature. It hides the characteristics of Pods, such as short lifecycle and dynamic IP changes, and decouples services from backend Pods. This ensures that other Pods or services within the cluster can stably access the target service.

* **External network**: It enables communication between services in the cluster and external clients. It achieves centralized management of Layer 4/7 (HTTP/HTTPS) traffic ingresses outside the cluster through core resources such as Ingresses. This achieves domain name routing, path forwarding, and traffic control, and securely and efficiently forwards external requests to the corresponding Service and Pod within the cluster.


<span id="K8vUJgaP"></span>
## Pod networking

<span id="snilBmFz"></span>
### VPC\-CNI network model

Virtual Private Cloud \- Container Network Interface (VPC\-CNI) is one of the container network solutions for VKE clusters. As an underlay network mode, it is implemented based on the Container Network Interface (CNI) standard and VPC elastic network interface (ENI) capabilities. In this mode, Pods and nodes are on the same VPC network plane. They directly reuse underlying VPC network resources without additional tunnel encapsulation. This mode delivers high performance and high compatibility, and is widely used in scenarios such as latency\-sensitive workloads and migration of traditional architectures.

<span id="9hcnZwRL"></span>
#### Shared ENI

This mode is the default ENI allocation mode for VKE clusters in the VPC\-CNI network model. In this mode, multiple Pods share a single VPC secondary ENI. The IPAM add\-on assigns multiple IP addresses to the ENI and allocates the IP addresses to different pods for use. In this mode, node resource consumption is low, and Pod deployment density per node can be increased. This makes the mode the preferred choice for most scenarios.

The network communication process in shared ENI mode is as follows:


* **Pod communication within the same node**: When a Pod accesses another Pod on the same node, the forwarding path varies based on whether the Pods use the same ENI.

   * When a Pod communicates with another Pod that is deployed on the same node and shares the same ENI, forwarding is directly performed via IPvlan. Traffic does not pass through the ENI for forwarding, resulting in extremely low latency.

   * When a Pod communicates with another Pod that is deployed on the same node but uses a different ENI, the routing capability of VPC is used to forward traffic to the Pod on another ENI.

* **Pod communication across nodes**: When a Pod accesses another pod on a different node, traffic first reaches the default gateway based on the routes in the VPC route table. Then, the traffic is forwarded to the Pod on another node through the routing capability of the VPC.

* **Pod access to the public network**: When a Pod accesses the public network, the system performs SNAT on the private IP of the Pod via the NAT gateway in the VPC to enable the Pod to access the public network.


<span id="vOmQwi9Z"></span>
#### Exclusive ENI (Trunk ENI)

VKE supports the exclusive ENI mode based on Trunk ENI. In this mode, the system binds a Trunk ENI to each node. Each Pod requiring an exclusive ENI is bound to a Branch ENI of the Trunk ENI, which achieves exclusive ENI binding. In this mode, you can configure a fixed IP address and associate an independent security group with the Pod ENI. This achieves network isolation between Pods.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_dc144d48e51f088082ecad541d0c36be.png) </span>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For instructions on configuring Pod exclusive ENIs based on Trunk ENI, see <a href="https://docs.byteplus.com/en/docs/vke/Using-Trunk-ENI-to-enable-the-exclusive-ENI-mode-for-pods">Exclusive ENIs for pods based on Trunk ENI</a> and <a href="https://docs.byteplus.com/en/docs/vke/Configuring-a-fixed-IP-address-for-a-pod">Configuring static IPs for Pods</a>.</div>


<span id="2LIMAYVD"></span>
### Flannel network model

Flannel is an open source, lightweight container network solution. VKE supports this network model and adopts the VPC Router mode, thereby achieving pod communication across nodes by using the default route table in the VPC. No tunnel encapsulation overhead is generated during the process. As an underlay network solution, it delivers excellent performance.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_89c66334a5f4f0e3712d7f6c59c59492.png) </span>

<span id="1mP12PcM"></span>
### Network model differences

The characteristics, such as Pod density and validation rules, differ among various container network models. The following table describes the details.


|Item |VPC\-CNI network model |Flannel network model |
|---|---|---|
|Number of node Pods |It is determined by the ECS specifications of nodes and the node kubelet parameter `max-pods`. For details, see [Calculating schedulable Pod density for nodes](https://docs.byteplus.com/en/docs/vke/Pod-scheduling-density-calculation-for-nodes). |It is determined by the **Maximum number of Pod instances per node** parameter and the node kubelet parameter `max-pods` specified during cluster creation. For details, see [Calculating schedulable Pod density for nodes](https://docs.byteplus.com/en/docs/vke/Pod-scheduling-density-calculation-for-nodes). |
|Pod networking |* The Pod CIDR block is directly allocated from the VPC CIDR block, which results in high consumption of VPC IP addresses. Therefore, you need to select an appropriate VPC CIDR block and subnets based on the cluster scale or business scale to ensure that each subnet has enough available IP addresses.<br><br>   * The number of IP addresses for the node subnets must match your business scale. Otherwise, nodes cannot be created due to insufficient IP addresses.<br><br>   * The number of IP addresses for the Pod subnets must match your business scale. Otherwise, Pods cannot be created due to insufficient IP addresses.<br><br>* The Service CIDR block is independent of the VPC CIDR block and must not conflict with it.<br><br>* Container network expansion is supported. For details, see [Expanding cluster subnets](https://docs.byteplus.com/en/docs/vke/Expanding-cluster-subnets). |* The container CIDR block is independent of the VPC CIDR block. Flannel allocates a subnet CIDR block from the configured container CIDR block for each node in the cluster, and the IP addresses of all Pods on the node are allocated from the subnet CIDR block.<br><br>* The Pod CIDR block, VPC CIDR block, and Service CIDR block are independent of each other and cannot overlap.<br><br>   * The Pod CIDR block cannot conflict with the VPC CIDR block.<br><br>   * The Pod CIDR block cannot conflict with the Pod CIDR block of other clusters under the same VPC.<br><br>   * The Service CIDR block cannot conflict with the VPC CIDR block.<br><br>   * The Service CIDR block cannot conflict with the Pod CIDR block of other clusters under the same VPC.<br><br>* Container network expansion is not supported.. |
|Network security |* The Kubernetes native network policy NetworkPolicy is supported, which allows custom access control among containers. For details, see [Using a NetworkPolicy for network access control](https://docs.byteplus.com/en/docs/vke/Using-NetworkPolicies-for-network-access-control).<br><br>* QoS bandwidth limits can be configured for pods. For details, see [Configuring QoS bandwidth limits for pods](https://docs.byteplus.com/en/docs/vke/Configuring_QoS_bandwidth_limits_for_pods). |* NetworkPolicy is not supported.<br><br>* QoS bandwidth limits cannot be configured. |
|IPv4/IPv6 dual\-stack |Dual stack is supported. For details, see [Creating IPv4/IPv6 dual-stack clusters](https://docs.byteplus.com/en/docs/vke/Deploying-an-IPv4_IPv6-dual-stack-cluster-using-VKE). |Dual stack is not supported. |
|Fixed Pod IP |Fixed IP addresses can be configured for Pods. For details, see [Configuring static IPs for Pods](https://docs.byteplus.com/en/docs/vke/Configuring-a-fixed-IP-address-for-a-pod). |Fixed IP addresses cannot be configured for Pods. |


<span id="8EFJpHGC"></span>
## Service

As temporary resources in clusters, Pods have short lifecycles and dynamically changing IP addresses. Therefore, they cannot be directly used as service access points. In Kubernetes, a Service is defined as a service abstraction layer. It provides a fixed access endpoint, load balancing, and service discovery for a group of Pods that provide the same feature. It shields dynamic Pod scaling and IP changes and decouples the service from the backend Pods.

Services are mainly categorized into the following types:


* **ClusterIP**: (default type) It allocates a virtual IP address within the cluster. Only allowing access within the cluster, it is used for internal communication between services.

* **NodePort**: Based on ClusterIP, it opens a fixed port on each node, which enables access to the service from outside the cluster via `node IP + port`.

* **LoadBalancer**: Connecting to CLB, it automatically creates Internet\-facing or internal\-facing CLB instances and allocates independent EIPs to expose cluster services.

* **ExternalName**: It maps an external service to an internal cluster domain name, which achieves centralized access to the external service from within the cluster. It does not allocate IP addresses but only maps domain names.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For a detailed introduction and configuration steps for services, see <a href="https://docs.byteplus.com/en/docs/vke/Service-overview">Service overview</a>.</div>


<span id="xaGD5ByL"></span>
## Ingress

LoadBalancer Services only support Layer 4 traffic forwarding. However, based on Layer 7 HTTP and HTTPS protocols, Ingresses can forward traffic to multiple backend Services within the cluster by using different forwarding rules. This enables advanced traffic management features such as domain name routing, path forwarding, redirection, and rate limiting.

Ingresses, as independent resources within a Kubernetes cluster, mainly consist of the following resources:


* **Ingress resource**: A Kubernetes API object that defines traffic routing rules, such as domain name, path, target Service, and HTTPS certificate. It only specifies rules and does not perform actual traffic forwarding.

* **Ingress Controller**: It is used for listening to external network traffic to the cluster, parsing ingress rules, and forwarding traffic to backend services. Ingress controllers include APIG Ingress Controller, ALB Ingress Controller, CLB Ingress Controller, and more.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For a detailed introduction and configuration steps for Ingresses, see <a href="https://docs.byteplus.com/en/docs/vke/Ingress-overview">Ingress overview</a>.</div>


<span id="LWOameHE"></span>
## DNS

The VKE cluster uses CoreDNS to achieve service discovery and DNS resolution within the cluster. CoreDNS is deployed as an add\-on in the kube\-system namespace and runs as a Pod. By default, all Pods in the cluster use CoreDNS as their DNS server, which automatically resolves internal cluster domain names and external public domain names.

The cluster allocates a fixed fully qualified domain name (FQDN) for each Service, which is in the format of `<service-name>.<namespace>.svc.cluster.local`.


* `<service-name>`: The service name.

* `namespace`: The namespace to which the service belongs.

* `cluster.local`: The default root domain name of the cluster, which can be modified.


For example, if you create a Service named service\-demo in the default namespace of the cluster, its default domain name is service\-demo.default.svc.cluster.local. Any Pod within the cluster can directly access this service by using the domain name.

<span id="vcfCxTas"></span>
##

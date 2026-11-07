---
title: "Configuring security groups"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Security-group-settings"
---

A security group is virtual firewall that implements access policies for ECS (Elastic Compute Service) instances, which share the same security requirements and trust each other in the same VPC (Virtual Private Cloud). It is an important network security mechanism that features state detection and packet filtering, and can establish a secure domain on the cloud.

With the rules of security groups, you can control inbound and outbound traffic on ECS instances. For details about security groups, see [Security groups](https://docs.byteplus.com/en/docs/vpc/Security-group-overview).

<span id=".5a655Zmo5pyN5Yqh5a6J5YWo57uE55qE5L2_55So5Y6f5YiZ"></span>
## Security group usage principles


* In a VKE cluster, business service instances are usually distributed on different nodes. To ensure requests to the services in a cluster are forwarded smoothly, all the nodes in that cluster need to share the same security group, and this security group should not be associated with any additional ECS instances.

* Security groups follow the principle of minimum necessary permissions. For the recommended and minimum scopes of the outbound and inbound rules of custom security groups, see [Access rules for clusters](https://docs.byteplus.com/en/docs/vke/Cluster-access-rules).

* To ensure a cluster can work properly, the following rules for ports that VKE relies on need to be added to the security group:

   * Allow port 22 for SSH login.

   * Allow ports from 30000 to 32768 to forward requests to NodePort services.

   * Allow port 6443 for secured requests to the Kubernetes API Server.

   * Allow port 10250, the default port exposed on the kubelet.

   * Allow container (pod) and node networks.

   * If clusters in the same VPC need to communicate with each other, you must also add rules that allow traffic from the container (Pod) and node networks of those clusters.


<span id=".6IqC54K56buY6K6k5a6J5YWo57uE6KeE5YiZ"></span>
## Default node security groups

VKE provides a security group by default for nodes named in the pattern `<cluster ID>-common` (such as `cc9l5hi6rsfek********-common`). A default security group ensures cluster and node functionality, maintains their network connectivity, and shields them from issues caused by invalid security groups. If the default security group cannot meet your requirements, you can create a security group for nodes with the necessary rules.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>



* <div data-tips="true" data-tips-type="warning">Do not modify or delete rules in node security groups unless necessary. Any changes to these rules, especially those for ports that VKE depends on, may adversely affect the cluster. </div>


* <div data-tips="true" data-tips-type="warning">Deny rules take precedence over allow rules when they share the same priority. When adding rules, ensure the new ones do not conflict with existing rules in the default security group.</div>


* <div data-tips="true" data-tips-type="warning">When a cluster is deleted, the node security groups created and applied to it will be deleted too.</div>



<span id=".5YWl5pa55ZCR6KeE5YiZ"></span>
### Inbound rules

The inbound rules of the default security group for nodes need to allow all traffic from sources within this security group. Other inbound rules can be configured according to the following table:


* Clusters with the Flannel network model:

   
   |Type |Priority |Policy |Protocol |Port range |Source address |Description |
   |---|---|---|---|---|---|---|
   |IPv4 |1 |Allow |All |\- |cd6f6astnt\*\*\*\-common (local security group) |Allow communication between nodes within this security group. Allow kube\-apiserver and virtual\-kubelet to communicate with the nodes within this security group. |
   |IPv4 |1 |Allow |All |\- |cd6f6astnt\*\*\*\-pod (Pod security group) |Allow communication between pods and nodes. |
   |IPv4 |1 |Allow |ICMP |\- |0.0.0.0/0 |Allow the ICMP protocol to support Ping. |
   |IPv4 |1 |Allow |TCP |22 |0.0.0.0/0 |Allow SSH login port. |
   |IPv4 |1 |Allow |TCP |6443 |0.0.0.0/0 |Allow public access to the API Server port. |
   |IPv4 |1 |Allow |TCP |10250 |0.0.0.0/0 |Allow the port for accessing the kubelet. |
   |IPv4 |1 |Allow |TCP |30000\-32768 |0.0.0.0/0 |Allow NodePort access on the node (LoadBalancer service usually forwards traffic based on NodePort). |
   |IPv4 |1 |Allow |UDP |30000\-32768 |0.0.0.0/0 |Allow NodePort access on the node (LoadBalancer service usually forwards traffic based on NodePort). |
   

* Clusters with the VPC\-CNI network model:

   
   |Type |Priority |Policy |Protocol |Port range |Source address |Description |
   |---|---|---|---|---|---|---|
   |IPv4 |1 |Allow |All |\- |192.168.0.0/16 (VPC CIDR) |By default, the CIDR block of the VPC is allowed, which enables all resources in the VPC to access each other. This topic uses `192.168.0.0/16` as an example. |
   |IPv4 |1 |Allow |ICMP |\- |0.0.0.0/0 |Allow the ICMP protocol to support Ping. |
   |IPv4 |1 |Allow |TCP |22 |0.0.0.0/0 |Allow SSH login port. |
   |IPv4 |1 |Allow |TCP |6443 |0.0.0.0/0 |Allow public access to the API Server port. |
   |IPv4 |1 |Allow |TCP |10250 |0.0.0.0/0 |Allow access to the kubelet port. |
   |IPv4 |1 |Allow |TCP |30000\-32768 |0.0.0.0/0 |Allow NodePort access on the node (LoadBalancer service usually forwards traffic based on NodePort). |
   |IPv4 |1 |Allow |UDP |30000\-32768 |0.0.0.0/0 |Allow NodePort access on the node (LoadBalancer service usually forwards traffic based on NodePort). |
   


<span id=".5Ye65pa55ZCR6KeE5YiZ"></span>
### Outbound rules

The outbound rules of the default security group for nodes allow all traffic by default. The following table contains details:


|Type |Priority |Policy |Protocol |Port range |Destination address |Description |
|---|---|---|---|---|---|---|
|IPv4 |1 |Allow |All |\- |0.0.0.0/0 |Allow all traffic by default. |


<span id=".cG9kLem7mOiupOWuieWFqOe7hOinhOWImQ=="></span>
## Default Pod security groups

In addition to providing the default node security group `<cluster ID>-common`, the system also automatically creates a default security group whose name is in the format of `<cluster ID>-pod`, such as `cc9l5hi6rsfek********-pod`. This group is used to configure security group policies for pods.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>



* <div data-tips="true" data-tips-type="warning">The default security group for pods is only available for <strong>VPC\-CNI\-enabled</strong> clusters. <strong>Flannel\-enabled</strong> clusters do not support it.</div>


* <div data-tips="true" data-tips-type="warning">Do not modify or delete rules in Pod security groups unless necessary. Any changes to these rules, especially those for ports that VKE depends on, may adversely affect the cluster. </div>


* <div data-tips="true" data-tips-type="warning">When a <strong>VPC\-CNI\-enabled</strong> cluster is deleted, the pod security groups created and applied to it will be deleted too.</div>



<span id=".5YWl5pa55ZCR6KeE5YiZ"></span>
### Inbound rules

The inbound rules of the default security group for pods allow all traffic by default. The following table contains details:


* Clusters with the Flannel network model:

   
   |Type |Priority |Policy |Protocol |Port range |Source address |Description |
   |---|---|---|---|---|---|---|
   |IPv4 |1 |Allow |All |\- |cd6f6astnt\*\*\*\-pod (local security group) |Allow mutual trust between pod security groups and node security groups. |
   |IPv4 |1 |Allow |All |\- |0.0.0.0/0 |Allow all traffic by default. |
   

* Clusters with the VPC\-CNI network model:

   
   |Type |Priority |Policy |Protocol |Port range |Source address |Description |
   |---|---|---|---|---|---|---|
   |IPv4 |1 |Allow |All |\- |192.168.0.0/16 (VPC CIDR) |By default, the CIDR block of the VPC is allowed, which enables all resources in the VPC to access each other. This topic uses `192.168.0.0/16` as an example. |
   |IPv4 |1 |Allow |All |\- |0.0.0.0/0 |Allow all traffic by default. |
   


<span id=".5Ye65pa55ZCR6KeE5YiZ"></span>
### Outbound rules

The outbound rules of the default security group for pods allow all traffic by default. The following table contains details:


|Type |Priority |Policy |Protocol |Port range |Destination address |Description |
|---|---|---|---|---|---|---|
|IPv4 |1 |Allow |All |\- |0.0.0.0/0 |Allow all traffic by default. |

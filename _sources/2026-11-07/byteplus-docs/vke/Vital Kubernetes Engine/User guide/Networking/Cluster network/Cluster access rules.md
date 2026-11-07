---
title: "Cluster access rules"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Cluster-access-rules"
---

After you create a cluster or node pool and specify a security group, the system applies only the default rules of VKE. No additional access rules are configured. You need to manage the security group rules yourself. This topic describes the recommended scope and minimum scope of the inbound and outbound rules that you need to configure when managing the security groups for VKE. By configuring security group rules, you can allow or deny nodes (ECS instances) inside a security group from accessing the Internet or private networks. For details on settings, see [Security group settings](https://docs.byteplus.com/en/docs/vke/Security-group-settings). For details on management, see [Management of access rules in security groups](https://docs.byteplus.com/en/docs/vpc/Managing-security-group-rules).

<span id=".5YWl5pa55ZCR6K6_6Zeu6KeE5YiZ"></span>
## Inbound access rules


|Cluster access rule |Protocol |Port |Authorized object |
|---|---|---|---|
|Recommended scope |ICMP |All |0.0.0.0/0 |
||All |All |* The default security group IDs for nodes<br><br>* The default security group IDs for pods (VPC\-CNI network model), or pod CIDR (Flannel  network model) |
|Minimum scope |All |53/53 (DNS) |* The default security group IDs for nodes<br><br>* The default security group IDs for pods  (VPC\-CNI network model), or pod CIDR (Flannel  network model) |
||ICMP |All ||
||TCP |* 10250 (Kubelet)<br><br>* 10255 (Kubelet)<br><br>* 443 (Webhook)<br><br>* 6443 (APIServer) ||
||All |Any ports that applications or add\-ons need to expose |* Any IPs of applications or add\-ons that need to be accessed<br><br>* Any IDs of security groups through which applications or add\-ons need to be accessed |


<span id=".5Ye65pa55ZCR6K6_6Zeu6KeE5YiZ"></span>
## Outbound access rules


|Cluster access rule |Protocol |Port |Authorized object |
|---|---|---|---|
|Recommended scope |All |All |0.0.0.0/0 |
|Minimum scope |All |All |100.64.0.0/10 (network segment for cloud products) |
||All |53/53 (DNS) |* The CLB IP address used by the cluster API Server<br><br>* The default security group IDs for nodes<br><br>* The default security group IDs for pods (VPC\-CNI network model), or the pod CIDR (Flannel network model) |
||TCP |* 10250 (Kubelet)<br><br>* 10255 (Kubelet)<br><br>* 443 (APIServer)<br><br>* 6443 (APIServer) ||
||All |All destination ports that applications or add\-ons need to access |* Any IPs of applications or add\-ons that need to be accessed<br><br>* Any IDs of security groups through which applications or add\-ons need to be accessed |

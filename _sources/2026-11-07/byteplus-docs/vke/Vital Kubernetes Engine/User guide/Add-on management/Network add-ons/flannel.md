---
title: "flannel"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/flannel-add-on"
---

flannel is a VKE cluster network add\-on that enables stable, efficient cross\-node container communication. This topic describes how to deploy and use the flannel add\-on in clusters.

<span id="FX4QyFvL"></span>
## Add\-on overview

flannel add\-on is a core part of the network infrastructure for VKE clusters. It uniformly assigns independent, non\-conflicting IP addresses to Pods on each node within a cluster. When combined with routing rules for the underlying VPC, it enables ‌efficient, direct cross\-node communication‌ between Pods running on different machines. For more details, see [Network overview](https://docs.byteplus.com/en/docs/vke/Container-networks).

After the add\-on is installed in the cluster, the system will create the following Kubernetes resources in the kube\-flannel namespace.


|Resource name |**Resource type** |**Resource description** |
|---|---|---|
|kube\-flannel\-ds |DaemonSet |The network proxy on nodes. It requests node\-level subnets from the control plane and automatically generates underlying CNI configuration files and host routing tables on the node. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">This add\-on is mandatory and only supported in clusters that use the Flannel network model.</div>


* <div data-tips="true" data-tips-type="default">The preceding table only lists the main resources of the add\-on, as well as resources that may be used when the add\-on or the corresponding feature is configured. This helps you understand the main components of this add\-on. Other resources, such as ConfigMap and Secret, related to the add\-on are not described here. The actual resources in the cluster shall prevail.</div>



<span id="hPDKhjgu"></span>
## Add\-on versions

For information about the historical release records of the add\-on, as well as new features and optimization descriptions for each version, see [Add-on release records](https://docs.byteplus.com/en/docs/vke/flannel).

<span id="Wk3ka7Ik"></span>
## Installing add\-ons

This add\-on is mandatory for clusters. It is automatically installed upon cluster creation, requiring no manual installation.

<span id="kJUPszyt"></span>
## Upgrading add\-ons

The add\-on is released in new versions at irregular intervals to provide new features or fix known bugs. When the add\-on card displays that a new version is available, we recommend upgrading the add\-on promptly. To ensure a smooth service transition, perform the upgrade during off\-peak hours whenever possible. For upgrade procedures and considerations, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

<span id="My0zaswI"></span>
## Related documentation


* [Network overview](https://docs.byteplus.com/en/docs/vke/Container-networks)

* [Creating managed clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster)

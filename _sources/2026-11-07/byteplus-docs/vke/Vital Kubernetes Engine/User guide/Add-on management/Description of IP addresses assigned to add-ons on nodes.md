---
title: "Description of IP addresses assigned to add-ons on nodes"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Node-IP-addresses-used-by-add-ons"
---

This topic mainly describes the number of IP addresses that can be associated with node elastic network interfaces (ENIs) used by various add\-ons in a VPC\-CNI network model cluster.

<span id=".aXAt5Y2g55So6K-05piO"></span>
## IP address usage description

When you install some add\-ons that are deployed through **DaemonSets** in a cluster that uses the VPC\-CNI network model, the add\-ons will use the number of IP addresses that can be associated with ENIs on the nodes in the cluster. For example, 10 IP addresses can be associated with ENIs on Node A in a VPC\-CNI cluster. If the csi\-ebs add\-on is installed in the cluster, the add\-on will use one IP address. As a result, the number of IP addresses that can be associated with the ENIs on Node A will change to 9.

<span id=".aXAt5Y2g55So5YiX6KGo"></span>
## Number of used IP addresses


|Add\-on name |Add\-on description |Number of used IP addresses |
|---|---|---|
|csi\-ebs |The storage service add\-on. |1 |
|csi\-local\-storage |The local data volume service add\-on. |1 |
|log\-collector |The cluster log collection add\-on. |1 |
|mgpu |The GPU sharing add\-on. |* 1 if mgpu\-exporter is not selected when the add\-on is being installed<br><br>* 2 if mgpu\-exporter is selected when the add\-on is being installed |
|node\-problem\-detector |The node health monitoring add\-on. |1 |
|nvidia\-device\-plugin |The GPU device management add\-on. |* 1 if dcgm\-exporter is not selected when the add\-on is being installed<br><br>* 2 if dcgm\-exporter is selected when the add\-on is being installed |
|p2p\-accelerator |[Public beta] The P2P container image acceleration add\-on. |1 |

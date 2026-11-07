---
title: "Associating or disassociating cloud resources"
product: "Bandwidth Package"
product_code: "bandwidthpackage"
source: "https://docs.byteplus.com/en/docs/bandwidthpackage/Associating-or-disassociating-cloud-resources"
---

This topic describes how to associate and disassociate cloud resources with elastic IP addresses (EIPs) in a Bandwidth Package.

> You can also associate and disassociate cloud resources on the EIP console. For more information, refer to [EIP> Associating cloud resources](https://docs.byteplus.com/en/docs/eip/Associating-Cloud-Resources-with-an-EIP) and [EIP >Disassociating cloud resources](https://docs.byteplus.com/en/docs/eip/Disassociating-Cloud-Resource-from-an-EIP5).


<span id="associating-cloud-resources"></span>
## Associating cloud resources

<span id="instructions"></span>
### Instructions

After an EIP is associated with an Elastic Compute Service (ECS) instance, the EIP is used as a resource of the ECS instance, just like a system volume, data volume, or primary network interface. When the ECS instance is switched to another project, the EIP is automatically switched to the project.

<span id="procedure"></span>
### Procedure


1. Log on to the [Bandwidth Package console](https://console.byteplus.com/eip/cbwps).

2. In the top navigation bar, select the region and project to which the target Bandwidth Package belongs.

3. In the Bandwidth Package list, click **Manage EIP** next to the target Bandwidth Package.

4. Click **Associate** next to the target EIP and select the target cloud resource instance.

5. Click **OK**.


<span id="disassociating-cloud-resources"></span>
## Disassociating cloud resources

<span id="limits"></span>
### Limits


* EIPs associated with a public Cloud Load Balancer (CLB) are automatically disassociated when the public CLB is changed to a private CLB.

* EIPs associated with a Internet NAT Gateway need to be disassociated on the [Internet NAT Gateway console](https://console.byteplus.com/nat/nats).


<span id="procedure"></span>
### Procedure


1. Log on to the [Bandwidth Package console](https://console.byteplus.com/eip/cbwps).

2. In the top navigation bar, select the region and project to which the target Bandwidth Package belongs.

3. In the Bandwidth Package list, click **Manage EIP** next to the target Bandwidth Package.

4. Click **Disassociate** next to a target EIP. A confirmation pop\-up window appears.

5. After confirming the information, click **OK**.

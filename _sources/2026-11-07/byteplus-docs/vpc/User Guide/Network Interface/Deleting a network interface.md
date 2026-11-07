---
title: "Deleting a network interface"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Deleting-a-network-interface"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

You can see the following actions to delete network interfaces no longer required.

<span id=".5pON5L2c6K-05piO"></span>
## Action description


* A secondary network interface that is attached to an Elastic Compute Service (ECS) instance cannot be deleted. If you need to delete it, detach it first.

* A secondary network interface with [enabling Deleted with ECS instance](https://docs.byteplus.com/en/docs/vpc/Enabling-or-disabling-deletion-with-the-ECS-instance) will be automatically deleted when the associated ECS instance is deleted.

* Neither the service network interface nor the primary network interface can be deleted from the Network Interface Console. 

   * Primary network interface: [After deleting ECS instance, ](https://docs.byteplus.com/en/docs/ecs/Deleting-ECS-instances)the primary network interface is automatically deleted with it.

   * Service network interface: To delete this network interface, simply delete the associated  service to which it belongs.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures


1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Network Interface**.

3. In the top menu bar, select the target project and region.

4. Locate the target secondary network interface, click the  **···**  ** \> Delete**.

5. Click **Delete** to complete the action.


<span id="LiRPnz18"></span>
## Related documents

[DeleteNetworkInterface](https://docs.byteplus.com/en/docs/vpc/DeleteNetworkInterface)

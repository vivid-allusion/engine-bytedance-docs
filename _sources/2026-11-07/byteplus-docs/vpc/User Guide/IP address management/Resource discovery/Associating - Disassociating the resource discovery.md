---
title: "Associating/Disassociating the resource discovery"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Associating-Disassociating-the-resource-discovery"
---

## Scenarios

Resource Discovery automatically identifies and continuously tracks the network segment usage of resources such as VPCs and subnets in a region. It cannot be used independently; it must be associated with an IPAM instance, after which IPAM can update IP address usage based on its data.

## Associate custom resource discovery

### Instructions

* The default Resource Discovery is automatically associated with the IPAM instance to which it belongs; no manual association is required.

* Before associating the Resource Discovery, the owner of the Resource Discovery has initiated the sharing, and the owner of the IPAM instance has accepted the share. For procedures, see [Shared resource discovery](https://docs.byteplus.com/en/docs/vpc/Sharing-Resource-Discovery).

* A single custom Resource Discovery can be shared with multiple accounts, but it can be associated with only one IPAM instance at a time.

* The region of the Resource Discovery instance must be consistent with the region of the IPAM instance for association to be successful.

* After a custom Resource Discovery is associated with an IPAM instance, the initial full synchronization is expected to take 5–15 minutes. After synchronization is complete, you can view the relevant VPC resources in the IPAM scope. For example, in the default IPAM scope, you can view monitoring metrics such as CIDR overlap and IP address utilization.

### Procedure

1. Log in to the [IPAM console](https://console.byteplus.com/ipam/ipam).

2. In the top menu bar, select the Region.

3. Click the name of the IPAM instance to enter the details page.

4. In the **Associated Resource Discovery** tab, click **Associate Resource Discovery**.

5. From the dropdown menu, select the Resource Discovery to be associated.

6. Click **OK** to complete the action.

## Disassociate custom resource discovery

### Instructions

* The default resource discovery cannot be disassociated.

* After a custom resource discovery is disassociated from an IPAM instance, the following impacts will affect the custom resource discovery owner and the IPAM instance owner respectively:

   * **Impact on the custom resource discovery owner**

      * **CIDR allocation becomes unavailable**: You can no longer allocate CIDR blocks from the address pools of this IPAM instance.

      * **Release assigned network segments from IPAM management**: VPCs and their secondary network segments that were previously allocated CIDRs from this address pool will be released from IPAM management and managed by the custom resource discovery owner. Business resources using these network segments are not affected; only the network segment management method changes.

   * **Impact on the IPAM instance owner**

      * **Data synchronization stops**: The IPAM instance will no longer receive data collected by this resource discovery. Existing data will be cleared during the next data update cycle (approximately 5 minutes).

      * **Reclamation of allocated CIDR blocks**: The CIDR blocks previously allocated to the custom resource discovery owner will be reclaimed by IPAM back into the address pool and can be reallocated to other associated parties.

* Unsharing a custom resource discovery does not automatically disassociate it from the IPAM instance. To associate it with a different IPAM instance, you must first manually remove the current association.

### Procedure

1. Log in to the [IPAM console](https://console.byteplus.com/ipam/ipam).

2. In the top menu bar, select the Region.

3. Click the name of the IPAM instance to enter the details page.

4. On the **Associated Resource Discovery** tab, click **Disassociate** on the right side of the target associated resource discovery.

5. Click **OK** to complete the action.

## Related documents

* [AssociateIpamResourceDiscovery](https://docs.byteplus.com/en/docs/vpc/AssociateIpamResourceDiscovery): Associate an IPAM resource discovery with an IPAM instance.

* [DisassociateIpamResourceDiscovery](https://docs.byteplus.com/en/docs/vpc/DisassociateIpamResourceDiscovery): Disassociate the custom IPAM resource discovery from the IPAM instance.

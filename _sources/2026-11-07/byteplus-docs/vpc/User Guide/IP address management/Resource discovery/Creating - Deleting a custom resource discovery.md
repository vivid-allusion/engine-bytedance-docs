---
title: "Creating/Deleting a custom resource discovery"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/IPAM-Viewing-resource-discovery"
---

## Scenarios

Resource Discovery is used to automatically identify and continuously track the CIDR usage of resources such as VPCs and subnets within a region. This enables centralized resource management and provides data support for IP address planning and allocation.

## Create custom resource discovery

### Before you begin

* The account must not have a default Resource Discovery in the current region.

* The home region of the custom resource discovery to be associated must match the home region of IPAM. After the two are associated, IPAM manages only resources within the intersection of their effective regions.

### Procedure

1. Log in to the [IPAM console](https://console.byteplus.com/ipam/ipam).

2. In the top menu bar, select the Region.

3. In the left navigation pane, select **Resource Discovery**.

4. Click **Create resource discovery**. Configure relevant parameters based on the table below.

   |Name |Description |Example value |
   |---|---|---|
   |Name |Enter the name of resource discovery. |OrgB\-Cross\-Org\-Discovery |
   |Description |Enter a description for resource discovery. |IpamResourceDiscovery\-example |
   |Operating regions |Select effective regions from the drop\-down; multiple selections are supported.<br><br><br>* The home region (i.e., the current region in the top menu bar) is selected by default and cannot be deselected. To change the home region, switch the current region in the top menu bar.<br><br>* In addition to the home region, you can select multiple other regions as effective regions. |China (Beijing) |
   |Project |Select the project to which the custom resource discovery belongs. For more information, see [Project management](https://docs.byteplus.com/en/docs/vpc/Managing-projects). |default |
   |Tag |Add one or more custom tags to custom resource discovery as needed.<br><br>A tag consists of a key\-value pair and is used for categorizing and searching resources. For more information, see [Tag management](https://docs.byteplus.com/en/docs/vpc/Managing-tags). |ResourceDiscovery:example |

5. Select the checkbox to **Allow IPAM to copy data from the source account to the IPAM admin account**.

6. Click **Create** to complete the action.

## Delete custom resource discovery

### Instructions

* Deleting default resource discovery is not supported.

* A custom Resource Discovery can be deleted only after it has been unshared.

### Procedure

1. Log in to the [IPAM console](https://console.byteplus.com/ipam/ipam).

2. In the top menu bar, select the Region.

3. In the left navigation pane, select **Resource Discovery**.

4. Click **Delete** to the right of the target Resource Discovery instance.

5. After confirming the information is correct, click **Delete** to complete the action.

## Related documents

* [CreateIpamResourceDiscovery](https://docs.byteplus.com/en/docs/vpc/CreateIpamResourceDiscovery): Create custom IPAM Resource Discovery.

* [DeleteIpamResourceDiscovery](https://docs.byteplus.com/en/docs/vpc/DeleteIpamResourceDiscovery): Delete custom IPAM Resource Discovery.

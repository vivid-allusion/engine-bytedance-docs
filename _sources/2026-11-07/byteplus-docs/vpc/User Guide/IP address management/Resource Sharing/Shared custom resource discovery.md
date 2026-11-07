---
title: "Shared custom resource discovery"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Sharing-Resource-Discovery"
---

## Scenarios

Sharing a Resource Discovery means sharing a Resource Discovery created in your own account with another account. After the recipient account accepts the share, it can associate the Resource Discovery with its own IPAM instance. Once associated, that IPAM instance can use this Resource Discovery to discover and monitor VPC resources within the coverage scope of the Resource Discovery.

Resource Discoveries created by different entities have different scopes of discoverable resources, as detailed below:

|Creation entity |Resource discovery identification scope |
|---|---|
|IPAM delegated admin |VPC resources of all member accounts within the enterprise organization that have not created a separate Resource Discovery |
|Accounts that are not IPAM delegated admins or have not joined the enterprise organization are excluded from the scope |Only VPC resources within the current account |

> **tip**

> The default Resource Discovery cannot be shared; only custom Resource Discoveries can be shared.

## Shared resource discovery

### Prerequisites

Custom resource discovery has been created. If not created, see [Creating a resource discovery](https://docs.byteplus.com/en/docs/vpc/IPAM-Viewing-resource-discovery).

### Procedures

1. Log in to the [IPAM console](https://console.byteplus.com/ipam/ipam) using the IPAM address pool owner account.

2. In the left navigation tree, select **Resource sharing \> Shared by me**.

3. In the top menu bar, select the Region.

4. On the **Shared unit** tab, click **Create shared unit**.

5. Configure parameters based on the table below.

   |Parameters |Notes |Example A |
   |---|---|---|
   |Unit name |Type in a name for the shared unit. |Resource discovery\-A |
   |Region |Select the region where the resource discovery resides. |China (Beijing) |
   |Product |Select VPC \- IPAM resource discovery. |VPC \- IPAM resource discovery |
   |Resource ID |Select the ID of the IPAM resource discovery to be shared. |Select the ID of the IPAM resource discovery |
   |Shared policy name |Defaults to and only supports RSDefaultPermissionIpamResourceDiscovery. |RSDefaultPermissionIpamResourceDiscovery |
   |Resource user |You must select **Allow sharing with any account**. |Allow sharing with any account |
   |User type |Select the root user. |Root user |
   |User ID |Enter the IPAM delegated admin account ID of the shared user. |2100\*\*\*\* |

6. Click **Next**, confirm everything is correct, then click **Confirm** to complete the actions.

## Accept shared resource discovery

### Action notes

* After accepting the shared Resource Discovery, you still need to associate it with an IPAM instance for it to take effect. For instructions, see [Attaching a custom resource discovery](https://docs.byteplus.com/en/docs/vpc/IPAM-Viewing-resource-discovery).

   > **tip**

   > A single custom Resource Discovery can be shared with multiple accounts, but it can be associated with only one IPAM instance at a time.

* Currently, resource discovery updates every 5 minutes, displaying the latest resource data.

* The initial full synchronization is expected to take 5–15 minutes. After synchronization is complete, you can view the relevant VPC resources in the IPAM scope. For example, in the default IPAM scope, you can view monitoring metrics such as CIDR overlap and IP address utilization.

### Procedures

1. Log in to the [Resource Sharing console](https://console.byteplus.com/resourcemanager/region:resource-manager+cn-beijing/resource_share/owned) using the IPAM pool owner account.

2. On the **Shared with me** page, select the region where the Resource Discovery resides.

3. Click **Accept** to the right of the IPAM Address Pool owner account.

###

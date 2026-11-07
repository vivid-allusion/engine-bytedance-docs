---
title: "Creating/Deleting an IPAM scope"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Managing-IPAM-scopes"
---

## Scenarios

An IPAM scope is the top\-level container in IPAM, where each scope represents an independent IP address space. Address pools can be created under a scope.

## Create scope

### Instructions

* Before creating an IPAM scope, you must create an IPAM instance in the target region. For the steps, see [Creating an IPAM instance](https://docs.byteplus.com/en/docs/vpc/Managing-IPAM-instances).

* A single IPAM instance supports a maximum of 5 scopes.

* Upon creation of an IPAM instance, a default private scope is automatically created by the system.

### Procedure

1. Log in to [IPAM console](https://console.byteplus.com/ipam/ipam).

2. In the top menu bar, select the region.

3. In the left navigation pane, select **IPAM Scope**.

4. Click **Create scope**.

5. Configure relevant parameters based on the table below.

   |Parameter |Description |Example |
   |---|---|---|
   |Name |Enter the name of scope. |IpamScope\-A |
   |IPAM |Fixed as the IPAM instance of that specific region.<br><br>Because only one IPAM instance is supported per region. |Ipam\-A |
   |Type |Currently, only private networks are supported. |VPC |
   |Affiliated project |Select a project for the IPAM scope. For more information, see [Project management](https://docs.byteplus.com/en/docs/vpc/Managing-projects). |default |
   |Tag |Add one or more custom tags to the IPAM scope as needed.<br><br>A tag consists of a key\-value pair and is used for categorizing and searching resources. For more information, see [Tag management](https://docs.byteplus.com/en/docs/vpc/Managing-tags). |* Tag key: Scope\-key<br><br>* Tag value: Scope\-v1 |

6. Click **OK** to complete the action.

## **Delete scope**

### Prerequisites

* Default scopes cannot be manually deleted and will only be deleted when the IPAM instance is deleted.

* The target scope contains no pools. If any exist, [delete pool](https://docs.byteplus.com/en/docs/vpc/Managing-IPAM-pools#kqek2jFH) first.

### Procedure

1. Log in to the [IPAM console](https://console.byteplus.com/ipam/ipam).

2. In the top menu bar, select the region.

3. In the left navigation pane, select **IPAM Scope**.

4. Click **Delete** to the right of the target IPAM instance.

5. Click **Delete** to complete the action.

## Related documents

* [CreateIpamScope](https://docs.byteplus.com/en/docs/vpc/CreateIpamScope): Create custom scope.

* [DeleteIpamScope](https://docs.byteplus.com/en/docs/vpc/DeleteIpamScope): Delete custom scope.

---
title: "Creating/Deleting an IPAM instance"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Managing-IPAM-instances"
---

## Scenarios

The IPAM instance is the core component that hosts the entire IP address management feature.

## Create IPAM instance

### Instructions

* Before creating an IPAM instance, it is recommended that you familiarize yourself with [IPAM address planning](https://docs.byteplus.com/en/docs/vpc/IPAM-address-planning).

* Only one IPAM instance can be created per account per region.

* If a custom Resource Discovery is created, you cannot create an IPAM instance.

* After creation, the system automatically creates one **Resource Discovery** and one **Private network scope.**

### Procedure

1. Log in to the [IPAM console](https://console.byteplus.com/ipam/ipam).

2. In the top menu bar, select the Region.

3. In the left navigation pane, select **IPAM**.

4. Click **Create IPAM**.

5. Configure the relevant parameters based on the table below.

   |Parameter |Description |Example |
   |---|---|---|
   |Operating regions |By default, the region currently selected in the top navigation bar is used as the primary region. In addition, you can also select multiple effective regions in the drop\-down menu. |China (Beijing) |
   |Name |Enter the IPAM name. |IPAM\-A |
   |Project |Select the project to which the IPAM instance belongs. For more information, see [Project management](https://docs.byteplus.com/en/docs/vpc/Managing-projects). |default |
   |Tags |Add one or more custom tags to the IPAM instance as needed.<br><br>A tag consists of a key\-value pair and is used for categorizing and searching resources For more information, see [Tag management](https://docs.byteplus.com/en/docs/vpc/Managing-tags). |* tag key: IPAM\-key<br><br>* Tag value: IPAM\-v1 |

6. Click **OK** to complete the action.

## Delete IPAM instance

### Instructions

* Apart from the default scope, no other scopes exist in the IPAM instance. If any exist, first [Delete scope](https://docs.byteplus.com/en/docs/vpc/Managing-IPAM-scopes).

* The default scope contains no address pools. If any exist, first [Delete pool](https://docs.byteplus.com/en/docs/vpc/Managing-IPAM-pools#kqek2jFH).

### Procedure

1. Log in to the [IPAM console](https://console.byteplus.com/ipam/ipam).

2. In the top menu bar, select the Region.

3. In the left navigation pane, select **IPAM**.

4. Click **Delete** to the right of the target IPAM instance.

5. Click **Delete** to complete the action.

## Related documents

* [CreateIpam](https://docs.byteplus.com/en/docs/vpc/CreateIpam): Create IPAM instance.

* [DeleteIpam](https://docs.byteplus.com/en/docs/vpc/DeleteIpam): Delete IPAM instance.

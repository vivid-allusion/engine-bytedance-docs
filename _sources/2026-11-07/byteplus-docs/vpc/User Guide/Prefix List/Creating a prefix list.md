---
title: "Creating a prefix list"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Creating-a-prefix-list"
---

## Procedures

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Prefix List**.

3. In the top menu bar, select the target project and region.

4. Click **Create Prefix List**.

5. Configure relevant parameters based on the table below.

   |Parameter |Description |Sample value |
   |---|---|---|
   |Name |Enter the name of prefix list. |PrefixList\-1 |
   |Address type |Select the address type for the CIDR blocks that can be added to the prefix list. Once a type is selected, only CIDR blocks of that type can be added.<br><br><br>* IPv4: IPv4 type.<br><br>* IPv6: IPv6 type. |IPv4 |
   |Max entries |The maximum number of prefix list entries that can be added to an imported prefix list ranges from 1 to 200.<br><br>> **tip**<br><br><br>> Prefix list's maximum entry count consumes associated resource quota. We recommend setting this after evaluating related resource quotas. You can also [modify the maximum entries](https://docs.byteplus.com/en/docs/vpc/Modifying-the-prefix-list) after creation.<br> |100 |
   |Prefix List Entry |Enter one or more CIDRs as needed. After creation, you can also add prefix list entries as needed. For details, see [Add a prefix list entry](https://docs.byteplus.com/en/docs/vpc/Managing-entries-in-the-prefix-list#.5re75Yqg5YmN57yA5YiX6KGo5p2h55uu). |10.0.0.0/24<br><br>192.168.1.0/24 |
   |Related project |Select the project to which the prefix list belongs. For more information, see [Project management](https://docs.byteplus.com/en/docs/vpc/Managing-projects). |default |
   |Tags |Add one or more custom tags to the prefix list as needed. A tag consists of a Tag Key and a Tag Value. Tags can be used to categorize and filter prefix lists. More information is available in [Tag management](https://docs.byteplus.com/en/docs/vpc/Managing-tags). |PrefixList1:v1 |

6. Click **Create** to complete the action.

## Related documents

[CreatePrefixList](https://docs.byteplus.com/en/docs/vpc/CreatePrefixList)

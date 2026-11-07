---
title: "Managing Traffic Mirror Filter"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Managing-traffic-mirror-filter"
---

## Create traffic mirror filter

### Action description

A single account in a single region supports creating up to 10,000 Mirror Filters.

### Procedures

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select Traffic Mirror \> Filter.

3. Click **Create Mirror Filter**.

4. Enter the traffic mirror filter name. This topic uses Filter\-A.

5. Click  **+Add rule** to add more inbound or outbound traffic mirror filter rules.

6. Please see the table below to configure the relevant parameters for inbound rules and outbound rules.

   |Parameter |Description |Inbound rule example |Outbound rule example |
   |---|---|---|---|
   |Priority |The priority of a filter rule, ranging from 1 to 1000, with 1 being the highest priority. For the same Mirror Filter and the same direction (inbound/outbound), the priority must be unique. |1 |1 |
   |Strategy |Policy for the Traffic Mirror Filter.<br><br><br>* Allow: When traffic from the mirror site matches this rule, it is copied to the Mirror Target for monitoring and analysis.<br><br>* Deny: When traffic from the mirror site matches this rule, it is not copied, meaning monitoring and analysis for this traffic is rejected. |Allow |Allow |
   |Agreement |Supports ALL, TCP, UDP, ICMP，ICMPv6 protocols. |ALL |ALL |
   |Source address and port |Set the source address (supports IPv4 and IPv6) and port of traffic. |0.0.0.0/0<br><br>ALL |192.168.0.11/32<br><br>ALL |
   |Destination address and port |Set the destination address(supports IPv4 and IPv6)  and port for the traffic. |192.168.0.11/32<br><br>ALL |0.0.0.0/0<br><br>ALL |

7. View the table below to configure projects and tags.

   |Parameter |Description |Sample value |
   |---|---|---|
   |Related project |Select the project to which the Mirror Filter belongs. For more information, see [Project management](https://docs.byteplus.com/en/docs/vpc/Managing-projects). |default |
   |Tags |Add one or more custom tags as needed for the filter criteria.<br><br>A tag consists of a Tag Key and a Tag Value, and is used to categorize and organize Mirror Filters. For more information, see [Tag management](https://docs.byteplus.com/en/docs/vpc/Managing-tags).<br><br>Click the add icon to add multiple tags. |Target:v1 |

8. Click **Create** to complete the action.

## Delete Traffic Mirror Filter

**Prerequisites**

The traffic mirror filter is not associated with any traffic mirror session. If associated, [delete the traffic mirror session](https://docs.byteplus.com/en/docs/vpc/Managing-a-Traffic-Mirror-session).

**Procedures**

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Traffic Mirror \> Mirror Filter**.

3. Click **Delete ** on the right side of the target traffic mirror filter.

4. Click **Delete** to complete the action.

## Add filter rule

**Prerequisites**

Traffic Mirror Filter is created. If not created, [create a mirror session](https://docs.byteplus.com/en/docs/vpc/Managing-a-Traffic-Mirror-session).

**Procedures**

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Traffic Mirror \> Mirror Filter**.

3. Click the name of the target traffic mirror filter.

4. On the Inbound rules or Outbound rules tab, click **Add rule**, which will open a window for creating inbound or outbound rules.

5. Configure the related parameters. For details, see [Creating Traffic Mirror Filter](https://docs.byteplus.com/en/docs/vpc/Managing-traffic-mirror-filter#5WuHa71Y).

6. Click  **+Add rule** to add more inbound or outbound traffic mirror filter rules.

7. Click **Add** to complete the action.

## Modify filter rule

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Traffic Mirror \> Mirror Filter**.

3. Click the name of the target traffic mirror filter.

4. On the Inbound rules or Outbound rules tab, find the target security group rule, then click **Modify** on the right side to modify the rule.

5. After modifying the relevant arguments as needed, click **Save** to complete the action.

## Delete filter rule

Deleting a traffic mirror filter will automatically delete all filter rules contained within it.

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Traffic Mirror \> Mirror Filter**.

3. Click the name of the target traffic mirror filter.

4. On the Inbound rules or Outbound rules tab, find the target traffic mirror filter rule, then click **Delete** on the right side.

5. Click **Delete** to complete the action.

## Related documents

* [CreateTrafficMirrorFilter](https://docs.byteplus.com/en/docs/vpc/CreateTrafficMirrorFilter)

* [DeleteTrafficMirrorFilter](https://docs.byteplus.com/en/docs/vpc/DeleteTrafficMirrorFilter)

* [CreateTrafficMirrorFilterRule](https://docs.byteplus.com/en/docs/vpc/CreateTrafficMirrorFilterRule)

* [ModifyTrafficMirrorFilterRuleAttributes](https://docs.byteplus.com/en/docs/vpc/ModifyTrafficMirrorFilterRuleAttributes)

* [DeleteTrafficMirrorFilterRule](https://docs.byteplus.com/en/docs/vpc/DeleteTrafficMirrorFilterRule)

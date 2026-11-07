---
title: "Optimizing paths for different subnets within a VPC to reach an on-premises data center via Direct Connects"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Realize-the-Optimization-of-Different-Subnets-in-VPC-to-Access-IDC"
---

This topic describes how to enable different subnets within a Virtual Private Cloud (VPC) to access an on\-premises data center through different Direct Connect (DC) links.

<span id=".5Zy65pmv5LuL57uN"></span>
## Scenarios

Transit Router (TR) offers rich routing capabilities. By configuring forwarding and route policies, traffic from different subnets within the same VPC can use separate links to access the on\-premises data center, enabling active\-standby failover configuration for DC links.

As shown in the networking scenario below, the subnet (subnet01) accesses the data center with dcv01 as the primary link and dcv02 as the secondary, while subnet02 accesses the data center with dcv02 as the primary and dcv01 as the secondary.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_199b76a2c4abe722a398daf6dd876bcb.png) </span>

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

You have properly connected the VPC and two DC Gateways to the TR instance and achieved interconnection between the VPC and the on\-premises data center.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The system route table of the TR instance is named tr01\-rtb\-sys and used as an example.</div>


<span id=".5pWw5o2u6KeE5YiS"></span>
## Data planning

Before configuration, plan the CIDR blocks, routes, and other data parameters for each network resource in the diagram as shown below.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_52d8fad9dcf1d07aa356bfb2c0087023.png) </span>

<span id=".6YWN572u5q2l6aqk"></span>
## Configuration procedures

<span id=".5q2l6aqk5LiA77ya5Yib5bu6VFLot6_nlLHooajlubbphY3nva7ot6_nlLE="></span>
### Step 1: Create a TR route table and configure routing


1. Follow the procedure in [Creating a route table](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-03) to create a TR route table (named tr01\-rtb\-set).

2. Follow the procedure in [Create a route learning rule](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-06#.5Yib5bu66Lev55Sx5a2m5Lmg) to configure routes for tr01\-rtb\-set. Select the attachment types as the VPC (vpc01), DC Gateways (dcg01 and dcg02), and the TR instance in sequence.


<span id=".5q2l6aqk5LqM77ya6YWN572u6Lev55Sx562W55Wl"></span>
### Step 2: Configure route policy


1. Follow the procedure in [Creating a route policy](https://docs.byteplus.com/en/docs/transitrouter/Creating-a-routing-policy) to create two inbound route policies. The specific policy entries are shown in the table below.

   * Route policy 1

      
      |Priority |Match conditions |Policy action |Route attribute settings |
      |---|---|---|---|
      |1 |Source instance ID = ID of DC Gateway (dcg02) |Allow |Append AS Path, `123` |
      

   * Route policy 2

      
      |Priority |Match conditions |Policy action |Route attribute settings |
      |---|---|---|---|
      |1 |Source instance ID = ID of DC Gateway (dcg01) |Allow |Append AS Path, `123` |
      

2. Associate the two route policies from the previous step to the respective TR route tables (tr01\-rtb\-sys and tr01\-rtb\-set) following the instructions in [Associate a route policy to TR route table](https://docs.byteplus.com/en/docs/transitrouter/Binding-Unbinding-Modifying-routing-policy-for-TR-route-table).

3. Select the **Route entry** tab. Review that all routes with the next hop as the DC Gateway have routing property added, and the status of entries with longer AsPath becomes **Not effective**. The details are shown in the diagram below (using tr01\-rtb\-sys as an example).


<span id=".5q2l6aqk5LiJ77ya6YWN572u6L2s5Y-R562W55Wl"></span>
### Step 3: Configure forwarding policy


1. Follow the procedure in [Creating a forwarding policy](https://docs.byteplus.com/en/docs/transitrouter/Creating-a-forwarding-policy) to create one forwarding policy for the TR instance. The specific policy entries are shown in the table below.

   
   |Priority |Source |Forward route table |
   |---|---|---|
   |1 |172.16.2.0/24 |tr01\-rtb\-set |
   

2. Follow the procedure in [Configuring forwarding policy for an attachment](https://docs.byteplus.com/en/docs/transitrouter/Enabling-Disabling-Modifying-forwarding-policy) to apply the forwarding policy from Step 1 to the VPC attachment. This enables the traffic from the subnet (subnet02) to be forwarded based on the TR route table (tr01\-rtb\-set).


<span id=".57uT5p6c6aqM6K-B"></span>
## Result validation


1. Log in to Elastic Compute Service (ECS) instances in respective subnets (subnet01 and subnet02). For procedure, see [Logging on to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance) or [Logging on to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Execute the following commands on both ECS instances to consecutively send data to the on\-premises data center.

   * The instance in subnet01

      * Linux: `ping -s 5000 -c 10000 192.168.1.12`

      * Windows: `ping -l 5000 192.168.1.12 -t`

   * The instance in subnet02

      * Linux: `ping -s 10000 -c 10000 192.168.1.12`

      * Windows: `ping -l 10000 192.168.1.12 -t`

4. Observe the monitoring metric "Attachment inbound bandwidth" of the attachment.

   Based on the commands set in step 2, the "Attachment inbound bandwidth" for attachments (attach\-dcg01 and attach\-dcg02) is approximately in a 1:2 ratio. This indicates that access traffic from subnet01 is forwarded via TR to dcg01 to access the on\-premises data center, while traffic from subnet02 is forwarded via TR to dcg02 to access the data center.

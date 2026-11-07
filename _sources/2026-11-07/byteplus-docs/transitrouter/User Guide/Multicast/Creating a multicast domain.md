---
title: "Creating a multicast domain"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Creating-a-multicast-domain"
---

<span id="evnOzY1P"></span>
## Prerequisites


* Ensure that the Transit Router (TR) instance has multicast enabled. If it is not enabled, create a new TR instance with multicast enabled.

* Ensure that a Virtual Private Cloud (VPC) attachment has been created in the target TR.


<span id="CmcjtUij"></span>
## Instructions


* A single TR instance can create up to 20 multicast domains by default.

* A single multicast domain supports associating a maximum of 10 subnets by default. If the default quota is insufficient,[ create a quota application](https://console.byteplus.com/quota/productList) to request a quota increase.

* Multicast traffic is not affected by subnet ACLs at the attachment point, but is subject to the subnet ACL and security group of the Elastic Compute Service (ECS).


<span id="xnzQ0nzc"></span>
## Procedure


1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Click the name of the target TR instance.

3. In the zone below **Basic information**, select the **Multicast domain** tab.

4. Click **Create Multicast Domain** and configure the multicast domain based on the table below.

   
   |Parameter |Description |Example |
   |---|---|---|
   |**Basic information** |||
   |Transit Router |Defaults to the selected TR instance, requiring no manual configuration. |tr01 |
   |Name |Input the name of the multicast domain. |MulticastDomain\-Uf7N |
   |**Attach subnet** |||
   |VPC/Subnet |Select the VPC that has attached to the TR instance, and then select the subnet to be added to the multicast domain. |vpc01 |
   |**Advanced option** |||
   |Tags |A tag is a tag key\-value object and is used to categorize and search for resources. [Learn more](https://docs.byteplus.com/en/docs/transitrouter/Tags)<br><br>Click Add tag, enter the tag key and tag value, then add a tag to the multicast domain. |* Tag key: md\-k1<br><br>* Tag value: md\-v1 |
   

5. Click **Create** to complete the action.


<span id="QTe4DL2F"></span>
## What to do next

Add a multicast source to the multicast domain, specify the multicast group it belongs to, and add multicast members. Once configured, the multicast source will send multicast traffic to the multicast group, and all multicast members in the group will receive the multicast traffic sent by the source.


* [Add a multicast source](https://docs.byteplus.com/en/docs/transitrouter/Managing-the-multicast-source#yWkTcEed)

* [Add a multicast member](https://docs.byteplus.com/en/docs/transitrouter/Managing-multicast-members#Udkr59Yx)


<span id="9Jc3xsET"></span>
## Related documentation

[CreateTransitRouterMulticastDomain](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterMulticastDomain): Create a multicast domain for a specified TR instance.

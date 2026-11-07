---
title: "Creating a Transit Router instance"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/TransitRouter-instances-01"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

When you require private network communication between parts of multiple Virtual Private Clouds (VPCs) or between a VPC and a data center, Transit Router (TR) will help. To configure a TR, first create a TR instance.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Ensure you have completed BytePlus [account registration](https://docs.byteplus.com/en/docs/6261/64925) and real\-name authentication.

* Complete [account recharge](https://docs.byteplus.com/en/docs/6269/100434) and ensure the total value of your BytePlus account balance (cash balance) plus available coupons is equal to or greater than USD 100. Otherwise, you will be unable to purchase TR or other cloud resources.


<span id=".5pON5L2c6K-05piO"></span>
## Instructions

By default, a single account supports a maximum of 5 TR instances in a single region. If this quota is insufficient, you can request an increase through the [Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=Auto_Scaling), up to an absolute upper limit of 10 instances.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. In the top menu bar, select the target project and region.

3. Click **Create TR** and configure related parameters based on the table below.

   
   |Parameter |Description |Example |
   |---|---|---|
   |Regions |Select the region for the TR instance. |China (Guangzhou) |
   |Name |Type the name for the TR instance to be created. |tr01 |
   |ASN |An Autonomous System (AS) is a network unit on the internet with a unified routing policy, composed of one or more networks and identified by a unique Autonomous System Number (ASN). Specify a private ASN for the TR instance from the range of 64512–65534 or 4200000000–4294967294.<br><br><br>* When networking within the same region, you can assign any ASN from the specified range for the TR instance.<br><br>* When networking across regions, you must assign different ASNs for TR instances in different regions.<br><br>* When connecting on\-premises data centers via a TR and a Direct Connect (DC), the ASNs for the TR and the DC Gateway must be unique.<br><br>* When connecting a single TR instance to multiple DC Gateways to access different data centers, the ASNs for these DC Gateways must also be unique.<br><br><br>After being assigned with an ASN, the TR automatically prepends the ASN to the AsPath attribute of routes published to other network instances.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"> For cross\-region networking scenarios, it is strongly recommended to use ​​different ASNs for Transit Routers in different regions​​; otherwise, cross\-region route propagation may break.</div><br> |64512 |
   |Multicast |Specify whether to enable multicast for the TR instance. [Learn more](https://docs.byteplus.com/en/docs/transitrouter/Multicast-Overview)<br><br>Multicast is a point\-to\-multipoint communication method that supports data packets sent by one server being received by multiple clients simultaneously.<br><br><br>* Only TR instances with multicast enabled support multicast configuration.<br><br>* Multicast can only be enabled when creating the TR instance. After creation, this setting cannot be modified. |Check |
   |Related project |Select the project to which the TR instance belongs. After you select a project, only users that have permissions on the project can use the created instance. [Learn more](https://docs.byteplus.com/en/docs/transitrouter/Projects)<br><br><br>* If you select **All Resources** in the top menu bar before entering the creation page, the TR instance belongs to the default project. You can reselect a project as needed.<br><br>* If you select a specific project in the top menu bar before entering the creation page, the TR instance belongs to that project by default. To associate it with another project, change the project to **All Resources** or the target project in the top menu bar.<br><br>* When you create a TR instance, the system automatically generates a system route table for it. This TR system route table belongs to the same project as the TR instance. |default |
   |Tags |A tag consists of a key\-value pair and is used for categorizing and searching resources. [Learn more](https://docs.byteplus.com/en/docs/transitrouter/Tags)<br><br>Click **Add tag**, type the tag key and tag value to add tags to the TR instance. |* Tag key: tr\-k1<br><br>* Tag value: tr\-v1 |
   |Agreement |Follow the console guidance to review and accept the legal terms. |Check |
   

4. Click **Create** to complete the action.

5. Click **Go to console** to view the created TR instance.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next

When you create a TR instance, the system automatically creates a system route table for it. To forward TR traffic to other network resources (such as a VPC), you also need to create attachments for this TR instance. For procedure, see [Intra-region attachments](https://docs.byteplus.com/en/docs/transitrouter/Attachments-vpc).

<span id=".55u45YWz5paH5qGj"></span>
## Related documentation


* [CreateTransitRouter](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouter): Create a TR instance.

* [What's the difference between Transit Router (TR) and Cloud Enterprise Network (CEN)](https://docs.byteplus.com/en/docs/transitrouter/Product-Overview-01#.5Lit6L2s6Lev55Sx5Zmo5LiO5LqR5LyB5Lia572R55qE5a-55q-U)

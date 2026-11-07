---
title: "Associating EIPs"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/associating-an-EIP"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Applicable scenario

You can associate an ECS instance with an Elastic IP Address (EIP) to enable the instance to access the internet.

This topic describes how to associate an ECS instance with an EIP (specifically, the "ECS instance" here refers to the primary private IPv4 address of the primary network interface associated with the instance).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To associate an EIP with the secondary private IPv4 address of the primary network interface or the private IPv4 address of a secondary network interface for an ECS instance, refer to <a href="https://docs.byteplus.com/en/docs/vpc/Associating-or-disassociating-an-EIP">Associating an EIP with a network interface</a>.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite

You have not associated the ECS instance (the primary private IPv4 address of the instance primary network interface) with an EIP.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left\-side navigation pane, select "Instances & Images \> Instances".

3. In the top menu bar, select the region and project of the target instance.

4. On the Instances page, select "··· \> Network and security group \> Associate Elastic IP Address" on the right side of the target instance. Then, the "Bind Elastic IP address (EIP)" window pops up.

   You can also click the instance name to go to the instance overview page. Then, in the EIP section, click the "Associate Elastic IP Address" button.

5. Select the target EIP and click the "Attach" button to complete the operation.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To associate an EIP with an ECS, you can perform this action in the ECS console or EIP console. For details, refer to <a href="https://docs.byteplus.com/en/docs/eip/Associating-Cloud-Resources-with-an-EIP">Associating cloud resources</a>.</div>


<span id=".5pON5L2c57uT5p6c"></span>
## Operation results

The instance page will display the associated EIP of the selected instance.

> If an ECS instance cannot connect to the Internet after you associate an EIP with it, refer to [Why can't an ECS instance associated with an EIP connect to the Internet?](https://docs.byteplus.com/en/docs/eip/EIP-FAQs#.5Li65LuA5LmI5LqR5pyN5Yqh5Zmo5a6e5L6L57uR5a6a5YWs572RaXDku43nhLbml6Dms5Xov57mjqXkupLogZTnvZHvvJ8=).


After you associate an ECS instance with an EIP, their relations are as follows:


* EIP becomes a sub\-resource of the ECS instance, such as the system volume, data volume, and primary network interface of the instance. When you transfer an ECS instance to another project, the associated EIP will change to that project accordingly.

* When you renew or unsubscribe from a subscription\-based instance, you can select whether to renew or unsubscribe from the associated subscription\-based EIP.

* When you renew or unsubscribe from a subscription\-based EIP, you can select whether to renew or unsubscribe from the associated subscription\-based instance.


<span id=".55u45YWz5paH5qGj"></span>
## Related document

[AssociateEipAddress](https://docs.byteplus.com/en/docs/eip/AssociateEipAddress): Associate EIPs with cloud resources.

---
title: "Disassociating EIP"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Disassociating-an-EIP"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Applicable scenarios

This topic describes how to disassociate an EIP from an ECS instance (that is, the primary private IPv4 address of the primary network interface) in the ECS console.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">To associate an EIP with the secondary private IPv4 address of a primary network interface, or to associate an EIP with a private IPv4 address of a secondary network interface, refer to <a href="https://docs.byteplus.com/en/docs/vpc/Associating-or-disassociating-an-EIP">Disassociating EIPs from network interfaces.</a></div>


* <div data-tips="true" data-tips-type="tip">You can also disassociate an EIP from an ECS instance in the EIP console. For more information, see <a href="https://docs.byteplus.com/en/docs/eip/Disassociating-Cloud-Resource-from-an-EIP">Disassociating cloud resources</a>.</div>


* <div data-tips="true" data-tips-type="tip">An EIP that is disassociated from an ECS instance is not released automatically and you are still charged for the EIP. If you no longer use the EIP, you can <a href="https://docs.byteplus.com/en/docs/eip/Releasing-an-EIP">release the EIP</a>.</div>



<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left\-side navigation pane, select "Instances & Images \> Instances".

3. In the top menu bar, select the region and project of the target instance.

4. On the Instances page, click "... \> Network and security group \> Disassociate Elastic IP Address" in the "Actions" column of the target instance.

   You can also click the instance name to go to the instance overview page and click "Disassociate Elastic IP Address" in the public IP address field.

5. Click "Disassociate" to complete the operation.


<span id=".5pON5L2c57uT5p6c"></span>
## Operation result

On the instance list page, the public IP address is no longer displayed for the corresponding instance.

<span id=".55u45YWz5paH5qGj"></span>
## Related document

[DisassociateEipAddress](https://docs.byteplus.com/en/docs/eip/DisassociateEipAddress): Disassociates EIPs from cloud resources.

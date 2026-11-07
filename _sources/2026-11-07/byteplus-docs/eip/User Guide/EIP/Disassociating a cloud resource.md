---
title: "Disassociating a cloud resource"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/Disassociating-Cloud-Resource-from-an-EIP"
---

If your cloud resource no longer needs to access the internet or requires replacing the Elastic IP Address (EIP), disassociate it from the EIP. After disassociating the EIP, the Elastic Compute Service (ECS) instance loses internet access. Proceed only after confirming no impact on your business.

<span id=".57qm5p2f6ZmQ5Yi2"></span>
## Limits


* Public Load Balancers do not support disassociating EIPs. You can [convert them to private Load Balancers](https://docs.byteplus.com/en/docs/clb/CLB-instances-04) before disassociating.

* An EIP associated with an Internet NAT gateway must be disassociated on the Internet NAT Gateway page.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


<Tabs>
<Tab zoneid="TflKwIFARE" title="Disassociate General">
<TabTitle>Disassociate General</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Tip</div>


<div data-tips="true" data-tips-type="default">Here, general instances refer to ECS instances, Private Cloud Load Balancers (CLBs), secondary network interfaces, High\-Availability Virtual IP Addresses (HAVIPs) and IP addresses.</div>



1. Log in [to the EIP console](https://console.byteplus.com/eip/eips).

2. In the top menu bar, select the region and project of your target EIP.

3. In the EIP list, click **Disassociate ** to the right of the target EIP to open the confirm detachment dialog.

4. Click **Disassociate** to complete the action.


</Tab>
<Tab zoneid="PKlcxUMbbS" title="Disassociate Internet NAT Gateway">
<TabTitle>Disassociate Internet NAT Gateway</TabTitle>

<span id="B5atPp3P"></span>
### Disassociate Internet NAT Gateway

The target EIP must not be attached to any SNAT entry or DNAT entry before disassociation. If attached, refer to [deleting an SNAT entry](https://docs.byteplus.com/en/docs/natgateway/Managing-SNAT-rules#.5Yig6ZmkU05BVOinhOWImQ==) or [deleting a DNAT entry](https://docs.byteplus.com/en/docs/natgateway/Managing-DNAT-rules#.5Yig6ZmkRE5BVOinhOWImQ==).


1. Log in [to the EIP console](https://console.byteplus.com/eip/eips).

2. In the top menu bar, select the region and project of your target EIP.

3. In the EIP list, click the name of the Internet NAT gateway to the right of the target EIP.

4. On the EIP tab, click **Disassociate** to the right of the target EIP, and a confirmation dialog box appears.

5. Click **Disassociate** to complete the action.


</Tab>
</Tabs>


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[DisassociateEipAddress](https://docs.byteplus.com/en/docs/eip/DisassociateEipAddress): Disassociate an EIP from its associated cloud resource instance.

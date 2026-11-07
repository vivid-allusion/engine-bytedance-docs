---
title: "Managing an SNAT entry"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/Managing-SNAT-rules"
---

An Elastic Compute Service (ECS) instance without an associated Elastic IP Address (EIP) can access the internet through the SNAT entry of an Internet NAT Gateway. This topic describes how to create, modify, and delete an SNAT entry.

<span id=".5Yib5bu6U05BVOinhOWImQ=="></span>
## Create an SNAT entry

After creating an SNAT entry, your ECS instances can share the EIP associated with the SNAT entry to access the internet.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
### Prerequisites


* The Internet NAT Gateway is associated with an EIP.

* The CIDR block for the newly created SNAT entry cannot be the same as any existing SNAT entries.

* When multiple SNAT entries have overlapping CIDR blocks, the system matches SNAT entries based on the longest subnet mask. That is, the longer the subnet mask of the SNAT entry, the higher the priority. For example, an SNAT entry at granularity of ECS with a subnet mask of /32 has the highest priority due to its longest length.

* Make sure the route table linked to your ECS instance's subnet (for the SNAT entry) includes a custom route entry.The recommended destination Classless Inter\-Domain Routing (CIDR) block for this entry is 0.0.0.0/0, with the target Internet NAT Gateway instance as the next hop. This ensures the SNAT entry takes effect. For specific actions, see [Add route](https://docs.byteplus.com/en/docs/vpc/Managing-a-route-entry).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you create your first Internet NAT Gateway in a Virtual Private Cloud (VPC), the system automatically adds a custom route entry with a destination CIDR block of 0.0.0.0/0 and the next hop of the Internet NAT Gateway instance in the system route table, routing traffic to the Internet NAT Gateway.   </div>
   

<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in to the [Internet NAT Gateway console](https://console.byteplus.com/nat/nats).

2. In the top menu bar, select a target region and project.

3. In the list of Internet NAT Gateways, click the name of the target NAT Gateway.

4. Select the **SNAT rules** tab, then click **Create SNAT rule**.

5. Configure relevant parameters based on the table below.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |Name |Enter the name of the SNAT rule. Enter the name of the SNAT rule. |snat\-1snat\-1 |
   |Granularity |Set the granularity of the SNAT entry.<br><br><br>* Subnet: The subnet of the VPC to which your Internet NAT Gateway belongs. All ECS instances that are not associated with any EIPs within this subnet can access the internet through the SNAT entry.<br><br>* VPC: The VPC to which your Internet NAT Gateway belongs. All ECS instances that are not associated with any EIPs within the VPC can access the internet through the SNAT entry.<br><br>* ECS: select an ECS instance within the VPC of the Internet NAT Gateway. The selected instance can access the internet through the SNAT entry.<br><br>* Custom CIDR: The custom CIDR block. All ECS instances that are not associated with any EIPs within the specified CIDR block can access the internet through the SNAT entry. |Subnet<br><br>subnet\-1\|192.XX.XX.0/24 |
   |EIP |Select the EIP associated with the Internet NAT Gateway.<br><br><br>* Select a single EIP: Select a single EIP from the dropdown list. All business connections access the internet through this EIP.<br><br>* Select multiple EIPs: Select multiple EIPs from the dropdown list. Business connections access the internet through relative EIPs assigned by the five\-tuple hashing algorithm.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When a SNAT rule is associated with multiple EIPs, we recommend adding the EIPs to a Bandwidth Package to prevent any traffic packet loss caused by any one EIP reaching its bandwidth limit.​​</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you associate the same EIP with both your DNAT entry and SNAT entry, service preemption may occur. Therefore, we recommend that you associate your DNAT entry and SNAT entry with different EIPs.</div><br> |12.XX.XX.89\|eip\-1 |
   

6. Click **OK** to complete the action.


<span id=".5L-u5pS5U05BVOinhOWImQ=="></span>
## Modify an SNAT entry

After creating an SNAT entry, you can modify its name and EIP.

<span id="FR2mGUXp"></span>
### Instructions

Modifying an EIP in an SNAT entry will cause the existing SNAT connection drop. To re\-establish the connection, a request made from the ECS instance is required. Proceed with caution.

<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in to the [Internet NAT Gateway console](https://console.byteplus.com/nat/nats).

2. In the top menu bar, select a target region and project.

3. In the list of Internet NAT Gateways, click the name of the target NAT Gateway.

4. Select the **SNAT rules** tab. On the right side of the target SNAT entry list, click **Edit** to modify the name and EIP.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Note the following when modifying the EIP of the SNAT entry:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Single EIP: If you select a single EIP from the drop\-down list, all business connections access the internet through the EIP.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Multiple EIPs: If you select multiple EIPs from the drop\-down list, business connections access the internet through relative EIPs assigned by the five\-tuple hashing algorithm. It is recommended to add the EIPs to a Shared Bandwidth Package to prevent any traffic packet loss caused by reaching the bandwidth cap of a single EIP.   </div>
   

5. Click **OK** to complete the action.


<span id=".5Yig6ZmkU05BVOinhOWImQ=="></span>
## Delete an SNAT entry

If you no longer need an SNAT entry, you can follow this procedure to delete it.


1. Log in to the  [Internet NAT Gateway console](https://console.byteplus.com/nat/nats).

2. In the top menu bar, select a target region and project.

3. In the list of Internet NAT Gateways, click the name of the target NAT Gateway.

4. Select the **SNAT rules** tab, click **Delete** on the right side of the target SNAT entry list.

5. Click **Delete** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [CreateSnatEntry](https://docs.byteplus.com/en/docs/natgateway/CreateSnatEntry): Create an SNAT entry.

* [ModifySnatEntryAttributes](https://docs.byteplus.com/en/docs/natgateway/ModifySnatEntryAttributes): Modify the name and associated EIPs of an SNAT entry.

* [DeleteSnatEntry](https://docs.byteplus.com/en/docs/natgateway/DeleteSnatEntry): Delete an SNAT entry.

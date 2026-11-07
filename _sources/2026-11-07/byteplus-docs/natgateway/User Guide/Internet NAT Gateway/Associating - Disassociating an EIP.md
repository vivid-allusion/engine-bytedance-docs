---
title: "Associating/Disassociating an EIP"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/Associating-or-disassociating-an-EIP"
---

This topic describes how to associate or disassociate an Elastic IP Address (EIP).

<span id=".57uR5a6a5YWs572RSVA="></span>
## Associate an EIP

<span id=".5YmN5o-Q5p2h5Lu2"></span>
### Prerequisites


* An unassociated EIP is available; if none, [apply for an EIP](https://docs.byteplus.com/en/docs/eip/Applying-for-an-EIP).

* The number of EIPs already associated with the target Internet NAT Gateway has not reached the quota. See [Limits](https://docs.byteplus.com/en/docs/natgateway/Limits).

* The current account is in arrears or entering arrears less than 2 hours. For more operations, see [Recharge guide](https://docs.byteplus.com/en/docs/6269/100434).

* A single Internet NAT Gateway supports associating up to 10 EIPs. If the default quota cannot meet your needs, go to [Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=NATGW) to increase the corresponding quota.


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in to the [Internet NAT Gateway console](https://console.byteplus.com/nat/nats).

2. In the top menu bar, select a target region and project.

3. Locate the target Internet NAT gateway and click **Configure EIP** on its right side.

4. Click **Associate EIP**.

5. Select one or more EIPs.

6. Click **OK** to complete the action.


<span id=".6Kej57uR5YWs572RSVA="></span>
## Disassociate an EIP

<span id=".5YmN5o-Q5p2h5Lu2"></span>
### Prerequisites


* The EIP is not attached to an SNAT entry. If attached, see Deleting SNAT entry.

* Internet IP is not associated with a DNAT entry. If it has been attached, see Deleting DNAT entry.


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in to the [Internet NAT Gateway console](https://console.byteplus.com/nat/nats).

2. In the top menu bar, select a target region and project.

3. In the Internet NAT Gateway list, click the name of the target NAT gateway.

4. On the EIPs tab, click **Disassociate** to the right of the target EIP.

5. Click **OK** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [AssociateEipAddress](https://docs.byteplus.com/en/docs/eip/AssociateEipAddress): Associate an EIP with a cloud resource.

* [DisassociateEipAddress](https://docs.byteplus.com/en/docs/eip/DisassociateEipAddress): Disassociate an EIP from a cloud resource.

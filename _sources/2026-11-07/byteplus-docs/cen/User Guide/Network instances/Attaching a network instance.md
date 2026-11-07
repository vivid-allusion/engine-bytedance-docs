---
title: "Attaching a network instance"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/Network-instances-01"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

When multiple network instances (specifically Virtual Private Clouds (VPC) and Direct Connect Gateways) require private network connectivity, they can be attached to the same Cloud Enterprise Network (CEN) instance.

<span id=".5pON5L2c6K-05piO"></span>
## Action description


* A Direct Connect Gateway that has already been installed on a Transit Router cannot be attached to a CEN instance.

* A network instance can only be installed on one CEN instance.

* If the network instance is not from this Account, please authorize it to CEN of this Account. The operations for different types of network instances are as follows:

   * Virtual Private Cloud (VPC): see [Adding cross-account authorization](https://docs.byteplus.com/en/docs/vpc/Managing-CEN-cross-account-authorization).

   * Direct Connect: see [CEN cross-account authorization](https://docs.byteplus.com/en/docs/directconnect/Cross-account-authorization).

* If the subnet CIDR block of a VPC conflicts with that of a VPC already installed on the CEN instance, routes for the conflicting CIDR block will not be published.

* If there are custom route entries in the VPC's system route table, you can [publish them to the Cloud Enterprise Network (CEN)](https://docs.byteplus.com/en/docs/vpc/Publishing-or-canceling-a-route-for-a-CEN#.5Y-R5biD6Lev55Sx5p2h55uu5Yiw5LqR5LyB5Lia572R) as needed.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures


1. Log in to the [CEN console](https://console.byteplus.com/cen/EnterpriseNetwork).

2. In the top navigation bar, select the target project.

3. Click the target CEN instance name.

4. On the **Network Instances** tab, click **Attach Network Instance**.

5. Configure relevant parameters based on the table below.

   
   |Parameter |Explanation |Sample value |
   |---|---|---|
   |Account |Select the account to which the network instance belongs.<br><br><br>* This Account: the Account to which the CEN belongs.<br><br>* Cross\-Account: Enter the peer account ID. |Cross\-account |
   |Regions |Select the region where the network instance resides. |China (Beijing) |
   |Instance type |Supports selecting the network instance type.<br><br><br>* VPC<br><br>* Direct Connect Gateway<br><br><br>If you select Direct Connect Gateway, you also need to use it with the Direct Connect service. For details, see [Direct Connect Quick Start Guide](https://docs.byteplus.com/en/docs/directconnect/Quick-start). |VPC |
   |Network Instances |Select a network instance. |VPC\-2 |
   

6. Click **Attach** to complete the action.

7. To install multiple network instances, repeat the steps above.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[AttachInstanceToCen](https://docs.byteplus.com/en/docs/cen/AttachInstanceToCen)

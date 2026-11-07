---
title: "Managing a DNAT rule"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/Managing-DNAT-rules-vpcnat"
---

This topic describes how to create, modify, or delete a DNAT rule for VPC NAT Gateway.

<span id=".5Yib5bu6RE5BVOinhOWImQ=="></span>
## Create a DNAT rule

<span id=".5pON5L2c6K-05piO"></span>
### Instructions

You can create a maximum of 100 DNAT rules for a single NAT Gateway. If the default quota cannot meet your needs, go to [Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=NATGW) to increase the corresponding quota.

<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in to the [VPC NAT Gateway console](https://console.byteplus.com/nat/vpcNat).

2. In the top menu bar, select a target region and project.

3. In the VPC NAT Gateway list, click  **··· \> Configure DNAT rule** on the right side of the target VPC NAT Gateway.

4. On the **DNAT rules** tab, click **Create DNAT rule**

5. Configure relevant parameters based on the table below.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |Name |Enter the name of the DNAT entry. |dnat\-1 |
   |Protocol |Select protocol type. Supported protocols include TCP, UDP. |TCP |
   |Local IP |Set the private IP address of the Elastic Compute Service instance and the port or port range that provides external services.<br><br><br>* The valid range is 1 to 65535.<br><br>* If entering a port range, separate the start and end ports with a hyphen (\-), for example, 20\-25. |192.168.XX.XX<br><br>80 |
   |NAT IP |Set the NAT IP address of the VPC NAT Gateway and the port or port range that receives private network requests from outside this VPC.<br><br>The port number of the NAT IP address must match the port number of the Local IP. For example, if the Local IP port is 20, the NAT IP port must also be 20; if the Local IP port is 20\-25, the NAT IP port must also be 20\-25.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the DNAT entry and SNAT entry link to the same NAT IP address, service conflicts may occur. It is recommended to associate different NAT IP addresses with DNAT and SNAT entries.</div><br> |natip\-1<br><br>80 |
   

6. Click **Create** to complete the action.

7. After the DNAT entry is created, you also need to allow the corresponding traffic in the security group.

   1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

   2. Click the ECS instance name, select the Security Group tab, and click the security group name.

   3. On the **Access rules \> Inbound** tab, add a rule. Set policy to Allow, protocol type to TCP/UDP, port range to Local IP ports, and source address to 0.0.0.0/0. For more details, see Security group overview.


<span id=".5L-u5pS5RE5BVOinhOWImQ=="></span>
## Modify a DNAT rule

You can follow this procedure to modify the DNAT rule's name, protocol, local IP, local IP port, NAT IP, and NAT IP port as needed.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The NAT IP port number and local IP port number must be consistent.</div>



1. Log in to the [VPC NAT Gateway console](https://console.byteplus.com/nat/vpcNat).

2. In the top menu bar, select a target region and project.

3. In the VPC NAT Gateway list, click  **··· \> Configure DNAT rule** on the right side of the target VPC NAT Gateway.

4. On the **DNAT rules** tab, click **Edit** on the right side of the target DNAT entry list. Modify the name, protocol, local IP address, port of the local IP address, NAT IP address, and port of the NAT IP address as needed.

5. Click **OK** to complete the action.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you modify the local IP or its port in the DNAT rule, open the corresponding security group rules in the VPC. For details, see <a href="https://docs.byteplus.com/en/docs/vpc/Security-group-overview">Security group overview</a>.</div>


<span id=".5Yig6ZmkRE5BVOinhOWImQ=="></span>
## Delete a DNAT rule

When a DNAT rule is no longer needed, you can follow this procedure to delete it.


1. Log in to the [VPC NAT Gateway console](https://console.byteplus.com/nat/vpcNat).

2. In the top menu bar, select a target region and project.

3. In the VPC NAT Gateway list, click  **... \> Configure DNAT rule** on the right side of the target VPC NAT Gateway.

4. On the **DNAT rules** tab, click **Delete** on the right side of the target DNAT entry.

5. Click **Delete** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [CreateDnatEntry](https://docs.byteplus.com/en/docs/natgateway/CreateDnatEntry): Create a DNAT rule.

* [ModifyDnatEntryAttributes](https://docs.byteplus.com/en/docs/natgateway/ModifyDnatEntryAttributes): Modify a DNAT rule.

* [DeleteDnatEntry](https://docs.byteplus.com/en/docs/natgateway/DeleteDnatEntry): Delete a DNAT rule.

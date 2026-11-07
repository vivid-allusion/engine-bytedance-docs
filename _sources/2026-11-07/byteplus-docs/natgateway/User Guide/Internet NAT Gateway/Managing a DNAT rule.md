---
title: "Managing a DNAT rule"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/Managing-DNAT-rules"
---

ECS instances without EIPs can provide services to the internet through the DNAT rules of the Internet NAT Gateway. This topic explains how to create, modify, and delete DNAT rules.

<span id=".5Yib5bu6RE5BVOinhOWImQ=="></span>
## Create DNAT rule

After creating a DNAT rule, ECS instances without EIPs can provide services to the internet.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
### Prerequisites


* The Internet NAT gateway is associated with an EIP.

* The ECS instance is not associated with an Elastic IP (EIP). EIPs have a higher priority than route tables. If the ECS instance is assigned an EIP, traffic is forwarded to the EIP instead of the Internet NAT gateway.


<span id=".5pON5L2c6K-05piO"></span>
### Action description

You can create a maximum of 100 DNAT rules for a single NAT gateway. If the default quota cannot meet your needs, go to [Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=NATGW) to increase the corresponding quota.

<span id=".5pON5L2c5q2l6aqk"></span>
### Procedures


1. Log in to the  [Internet NAT Gateway console](https://console.byteplus.com/nat/nats).

2. In the top menu bar, select a target region and project.

3. In the list of Internet NAT gateways, click the name of the target NAT gateway.

4. Select the **DNAT rules** tab, and click **Create DNAT rule**.

5. Enter the name of the DNAT rule, such as dnat\-1.

6. Select the port type, and configure related parameters according to the table below.

   * All ports: Refers to IP mapping. Resources with a private IP can communicate with the internet via the EIP, and this EIP cannot be associated with other SNAT or DNAT rules.

      
      |Parameter |Explanation |Sample value |
      |---|---|---|
      |Agreement |Only ANY is supported. |ANY |
      |Private IP and its port |Enter the private IP address of the cloud resource. Port input is not supported here. |10.XX.XX.12 |
      |Elastic IP (EIP) and its port |Select the EIP from the dropdown menu. Port input is not supported here. |12.XX.XX.89\|eip\-1 |
      

   * Specific port: Refers to port mapping. For requests accessing the EIP, the Internet NAT Gateway will forward them to the corresponding private IP and port based on the protocol and port.

      Refer to the table below to configure the relevant parameters:

      
      |Parameter |Explanation |Sample value |
      |---|---|---|
      |Agreement |Select protocol type. Supported protocols include TCP, UDP. |TCP |
      |Private IP and its port |Set the private IP of the ECS instance and the port or port range on which it provides services to the internet.<br><br><br>* The valid range is 1 to 65535.<br><br>* If entering a port range, separate the start and end ports with a hyphen (\-), for example, 20\-25. |10.XX.XX.12<br><br>80 |
      |Elastic IP (EIP) and its port |Set the EIP bound to the Internet NAT Gateway and the port or port range on which it receives requests from the internet.<br><br><br>* The valid range is 1 to 65535.<br><br>* If a port range is entered for the private IP port, a port range must also be entered for the EIP port. The number of ports must be the same for both, and the start and end ports are separated by a hyphen (\-). For example, if the private IP port is 20\-25, the EIP port should be 30\-35.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you associate the same EIP with both your DNAT entry and SNAT entry, service preemption may occur. Therefore, we recommend that you associate your DNAT entry and SNAT entry with different EIPs.</div><br> |12.XX.XX.89\|eip\-1<br><br>80 |
      

7. After the DNAT rule is created, you also need to allow the corresponding traffic in the security group.

   1. Log in to the  [ECS console ](https://console.byteplus.com/ecs/instance).

   2. Click the ECS instance name, select the Security Group tab, and click the security group name.

   3. On the **Access rules \> Inbound** tab, add a rule. Set the policy to **Allow**, select the protocol type as **TCP** or **UDP**, set the port range to **Private IP Port**, and set the source address to **0.0.0.0/0**. For more details, see [Security group overview](https://docs.byteplus.com/en/docs/vpc/Security-group-overview).


<span id=".5L-u5pS5RE5BVOinhOWImQ=="></span>
## Modify DNAT rule

You can refer to this operation to modify the name, protocol, private IP, private IP port, EIP, and EIP port of the DNAT rule as needed.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When the port type in the DNAT rule is All Ports, only the name, private IP, and EIP can be modified.</div>



1. Log in to the  [Internet NAT Gateway console](https://console.byteplus.com/nat/nats).

2. In the top menu bar, select a target region and project.

3. In the list of Internet NAT gateways, click the name of the target NAT gateway.

4. Select the **DNAT rules** tab, click **Edit** on the right side of the target DNAT entry list, and modify the DNAT entry's name, protocol, private IP address and its port, and EIP and its port as needed.

5. Click **Migrate** to complete the action.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you modify the private IP or private IP port of a DNAT rule, please ensure the corresponding security group rules are allowed in the VPC. For details, see <a href="https://docs.byteplus.com/en/docs/vpc/Security-group-overview">Security group overview</a>.</div>


<span id=".5Yig6ZmkRE5BVOinhOWImQ=="></span>
## Delete DNAT rule

When a DNAT rule is no longer needed, you can refer to this operation to delete it.


1. Log in to the  [Internet NAT Gateway console](https://console.byteplus.com/nat/nats).

2. In the top menu bar, select a target region and project.

3. In the list of Internet NAT gateways, click the name of the target NAT gateway.

4. Select the **DNAT rules** tab, and click **Delete** to the right of the target DNAT entry.

5. Click **Migrate** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [CreateDnatEntry](https://docs.byteplus.com/en/docs/natgateway/CreateDnatEntry): Create DNAT rules.

* [ModifyDnatEntryAttributes](https://docs.byteplus.com/en/docs/natgateway/ModifyDnatEntryAttributes): Modify DNAT rules.

* [DeleteDnatEntry](https://docs.byteplus.com/en/docs/natgateway/DeleteDnatEntry): Delete DNAT rules.

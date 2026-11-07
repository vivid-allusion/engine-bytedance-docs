---
title: "NAT Gateway FAQs"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/NAT-gateway-FAQ"
---

* [Why did the Internet NAT Gateway creation fail?](https://docs.byteplus.com/en/docs/51/10041#.5Yib5bu65YWs572RTkFU572R5YWz5aSx6LSl5piv5LuA5LmI5Y6f5Zug77yf)

* [Why is NAT Gateway traffic not flowing?](https://docs.byteplus.com/en/docs/51/10041#bG3m29ZX)

* [How many SNAT rules and DNAT rules can a single Internet NAT Gateway support?](https://docs.byteplus.com/en/docs/51/10041#.5LiA5Liq5YWs572RTkFU572R5YWz5pyA5aSa5pSv5oyB5Yib5bu65aSa5bCR5p2hU05BVOinhOWIme-8jOWkmuWwkeadoUROQVTop4TliJnvvJ8=)

* [How many Internet NAT Gateway instances can be created in a single VPC?](https://docs.byteplus.com/en/docs/51/10041#.5LiA5LiqVlBD5pSv5oyB5Yib5bu65aSa5bCR5Liq5YWs572RTkFU572R5YWz5a6e5L6L77yf)

* [What is the maximum number of EIPs that a single Internet NAT Gateway instance can bind?](https://docs.byteplus.com/en/docs/51/10041#.5LiA5Liq5YWs572RTkFU572R5YWz5a6e5L6L5pyA5aSa5pSv5oyB57uR5a6a5aSa5bCR5Liq5YWs572RSVDvvJ8=)

* [Can a single EIP be associated with both an SNAT rule and a DNAT rule simultaneously?](https://docs.byteplus.com/en/docs/51/10041#.5LiA5Liq5YWs572RSVDlj6_ku6XlkIzml7blhbPogZRTTkFU6KeE5YiZ5ZKMRE5BVOinhOWImeWQl--8nw==)

* [Which protocol packets does the Internet NAT Gateway support forwarding?](https://docs.byteplus.com/en/docs/51/10041#.5YWs572RTkFU572R5YWz5pSv5oyB6L2s5Y-R5ZOq5Lqb5Y2P6K6u55qE5oql5paH77yf)

* [Do Internet NAT Gateways support ICMP proxy?](https://docs.byteplus.com/en/docs/51/10041#.5YWs572RTkFU572R5YWz5pSv5oyBSUNNUOS7o-etlOWQl--8nw==)

* [What is the relationship between a VPC, ECSs, EIPs, and an Internet NAT Gateway?](https://docs.byteplus.com/en/docs/51/10041#.56eB5pyJ572R57uc44CB5LqR5pyN5Yqh5Zmo44CB5YWs572RSVDjgIHlhaznvZFOQVTnvZHlhbPkuYvpl7TmnInku4DkuYjlhbPns7vvvJ8=)

* [Is there a difference between an ECS using an Internet NAT Gateway and directly binding an EIP?](https://docs.byteplus.com/en/docs/51/10041#.5LqR5pyN5Yqh5Zmo5L2_55So5YWs572RTkFU572R5YWz5ZKM55u05o6l57uR5a6a5YWs572RSVDmnInljLrliKvlkJfvvJ8=)

* [Does the Internet NAT Gateway support changing its associated VPC?](https://docs.byteplus.com/en/docs/51/10041#.5YWs572RTkFU572R5YWz5piv5ZCm5pSv5oyB5pu05o2iVlBD77yf)

* [How does the Internet NAT Gateway achieve high availability?](https://docs.byteplus.com/en/docs/51/10041#.5YWs572RTkFU572R5YWz5aaC5L2V5a6e546w6auY5Y-v55So5oCn77yf)

* [How can I view the network interfaces and security groups of an Internet NAT Gateway?](https://docs.byteplus.com/en/docs/51/10041#.5aaC5L2V5p-l55yL5YWs572RTkFU572R5YWz55qE572R5Y2h5ZKM5a6J5YWo57uE77yf)

* [How do I configure and view the routes for an Internet NAT Gateway?](https://docs.byteplus.com/en/docs/51/10041#.5aaC5L2V6YWN572u5ZKM5p-l55yL5YWs572RTkFU572R5YWz6Lev55Sx77yf)

* [How can I monitor the traffic of an Internet NAT Gateway?](https://docs.byteplus.com/en/docs/51/10041#.5aaC5L2V55uR5o6n5YWs572RTkFU572R5YWz55qE5rWB6YeP77yf)

* [What is network ACL traffic control?](https://docs.byteplus.com/en/docs/51/10041#gQrzZ123)


<span id=".5Yib5bu65YWs572RTkFU572R5YWz5aSx6LSl5piv5LuA5LmI5Y6f5Zug77yf"></span>
## Why did the Internet NAT Gateway creation fail?

Possible causes:


|Cause |Description |
|---|---|
|No Internet NAT Gateway resources deployed in the availability zone |The availability zone where the subnet selected during Internet NAT Gateway creation is located has no Internet NAT Gateway resources deployed. For related actions, see [Creating an Internet NAT Gateway](https://docs.byteplus.com/en/docs/natgateway/Creating-an-Internet-NAT-gateway). |
|Exceeded quota limits |You have reached the maximum of Internet NAT Gateways that can be created in the VPC. For more details, see [Limits](https://docs.byteplus.com/en/docs/natgateway/Limits). |
|Insufficient balance |* When creating a Pay\-As\-You\-Go Internet NAT Gateway, the total value of the account's [Available Balance](https://docs.byteplus.com/en/docs/6269/100429) and vouchers applicable to Internet NAT Gateways was less than 100.00 USD, or the Available Balance was 0. For related procedures, see [Recharge guide](https://docs.byteplus.com/en/docs/6269/100434).<br><br>* When creating a Subscription Internet NAT Gateway, the total value of the account's [Available Balance](https://docs.byteplus.com/en/docs/6269/100429) and vouchers applicable to Internet NAT Gateways is insufficient to cover the cost. For related procedures, see [Recharge guide](https://docs.byteplus.com/en/docs/6269/100434). |
|Network lag |When creating a Subscription Internet NAT Gateway, network lag causing unsuccessful payment may also lead to creation failure. |
|API parameter error |Invalid parameters are provided when calling CreateNatGateway to create an Internet NAT Gateway. For details, see [Error codes](https://docs.byteplus.com/en/docs/natgateway/CreateNatGateway#.6ZSZ6K-v56CB). |


<span id="bG3m29ZX"></span>
## Why is NAT Gateway traffic not flowing?


* First NAT Gateway: If traffic cannot be forwarded properly between the NAT Gateway and the Virtual Private Cloud (VPC), it may be due to a conflict in the destination CIDR block of the system route. After the first NAT Gateway is created, the system automatically adds a custom route entry to the VPC route table with a destination CIDR block of 0.0.0.0/0 and the NAT Gateway instance as the next hop. If the VPC route table already contains a route entry with the destination CIDR block 0.0.0.0/0, the NAT Gateway traffic will be blocked. [Modify your route configuration](https://docs.byteplus.com/en/docs/vpc/Managing-a-route-entry), or see [Delete route entry](https://docs.byteplus.com/en/docs/vpc/Managing-a-route-entry#.5Yig6Zmk6Lev55Sx5p2h55uu) and [Withdraw route entry from CEN](https://docs.byteplus.com/en/docs/vpc/Publishing-or-canceling-a-route-for-a-CEN#.5LuO5LqR5LyB5Lia572R5pKk5Zue6Lev55Sx5p2h55uu) for solution.

* Additional NAT Gateways: If traffic is not flowing through an additional NAT Gateway, check whether its route table contains a custom route entry with a destination CIDR block of 0.0.0.0/0 and the target NAT Gateway instance as the next hop. For more details, see [Deploying multiple Internet NAT Gateways in a single VPC](https://docs.byteplus.com/en/docs/natgateway/Configuring-multiple-Internet-NAT-Gateways-in-a-VPC).


<span id=".5LiA5Liq5YWs572RTkFU572R5YWz5pyA5aSa5pSv5oyB5Yib5bu65aSa5bCR5p2hU05BVOinhOWIme-8jOWkmuWwkeadoUROQVTop4TliJnvvJ8="></span>
## How many SNAT rules and DNAT rules can a single Internet NAT Gateway support?

By default, a maximum of 40 SNAT rules and 100 DNAT rules are supported. If the default quota is insufficient, visit the BytePlus [Quota Center](https://console.byteplus.com/quota/productList) to request an increase for the corresponding quota.

<span id=".5LiA5LiqVlBD5pSv5oyB5Yib5bu65aSa5bCR5Liq5YWs572RTkFU572R5YWz5a6e5L6L77yf"></span>
## How many Internet NAT Gateway instances can be created in a single VPC?

Up to 3.

<span id=".5LiA5Liq5YWs572RTkFU572R5YWz5a6e5L6L5pyA5aSa5pSv5oyB57uR5a6a5aSa5bCR5Liq5YWs572RSVDvvJ8="></span>
## What is the maximum number of EIPs that a single Internet NAT Gateway instance can bind?

Default: 10. If the default quota cannot meet your needs, go to BytePlus [Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=NATGW) to increase the corresponding quota.

<span id=".5LiA5Liq5YWs572RSVDlj6_ku6XlkIzml7blhbPogZRTTkFU6KeE5YiZ5ZKMRE5BVOinhOWImeWQl--8nw=="></span>
## Can a single EIP be associated with both an SNAT rule and a DNAT rule simultaneously?

Yes, but it is not recommended, because the SNAT rule and DNAT rule are associated with the same Elastic IP Address (EIP), which may cause service contention issues.

<span id=".5YWs572RTkFU572R5YWz5pSv5oyB6L2s5Y-R5ZOq5Lqb5Y2P6K6u55qE5oql5paH77yf"></span>
## Which protocol packets does the Internet NAT Gateway support forwarding?

The Internet NAT Gateway supports forwarding TCP, UDP, and ICMP packets. FTP protocol is currently not supported.

<span id=".5YWs572RTkFU572R5YWz5pSv5oyBSUNNUOS7o-etlOWQl--8nw=="></span>
## Do Internet NAT Gateways support ICMP proxy?

Yes, supported.

<span id=".56eB5pyJ572R57uc44CB5LqR5pyN5Yqh5Zmo44CB5YWs572RSVDjgIHlhaznvZFOQVTnvZHlhbPkuYvpl7TmnInku4DkuYjlhbPns7vvvJ8="></span>
## What is the relationship between a VPC, ECSs, EIPs, and an Internet NAT Gateway?


* A VPC is a virtual network environment for cloud resources. Different VPCs are isolated from each other.

* Elastic Compute Service (ECS) is a computing resource running within a VPC.

* EIPs provide public network access and bandwidth.

* The Internet NAT Gateway provides network address translation services and, combined with EIPs, enables ECS instances to communicate with the internet.


<span id=".5LqR5pyN5Yqh5Zmo5L2_55So5YWs572RTkFU572R5YWz5ZKM55u05o6l57uR5a6a5YWs572RSVDmnInljLrliKvlkJfvvJ8="></span>
## Is there a difference between an ECS using an Internet NAT Gateway and directly binding an EIP?

There is a difference.


* An ECS directly bound to an EIP has exclusive use of that EIP.

* Multiple ECS instances can share an EIP by using an Internet NAT Gateway.

* EIPs have a higher priority than route tables. If the ECS instance is assigned an EIP, traffic is forwarded to the EIP instead of the Internet NAT Gateway.


<span id=".5YWs572RTkFU572R5YWz5piv5ZCm5pSv5oyB5pu05o2iVlBD77yf"></span>
## Does the Internet NAT Gateway support changing its associated VPC?

Unsupported.

<span id=".5YWs572RTkFU572R5YWz5aaC5L2V5a6e546w6auY5Y-v55So5oCn77yf"></span>
## How does the Internet NAT Gateway achieve high availability?

An Internet NAT Gateway achieves high availability through dual\-cluster cold standby and cross\-AZ disaster recovery. During creation, the primary availability zone is automatically paired with a secondary availability zone. If the primary zone fails, the system automatically fails over to the secondary zone, ensuring continuous service availability.

<span id=".5aaC5L2V5p-l55yL5YWs572RTkFU572R5YWz55qE572R5Y2h5ZKM5a6J5YWo57uE77yf"></span>
## How can I view the network interfaces and security groups of an Internet NAT Gateway?


<Tabs>
<Tab zoneid="QDtdMuX0yr" title="View network interface of Internet NAT gateway">
<TabTitle>View network interface of Internet NAT gateway</TabTitle>

1. Log in to the [Internet NAT Gateway console](https://console.byteplus.com/nat/nats).

2. In the top menu bar, select a target region and project.

3. In the NAT Gateway List, click the target NAT Gateway name,

4. Click the name of the **Basic information** under **Network interface** to view network interface details.


</Tab>
<Tab zoneid="EMh5S9IPiN" title="View security group of Internet NAT gateway">
<TabTitle>View security group of Internet NAT gateway</TabTitle>

1. Log in to the [Internet NAT Gateway console](https://console.byteplus.com/nat/nats).

2. In the top menu bar, select a target region and project.

3. In the NAT Gateway List, click the name of the target Internet NAT Gateway.

4. Hover over the VPC name in the **Basic information** section, and click the copy icon in the popup to copy the VPC ID.

5. Click **Security group** in the left\-side navigation pane to access the security group page.

6. Click the drop\-down button next to the search box in the upper\-right corner of the page, select **VPC ID**, and paste the VPC ID into the search box.

7. The page will display all security groups under this VPC. The one named **nat\-default** with **Internet NAT Gateway Service Security Group \- Non\-operable** shown in the actions column is the Internet NAT Gateway's security group.


You can select **Name** in the search box and enter **nat\-default** in the search bar to find all Internet NAT Gateway security groups under the current account.


</Tab>
</Tabs>


<span id=".5aaC5L2V6YWN572u5ZKM5p-l55yL5YWs572RTkFU572R5YWz6Lev55Sx77yf"></span>
## How do I configure and view the routes for an Internet NAT Gateway?


<Tabs>
<Tab zoneid="GvPOG5IEQO" title="Configure Internet NAT gateway routes">
<TabTitle>Configure Internet NAT gateway routes</TabTitle>


|**Classification** |**Description** |
|---|---|
|First Internet NAT Gateway created in a VPC |The system automatically configures routes for it in the system route table. |
|Additional Internet NAT Gateway created in a VPC |You need to manually configure routes for it. |





</Tab>
<Tab zoneid="AEGtfdpfiu" title="View Internet NAT gateway routes">
<TabTitle>View Internet NAT gateway routes</TabTitle>

1. Log in to the [Internet NAT Gateway console](https://console.byteplus.com/nat/nats).

2. In the top menu bar, select a target region and project.

3. Hover the mouse over the name of the target Internet NAT Gateway's VPC and click the pop\-up <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_931330a0e5bfc2581cf4d4a1d33af3d9.png) </span>copy icon. Copy the VPC ID.

4. Click **VPC** in the left navigation pane.

5. Click the <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_9a8b40fe2eb46636dd6136bf3f12a89f.png) </span>drop\-down button next to the search box in the upper right corner of the page, select **ID**, and paste the VPC ID into the search box.

6. Click the VPC name, click **Route table**, and you can view the route table of this VPC.

7. Click the route table name, click the **Route entry** tab, and view the Internet NAT Gateway route.


> If multiple route tables exist, you need to click each route table name to check for the NAT Gateway's route entries. For more route table information, see [Route Table overview](https://docs.byteplus.com/en/docs/vpc/Route-table-overview).


</Tab>
</Tabs>


<span id=".5aaC5L2V55uR5o6n5YWs572RTkFU572R5YWz55qE5rWB6YeP77yf"></span>
## How can I monitor the traffic of an Internet NAT Gateway?


* You can monitor it through CloudMonitor for the Internet NAT Gateway. For details, see [Viewing monitoring data](https://docs.byteplus.com/en/docs/natgateway/Viewing-monitoring-data-vpcnat).

* Through VPC flow logs, for details, see [Viewing the traffic of the ECS instance accessing the internet or being accessed by the internet through the Internet NAT Gateway](https://docs.byteplus.com/en/docs/vpc/Use-cases#.5LqR5LiK5YWs572R).


<span id="gQrzZ123"></span>
## What is network ACL traffic control?

[Network ACL](https://docs.byteplus.com/en/docs/vpc/Network-ACL-overview) (Network Access Control List) controls inbound and outbound traffic for subnets. It is designed based on an allowlist model. Traffic entering or leaving a private subnet must be permitted by an ACL entry to pass through. The Network ACL traffic control feature is a switch provided on the NAT Gateway side that determines whether ACL entries apply to **traffic entering or leaving the NAT Gateway**. After a NAT Gateway instance is created, the system defaults to enable ACL entries. To change the enablement status of traffic control, please contact your account manager.

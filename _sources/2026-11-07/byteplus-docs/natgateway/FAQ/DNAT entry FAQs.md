---
title: "DNAT entry FAQs"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/DNAT-entry-FAQ"
---

* [Why use DNAT entries?](https://docs.byteplus.com/en/docs/51/10038#.5Li65LuA5LmI5L2_55SoRE5BVOinhOWIme-8nw==)

* [My ECS has a DNAT entry configured but is still not reachable from the Internet. Why?​](https://docs.byteplus.com/en/docs/51/10038#.5bey6YWN572uRE5BVOinhOWImeeahOS6keacjeWKoeWZqOaXoOazleiiq-WFrOe9keiuv-mXru-8nw==)

* [How many DNAT entries can a single Internet NAT gateway support?](https://docs.byteplus.com/en/docs/51/10038#.5Y2V5Liq5YWs572RTkFU572R5YWz5pSv5oyB5Yib5bu65aSa5bCR5p2hRE5BVOinhOWIme-8nw==)

* [Can a CLB use an Internet NAT Gateway's DNAT entry to provide external services?​](https://docs.byteplus.com/en/docs/51/10038#.6LSf6L295Z2H6KGh5pSv5oyB5L2_55So5YWs572RTkFU572R5YWz55qERE5BVOinhOWImeWvueWkluaPkOS-m-acjeWKoeWQl--8nw==)


<span id=".5Li65LuA5LmI5L2_55SoRE5BVOinhOWIme-8nw=="></span>
## Why use DNAT entries?

When multiple Elastic Compute Service (ECS) instances need to provide services to the Internet, it is recommended to use DNAT entries. Compared to binding an Elastic IP Address (EIP) to each ECS instance, DNAT entries allow multiple ECS instances to share one EIP and bandwidth, reducing Internet usage costs and simplifying unified management of the Internet entry point. For related actions, see Creating DNAT entries.

<span id=".5bey6YWN572uRE5BVOinhOWImeeahOS6keacjeWKoeWZqOaXoOazleiiq-WFrOe9keiuv-mXru-8nw=="></span>
## **My ECS has a DNAT entry configured but is still not reachable from the internet. Why?** 

Possible causes:


|Cause |Description |
|---|---|
|Route does not exist |Check if the attached route table of the subnet to which the ECS instance belongs contains a custom route entry with destination CIDR 0.0.0.0/0 and next hop as the target Internet NAT Gateway instance. If not, add it manually. For related operations, see [Add route](https://docs.byteplus.com/en/docs/vpc/Managing-a-route-entry#70HRpqsH). |
|Security group and network ACL configuration conflict |Check whether the corresponding security group and network ACL rules allow traffic. For more details, see [Network ACL overview](https://docs.byteplus.com/en/docs/vpc/Network-ACL-overview) and [Security group overview](https://docs.byteplus.com/en/docs/vpc/Security-group-overview). |
|Cloud resource exception |Check the status of the ECS, EIP, and Internet NAT Gateway, such as suspension due to expiration or suspension due to arrears. |
|Associate an EIP |Check whether the ECS instance is associated with an EIP. The priority of an EIP is higher than the route table. Therefore, after the ECS instance is associated with an EIP, its traffic is forwarded through the EIP and cannot use DNAT entries to provide services to the Internet. |


<span id=".5Y2V5Liq5YWs572RTkFU572R5YWz5pSv5oyB5Yib5bu65aSa5bCR5p2hRE5BVOinhOWIme-8nw=="></span>
## How many DNAT entries can a single Internet NAT Gateway support?

The default supports the creation of 100 DNAT entries. If the default quota is insufficient, please go to BytePlus [Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=NATGW) to increase the corresponding quota.

<span id=".6LSf6L295Z2H6KGh5pSv5oyB5L2_55So5YWs572RTkFU572R5YWz55qERE5BVOinhOWImeWvueWkluaPkOS-m-acjeWKoeWQl--8nw=="></span>
## Can a CLB use an Internet NAT Gateway's DNAT entry to provide external services?

Yes. When creating a DNAT entry, set the private IP and port parameters to match the private IP and port of the target Classic Load Balancer (CLB).

The target CLB instance cannot bind to an EIP because the EIP has higher priority than the route table. If the CLB instance binds an EIP, its traffic forwards through the EIP and cannot use the DNAT feature of the Internet NAT Gateway.

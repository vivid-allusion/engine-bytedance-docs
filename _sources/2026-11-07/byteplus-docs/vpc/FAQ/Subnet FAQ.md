---
title: "Subnet FAQ"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Subnet-FAQ"
---


|Issue category |Issue |
|---|---|
|Limits |* [How many subnets can be created per account?](https://docs.byteplus.com/en/docs/47/4635#.5LiA5Liq6LSm5Y-35pSv5oyB5Yib5bu65aSa5bCR5Liq5a2Q572R77yf)<br><br>* [What CIDR blocks can subnets use?](https://docs.byteplus.com/en/docs/47/4635#.5a2Q572R5YWB6K645L2_55So55qE572R5q615piv5LuA5LmI77yf) |
|Feature |* [Can subnets communicate with each other?](https://docs.byteplus.com/en/docs/47/4635#.5a2Q572R6Ze05piv5ZCm5Y-v5Lul5LqS55u46YCa5L-h77yf)<br><br>* [Can subnet CIDR blocks be modified?](https://docs.byteplus.com/en/docs/47/4635#.5a2Q572R55qE572R5q615piv5ZCm5Y-v5Lul5L-u5pS577yf)<br><br>* [How to identify resources preventing subnet deletion?](https://docs.byteplus.com/en/docs/47/4635#.5a2Q572R5Lit5bey5Yib5bu66LWE5rqQ77yM5a-86Ie05peg5rOV5Yig6Zmk5a2Q572R5pe277yM5aaC5L2V5o6S5p-l55u45YWz6LWE5rqQ77yf)<br><br>* [Do ECSs support switching from their current subnet to another subnet?](https://docs.byteplus.com/en/docs/47/4635#.5piv5ZCm5pSv5oyB5LqR5pyN5Yqh5Zmo5LuO5b2T5YmN5a2Q572R5YiH5o2i6Iez5YW25LuW5a2Q572R77yf) |


<span id=".6ZmQ5Yi2"></span>
## Limit

<span id=".5LiA5Liq6LSm5Y-35pSv5oyB5Yib5bu65aSa5bCR5Liq5a2Q572R77yf"></span>
### How many subnets can be created per account?

No quota restrictions.

<span id=".5a2Q572R5YWB6K645L2_55So55qE572R5q615piv5LuA5LmI77yf"></span>
### What CIDR blocks can subnets use?

Subnet CIDR blocks must fall within the VPC CIDR block range. For the VPC CIDR block, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

<span id=".5Yqf6IO9"></span>
## Feature

<span id=".5a2Q572R6Ze05piv5ZCm5Y-v5Lul5LqS55u46YCa5L-h77yf"></span>
### Can subnets communicate with each other?

Subnets within the same VPC have default private connectivity. Subnets across different VPCs are isolated by default.

<span id=".5a2Q572R55qE572R5q615piv5ZCm5Y-v5Lul5L-u5pS577yf"></span>
### Can subnet CIDR blocks be modified?

Subnet CIDRs cannot be modified after creation.

<span id=".5a2Q572R5Lit5bey5Yib5bu66LWE5rqQ77yM5a-86Ie05peg5rOV5Yig6Zmk5a2Q572R5pe277yM5aaC5L2V5o6S5p-l55u45YWz6LWE5rqQ77yf"></span>
### How to identify resources preventing subnet deletion?

You can log in to the [Subnet console](https://console.byteplus.com/vpc/subnet). In the subnet list: Check the IP Utilization column for occupied IPs. If IPs are in use, inspect resources in the VPC via [Viewing VPC Details](https://docs.byteplus.com/en/docs/vpc/Viewing-details-of-a-VPC).

For details on deleting subnets, see [Deleting a subnet](https://docs.byteplus.com/en/docs/vpc/Deleting-a-subnet).

<span id=".5piv5ZCm5pSv5oyB5LqR5pyN5Yqh5Zmo5LuO5b2T5YmN5a2Q572R5YiH5o2i6Iez5YW25LuW5a2Q572R77yf"></span>
### Do ECSs support switching from their current subnet to another subnet?

Yes, supported. For actions, see [Changing Virtual Private Cloud or subnet](https://docs.byteplus.com/en/docs/ecs/Changing-the-VPC-or-subnet-of-an-ECS-instance).

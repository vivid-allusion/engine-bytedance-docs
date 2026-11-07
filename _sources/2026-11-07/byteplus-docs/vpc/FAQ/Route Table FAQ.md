---
title: "Route Table FAQ"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Route-table-FAQ"
---

|Issue category |Classification |
|---|---|
|Billing |[Are route tables billed?](https://docs.byteplus.com/en/docs/47/4633#.6Lev55Sx6KGo5piv5ZCm6K6h6LS577yf) |
|Limits |[How many routes can a single route table hold?](https://docs.byteplus.com/en/docs/47/4633#.5Y2V5Liq6Lev55Sx6KGo5YaF5Y-v5Lul5re75Yqg5aSa5bCR6Lev55Sx5p2h55uu77yf) |
|Feature |* [Can route tables span multiple VPCs?](https://docs.byteplus.com/en/docs/47/4633#.5ZCM5LiA5Liq56eB5pyJ572R57uc5LiL77yM5LiT57q_6L-e5o6l5LiO6Lev55Sx5p2h55uu55qE55uu5qCH572R5q615Yay56qB5pe25piv5ZCm5pyJ5LyY5YWI57qn5YWz57O777yf)<br><br>* [In the same VPC: If ESC Instance A has a bound EIP and configured custom route to access the internet via Instance B. How does Instance A reach the internet?](https://docs.byteplus.com/en/docs/47/4633#.5ZCM5LiA56eB5pyJ572R57uc5LiL77yM5LqR5pyN5Yqh5Zmo5a6e5L6LQee7keWumuS6huWFrOe9kUlQ77yM5ZCM5pe25Lmf6YWN572u5LqG6Lev55Sx5p2h55uu6YCa6L-H5a6e5L6LQuiuv-mXruWFrOe9ke-8jOWunuS-i0HlpoLkvZXorr_pl67lhaznvZHvvJ8=)<br><br>* [Within the same VPC, do Direct Connect connections and custom route entries have priority when their destination CIDRs conflict?](https://docs.byteplus.com/en/docs/47/4633#.5ZCM5LiA5Liq56eB5pyJ572R57uc5LiL77yM5LiT57q_6L-e5o6l5LiO6Lev55Sx5p2h55uu55qE55uu5qCH572R5q615Yay56qB5pe25piv5ZCm5pyJ5LyY5YWI57qn5YWz57O777yf)<br><br>* [How is traffic forwarded when destination CIDR blocks overlap?](https://docs.byteplus.com/en/docs/47/4633#.55uu5qCH572R5q616YeN5Y-g5pe277yM5rWB6YeP5aaC5L2V6L2s5Y-R77yf) |

## Are route tables billed?

No, route tables are free.

## How many routes can a single route table hold?

The default maximum is 200 custom route entries per route table. If the default quota does not meet your needs, please go to the [Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=VPC) to apply for a quota increase.

## Can route tables span multiple VPCs?

No.

Route tables are integral components of a VPC, comprised of a series of routing rules that govern the traffic flow (both ingress and egress) for resources within its subnets. When a VPC is created, a system route table is automatically generated. All subnets are associated with this table by default. You can also create custom route tables and associate target subnets with these custom tables.

A subnet can only be associated with one route table, while a single route table can be associated with multiple subnets.

## In the same VPC, ESC Instance A has an EIP bound and a custom route configured to access the Internet via Instance B. How does Instance A reach the Internet?

The EIP takes precedence over custom routes. Thus, Instance A accesses the internet directly through its EIP.

## Within the same VPC, do Direct Connect connections and custom route entries have priority when their destination CIDRs conflict?

No priority relationship exists. Direct connect enables cloud\-to\-on\-premises IDC connectivity, while custom routes govern intra\-cloud traffic flow. These operate in distinct domains without routing precedence conflicts.

## How is traffic forwarded when destination CIDRs overlap?

Traffic follows the Longest Prefix Match (LPM) principle: The route with the longest subnet mask (most specific match) always takes priority.

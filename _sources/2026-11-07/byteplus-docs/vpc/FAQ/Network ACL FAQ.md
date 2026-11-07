---
title: "Network ACL FAQ"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Network-ACL-FAQ"
---

<span id="AZKc0JRl"></span>
## How many network ACLs can an account own? How many network ACL rules are allowed? How many network ACLs can a subnet be associated with?


* There is no limit on the total number of network ACLs an account can own. Within a single VPC, you can create up to 200 network ACLs.

* Default rule capacity per Network ACL:

   * Inbound: 20 IPv4 rules, 20 IPv6 rules;

   * Outbound: 20 IPv4 rules, 20 IPv6 rules;

   * The default rule with priority \* does not count against your rule quota.

   * If the default quota does not meet your needs, pleasego to [go to the Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=VPC) to apply for a quota increase.

* Each subnet can be associated with exactly one network ACL. However, a single network ACL can be associated with multiple subnets.


<span id=".572R57ucQUNM5pyN5Yqh5aaC5L2V5pS26LS577yf"></span>
## Is there a charge for the Network ACL service?

Currently, no charges apply for using Network ACLs.

<span id=".572R57ucQUNM5ZKM5a6J5YWo57uE55qE5Yy65Yir77yf"></span>
## What is the difference between a Network ACL and a Security Group?

Both Network ACLs and Security Groups are security access control policies. Security Groups provide instance\-level protection, while ACLs offer an additional subnet\-level security layer. For full comparison, see [Network ACL and Security Group differences](https://docs.byteplus.com/en/docs/vpc/Network-ACL-overview#.572R57ucQUNM5LiO5a6J5YWo57uE5beu5byC).

<span id=".5Li65LuA5LmI572R57ucQUNM5re75Yqg5LqG5ouS57ud54m55a6aSVDlnLDlnYDorr_pl67nmoTop4TliJnvvIzkvYbku43lj6_ku6Xorr_pl67vvJ8="></span>
## Why can a specific IP still access after adding a deny rule?

Your deny rule for specific IP addresses isn't working because its priority is lower than your allow rule. Rules execute in priority order (lower numerical value = higher priority). The default rule (\*) has the lowest priority. When rules conflict, higher\-priority rules override lower\-priority ones. To make your deny rule effective: [Modifying ACL Entry priority](https://docs.byteplus.com/en/docs/vpc/Managing-network-ACL-rules#.5YW25LuW5pON5L2c) to be higher than the conflicting allow rule.

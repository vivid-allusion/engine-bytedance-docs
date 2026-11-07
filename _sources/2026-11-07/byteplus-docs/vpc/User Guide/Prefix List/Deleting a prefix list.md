---
title: "Deleting a prefix list"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Deleting-the-prefix-list"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Prerequisites


* The prefix list is not referenced by VPC security group rules. If referenced, first [delete the security group rule](https://docs.byteplus.com/en/docs/vpc/Managing_a_security_group_rule).

* The prefix list is not referenced by VPC route entries. If referenced, first [delete the route entry](https://docs.byteplus.com/en/docs/vpc/Managing-a-route-entry).

* The prefix list is not referenced by TR static routing. If referenced, first [delete static routing](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-05).

* The prefix list is not referenced by TR route policy. If already referenced, first [delete the route policy entry](https://docs.byteplus.com/en/docs/transitrouter/Managing-the-routing-policy-entries).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures


1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Prefix List**.

3. In the top menu bar, select the target project and Region.

4. Click **Delete** to the right of the target prefix list.

5. Click **Delete** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[DeletePrefixList](https://docs.byteplus.com/en/docs/vpc/DeletePrefixList)

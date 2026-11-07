---
title: "Modifying max entries"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Modifying-the-prefix-list"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Limits


* The max entries of the prefix list will occupy the quota of the resources referencing this list. Please evaluate the business impact carefully before proceeding.

* If the prefix list is not referenced, the max entries must not exceed 200.

* If the prefix list is referenced, the maximum number of entries is limited to 200 and is also subject to the quota of the resources referencing this list.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures


1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Prefix List**.

3. In the top menu bar, select the target project and region.

4. Click **Modify max entries** on the right side of the target prefix list.

5. Modify the maximum number of entries as needed, and click **Save** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[ModifyPrefixList](https://docs.byteplus.com/en/docs/vpc/ModifyPrefixList)

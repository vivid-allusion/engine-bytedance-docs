---
title: "Managing a security group rule"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Managing_a_security_group_rule"
---

Changes to security group rules (including adding, modifying, copying, or deleting rules) take effect immediately. These rules control both existing connections and any new connections established by the associated network interfaces. Please thoroughly evaluate the potential impact on live services and proceed with extreme caution.

<span id="1nbUU3hj"></span>
## Modify security group rule

You can modify security group rules as needed based on your business requirements. Supported modifications include the rule's policy, priority, port, protocol, source address, and other fields.


1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Security Group**.

3. In the top menu bar, select the target project and region.

4. Click **Configure** on the right side of the target security group.

5. On the **Inbound rule** or **Outbound rule** tab, find the target security group rule, then click **Modify** on the right side to modify the rule.

6. Click **Confirm** to complete the action.


<span id="Zu8NO4gd"></span>
## Copy security group rule

Duplicate security group rules cannot be added to the same security group. Therefore, if you copy a rule without making any modifications, the operation will be skipped (or: the duplicate rule will be discarded).


1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Security Group**.

3. In the top menu bar, select the target project and region.

4. Click **Configure** on the right side of the target security group.

5. On the **Inbound rule** or **Outbound rule** tab, find the target security group rule, then click **Copy** on the right side to copy the rule.

6. Click **Confirm** to complete the action.


<span id="uCo83cXG"></span>
## Delete security group rule


1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Security Group**.

3. In the top menu bar, select the target project and region.

4. Click **Configure** on the right side of the target security group.

5. In the **Inbound rule** tab or **Outbound rule** tab, click **Delete** on the right of the target security group rule.

6. Check **I confirm the rule deletion will have no service impact.** , then click **Delete** to complete the actions.


<span id="uDRUG4EA"></span>
## Related documents


* [ModifySecurityGroupRuleDescriptionsEgress](https://docs.byteplus.com/en/docs/vpc/ModifySecurityGroupRuleDescriptionsEgress)

* [ModifySecurityGroupRuleDescriptionsIngress](https://docs.byteplus.com/en/docs/vpc/ModifySecurityGroupRuleDescriptionsIngress)

* [RevokeSecurityGroupIngress](https://docs.byteplus.com/en/docs/vpc/RevokeSecurityGroupIngress)

* [RevokeSecurityGroupEgress](https://docs.byteplus.com/en/docs/vpc/RevokeSecurityGroupEgress)

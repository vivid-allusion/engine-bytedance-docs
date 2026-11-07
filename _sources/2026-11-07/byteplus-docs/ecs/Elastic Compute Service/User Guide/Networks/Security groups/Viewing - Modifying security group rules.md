---
title: "Viewing/Modifying security group rules"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Modifying-security-group-rules"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Applicable scenarios

As your business grows or you adjust or migrate services, you may need to tighten or loosen access permissions to your ECS instances. To achieve this, you can modify security group rules. For example, you can tighten remote access permissions by changing the policy from allowing any terminal remote login to allowing only specified terminals.

For use cases of security groups, refer to [Security group use cases](https://docs.byteplus.com/en/docs/vpc/Security-group-use-cases).

<span id=".5pON5L2c6K-05piO"></span>
## Usage note

Changes to security group rules take effect immediately.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".6YCa6L-H5LqR5pyN5Yqh5Zmo5o6n5Yi25Y-w5p-l55yLL-S_ruaUueiuv-mXruinhOWImQ=="></span>
### View/Modify access rules in the ECS console


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the top menu bar, select the target region.

3. In the left\-side navigation pane, click "Instances".

4. Click the name of the target instance.

5. On the "Security Group" tab, view the rule status of network interfaces associated with the instance.

6. Click "Edit rule" on the right side of the target security group to modify or add rules.

   * **Add rules**: After selecting the tab of outbound or inbound rules, you can click "Add rule" to add outbound or inbound rules.

      You can click "Add rule" to add multiple rules in sequence and add up to 10 rules each time.

   * **Modify rules**: After selecting the tabs of outbound/inbound rules, you can click the "Modify" button next to the target security group rule to edit it.

7. Click "Add". The action is complete.


<span id=".6YCa6L-H5a6J5YWo57uE5o6n5Yi25Y-w5p-l55yLL-S_ruaUueiuv-mXruinhOWImQ=="></span>
### View/modify access rules in the Security Group console


1. Log in to [the Security Group console](https://console.byteplus.com/vpc/securityGroup). 

2. In the top menu bar, select a region.

3. Click "Edit rule" in the "Actions" column on the right side of the target security group to view current rules.

4. Then, select to modify or add rules.

   * **Add rules**: After selecting the tab of outbound or inbound rules, you can click "Add rule" to add outbound or inbound rules.

      You can click "Add rule" to add multiple rules in sequence.

   * **Modify rules**: After selecting the tabs of outbound/inbound rules, you can click the "Modify" button next to the target security group rule to edit it.

5. Click "Save". The action is complete.


<span id=".55u45YWz5paH5qGj"></span>
## FAQs


* [Why can't I access services deployed on an ECS instance after I configure the security group for the instance?](https://docs.byteplus.com/en/docs/ecs/Network-FAQs#.5Li65LuA5LmI5LqR5pyN5Yqh5Zmo6YWN572u5LqG5a6J5YWo57uE77yM5YW26YOo572y55qE5pyN5Yqh6L-Y5piv5peg5rOV6KKr6K6_6Zeu77yf)

* [How can I see whether ports enabled in a security group take effect?](https://docs.byteplus.com/en/docs/ecs/Network-FAQs#.5aaC5L2V5Yik5pat5a6J5YWo57uE5byA5pS-55qE56uv5Y-j5piv5ZCm55Sf5pWI77yf)


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [AuthorizeSecurityGroupIngress](https://docs.byteplus.com/en/docs/vpc/AuthorizeSecurityGroupIngress): Add an inbound rule to security groups.

* [AuthorizeSecurityGroupEgress](https://docs.byteplus.com/en/docs/vpc/AuthorizeSecurityGroupEgress): Add an outbound rule to security groups.

* [ModifySecurityGroupRuleDescriptionsIngress](https://docs.byteplus.com/en/docs/vpc/ModifySecurityGroupRuleDescriptionsIngress): Modify the description of inbound rules for the security group.

* [ModifySecurityGroupRuleDescriptionsEgress](https://docs.byteplus.com/en/docs/vpc/ModifySecurityGroupRuleDescriptionsEgress): Modify the description of outbound rules for the security group.

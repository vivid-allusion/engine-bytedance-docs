---
title: "Set Automatic Approval Rules"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/Set_Automatic_Approval_Rules"
---

This feature allows you to set automatic approval rules for different confidentiality levels of access types to global resources. This guide explains how to configure the settings accordingly.

<span id="e878643d"></span>
## Constraints

Currently, automatic approval rules can only be set for the authority owner node of global resources. If you only need to set automatic approval for certain resources or other node types, go to the **Permission Settings** page for configuration. See related instructions in [Set Auto Approval Rule](https://docs.byteplus.com/docs/dataleap/Set_Auto_Approval_Rule).

<span id="_1-设置自动审批"></span>
## Operation Steps


1. Log in to the DataLeap console.

2. Select **Overview \> Security \> Approval Hub \> Approval Settings \> Auto Approval** to enter the **Auto Approval** page.

3. Set automatic approval separately for L2 and L3 confidentiality levels.

   1. Click the **L2 automatic approval** or **L3 automatic approval** settings section's **Automatic Approval Rule** button to open the corresponding automatic approval settings window.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f23c5693838241a2b9be452e2201fb99~tplv-goo7wpa0wc-image.image) </span>

   2. After choosing the permission type, click the **Confirm** button to add the rule.

      Permission type options include all permission types, package, DB read only, DB read\-write, DB create table, table read only, table read\-write, ordinary column read only, and row\-level\-access read only; these options appear in a dropdown and support multiple selection.

   3. The following actions can be performed on the added automatic approval rules:

      * Click the **Edit** button in the **Action** column of the L2 or L3 automatic approval rule to change the permission type for that rule, then click the **Save** button to complete the modification.

      * Click the **Delete** button in the **Action** column of the L2 or L3 automatic approval rule, which opens a confirm deletion dialog; click the **Delete** button to remove the rule.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">L1 applications auto\-approve without configuration; L4, due to the highest confidentiality level and for security reasons, does not support automatic approval yet.</div>


<span id="0b1d446b"></span>
## Subsequent Operations

After setting the automatic approval rule, it applies to the approval flow for permission applications; the authority owner node you belong to will auto\-approve permission applications of that type.

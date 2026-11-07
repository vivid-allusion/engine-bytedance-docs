---
title: "Set Assignee"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/Set_Assignee"
---

If you plan to travel, take leave, or temporarily cannot handle application work orders for other reasons, you can set an assignee with authority owner permissions to approve on your behalf. This article introduces how to set an assignee.

<span id="e878643d"></span>
## Operation Steps


1. Log in to the DataLeap console.

2. Select **Overview \> Security \> Approval Hub \> Approval Settings \> Assignee Settings** to enter the **Assignee Settings** page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/92acd92f1aaa4bdaa605672a5be11db8~tplv-goo7wpa0wc-image.image) </span>

3. Click the **Add Assignee** button to open the create assignee window.

4. After setting the assignee information, click the **OK** button to complete the setting and display the operation result.

   The parameters related to setting the assignee information are shown in the following table. Parameters marked with \* before the name are required, while those without \* are optional.

   
   |parameters |description |
   |---|---|
   |\*Approval Role |Create an assignee’s approval role, offering options such as System Roles, Custom Approvers, Custom Approval Roles, Invited Approvers, Reassigned Approvers, etc. Selectable from the dropdown, multiple selections supported. |
   |\*Assignee |Personnel authorized to approve work orders on behalf of the Authority Owner. Supports selecting individuals or Custom Approval Roles.<br><br><br>* Individual: enter tenant account keywords for dropdown selection.<br><br>* Custom Approval Role: select from the dropdown the preconfigured approval roles. For details, refer to [Set Custom Role](https://docs.byteplus.com/docs/dataleap/Set_Custom_Role). |
   |Involve me |Choose whether you want to participate in approval. Default is **No**.<br><br><br>* If you choose **Yes**, you will receive approval notifications and can approve work orders as you wish.<br><br>* If you choose **No**, you will not receive approval notifications, and all approvals will be handled by the assignee. |
   

5. Also supports the following actions:

   * Click the **Edit** button in the **Action** column of a role's information to open the assignee editing page, where you can change or add assignees.

   * Click the **Delete** button in the **Action** column of a role's information to cancel the assignee settings.

   * Check one or more role information entries to batch modify or delete the corresponding assignee information.


<span id="b4f82c9d"></span>
## Operation Result

After setting assignees, it takes effect immediately for in\-progress work orders and subsequently generated work orders.

<span id="_3-设置自定义角色"></span>
## Subsequent Actions

After setting assignees, any in\-progress and new work orders requiring your approval can be approved by your assignees.

---
title: "Set Custom Role"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/Set_Custom_Role"
---

With this function, you can customize an approval role and add members as approvers to assign this role for approval during the resource approval process. This article introduces how to set up a custom role.

<span id="e878643d"></span>
## Constraints

You can modify role information as needed. Note that the effective time for role information changes varies by application scenario:


* If the role is used in the **Assignee** scenario, the assignee node updates in real time.

* If the role is used in other scenarios (such as authority owner), changes only apply to new submitted requests; already submitted requests cannot be updated.


<span id="_1-设置自动审批"></span>
## Operation Steps


1. Log in to the DataLeap console.

2. Select **Overview \> Security \> Approval Hub \> Approval Settings \> Role Settings** to enter the **Role Settings** page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9fc321e5f4a45698aa7c4f86285da77~tplv-goo7wpa0wc-image.image) </span>

3. You can perform the following operations:

   * Create custom roles

      Click the **New custom role** button, set the role information in the pop\-up window, then click **OK** to complete creation.

      
      |Parameters |Description |
      |---|---|
      |\*Custom role name |Name the approval role as desired. |
      |\*Admin |The person managing the approval role can modify the name, add or remove members, and delete the approval role.<br><br>Default is the current account; after inputting tenant account keywords, a dropdown will appear for selection. Multiple can be set. |
      |\*Role member |Actual members involved in approval during application use; multiple can be set.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When multiple role members are configured, approval of the corresponding work order node can be completed once any one of them executes the operation.</div><br> |
      

   * Search roles

      Set search criteria to view the list of roles that match the conditions.

   * Edit roles

      Click the **Edit** button in the **Action** column for a role to modify its information.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The effective time of role information changes varies across different application scenarios.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If this role is applied in the <strong>Assignee</strong> scenario, the assignee node will update in real time.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If this role is applied in other scenarios (such as authority owner), it only takes effect for new work order applications; submitted ongoing work orders cannot be updated temporarily.      </div>
      

   * Delete roles

      Click the **Delete** button in the **Action** column of a role entry, and confirm to delete the information. After deletion, the **approval flow nodes** using this custom approval role will also be removed.


<span id="0b1d446b"></span>
## Follow\-up Actions

After setting up the role, you can apply it to the resource's custom approval flows, approval assignees, or permission owner settings. See the related instructions in [Set Approval Flow](https://docs.byteplus.com/docs/dataleap/Set_Approval_Flow), [Set Assignee](https://docs.byteplus.com/docs/dataleap/Set_Assignee), and [Set Application Permissions](https://docs.byteplus.com/docs/dataleap/Set_Application_Permissions).

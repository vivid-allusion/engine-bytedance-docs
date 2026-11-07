---
title: "Approve Applications"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/Approval_Applications"
---

Depending on the resource approval flow settings, as the authority owner, related roles (such as warehouse manager, table owner), or custom approver, you may receive permission approval notifications and need to approve the applications. This article introduces how to manually approve applications.

<span id="_1-约束限制"></span>
## Constraints

Only approvers assigned to approval nodes in the data resource approval flow can approve applications. For instructions on setting up resource approval flows, see [Set Approval Flow](https://docs.byteplus.com/docs/dataleap/Set_Approval_Flow).

<span id="60a69647"></span>
## Approval Reminders

After the applicant submits a permission application ticket, as the approver, if you have configured your email, you will receive an email notification when it's your turn to approve, allowing you to quickly access the relevant approval page via a jump link for efficient approval.

<span id="_2-审批工单"></span>
## View Work Order


1. Log in to the DataLeap console.

2. Select **Overview \> Security \> Approval Hub \> Applications \> Awaiting My Approval** to enter the **Awaiting My Approval** page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7644e221af80423c93af321087d9ef23~tplv-goo7wpa0wc-image.image) </span>

3. Set search criteria such as application ID, applicant, requested resource information, parameter filtering, and sorting order to query the list of tickets awaiting approval that meet the conditions.

   When multiple search criteria are set, the query will use the intersection of all conditions.

4. Click the **Application ID** of a ticket to enter its application details page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/36673adb859041dd8b06829025752e71~tplv-goo7wpa0wc-image.image) </span>

5. You can view the application details and approval status of this ticket and perform the following actions:

   * Under the **Awaiting My Approval** tab

      * Click the resource name of a resource to view detailed information about the requested resource, including table owner, description, and field info.

      * Click the **View** button in the **Approval Flow** column of an item to see the resource permission approval flow.

      * Click **Access Type** or **Validity Period** to modify the corresponding permission application information. Example: the ticket’s validity period changes from **365 days** to **180 days**.

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">The validity period can only be adjusted to less than or equal to the currently applied duration.         </div>
         

      * Approve the requested resources in this ticket. Related operations refer to the **Approve Applications** section.

   * Under the **Other Requested Resources** tab, you can view detailed info and approval status of resources that include you in the approval nodes and have entered your approval stage, including resources with completed approvals and those not yet completed but where one or more nodes have been approved by you or others.


<span id="1"></span>
## Approve Applications


1. Log in to the DataLeap console.

2. Choose **Overview \> Security \> Approval Hub \> Awaiting My Approval** to enter the **Awaiting My Approval** page.

3. You can perform the following approval actions:

   * Approve application

      * Click the **Approve** button in the **Action** column of a ticket in the list or the **Approve** button on the ticket details page. In the pop\-up window, click **Confirm** to approve the application.

      * After selecting one or more options, click the **Approve** button below the list. In the pop\-up window, click **Confirm** to approve applications in bulk.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/915459f5f0e7488aad8c16a906c172ad~tplv-goo7wpa0wc-image.image) </span>

   * Deny application

      * Click the **Reject** button in the **Action** column of a ticket in the list or the **Reject** button on the ticket details page. In the pop\-up window, enter the reason for rejection and click **Confirm** to deny the application.

      * After selecting one or more options, click the **Reject** button below the list. In the pop\-up window, click **Confirm** to deny applications in bulk.

   * Add approver approval

      This means that after the current approver approves, the add approver still needs to participate in the approval.

      * Click the **Add Approver** button in the **Action** column of a ticket in the ticket list, or the **Add Approver** button on the ticket application details page. In the popped\-up **Add Approver** window, set the add approver information, then click the **Confirm** button to complete the add approver approval for the application.

      * After selecting one or more options, click the **Add Approver** button below the list. In the popped\-up window, set the add approver information, then click the **Confirm** button to complete batch add approver.

   * Reassign

      If you are unsure or unable to approve a ticket, you can choose to reassign it to other relevant personnel.

      * Click the **Transfer** button in the **Action** column of a ticket in the ticket list, or the **Transfer** button on the ticket application details page. In the popped\-up **Transfer** window, set the reassign information, then click the **OK** button to complete the reassignment of the application approval.

      * After selecting one or more options, click the **Transfer** button below the list. In the popped\-up window, set the reassign information, then click the **OK** button to complete batch reassignment.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When the applicant and approver are the same person, the application ticket will auto\-approve and be directly displayed on the <strong>Approval History</strong> page.</div>


<span id="ba92fbd4"></span>
## Operation Result

After the ticket approval is complete, it will be displayed on the **Approval History** page for your review.

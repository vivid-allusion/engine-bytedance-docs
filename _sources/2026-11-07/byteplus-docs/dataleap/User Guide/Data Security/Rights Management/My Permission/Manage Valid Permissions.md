---
title: "Manage Valid Permissions"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/Manage_Current_Permissions"
---

This feature allows you to view all approved application tickets, including owned permissions, permission expiration times, and more. You can also return or renew permissions here.

<span id="67a3f6f5"></span>
## Constraints


* If the resource has a no\-renewal policy, renewal is not allowed. If continued use is needed, you must reapply.

* Renewal requests can only be made when the resource permission expires in less than 14 days.


<span id="3d4b6bb0"></span>
## Prerequisites

You must have applied for resource access permission, and the application ticket must be approved. For related operation instructions, refer to [Apply Permission](https://docs.byteplus.com/docs/dataleap/Apply_Permission) and [Approve Applications](https://docs.byteplus.com/docs/dataleap/Approval_Applications).

<span id="be3ce5fe"></span>
## Expiration Reminders

When resource permission expiration is less than 14 days, the platform will send you a renewal reminder.


* Email reminders: when the expiration time is less than 14, 7, 2, and 1 days, the platform will send you email reminders to renew. The email subject is “【Data Security】Permission Expiration Notice.”

* SMS reminders: when the expiration time is less than 1 day, the platform will send you an SMS renewal reminder.


<span id="1bf8d9d4"></span>
## Operation Steps


1. Log in to the DataLeap console.

2. Select **Overview \> Security \> Authorization Management \> My Authorizations** to enter the **Valid Permissions** page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a254fa3bf77749ae8b89440bdb5899aa~tplv-goo7wpa0wc-image.image) </span>

3. You can perform the following actions:

   * Search resource

      Set resource type, resource name, parameter filters, and other search criteria to view matching resource information. When multiple search criteria are set, the query will use the intersection of all conditions.

   * View resource details

      Click a resource name in the list to open a side panel displaying the resource’s basic information along with its included table or field info.

   * Renew a single resource or renew in batch

      Click the **Renew** button in the **Action** column of a resource in the list, or select one or more options and click the **Batch Renew** button. In the popup window, set the renewal info and click **OK**.

      The table below explains the parameters related to resource renewal.

      
      |Parameters |Description |
      |---|---|
      |* Validity period |Renewal duration can be selected from the dropdown or entered manually.<br><br>The maximum validity period must not exceed the duration approved last time; to extend the validity, reapply. |
      |\*Request type |Reason classification for resource permission renewal, selectable from the dropdown.<br><br>The request type must match the one used when applying for permission and cannot be changed. If the permission is needed for a different reason, a new application is required. |
      |\*Description |Detailed explanation of the reason for resource permission renewal.<br><br>The detailed reason must match the one used when applying for permission and cannot be changed. If the permission is needed for a different reason, a new application is required. |
      

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If a resource shows as <strong>prohibited from renewal</strong>, hover over the button and click <strong>reapply</strong> in the popup to submit a new permission request for that resource.      </div>
      

   * Return permissions individually or in batch

      If a resource permission is no longer needed for work, you can return it proactively.

      1. Click the **Return** button in the **Action** column of a resource in the list, or select one or more options and click the **Batch Return** button to open the permission return window.

      2. After setting the returned information, click the **OK** button to display the return confirmation dialog.

      3. Click the **OK** button to complete the permission return.

   * Apply on behalf of others

      1. After selecting one or more options, click the **Batch Apply** button to quickly fill the application page with the corresponding resource permissions you own.

      2. After setting other information, click the **Submit** button to quickly submit permission applications for others.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When returning permissions, the system checks for any related data development tasks. When unrelated tasks appear, it does not necessarily mean there are no dependencies; tasks submitted from other entry points may temporarily be unavailable for display.   </div>

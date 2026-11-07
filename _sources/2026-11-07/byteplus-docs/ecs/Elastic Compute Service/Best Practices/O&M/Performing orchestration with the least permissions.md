---
title: "Performing orchestration with the least permissions"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Executing_workflow_orchestration_with_minimum_authorization"
---

To access resources specified by an orchestration task, the orchestration feature first needs to assume a role in your account that is granted with read and write permissions on ECS resources. This topic mainly describes how to restrict role permissions through the custom policies of the [policy management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-policies) feature to ensure the security of cloud resources.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure 


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the top menu bar, select the region where your business is located.

3. In the left\-side navigation pane, select "Maintenance & Monitoring \> Orchestration" to go to the orchestration list page.

4. Click the "Orchestrate tasks" tab.

5. Click the "Create orchestration task" button.

6. Enter task information except for the "Role" field, based on the [guide for creating an O&M orchestration task](https://docs.byteplus.com/en/docs/ecs/Manage_orchestration_tasks#.5Yib5bu65rWB56iL57yW5o6S5Lu75Yqh).

7. Click the "View permissions required for the task" button, and then, on the permissions page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_341f2540a8a5d302f45f4a49e9ff0ec0.png) </span> button. Copy the permission policy required to execute the configuration in "Step 5".

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Proceed to this step only after the above steps are completed. If subsequent task steps are adjusted, recopy the permissions required for the task and update the policy permissions by following the guide for <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-editing-a-user-custom-policy">editing custom policies</a>.   </div>
   

8. Click the "Navigate to role management" button to enter the Role Management page.

9. In the left\-side navigation pane, select "Policy Management" to enter the policy list page.

10. Click the "Create custom policy" button, enter the following content on the new policy page, and then click the "Create Policy" button to complete the creation.

   
   |Parameter |Description |Example value |
   |---|---|---|
   |Strategy name |Enter the policy name. |VOS_1_Access |
   |Edit policy content |Replace the policy with the content copied in "Step 6". |\- |
   

11. In the directory tree on the left, select "Identity Management \> Role" to open the role list page. Create a role based on the guide for [permission management](https://docs.byteplus.com/en/docs/ecs/Preparation).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When you grant permissions, search for and add the custom policy created in "Step 9".   </div>
   

12. Return to the Create orchestration task page, and then choose the role created in "Step 10" in "Role".

13. Click the "Confirm" button to complete the operation. The system then executes the O&M orchestration task based on the principle of least permissions.

14. You can view the execution details of the O&M orchestration task afterward, based on the guide for [viewing task details](https://docs.byteplus.com/en/docs/ecs/Manage_orchestration_tasks#.5p-l55yL5Lu75Yqh6K-m5oOF).

---
title: "Updating agent visibility scope"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Updating_agent_visibility_scope"
---

This topic describes how ** administrators** of a shared Claw grant agent usage permission to relevant personnel. After authorization, enterprise employees who are not shared Claw administrators can also use this agent to initiate tasks.

<span id="uW0j5fcL"></span>
## Procedure


1. Log in to the ArkClaw console as the shared Claw administrator and switch to the target shared Claw instance page in the left pane.

2. In the left navigation pane, select "Agent center".

3. Click the "View details" button on the target card.

4. In the upper\-right corner of the page, click the<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0fda1aac111c099ce94607c6b04f616d.png) </span>.

5. In the pop\-up window, select a permission mode as needed:

   * **Not open yet**: Only administrators can view and use this Claw. Suitable for scenarios where the Claw is not yet ready to be shared.

   * **Partially visible**: Only specified departments, user groups, or users can view and use this Claw. Suitable for scenarios where access needs to be controlled by team, role, or individual.

      > To create departments, user groups, or users, contact your enterprise administrator.      
      

      When "Partially visible" is selected, you can specify who can access the Claw by using the following methods:

      * Department: Enter the full department name to search, and then select the target department from the result.

      * User group: Enter the full user group name to search, and then select the target user group from the result.

      * User: Enter the user name to search, and then select the target user from the results.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If a department or user group is selected as the grantee, users subsequently added to this scope automatically inherit the corresponding permissions. When users are removed from the department or user group, the permissions will be automatically revoked. This can effectively reduce the permission maintenance workload caused by personnel changes.      </div>
      

   * **Visible to all**: All members in the current space can view and use this Claw. Suitable for general\-purpose capability, common workflow, or team\-sharing scenarios.

      6. After configuration, click "Confirm" to complete the permission configuration.

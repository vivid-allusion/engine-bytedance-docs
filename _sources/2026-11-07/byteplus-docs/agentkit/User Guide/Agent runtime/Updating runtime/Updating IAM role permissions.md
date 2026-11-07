---
title: "Updating IAM role permissions"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Updating_IAM_role_permissions"
---

This topic describes the procedure for adding or removing permissions for an IAM role. Changing IAM roles is not supported.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After you update the permissions of an IAM role, you need to click Release in the upper right corner of the page. The new configuration will take effect only after republishing, and a new version will be generated simultaneously. Once published, the latest version will be automatically used for subsequent agent runtime calls.</div>


<span id="9tbYVQQc"></span>
## Procedure


1. Log in to [the AgentKit console](https://console.byteplus.com/agentkit). 

2. In the left\-side navigation pane, select "Agent Runtime".

3. In the agent runtime list, click the name of the target agent runtime.

4. Click the "Configuration information" tab.

5. In the "Permission and access control" section, click "Edit role permission" next to the IAM role.

6. On the role details page, remove or add permissions.

7. Click "Confirm" to complete the operation.

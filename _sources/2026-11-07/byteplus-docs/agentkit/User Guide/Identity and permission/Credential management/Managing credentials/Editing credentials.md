---
title: "Editing credentials"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/editing-credentials"
---

When a credential's basic information, parameters, or usage notes change, you can update the target credential by editing it.

## Instructions

After a credential is updated, the new configuration applies to subsequent credential retrieval, OAuth authorization, and STS temporary credential requests. If the credential is in use by a running agent, parameter changes may cause authentication failures, authorization errors, or insufficient permissions in subsequent requests. We recommend that you review the credential's references and the affected workflows before making changes.

## Procedure

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Identity and Permission  **\>**  Credential management".

3. In the "Actions" column of the target credential, click the "Edit" button.

4. On the "Edit" page, update the editable parameters for the credential type. For field definitions and requirements, see:

   * [Creating third-party API Key credentials](https://docs.byteplus.com/en/docs/agentkit/creating-third-party-api-key-credentials?lang=en)

   * [Creating OAuth connection credentials](https://docs.byteplus.com/en/docs/agentkit/creating-oauth-connection-credentials?lang=en)

   > **warning**

   > The editable fields vary by credential type, creation method, and authorization mode. **Fields that cannot be modified are displayed as read\-only**. Refer to the console page for the exact editable scope.

5. Review the changes and confirm that the affected services are correct. Click "Confirm" to save the changes.

   > After you update a credential's configuration, all services that reference this credential are affected. You can verify the affected agents and workflows by credential type.

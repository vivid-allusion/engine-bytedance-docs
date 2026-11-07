---
title: "Updating inbound identity authentication information"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Updating_inbound_identity_authentication"
---

Inbound identity authentication serves as the first security barrier for service access. It ensures that only authorized entities can call MCP toolsets and prevents unauthorized access, data leakage, and malicious attacks. After an MCP toolset is created, you can update its inbound identity authentication configuration if the caller or authentication policy changes or its credentials need to be rotated. This topic describes how to update the inbound identity authentication information of an MCP toolset.

## Scenarios

* You need to add, rotate, or delete an API key.

* You need to associate an OAuth JWT with a new user pool or client.

* You need to adjust the caller authorization scope of the MCP service.

> **warning**

* > **Switching** the inbound identity authentication type is not supported. You can only modify the authentication information based on the originally configured authentication type.

* > The authentication methods API Key and OAuth JWT are mutually exclusive. You can enable only one for the same MCP toolset. In API key mode, you can configure up to 5 API keys. **After authentication information is modified or deleted, callers who have not updated their credentials may be unable to call the MCP tool**.

## Prerequisites

* You have created an MCP toolset. For details, see [Creating MCP toolsets](https://docs.byteplus.com/en/docs/agentkit/MCP_toolset).

* (Optional) Before updating identity authentication of the OAuth JWT type, create a user pool and a client. For more information, see [Creating a user pool](https://docs.byteplus.com/en/docs/agentkit/create-user-pool?lang=en) and [Creating a client](https://docs.byteplus.com/en/docs/agentkit/create-client-side?lang=en).

## Procedure

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Gateway \> MCP integration", and click the "MCP Toolset" tab.

3. In the MCP toolset list, click the target toolset name. On the "Basic information" tab, click "Edit" next to "Inbound identity authentication".

4. On the "Edit identity authentication" page, update the inbound identity authentication information.

   * **API Key**

      * **Add a key**: Enter an API key name and the system will generate new authentication credentials. Adding a key does not affect existing keys.

      * **Delete a key**: Delete an existing API key name to revoke its authentication credentials. After a key is deleted, callers using that key will fail to authenticate.

   * **OAuth JWT**

      * Select the user pool and client to update. Callers must use the new authentication configuration to generate or pass an access token.

5. After the update is complete, go to the MCP toolset details page to view the inbound identity authentication information. The new configuration is displayed.

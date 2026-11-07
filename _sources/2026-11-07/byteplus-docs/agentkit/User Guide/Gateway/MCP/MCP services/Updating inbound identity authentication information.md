---
title: "Updating inbound identity authentication information"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Updating_inbound_identity_authentication_svc"
---

Inbound identity authentication serves as the first security barrier for service access. It verifies whether a caller is authorized to access an MCP service, ensuring that only authorized principals can invoke it and preventing unauthorized access, data leakage, and malicious attacks. After an MCP service is created, you can update its inbound identity authentication information if the service caller, authentication policy, or security requirements change. This topic describes how to update the inbound identity authentication information of an MCP service.

## Scenarios

* You need to add, rotate, or delete an API key.

* You need to associate an OAuth JWT with a new user pool or client.

* You need to adjust the caller authorization scope of the MCP service.

> **warning**

* > **Switching** the inbound identity authentication type is not supported. You can only modify the authentication information based on the originally configured authentication type.

* > API Key and OAuth JWT are mutually exclusive authentication methods. Only one of them can be enabled for the same MCP service. In API key mode, you can configure up to 5 API keys. **After authentication information is modified or deleted, callers that have not updated their credentials may be unable to access the MCP service**.

## Prerequisites

* An MCP service has been created. For more information, see [Creating MCP services](https://docs.byteplus.com/en/docs/agentkit/MCP_services).

* (Optional) Before updating identity authentication of the OAuth JWT type, ensure that you have created a user pool and a client. For more information, see [Creating a user pool](https://docs.byteplus.com/en/docs/agentkit/Identity_and_permission_01?lang=en#Gzz7rgDs) and [Creating a client](https://docs.byteplus.com/en/docs/agentkit/Identity_and_permission_01?lang=en#Gzz7rgDs).

## Procedure

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Gateway \> MCP integration", and click the "MCP Service" tab.

3. In the MCP service list, click the name of the target service. On the "Basic information" tab, click "Edit" next to "Inbound identity authentication".

4. On the "Edit identity authentication" page, update the inbound identity authentication information.

   * **API Key**

      * **Add a key**: Enter an API key name and the system will generate new authentication credentials. Adding a key does not affect existing keys.

      * **Delete a key**: Delete an existing API key name to revoke its authentication credentials. After a key is deleted, callers using that key will fail to authenticate.

   * **OAuth JWT**

      * Select the user pool and client to update. Callers must use the new authentication configuration to generate or pass an access token.

5. After the update is complete, go to the MCP service details page to view the inbound identity authentication information. The new configuration is displayed.

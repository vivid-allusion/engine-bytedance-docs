---
title: "Deleting access rules"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/deleting-access-rules"
---

When an access rule no longer meets business requirements, has an incorrectly configured authorization scope, or a temporary authorization has expired, you can delete the rule.

Once deleted, the rule immediately stops participating in permission evaluation. Related requests are evaluated by other active rules. If no allow rule is matched, the system applies a **default deny**. If both an allow rule and a deny rule are matched, the deny rule takes precedence.

> **warning**

> Deletion cannot be undone. After an active allow rule is deleted, users who previously had access may immediately lose access to the corresponding agent or tool. Before you delete a rule, we recommend that you review the rule's effect, principals, target resources, and scope of impact. You can also export all policy statements to retain the configuration. For more information, see [Exporting all statements](https://docs.byteplus.com/en/docs/agentkit/exporting-all-statements?lang=en).

## Impact of deletion

* **Delete an allow rule**: Affected users may lose access.

* **Delete a deny rule**: Users previously blocked may gain access. Evaluate the security impact carefully.

* **Other rules of the same type exist**: Deleting one rule does not necessarily change permissions. Other allow or deny rules may still match.

* **Accidental deletion**: Deleted rules cannot be directly restored. Recreate and publish the access rule using the original configuration.

## Procedure

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left navigation pane, select "Identity & Permission  **\>**  Policy management".

3. Click the name of the target permission policy space.

4. In the "Actions" column of the target access rule, click "Delete".

5. Confirm that the rule to be deleted is correct and click "Confirm" to complete the operation.

## Result verification

1. After deleting an access rule, return to the access rule list and **confirm that the target rule has been removed**.

2. To prevent unexpected allow or deny outcomes after deletion, we recommend that you use the affected user's credentials to send controlled requests. Test both scenarios: **requests that should be allowed** and **requests that should be denied**.

   > **tip**

   * > Should\-allow scenario: After this rule is deleted, the user can still access the target resource through other active rules in the system.

   * > Should\-deny scenario: After this rule is deleted, no other active rule grants the user access. The user no longer has permission to access the target resource.

   1. **Prepare a test user**

      The test user must belong to the user pool associated with the access rule. Confirm that the user's status is normal. Obtain the user's access token through the OAuth/OIDC login flow of the corresponding user pool client. For details, see:

      * [Creating users](https://docs.byteplus.com/en/docs/agentkit/create-user?lang=en)

      * [Creating user pools](https://docs.byteplus.com/en/docs/agentkit/create-user-pool?lang=en)

      * [Configuring user pool clients](https://docs.byteplus.com/en/docs/86848/2598357?lang=en)

      > Do not use admin credentials, runtime API Keys, or M2M client credentials in place of the affected user's credentials. These credential types do not represent a specific user. They cannot accurately verify access rules configured based on users, departments, or user groups.

         2. **Confirm that requests go through policy authorization**

      Before sending verification requests, confirm the following:

      * The request carries a valid identity token for the affected test user.

      * The target agent runtime or MCP service has inbound identity authentication configured.

      * The user pool and client used for inbound authentication match the identity source in the access rule.

      * The request passes through the AgentKit gateway and policy authorization point instead of directly calling the agent or MCP tool's backend API.

      > If the test request lacks the affected user's identity or bypasses policy authorization, the result only confirms that the resource is available. It does not verify the post\-deletion permissions.

         3. **Verify access permissions**

      **Verify agent access permissions**

Use the test user's access token to call the target agent runtime. Ensure the request follows the authorization flow configured with the access rule. For more information about agent runtime creation, invocation addresses, and inbound authentication configuration, see [Creating runtimes](https://docs.byteplus.com/en/docs/agentkit/Creating_agent_runtimes_in_console?lang=en).

      * Send a request using a **should\-allow user**. The request is expected to pass permission validation and reach the target agent.

      * Send the same request as a **should\-deny user**. The request is expected to be denied during policy authorization.

      > **tip**

      > If both users can access the agent, check whether other allow rules exist or whether the request bypassed policy authorization.

      > If both users are denied access, check the remaining allow rules, identity information, and whether the resource and operation types match.

      **Verify MCP tool access permissions**

Send a `tools/call` request using a test agent or a controlled MCP client connected to the target MCP tool. Include the test user's identity token to ensure that the request goes through policy\-based authentication by the AgentKit gateway.

      For more information about MCP service creation, inbound authentication, and tool call methods, see [Integrating existing REST APIs/OpenAPIs as MCP tools](https://docs.byteplus.com/en/docs/agentkit/Integrating_existing_REST_API_OpenAPI_as_MCP_tools?lang=en). For more information about gateway authentication and tool call chains, see [Gateway overview](https://docs.byteplus.com/en/docs/agentkit/MCP_Overview?lang=en).

      > Do not call the MCP backend REST API directly. Direct calls bypass the AgentKit gateway and cannot verify whether the MCP tool access rule takes effect.

      * Use a **should\-allow user** to call the target tool. The request is expected to pass permission validation, and the tool is expected to execute normally.

      * Use a **should\-deny user** to call the same tool. Policy authorization is expected to deny the request before the tool executes.

   4. **Check the verification result**

      |**Verification item** |**Check method and expected result** |
      |---|---|
      |Should\-allow request |Send a request using a user who still matches other allow rules after the deletion. The request is expected to pass permission validation and access the target agent or call the target MCP tool. |
      |Should\-deny request |Send a request using a user who no longer matches any allow rule, or who still matches a deny rule, after the deletion. The request is expected to be denied before reaching the target resource or executing the tool. |
      |Deleting an allow rule |Check whether users previously covered by the deleted rule still match other allow rules. If no other allow rule exists, requests should be denied by default. |
      |Deleting a deny rule |Check whether users who were previously blocked regain access through other allow rules. Confirm whether other deny rules or restrictions are still in effect. |
      |Multiple associated rules exist |Based on the final evaluation result, check whether other allow rules, deny rules, and condition expressions continue to participate in evaluation. When a deny rule and an allow rule are both matched, the deny rule should take precedence. |

      > **tip**

      > Both the should\-allow and should\-deny requests must be verified. A single successful call is not sufficient to confirm that permissions are correct. If results differ from expectations, review runtime logs by test time, user ID, operation type, target resource, and error message. For details, see [Viewing runtime instance logs](https://docs.byteplus.com/en/docs/agentkit/Viewing_runtime_instance_logs).

 **      **

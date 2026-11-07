---
title: "Simulating evaluation"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/simulating-evaluation"
---

Simulated evaluation allows you to pre\-verify the permission result for a specified user accessing target resources, without issuing a real agent request or actually calling any MCP tool. The system runs a permission computation based on the currently effective access rules and returns the access result.

Simulated evaluation allows you to quickly verify whether the permission boundary matches expectations. This feature also helps locate the root cause when an agent is unreachable or MCP tools cannot be called.

> **tip**

> Simulated evaluation only computes the permission result. It does not actually run the agent or call any MCP tool. Even when the simulated evaluation result is "Permission verified", it only indicates that permission verification has passed. This does not guarantee that the target agent or tool will execute successfully. The actual call may still fail due to invalid request parameters, service exceptions, unavailable tools, or expired downstream credentials.

## Recommended scenarios

* **Verify access rule change results**

   After creating, modifying, or deleting an access rule, you can initiate a simulated evaluation to verify whether the permission changes match expectations. For example, confirm whether a newly added rule has allowed the target user to access the specified agent or MCP tool, or whether deleting a rule has revoked the corresponding access for the relevant users.

* **Check the final result when multiple rules are matched simultaneously**

   When the same user, resource, and operation may match multiple allow or deny rules at the same time, use simulated evaluation to view the final decision. This helps you confirm whether the permission result that actually takes effect matches expectations and prevents accidental authorization or denial caused by overlapping rules.

* **Verify agent call chain permissions**

   When an agent accesses downstream agents or MCP tools through a call chain, you can include the call chain condition (the context of multi\-level cascaded agent calls) in the simulated evaluation to verify whether the access permission on the target resource matches expectations.

* **Validate permissions before launching production resources**

   Before an agent, an MCP tool, or a related capability is launched, we recommend using simulated evaluation to validate permissions for typical users, departments, user groups, and edge\-case users. This confirms that authorized users can access the resource and unauthorized users cannot, reducing the risk of unauthorized access or false denial after launch.

## Prerequisites

[An access rule ](https://docs.byteplus.com/en/docs/agentkit/Createaccessrules?lang=en)has been created.

## Procedure

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left navigation pane, select "Identity & Permission  **\>**  Policy management".

3. Click the name of the target permission policy space.

4. Click "Simulate evaluation" and configure the evaluation simulation parameters by referring to the following table.

   |Parameter​ |Description |
   |---|---|
   |Who |Select the user pool and the specific user for this simulated evaluation. This user serves as the access principal for this permission computation. Specific steps are as follows:<br><br><br>1. In the ** user pool** drop\-down list, select the user pool to which the user to be verified belongs.<br><br>2. In the **user** drop\-down list, select the user for this simulated access.<br><br>   > **tip**<br>   <br><br>   > The user list only displays users in the selected user pool.<br>    |
   |What to do |In the **What to do** drop\-down list, select the operation type to validate in this simulation. The selected operation must be consistent with the operation configured on the target resource and in the access rule. Supported:<br><br><br>* **Call**: Verify whether the selected user can access a specified agent or call a specified MCP tool.<br><br>* **Create internal service ticket**: Verify whether the selected user has permission to create an internal ticket. |
   |To what |Based on the operation type selected in the ** What to do ** parameter, select the target resource type and specific resource for this access simulation. The currently supported target resource types include agent and MCP service.<br><br>> Ensure that the selected resource matches the access target in the real request so that the simulation result accurately reflects the actual permission status.<br><br><br><br>* **Agent:**  If you select "Agent" as the target resource, the system simulates the inbound evaluation when the request enters the agent runtime. The request can enter the agent for execution only after the evaluation passes. Specific steps are as follows:<br><br>   1. In the resource type drop\-down list, select "Agent".<br><br>   2. In the drop\-down list on the right, select the specific agent whose access permission needs to be verified, and confirm that the selected agent matches the actual request target.<br><br>* **MCP service:**  If you select "MCP service" as the target resource, the system simulates the permission evaluation before the tool call is actually initiated. The target tool call can be initiated only after the evaluation passes. Specific steps are as follows:<br><br>   1. In the resource type drop\-down list, select "MCP service".<br><br>   2. In the next\-level drop\-down list, select the target MCP service to be verified.<br><br>   3. In the drop\-down list on the right, select the specific MCP tool under the service. [Learn more](https://docs.byteplus.com/en/docs/agentkit/Adding_MCP_tools?lang=en) |
   |Agents passed through (Optional) |If the request passes through one or more agents before reaching the target resource, click "+ Add agent" and add the agents strictly in the actual calling order. If the actual request involves a call chain, keep the user, operation, target resource, and agent order consistent with the real request during the simulation.<br><br>> **Before the call chain is used in the production environment**, verify the inbound access permissions and MCP tool call permissions of each agent node separately. Then, complete end\-to\-end verification through controlled requests to confirm that identity propagation, request parameters, outbound credentials, and downstream services all function properly.<br><br><br>> **tip**<br><br><br><br>* > You can add up to 5 agents.<br><br><br>* > If the actual request involves a call chain, we recommend keeping the chain configuration consistent during the simulation.<br> |

5. After confirming that the parameters to be evaluated are correct, click the "Start evaluation" button.

6. Review the simulated evaluation result, then determine whether the current permission configuration matches expectations.

   > **Simulated evaluation result: ** The simulated result only represents the permission decision under the currently selected user, operation, target resource, and call chain conditions. Only if the simulation feature explicitly supports per\-hop authorization checks can its result be interpreted as validating permissions across the entire call chain. Otherwise, the result should not be taken to mean that every node in the chain has passed authorization.

   * **Result: Passed**

      If the result is "Permission verified", this indicates that the selected user passes the permission verification when performing the specified operation on the target resource under the currently effective access rules.

      > **tip**

      * > Simulated evaluation only validates permissions and does not guarantee that the target agent or tool can run normally. After the permission check passes, we recommend that you perform an end\-to\-end validation using real business requests or a test environment to confirm that the target agent or tool can run normally.

      * > Actual calls may still fail because of parameter errors, service exceptions, or expired downstream credentials.

   * **Result: Denied**

      If the result is "Permission verification failed", this indicates that the selected user cannot perform the specified operation on the target resource under the currently effective access rules. You can troubleshoot the issue as follows:

      > **tip**

      > If a request does not match any allow rule, the system **denies it by default**. Only requests that explicitly match an allow rule are permitted. Unauthorized requests are blocked by default.

      * Check whether an allow rule that covers the current user and resource exists.

      * Check whether a deny rule is matched.

      * Check whether the user's department, user group, and login source are correct.

      * Check whether the target MCP service, tool, or agent is correctly selected.

      * Check whether the agent call chain in the simulation configuration is consistent with the actual request.

## What to do next

After the simulated evaluation passes and before the call chain is used in production, you still need to send real requests in a test environment or by using a controlled account to validate both the permission configuration and the business execution result. Simulated evaluation only computes the permission result and does not actually run the agent or call the MCP tool. Therefore, you should also complete the following validations:

* **Validate agent inbound access permissions**

   Send a test request to each agent in the call chain and confirm that the target user can pass identity authentication and access rule validation, and then enter the agent runtime normally. For runtime access modes, permission configuration, and validation methods, see [Creating runtimes](https://docs.byteplus.com/en/docs/agentkit/Creating_agent_runtimes_in_console?lang=en).

* **Verify MCP tool call permissions**

   Call the target MCP tool with the agent and user identity that match the actual business, and confirm that inbound identity authentication, tool access rules, and call permissions all function as expected. For MCP tool integration, identity authentication, and call validation methods, see [Integrating existing REST APIs/OpenAPIs as MCP tools](https://docs.byteplus.com/en/docs/agentkit/Integrating_existing_REST_API_OpenAPI_as_MCP_tools?lang=en).

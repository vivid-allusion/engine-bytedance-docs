---
title: "Creating access rules"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/creating-access-rules"
---

Access rules define the permissions users have on resources—that is, which users can perform which actions on which resources. This allows you to control the scope of access that users, departments, and user groups have to agents and MCP tools.

You do not need to write Cedar policy statements manually. On the relevant feature page, a four\-step visual wizard guides you through selecting a rule template, configuring target resources, specifying the user scope, and confirming the rule effect. Based on your configuration, the system automatically generates the corresponding policy statements, lowering the barrier to permission setup and reducing the risk of syntax errors.

## Why configure access rules

Configuring access rules translates business\-level permission boundaries into authorization policies that the system can enforce. When a user accesses an agent or an agent calls an MCP tool, the system evaluates the request against the rules currently in effect. The system then decides whether to allow or deny the request.

* **Control the scope of resource access**

   Specify which users, departments, user groups, or login sources can access a given agent or MCP tool, preventing resources from being exposed to unrelated personnel.

* **Implement the principle of least privilege**

   Grant users only the agent or tool permissions required for work, reducing unnecessary permission exposure and over\-authorization.

* **Protect sensitive resources**

   For resources that involve sensitive data, high\-risk operations, write operations, or production environments, you can configure a stricter personnel scope or use deny rules to restrict access by specified users.

* **Constrain the call chain**

   In multi\-agent chaining scenarios, you can require users to pass through a specified middle\-tier agent to call the target tool or agent. This approach prevents users from bypassing the controlled business agent and directly calling sensitive underlying tools.

* **Support dynamic management of organizational permissions**

   After permissions are configured through organizational relationships such as departments and user groups, permissions follow organizational changes as members join or leave the corresponding scope. This reduces the cost of maintaining rules user by user.

## Recommended scenarios

* **Authorize specified principals to access tools or agents**

   When a department or a specified user needs to call one or more tools or agents, you can create an access rule to grant the corresponding permissions. For example, you can grant a business team permission to call specified tools or allow a specific user to access a particular agent.

* **Restrict certain users from accessing specified resources**

   Certain tools or agents may involve sensitive data or high\-risk operations, or may be available only to a specific audience. In these cases, use access rules to restrict the scope of access and prevent unrelated users from calling those resources.

* **Verify permission boundaries before resources are launched**

   Before a tool, agent, or related capability goes live, configure access rules in advance and use simulated evaluation to verify the access results for different users, departments, or user groups. This ensures that the permission boundaries after launch match your expectations.

* **Adjust permissions after personnel or organizational changes**

   When users join or leave departments, user group membership changes, or business team responsibilities change, review and update access rules accordingly. This ensures that new members receive the necessary permissions and departing members no longer have access.

## Considerations

* **Denied by default**: Any request that does not match an allow rule is denied. Deny rules take precedence over allow rules.

* **Middle\-tier agent as an "AND" condition**: Once a middle\-tier agent is configured, a request must pass through every level of the configured chain in the exact order. A request does not match if it skips a level, passes through an extra level, or follows the levels out of order.

* **Not visible across projects**: The middle\-tier agent must be in the same project as the target tool. If the agent is migrated to another project later, the rule becomes invalid and must be updated promptly.

* **Rule review required after agent deletion**: If a middle\-tier agent is deleted, the system prompts you that the level no longer exists when you save the rule or run a simulated evaluation. Clean up or replace the affected rules promptly.

* **Do not use the middle\-tier agent as a substitute for least privilege**: The middle\-tier agent addresses the issue of "call chain convergence", but does not replace user\-level least\-privilege authorization. Both should be used together.

## Prerequisites

* **Create a user pool**

   Access rules rely on the user pool to identify the caller and other information, such as the departments and user groups to which the caller belongs. Create the user pool first, and make sure the target users have been added to the user pool. For more information, see [Creating user pools](https://docs.byteplus.com/en/docs/agentkit/create-user-pool?lang=en).

* **Register or create the target resource**

   Based on the type of object controlled by the access rule, prepare one of the following resources:

   > **tip**

   > You can select tool or agent resources as needed. To control both agent entry and MCP tool calling, create the corresponding access rules separately.

   * **Object type: Tool**. To select "Tool" as the object type, first[ create an MCP service](https://docs.byteplus.com/en/docs/agentkit/MCP_services?lang=en) and [configure the tools that need to be managed under that service](https://docs.byteplus.com/en/docs/agentkit/Adding_MCP_tools?lang=en). The rule performs permission evaluation before a tool call is actually initiated.

   * **Agent as the object type**: First[, create an agent runtime](https://docs.byteplus.com/en/docs/agentkit/Creating_agent_runtimes_in_console?lang=en), and ensure that the target agent [has been deployed to the agent runtime](https://docs.byteplus.com/en/docs/agentkit/Quick_start_with_AgentKit?lang=en). When a request enters the agent runtime, the rule performs permission evaluation.

* **Prepare the access principal**

   Based on the personnel scope required by the rule, complete the corresponding configuration:

   * **Authorize by department**: First, create a department in the user pool and add the target users to the corresponding department. For details, see [Managing users by department](https://docs.byteplus.com/en/docs/agentkit/create-user?TagIDs=2,484,400&lang=en#tRj3EL2e).

   * **Authorize by specific user**: Confirm that the target user already exists in the selected user pool and login source. For details, see[ Creating users](https://docs.byteplus.com/en/docs/agentkit/create-user?lang=en).

* **Prepare a middle\-tier agent (optional)**

   If a rule requires access to a resource through specified middle\-tier agents, first create and deploy those agents within the same project.

   > **warning**

   > The middle\-tier agent and the target resource must be in the same project. Otherwise, the agent cannot be found in the drop\-down list for selecting an agent.

* **Create a permission policy space (optional)**

   By default, the system maintains a default permission policy space for each project. When creating access rules, you can directly use the default space. To isolate access rules by business line, environment (production/test), or gateway instance when creating access rules, manually create a permission policy space in advance. For more information, see [Creating permission policy spaces](https://docs.byteplus.com/en/docs/agentkit/create-permission-policy-space).

## Procedure

### Step 1: Go to the access rule configuration page

1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left navigation pane, select "Identity & Permission  **\>**  Policy management".

3. Click the name of the target permission policy space.

4. Click the "Create access rule" button to go to the access rule configuration page.

### Step 2: Select a template

You can use templates to quickly choose a baseline access\-permission scheme. After you select a template, the system presets the authorization rules based on the template and automatically displays the corresponding follow\-up configuration items. We recommend that you first choose the template that best matches your business requirements. When a wizard template cannot cover special permission conditions, use custom statements to manually write a Cedar permission policy.

1. Select the target template. See the following table for the scenarios to which each template applies:

   > **tip**

   * > For long\-term permissions, scope the usage by department first; for temporary or exceptional permissions, use specific users. Avoid maintaining a large number of individual authorizations over the long term.

   * > Prioritize department or user group authorization rather than assigning permissions to individuals. This significantly reduces the maintenance cost caused by later personnel changes.

   |**Template** |Rule effect |**Application scenarios** |
   |---|---|---|
   |Available to all |Allows all users under the selected login source to access the target resource and perform the specified actions. |Applicable to resources such as agents and MCP tools that are open to internal company users or specific login sources. Before use, confirm that the resource does not involve sensitive data or high\-risk operations to avoid excessive authorization scope. |
   |Allow a specified department only |Only users in the selected departments can access the target resource. Users outside the selected departments cannot obtain permissions through this rule. |Applicable to resources that are open to specific departments only, such as development tools, departmental knowledge assistants, or internal business agents. When configuring, select the department that actually needs to use the resource. |
   |Allow specified users only |Only the selected users are allowed to access the target resource. Users who are not selected cannot obtain permissions through this rule. |Applicable to small\-scope authorization scenarios, such as core project members, temporary collaborators, test users, or specific owners. |
   |Deny access by specified users |Explicitly prohibits the selected users from accessing the specified resources or performing the corresponding operations. |Applicable to scenarios where, on top of an existing allow rule that already grants resource access, you add a deny rule to block permissions for specific principals. For example, when all team members are permitted to call a specific tool, you can additionally configure this deny rule to prohibit specified users from using that tool.<br><br>System default policy: Access requests that do not match any allow rule are denied by default.<br><br>> **warning**<br><br><br>> **Decision logic:**<br><br><br><br>* > When the same request matches both an allow rule and a deny rule, the deny rule takes precedence.<br><br><br>* > If a request does not match any allow rule, the system denies it by default.<br> |
   |Custom statement |Use Cedar policy statements to customize the access principal, actions, target resources, and effective conditions. This meets complex permission requirements that standard templates cannot cover. |This option applies to fine\-grained authorization scenarios that require combining multiple principals, resources, actions, or condition expressions. We recommend that users familiar with Cedar syntax and the business permission model configure this option and that they check the policy statement and run a simulated evaluation before publishing.<br><br>> **tip**<br><br><br>> We recommend that you configure access rules in the visual mode first. Use custom statements only when the business permission conditions cannot be expressed in the visual list, and the built\-in templates cannot cover your scenario.<br> |

2. In the Rule name field, enter a name for this access rule so that you can quickly identify, search for, and manage it later.

   > This field is optional. If you leave it empty, the system automatically generates a rule name.

3. Click the "Next" button to go to the **Select resource / Write rule** page.

### Step 3: Select resources or write rules

Specify the target resources and authorization conditions of the access rule, that is, identify which agent or tool the rule protects and which access actions are allowed or denied. The displayed configuration options vary depending on the template selected in Step 1:

* When a built\-in template is selected, you can select resources through a visual interface.

* When "Custom statement" is selected, you enter the policy editor to write the complete rule.

   > The current built\-in fixed templates do not support selecting user groups directly. To authorize by user group, select **Custom statement** and enter the unique ID of the target user group in the Cedar policy.

**Select a resource template visually**

1. Select the type of resources to be managed by this access rule. Both ** Tool** and ** Agent** are supported.

   > **tip**

   > Tool and Agent cannot be configured at the same time. After you select one object type, you can only select resources of that type.

   * **Tool**: Used to manage calling permissions for MCP tools.

      * **Call permission**: When the system is about to call a target MCP tool, this access rule is triggered for evaluation. The tool call is allowed only if the evaluation passes. Requests that do not match the rule are blocked.

      * **Applicable scenarios**: Allows specified users or user groups to call sensitive tools, or restricts them from doing so, such as tools that perform high\-risk operations like writing data, modifying code, or deleting files.

   * **Agent**: Used to manage entry calling permissions for agents.

      * **Calling permissions**: When an external request is dispatched to the agent runtime, this access rule is triggered immediately for validation. The agent proceeds with the request only after validation passes. Access requests that do not comply with the rule are blocked.

      * **Applicable scenarios**: Allows specified users or user groups to access a specific agent, or restricts them from doing so. Examples include a production agent, an internal\-only agent, or a canary\-release agent.

2. Based on the selected resource type, select the corresponding resource.

   **MCP tools**

1. Select individual tools that need to be controlled, such as Add, Divide, Multiply, and Subtract.

   2. (Optional) If you cannot find the target tool, click the blue link "Can't find the tool? Enter the tool name by service" and then manually enter the tool name under the corresponding service.

   3. After you select or manually enter the corresponding tool names, the MCP tool resource that needs to be managed is associated with the current access rule.

   **Agents**

1. Select the individual agent runtime instance that needs to be managed.

   2. (Optional) Enter the agent name in the top search box to quickly locate the target agent.

3. (Optional) Configure the middle\-tier agent.

   If the target resource is an MCP tool that is not intended to be called directly by users, click "Add agent" to select the target agent. This adds a middle\-tier agent to the current access rule, ensuring the tool can only be called through a controlled middle\-tier agent.

   * You can configure up to five levels of agents (levels 1 to 5). The level 1 agent is closest to the user.

   * After a middle\-tier agent is configured, the rule evaluates both of the following conditions. Access is allowed only when both conditions are met:

      * Whether the access principal (user/department/user group) is authorized.

      * Whether the request has passed through the entire middle\-tier agent chain specified in the configuration.

4. Click the "Next" button to go to the **Configure access principal** page.

**Custom statement**

When you choose "Custom statement" in [Select a template](https://docs.byteplus.com/en/docs/agentkit/Createaccessrules?lang=en#ynMhhuip), the system cannot automatically populate the authorization scope from a fixed template. In this case, edit the rule directly in this step. With custom statements, you can define the access principal, action type, target resource, and additional conditions at the same time. This lets you express complex permission requirements that the visual page cannot cover.

> **warning**

> Custom statements may expand the authorization scope or cause rule conflicts. Before publishing, check the syntax, target resources, and effects, and complete the [simulated evaluation](https://docs.byteplus.com/en/docs/agentkit/simulating-evaluation?lang=en) with real users and real resources.

1. In the policy editor, enter the Cedar statement and specify the principal, action, and resource.

2. Check the syntax hints and make sure that the page shows no errors or unrecognized fields.

3. Click the "Next" button to go to the **Confirm rule** page.

### Step 4: Configure the access principal

> **tip**

> If "Custom statement" is used, skip this step.

Define ** the user or personnel scope to which the rule applies**. By using login user pools, user groups, and specified users, you can let permissions change along with organization and project membership. When department permissions, project team permissions, external partner permissions, or temporary individual permissions change, adjust the authorized principal here.

1. Click the user pool drop\-down list to select the target user pool.

2. Configure the personnel scope based on the selected access template.

   > The personnel scope determines which principals are granted access and which users are explicitly denied access.

   * When **Allow a specified department only** is specified for the template **:**  Select the target departments to authorize. You can select a first\-level department or a first\-level department together with its sub\-departments. After the rule takes effect, only users within the selected department scope can gain access to the target resources through this rule.

      > **tip**

      * > Whether department authorization includes sub\-departments depends on the department hierarchy and authorization configuration of the current user pool. Selecting a parent department does not necessarily include all sub\-departments automatically. Refer to the actual selection scope shown on the page.

      * > Before configuration, verify the hierarchy, members, and sub\-department coverage of the selected department to avoid missing target users or granting permissions beyond the intended scope. For department details, see [Managing users by department](https://docs.byteplus.com/en/docs/agentkit/create-user?lang=en#tRj3EL2e).

   * When **Allow specified users only** is specified for the template, select the target users to authorize.

   * When **Deny access by specified users** is specified for the template, select the target users to restrict from the drop\-down list.

3. After the configuration is complete, click "Next" to go to the **Confirm rule** page.

### Step 5: Confirm the rule

1. On the Confirm rule page, verify whether the authorization scope and underlying policy statement meet expectations.

2. After you confirm the information, click the "Create rule" button to complete the operation.

## Subsequent steps

After the access rule is created, we recommend using the **Simulate evaluation** feature to verify the rule's effect. By simulating a specified user, accessed resources, and the call path, you can confirm in advance whether a newly created rule takes effect as expected, without affecting real online requests. For details, see [Simulating evaluation](https://docs.byteplus.com/en/docs/agentkit/simulating-evaluation?lang=en).

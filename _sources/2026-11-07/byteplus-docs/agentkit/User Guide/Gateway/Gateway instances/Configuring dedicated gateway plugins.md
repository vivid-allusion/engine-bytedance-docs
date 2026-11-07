---
title: "Configuring dedicated gateway plugins"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Dedicated_gateway_plugin_configuration_description"
---

Gateway plugins are extension capability modules installed on **dedicated gateway** instances. They intervene in data during the request or response processing pipeline. By installing and configuring plugin rules, you can transform credential locations, customize signing and authentication, and implement auditing and risk control. You can also control access based on identity and permission policies without modifying backend services. The gateway currently provides three plugins: **credential transformation**, **custom service extension**, and **Identity authentication**. This topic describes their use cases, installation methods, and rule configurations.

> **warning**

> Plugin capabilities are supported for **MCP\-type** dedicated gateways and **agent runtime\-type** dedicated gateways. Among them, the **Credential transformation** plugin only supports MCP\-type dedicated gateways; the **Custom service extension** plugin and **Identity authentication** plugin support both MCP\-type dedicated gateways and agent runtime\-type dedicated gateways.

## Plugin types

The gateway provides three plugins: **credential transformation**, **custom service extension**, and **Identity authentication**.

|**Plugin name** |**Purpose** |**Application scenarios** |
|---|---|---|
|**Credential transformation** |Transforms authentication credentials in requests according to configured rules before forwarding them to the backend service. If no rule matches or the corresponding credential does not exist in the request, the plugin is automatically skipped without affecting request forwarding. Only **MCP\-type** dedicated gateways are supported. |* Write authentication credentials from a Header or Query to a specified path in the JSON body of a POST request.<br><br>* Write authentication credentials from a Header to a Query parameter of a GET request.<br><br>* Write credentials from the original location to the target location and remove the original Header or Query parameter.<br><br>* Mask internal authentication headers and pass credentials to external services via custom headers to prevent internal authentication header exposure. |
|**Custom service extension** |Integrates your own service into the gateway processing pipeline. When a veFaaS function is selected as the extension service, the gateway calls the function during request or response processing and modifies the request headers, request body, response headers, or response body based on the function's return value. The function can also return a custom response directly. **MCP\-type** and **agent runtime\-type** dedicated gateways are supported. |* Custom signing or authentication: Generate a signature and write it to a Header, Query, or Body.<br><br>* Auditing, risk control, and blocking: Return a response directly when a rule is matched, or continue forwarding when no rule is matched. |
|**Identity authentication** |Controls access to MCP tools and agent runtimes based on verified identity and permission policies. The plugin extracts the token from the request header and authenticates it using the specified Identity permission space. Requests that fail authentication are rejected. **MCP\-type** and **agent runtime\-type** dedicated gateways are supported. |* You need to restrict MCP service access to callers with specified Identity permissions only.<br><br>* If the caller uses a non\-default token header or prefix, configure the gateway to support that token transmission method. |

## Prerequisites

* A dedicated gateway instance is created. For configuration operations, see [Creating dedicated gateways](https://docs.byteplus.com/en/docs/agentkit/Creating_gateway_instances).

* An MCP service or agent runtime in the **Running** state has been created. The "Credential transformation" plugin only requires an MCP service. For the "Custom service extension" and "Identity authentication" plugins, you can select either an MCP service or an agent runtime as the target resource. For configuration operations, see [Creating MCP services](https://docs.byteplus.com/en/docs/agentkit/MCP_services) and [Creating agent runtimes](https://docs.byteplus.com/en/docs/agentkit/Creating_agent_runtimes_in_console?lang=en).

* A veFaaS function is deployed and in a published or invocable state. For configuration operations, see [Deploying veFaaS functions](https://docs.byteplus.com/en/docs/agentkit/Deploying_veFaaS_functions).

* Before using the Identity authentication plugin, ensure a permission policy space is created in Identity and that access rules are configured for the identities that need to access resources. For configuration operations, see [Creating access rules](https://docs.byteplus.com/en/docs/agentkit/Createaccessrules?lang=en).

## Install a plugin

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Gateway \> Gateway overview". On the "Dedicated gateway" tab, click the name of the target MCP\-type or agent runtime\-type dedicated gateway.

3. On the "Plugin" tab, click the "Install" button in the "Actions" column for the target plugin.

   > **tip**

   > **MCP\-type** dedicated gateways support the "Credential transformation", "Custom service extension", and "Identity authentication" plugins. **Agent runtime\-type** dedicated gateways support the "Custom service extension" and "Identity authentication" plugins.

4. In the dialog box that appears, click the "Confirm installation" button to complete the plugin installation.

   > **tip**

   > After a plugin is installed successfully, it is available on the current gateway but does not automatically affect online requests. The plugin takes effect only after you configure rules.

5. (Optional) Uninstall the plugin. If you confirm that the plugin is no longer needed, you can uninstall the plugin.

   1. On the "Plugin" tab, click the "Uninstall" button in the "Actions" column for the target plugin.

      > **warning**

      * > **Uninstalling the plugin may affect online traffic on this gateway. Proceed with caution**.

      * > Plugins with **rules in the Enabled state** cannot be uninstalled. To uninstall a plugin, refer to the "Manage rules" section below to disable or delete all rules first.

   2. In the dialog box that appears, click the "Confirm uninstallation" button to complete the plugin uninstallation.

## Configure plugin rules

### Add a rule

After the plugin is installed, you need to add plugin rules before it can take effect for online requests. The configuration entry is located on the "Plugins" tab of the corresponding dedicated gateway details page. Currently, there is no independent plugin management entry. The "Credential transformation" plugin supports configuring rules at the **MCP service** level only. The "Custom service extension"and "Identity authentication" plugins support configuring rules at the **MCP service** or **agent runtime** level.

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Gateway \> Gateway overview". On the "Dedicated gateway" tab, click the name of the target MCP\-type or agent runtime\-type dedicated gateway.

3. Select the "Plugin" tab. In the plugin list, click the "Rule configuration" button in the "Actions" column for the target plugin.

4. Click the "Add rule" button and configure plugin rules according to the table below.

   **Credential transformation rule parameter configuration**

Configure the credential transformation rule by referring to the following table.

   > **tip**

   * > Each rule can be configured with up to 10 configuration groups.

   * > If a rule contains multiple configuration groups, they are matched in top\-to\-bottom order. You can adjust the order using the "Move up" and "Move down" buttons in the upper\-right corner of each configuration group.

   |Parameters |Description |
   |---|---|
   |**Basic information** ||
   |Effective scope |Select the resource scope where the plugin takes effect. The credential transformation plugin **currently supports "MCP Service" only**. |
   |Effective resource |Select the MCP services to which the plugin rule applies. Only MCP services that are in the **Running** state and have not been configured with this plugin rule can be selected. You can select multiple services.<br><br>> **tip**<br><br><br>> If an MCP service under "Effective resource" in a **credential transformation plugin** rule is deleted, the system automatically removes the service from "Effective resource" in that rule.<br> |
   |**Plugin\-specific configuration** ||
   |Match condition |Match conditions restrict a rule to specific requests only.<br><br><br>* **Configuration instructions**<br><br>   * Match conditions are optional. If no match conditions are configured, the rule takes effect on all requests.<br><br>   * To configure match conditions, click "Add match condition". Each configuration group supports a maximum of **5** match conditions. Multiple match conditions use **AND** logic: the rule takes effect only when all conditions are met.<br><br>* **Parameter description**<br><br>   * **Match target**: Specifies the source to match against. Currently, `Header`, `Query`, and `Method` are supported.<br><br>   * **Field name**: The name of the `Header` or `Query` field to match. `Header` names are case\-insensitive and are normalized to lowercase when loaded by the system. `Query` names are case\-sensitive.<br><br>   * **Match method**: The matching rule for the field value.<br><br>      * **Exact match**: The rule is triggered only when the field value exactly equals the match value.<br><br>      * **Prefix match**: The rule is triggered when the field value starts with the match value.<br><br>   * **Match value**: The expected value for the field. The rule is triggered when the value of this field in the request matches the value configured here. |
   |Transformation configuration |Transformation configuration specifies how credentials are processed. You can write credentials to a target location or remove specific parameters.<br><br><br>* **Transformation action**: Select how the credential is processed.<br><br>   * **Set:**  Reads the original credential and writes it to the target location.<br><br>   * **Remove**: Deletes the specified target parameter. This can be used to remove the original credential after writing it to the target location.<br><br>* **Original credential location**: Required only when the transformation action is "Set". The location of the original credential. `Header` and `Query` are supported.<br><br>* **Original credential field name**: Required only when the transformation action is "Set". The field name corresponding to the original credential, for example, `Authorization`.<br><br>* **Target location**: The location to write the credential to. `Header`, `Query`, and `Body` are supported.<br><br>   * `Header`: Requires a **target field name**. The name of the target `Header` field to write the credential to, for example, `X-API-Key`. Field names are case\-insensitive and will be normalized to lowercase after saving.<br><br>   * `Query`: Requires a **target field name**. The name of the target `Query` parameter to write the credential to, for example, `api_key`. Field names are **case\-sensitive**. Make sure the name is consistent with the parameter name actually received by the backend service.<br><br>   * `Body`: Requires a **Body format**. **JSON body** and **Form body** are supported.<br><br>      * **JSON Body**: Applicable to requests with Content\-Type: `application/json`. Enter the JSON Pointer path in the "JSON body write path" field, for example, `/api_key`.<br><br>      * **Form body**: Applicable to requests with Content\-Type: `application/x-www-form-urlencoded`. Enter the field name in the "Form body field name" field, for example, `api_key`. |

   **Custom service extension rule parameter configuration**

Configure the custom service extension rule by referring to the following table.

   > **tip**

   > Each rule supports a maximum of **1** request\-phase configuration group and **1** response\-phase configuration group.

   |Parameter​ |Description |
   |---|---|
   |**Basic information** ||
   |Effective scope |Select the resource scope where the plugin takes effect. Supported values are **MCP service** and **Agent runtime**. |
   |Effective resource |Select the MCP service or agent runtime where the plugin rule takes effect. Only resources **that are running and have not been configured with this plugin rule** can be selected. |
   |**Plugin\-specific configuration** ||
   |External service type |Select the type of external service. Currently, only **veFaaS function** is supported. |
   |veFaaS function |Select the veFaaS function to use. Only functions in a **published** or **invocable** state can be selected. If no function service is available, create one first. For details, see [Deploying veFaaS functions](https://docs.byteplus.com/en/docs/agentkit/Deploying_veFaaS_functions). |
   |Processing phase |Select the phase at which the plugin intervenes.<br><br><br>* **Request phase**: The function is called before the request is forwarded to the backend service.<br><br>* **Response phase**: The function is called after the backend service returns a response. |
   |Pass body |Whether to enable the "pass body" feature.<br><br><br>* **Enabled**: The external service can read and modify the request or response body.<br><br>* **Disabled**: The body is not passed to the external service. The function cannot read or modify the request or response body. |
   |Timeout |The maximum time that the gateway waits for the external veFaaS function to return a result.<br><br><br>* The default value is 30 **seconds.**  If the function does not return a result within this time, the call is considered timed out.<br><br>* The behavior after a timeout is determined by the **Fail open** setting: If "Fail open" is enabled, the plugin is skipped, and request processing continues. If "Fail open" is disabled, an error is returned. |
   |Fail open |Whether to enable the "Fail open" feature.<br><br><br>* **Enabled**: If the function call fails, the plugin is skipped, and request processing continues.<br><br>* **Disabled**: If the function call fails, an error is returned immediately. |

   **Identity authentication rule parameter configuration**

Configure the Identity authentication rule by referring to the table below.

   > **warning**

   > By default, the `X-Ve-TIP-Token` Token Header is used for identity authentication, and the handling method for authentication failures is set to "Deny request". When authentication fails, the request is rejected and is not forwarded to the backend MCP service.

   |Parameter​ |Description |
   |---|---|
   |**Basic information** ||
   |Effective scope |Select the resource scope where the plugin takes effect. **MCP Service** and **Agent Runtime** are supported. |
   |Effective resource |Select the MCP service or agent runtime where the plugin rule takes effect. Only resources that are in the **Running** state and have not been configured with this plugin rule can be selected. The selected resource must match the object configured in the Identity permission space policy. Otherwise, the corresponding rule does not take effect. |
   |**Plugin\-specific configuration** ||
   |Permission space |Select the Identity permission space to use for authentication. The gateway uses the identity and permission policies in this space to validate access requests. |
   |**Token location** ||
   |Token header name |Required. Enter the request header name used to pass the token.<br><br><br>* The default value is ` X-Ve-TIP-Token`.<br><br>* Header names are case\-insensitive and are converted to lowercase upon saving. If the caller passes the token via a different header, configure the actual header name. |
   |Token prefix |Optional. Enter the prefix of the token value, for example, Bearer.<br><br>Matching is case\-insensitive. After a successful match, the gateway removes this prefix from the Header value and then uses the remaining content for authentication. |

5. A rule is **enabled** immediately after it is added. You can view the rule status in the rule list.

### Manage rules

After plugin rules are added, you can enable, disable, edit, or delete rules to manage how they handle online requests.

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Gateway \> Gateway overview". On the "Dedicated gateway" tab, click the name of the MCP\-type gateway.

3. Select the "Plugin" tab. Click "Rule configuration" in the "Actions" column for the target plugin, and manage the target rule in the rule list.

   * **Disable/Enable a rule**: Click the "Enable" or "Disable" button in the "Actions" column for the target rule.

      > **tip**

      > You can only enable a disabled rule or disable an enabled rule.

   * **Edit a rule**: Click "Edit" in the "Actions" column for the target rule.

      > **tip**

      > Only "Plugin\-specific configuration" of a rule can be edited. The resource to which the rule applies cannot be modified.

   * **Delete a rule**: Click "Delete" in the "Actions" column for the target rule.

      > **warning**

      * > **Deletion cannot be undone. Proceed with caution**.

      * > Only rules that are in the **Disabled** state can be deleted. Rules that are in the **Enabled** state cannot be deleted. Disable a rule before deleting it.

---
title: "Connector MCP Function Configuration"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/connector-mcp-function-configuration"
---

The connector MCP function is used to connect the existing MCP services of the enterprise to the iDA ToB. You can manage the external system capabilities through the **connector**, and call the published MCP connectors in scenarios such as agents, session expansion, and skills.

**This feature is primarily targeted at enterprise administrators.**  This article will introduce in detail how to complete the specific operation steps of creating, managing and using MCP connectors in the management background. After the connector is released, you can select and use the MCP capability in the corresponding business scenario.

# Prerequisites/Precautions

* The current account needs to have connector management permission;

* The accessible MCP Server address is ready. Confirmed transport types supported by MCP Server, currently supported: Streamable HTTP, SSE;

* To upload a custom connector icon, prepare a picture file that meets the requirements. The connector icon supports the following formats: PNG, JPG, SVG, the recommended size is **48 × 48 px** , and the file size does not exceed **2MB;**

* After saving as a draft, the connector will not take effect and you cannot call it in a usage scenario. You need to save and publish or take it online before the connector becomes available.

# Connector function permission description

The functional permissions of the connector are divided into three levels: view, edit, and manage. Permissions are gradually included: having edit permissions means having view permissions at the same time, and having manage permissions means having view and edit permissions at the same time.

|Permission hierarchy |Available features |
|---|---|
|View |Review the list of connectors. |
|View/Edit |Review the list of connectors; create connectors; take connectors on and off; edit the MCP configuration and save it. |
|View/Edit/Manage |In addition to the view and edit permissions, additional support is provided for deleting connectors. |

> **说明**

* > The user cannot view and use the connector in the agent without permission or when the connector is disabled(offline); the skill invocation connector is also not available without permission or disabled.

* > The scope of availability of a connector is set by the creator in the **available roles** (all members, only the creator, or designated members). And above functional permissions jointly impose restrictions on whether the user can manage or use the connector.

# Go to the connector management page

On the iDA home page, hover over the user name in the lower left corner and click Settings in the options that appear. Navigate to the side of the management background and click Connectors to enter the connector management page.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/345da9edb6464929aa65f786e58d3674~tplv-goo7wpa0wc-image.image)

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3dea3c544c80418e8e1e32b039c18510~tplv-goo7wpa0wc-image.image)

# New MCP connector

The connector MCP function allows enterprise administrators to create and configure MCP services in the background, and connect external system capabilities to iDA, which can be used in scenarios such as sessions, agents, and skills after publication. The following are the relevant operation steps and configuration item instructions:

1. In the upper right corner of the connector management page list, click the Create Connector button, and the system redirects to fill in the configuration item page.

2. Please refer to the instructions in the following table to complete the configuration items on the page. After completing the configuration, you can choose according to the actual situation:

   * **Save as draft:**  Save configuration only, not effective immediately.

   * **Save and publish:**  Save the configuration and publish the connector, which can be called in supported use cases after publishing.

   * **Cancel:**  Abandon this creation and return to the previous page.

|**Configuration grouping** |**Configuration item** |**Is it required?**  |**Description** |
|---|---|---|---|
|Basic information |Connector name |Yes |To display and identify connectors, it is recommended to use a name that reflects the connected system or function. |
||Connector icon |Yes |Visual identity for connectors. Supports PNG, JPG, and SVG formats, with a recommended size of 48 x 48 px and no more than 2 MB. |
||Connector introduction |Yes |Describe the purpose, supported capabilities, and application scenarios of the connector to make it easier for users to understand and choose. |
||Available roles |Yes |Sets the available scope of the connector: **all members**, **creator only**, or **specified members**. |
|MCP service configuration |Source of service |Yes |Select the service source:<br><br><br>* **Publish the OpenAPI interface as MCP Server**, which is used to provide the existing API interface in the form of MCP service;<br><br>* **Register an existing MCP Server** to access deployed MCP services. |
||Server name |Yes |Used to identify the configured MCP service, distinguished from the "connector name" displayed to the user. |
||Transport type |Yes |This field is required when selecting the service source as "Register Existing MCP Server".<br><br>Select the communication method of the MCP service, which supports **Streamable HTTP** and **SSE** , and should be consistent with the types supported at the server level. |
||Server URL |Yes |This field is required when selecting the service source as "Register Existing MCP Server".<br><br>Fill in the access endpoint address of the existing MCP service, corresponding to the selected transport type. |
||Custom Header |No |Add request headers as required by the service to pass authentication credentials or other necessary information. Click "Add Header" to add a new configuration.<br><br>Each header contains a name and a value, which must be filled in according to the requirements of the MCP service provider. |

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/61c1e6aa9bac4cd7b368c27ebe012541~tplv-goo7wpa0wc-image.image)

# Connector list and management

Search for connector names at the top of the connector list page, and support filtering the list by status (published, unpublished, or draft). The following is a detailed description of the list operation:

|Operation |Applicable scenario |Operating instructions |
|---|---|---|
|**Go online** |When the connector is in **an unpublished state** and needs to be officially enabled |In the "Operations" column of the destination connector, click **Go online**. After going online, the status changes to **Published.**  |
|**Take offline** |When the connector is in a **published state** and needs to be suspended |In the "Operations" column of the target connector, click **Take offline**. After being taken offline, the user cannot continue to use the connector, but the historical configuration will be retained and can be reconnected later.<br><br>Note: Only connectors that are online support take offline operations. |
|**Tool management** |When you need to view, test, or add a connector tool |In the "Operations" column of the target connector, click **Tool Management** to view the tool name, model call ID, description, and Input Schema.<br><br><br>* When there are no tools, you can click the Add Tools button, fill in the basic information of the tool and add it.<br><br>* Once the addition is complete, click the Test button to verify the tool call. |
|**Edit** |When you need to adjust connector information or MCP service configuration |In the "Operation" column of the target connector, click **Edit** to enter the edit page and modify the configuration of the connector name, introduction, icon, server name, transport type, server URL, custom header, etc. Modifying the service source is not supported.<br><br>Detailed description of configuration items Refer to the previous section to create a connector configuration item description. |
|**Delete** |When confirming that the connector will not be used any more |In the "Operations" column of the target connector, click Delete.<br><br>> **注意**<br><br><br>> After deletion, the connector is no longer displayed and cannot continue to be called; this operation is unrecoverable and is recommended to be performed with caution.<br> |

Add tool configuration item description:

|Configuration item |Is it required? |Description |
|---|---|---|
|Display name |Yes |The name of the tool displayed in the list makes it easy to identify its purpose. |
|Identifier |Yes |The unique identifier used when the model invokes the tool.<br><br>Can only start with a lowercase letter, supports lowercase letters, numbers, `_`, `-`and `/`. |
|Description |Yes |Explain the function and purpose of the tool.<br><br>It is used to help AI agents understand when and how to invoke the tool. |
|Input Schema |Yes |JSON Schema for imported parameters, defining transferable parameters and their types and structures. |
|Request method |Yes |The HTTP method of the calling tool supports GET and POST. |
|Request URL |Yes |The interface address that the tool actually calls. |
|Request header |No |HTTP headers carried when calling an interface, such as authentication information or additional parameters required by the interface, can be added as many groups as needed. |
|Request Scheme (JSONata) |No |A conversion rule for a POST request body is defined in a JSONata expression to map model imported parameters to the request body required by the interface. |

# Usage scenarios of MCP connectors

After the connector is published, it can be used in the following scenarios:

* **New session extensions:**  In the **extension** entry of the iDA new session, you can select the MCP that you have configured and have permission to use. The custom MCP is collapsed and displayed in the MCP options.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/47886427582e4827b857c76ef876aa85~tplv-goo7wpa0wc-image.image)

* **Agent Configuration \- Content Configuration:**  The built\-in MCP connector can be selected as an external capability that the agent can invoke.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6060fd0f26ed4615948c6ce854c69fb0~tplv-goo7wpa0wc-image.image)

# Common problems

|**Common problem** |**Answer** |
|---|---|
|Can users use the MCP after saving it as a draft? |No. Saving as a draft only saves the configuration and will not take effect. It can only be used after "saving and publishing" or going online. |
|Will the configuration be deleted after the published connector goes offline? |No. After going offline, the connector cannot be used, but the historical configuration is still preserved and can go online again later. |
|Can it be restored after deleting the connector? |No. After deletion, the connector is no longer displayed, the history is not preserved, and cannot be restored. Please proceed with caution. |
|Do I have to fill in the custom header? |Not necessarily. If the MCP Server does not require authentication or additional request headers, do not fill in; if the service requires authentication, please add headers as required by the service. |
|Can regular users create MCP connectors? |No. When a normal user does not have administrative permission, it is not supported to create, edit, publish, or delete connectors. |

---
title: "Managing ArkClaw connectors"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Managing_ArkClaw_connectors"
---

Connectors connect ArkClaw to external systems or platforms, enabling agents to call external tools, read external data, or perform operations in external services. By adding different connectors to ArkClaw, you can flexibly expand its capabilities. This allows your ArkClaw to directly operate various external tools, read external data, or call external services.

This topic describes how to view and configure an existing ArkClaw connector, and how to create a custom connector to integrate third\-party or self\-hosted services.

<span id="OQaV1MLF"></span>
## Connector sources


|Plugin types |Description |
|---|---|
|Official preset |Connectors pre\-configured by BytePlus. Only simple authorization or association is required to get started. [Learn more](https://docs.volcengine.com/docs/87732/2596227#aWjFHXr8) |
|Enterprise\-configured |Connectors pre\-configured by your enterprise administrator for use by employees within the enterprise organization. [Learn more](https://docs.volcengine.com/docs/87732/2319793) |
|Custom |Connectors created by you. They can integrate third\-party or private services, and are only available within the current ArkClaw. [Learn more](https://docs.volcengine.com/docs/87732/2597517#UN8hlPwf) |


<span id="Mv8Ya6wW"></span>
## Procedure

<span id="xVIkGPpO"></span>
### View connector details

Before enabling a connector, you can view information about the connector, including its features, scope, and billing and usage methods, to ensure it meets your business requirements.


1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter.

2. Switch to the target ArkClaw and click the details icon at the top.

3. Select the "Plugins \> Connectors" tab.

4. Click the target connector card to view details such as its purpose, billing rules, feature scope, and prompt examples.


<span id="ubEfUOsp"></span>
### Configure an ArkClaw connector


1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter.

2. Switch to the target ArkClaw and click the details icon at the top.

3. Select the "Plugins \> Connectors" tab.

4. On the target connector card, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7361e3491df6d5cbece827580789ab86.png) </span> icon and complete the authorization as prompted. [Learn more](https://docs.volcengine.com/docs/87732/2586821#y2fajIVu)

5. After the configuration, you can enable or disable the connector from the quick access toolbar in the target ArkClaw chat box, and specify it in a conversation to complete tasks. [Learn more](https://docs.volcengine.com/docs/87732/2586821#paak50mj)


<span id="0tDcgDWu"></span>
### Manage a custom connector

<span id="UN8hlPwf"></span>
#### Create a custom connector

If the preset connectors do not meet your requirements, or you want to use a self\-hosted connector, you can create a custom connector.


1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter.

2. Switch to the target ArkClaw and click the details icon at the top.

3. Select the "Plugins \> Connectors" tab and click the "+ Custom" button.

4. Configure the following information, and click the "Confirm" button **.** 

   
   <Tabs>
   <Tab zoneid="oUM9tA8PrF" title="Manual configuration">
   <TabTitle>Manual configuration</TabTitle>
   
   * **Basic information**
   
      
      |Parameter​ |Description |
      |---|---|
      |Connector name |The name of the custom connector. |
      |Service endpoint URL |Specify the remote service address for calling the connector. |
      |Transport protocol |Specify the network transport protocol for accessing the remote service endpoint. Supported:<br><br><br>* **Streamable HTTP**: A streaming transport method based on the HTTP protocol. Supports dynamic data transfer within a single connection, with broad compatibility and simple deployment. Suitable for most remote MCP services. |
      |Connector description |Briefly describe the scenarios, features, and more information of the connector. It can contain up to 50 characters. |
      
   
   * **Authentication method**
   
      
      <Tabs>
      <Tab zoneid="VwxrzQWek2" title="No authentication required">
      <TabTitle>No authentication required</TabTitle>
      
      No authentication is required for this connector. Once added, it can be used immediately. Suitable for connectors that provide public services with no access restrictions.
      
      
      </Tab>
      <Tab zoneid="aBlZR25y2K" title="API Key">
      <TabTitle>API Key</TabTitle>
      
      This connector uses an API Key for authentication. When adding the connector, you need to enter the API Key provided by the service provider. The system will automatically include the key in requests to complete authentication.
      
      
      |Parameter​ |Description |
      |---|---|
      |Transfer location |Specify how the API Key is passed. Supported:<br><br><br>* **Header**: Passes the API Key in the request header. Required configurations:<br><br>   * **Header name**: Specify the field name for the API Key in the request header, for example, `Authorization`.<br><br>   * **Key prefix**: Specify the prefix to be prepended to the API Key value. The final format is `{prefix} {API Key}`, for example, `Bearer tiku8*****`.<br><br>* **Query**: Passes the API Key in the request URL query string. Required configurations:<br><br>   * **Query parameter name**: Specify the parameter name for the API Key in the request URL query string, for example, `api_key`. |
      |API Key |Specify the API Key value used to call the connector. |
      
      
      
      
      
      </Tab>
      </Tabs>
      
   
   
   </Tab>
   <Tab zoneid="adzNoHQ9Xc" title="Import JSON file configuration">
   <TabTitle>Import JSON file configuration</TabTitle>
   
   You can upload the connector configuration as JSON content or as a JSON file to BytePlus to quickly complete the creation.
   
   
   |Parameter​ |Description |
   |---|---|
   |Connector name |The name of the custom connector. |
   |Paste JSON |Enter the JSON configuration for the target connector. For parameter descriptions, see [Connector configuration examples](https://docs.volcengine.com/docs/87732/2596227#y3jG4spt). |
   |Upload JSON file |Upload a JSON file containing the configuration for the target connector. For parameter descriptions, see [Connector configuration examples](https://docs.volcengine.com/docs/87732/2596227#y3jG4spt). |
   |Connector description |Briefly describe the scenarios, features, and more information of the connector. It can contain up to 50 characters. |
   
   
   
   
   
   </Tab>
   </Tabs>
   


<span id="8pkUy6Ju"></span>
#### Modify a custom connector

You can modify the configuration of a connector you have created as needed to ensure it always meets your business requirements.


1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter.

2. Switch to the target ArkClaw and click the details icon at the top.

3. Select the "Plugins \> Connectors" tab.

4. Click the target connector card.

5. Click the "Edit" button and modify the connector configuration information as needed. For parameter details, refer to [Create a custom connector](https://docs.volcengine.com/docs/87732/2596227#UN8hlPwf).

6. Click the "Confirm" button to complete the operation.


<span id="7eiAKEJO"></span>
#### Delete a custom connector

If you no longer use a custom connector, you can delete it.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Deleted custom connectors cannot be recovered. Ensure that no tasks are using a custom connector before deleting it.</div>



1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter.

2. Switch to the target ArkClaw and click the details icon at the top.

3. Select the "Plugins \> Connectors" tab.

4. Click the target connector card.

5. Click the "Delete" button.

6. In the pop\-up window, review the note, and click the "Delete" button to complete the operation.


<span id="0wIkL3NP"></span>
## Appendix

<span id="y3jG4spt"></span>
### Connector configuration examples


* **No** ** authentication required**

   ```JSON
   
   {
     "mcpServers": {
       "my_mcp": {
         "url": "https://example.com/mcp",
         "transport": "streamable-http"
       }
     }
   }
   ```
   

   **Parameter descriptions:** 

   
   |Parameter​ |Description |
   |---|---|
   |my_mcp |Replace it with the name of a custom connector. |
   |url |Specify the remote service address for calling the connector. |
   |transport |Specify the network transport protocol for accessing the remote service endpoint. Supported:<br><br><br>* `streamable-http`: A streaming transport method based on the HTTP protocol. Supports dynamic data transfer within a single connection, with broad compatibility and simple deployment. Suitable for most remote MCP services. |
   

* **API Key**

   ```JSON
   {
     "mcpServers": {
       "my_mcp": {
         "url": "https://example.com/mcp",
         "transport": "streamable-http",
         "auth": {
           "type": "api_key",
           "in": "header",
           "name": "api_key",
           "value": "<API_KEY>"
         }
       }
     }
   }
   ```
   

   **Parameter description**

   
   |Parameter​ |Description |
   |---|---|
   |my_mcp |Replace it with the name of a custom connector. |
   |url |Specify the remote service address for calling the connector. |
   |transport |Specify the network transport protocol for accessing the remote service endpoint. Supported:<br><br><br>* `streamable-http`: A streaming transport method based on the HTTP protocol. Supports dynamic data transfer within a single connection, with broad compatibility and simple deployment. Suitable for most remote MCP services. |
   |auth |Specify the authentication information for the connector.<br><br><br>* `type`: Specify the authentication method. Supported:<br><br>   * `api_key`: Authenticates using an API Key.<br><br>* `in`: Specify how the API Key is passed. Supported:<br><br>   * `header`: Passes the API Key in the request header.<br><br>   * `query`: Passes the API Key in the request URL query string.<br><br>* `name`: Specify the field name for the API Key in the request.<br><br>* `value`: Specify the API Key value used to call the connector. |

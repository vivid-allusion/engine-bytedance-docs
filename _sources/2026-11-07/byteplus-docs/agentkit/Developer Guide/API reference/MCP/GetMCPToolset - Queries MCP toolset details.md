---
title: "GetMCPToolset - Queries MCP toolset details"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/GetMCPToolset_-_Queries_MCP_toolset_details"
---

You can call this operation to query MCP toolset details.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string</span><span data-api-tag="require|5F201K">必选</span>  `Sample value: GetMCPToolset`

The action that you want to perform. Value: GetMCPToolset.



**Version**<span data-label="purple"> string</span><span data-api-tag="require|lgf0A6">必选</span> `Sample value: 2025-10-30`

The API version. Value: 2025\-10\-30.



**MCPToolsetId**<span data-label="purple"> string</span><span data-api-tag="require|OboRJq">必选</span> ` Sample value: mt-ye7kx4****`

MCP toolset ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**MCPToolset ** <span data-label="purple">object </span>`Sample value: --`

MCP toolset information.


**AssociatedRuntimes ** <span data-label="purple">object[] </span>`Sample value: --`

Associated runtime information.


**Id ** <span data-label="purple">string </span>`Sample value: r-ye7f6gd7nktv3gi6c***`

ID of the runtime.



**Name ** <span data-label="purple">string </span>`Sample value: RuntimeName`

Runtime name.




**AuthorizerConfiguration ** <span data-label="purple">object </span>`Sample value: --`

Authentication configuration of the MCP toolset.


**Authorizer ** <span data-label="purple">object </span>`Sample value: --`

Authorizer configuration details.


**CustomJwtAuthorizer ** <span data-label="purple">object </span>`Sample value: --`

The OAuth JWT authentication configuration.


**AllowedClients ** <span data-label="purple">string[] </span>`Sample value: ["client1"]`

List of allowed clients.



**DiscoveryUrl ** <span data-label="purple">string </span>`Sample value: https://example.com/.well-known/openid-configuration`

Authentication service address.




**KeyAuth ** <span data-label="purple">object </span>`Sample value: --`

API Key authentication configuration.


**ApiKeyLocation ** <span data-label="purple">string </span>`Sample value: HEADER`

The location where the API Key is passed.



**ApiKeys ** <span data-label="purple">object[] </span>`Sample value: --`

API Key information.


**Key ** <span data-label="purple">string </span>`Sample value: 65a075a2-aeff-11f0-****-00163e72f914`

The value of the API Key.



**Name ** <span data-label="purple">string </span>`Sample value: k-ye7f6gd7nktv3gi6c***`

API Key name.




**Parameter ** <span data-label="purple">string </span>`Sample value: Authorization`

Name corresponding to the API Key carried in the Header.





**AuthorizerType ** <span data-label="purple">string </span>`Sample value: ApiKey`

The type of identity authentication for the MCP toolset. Valid values:


* ApiKey: API Key\-based authentication.

* CustomJWT: OAuth JWT\-based authentication.




**CreatedAt ** <span data-label="purple">string </span>`Sample value: 2006-01-02T15:04:05Z07:00`

Creation time of the MCP toolset.



**MCPServices ** <span data-label="purple">object[] </span>`Sample value: --`

Details of the MCP service associated with the MCP toolset.


**CreatedAt ** <span data-label="purple">string </span>`Sample value: 2006-01-02T15:04:05Z07:00`

Creation time of the MCP service.



**IsAllTools ** <span data-label="purple">boolean </span>`Sample value: true`

Whether the toolset includes all tools under the MCP services.



**MCPServiceId ** <span data-label="purple">string </span>`Sample value: m-ye7f6gd7nktv3gi6c***`

MCP service ID.



**Name ** <span data-label="purple">string </span>`Sample value: name ye7f6gd7nktv3gi6c***`

The name of the MCP service.



**NetworkConfigurations ** <span data-label="purple">object[] </span>`Sample value: --`

Network configuration details of the MCP service.


**Endpoint ** <span data-label="purple">string </span>`Sample value: ***.apigateway-ap-southeast-1.volceapi.com`

Endpoint for access.



**NetworkType ** <span data-label="purple">string </span>`Sample value: Public`

The access type enabled. Valid values:


* Public: Public network access.

* Private: Access using private network



**VpcConfiguration ** <span data-label="purple">object </span>`Sample value: --`

VPC configuration information.


**SubnetIds ** <span data-label="purple">string[] </span>`Sample value: ["subnet-ye7s6jatq8rxg218****"]`

List of subnet IDs.



**VpcId ** <span data-label="purple">string </span>`Sample value: vpc-ye7s6jatq8rxg218****`

VPC ID.




**EnableSharedInternetAccess ** <span data-label="purple">boolean </span>`Sample value: false`

Specifies whether to enable shared public network access.


* false: Not enabled.

* true: Enabled.




**Path ** <span data-label="purple">string </span>`Sample value: /mcp`

Access path of the MCP service.



**ProjectName ** <span data-label="purple">string </span>`Sample value: default`

Project name of the MCP toolset.



**ProtocolConfiguration ** <span data-label="purple">object </span>`Sample value: --`

Protocol configuration details of the MCP service.


**ProtocolConvertConfiguration ** <span data-label="purple">string </span>`Sample value: --`

When the MCP service backend is of the HTTP type, parse the result based on the API information.




**ProtocolType ** <span data-label="purple">string </span>`Sample value: HTTP`

The access method for the MCP service. Valid values:


* HTTP: HTTP to MCP.

* MCP: Direct access to MCP.



**Status ** <span data-label="purple">string </span>`Sample value: Ready`

MCP service status. Value:


* Ready: Running.

* Creating: Being created.

* Updating: Being updated.

* Deleting: Being deleted.

* Error: Unavailable.



**Tags ** <span data-label="purple">object[] </span>`Sample value: --`

MCP service tags.


**Key ** <span data-label="purple">string </span>`Sample value: k1`

The tag key.



**Type ** <span data-label="purple">string </span>`Sample value: env`

Tag type.



**Value ** <span data-label="purple">string </span>`Sample value: v1`

The tag value.




**UpdatedAt ** <span data-label="purple">string </span>`Sample value: 2006-01-02T15:04:05Z07:00`

Update time of the MCP service.




**MCPToolsetId ** <span data-label="purple">string </span>`Sample value: mt-ye7f6gd7nktv3gi6c***`

MCP toolset ID.



**Mode ** <span data-label="purple">string </span>`Sample value: SemanticSearch`

The calling mode of the MCP toolset.


* SemanticSearch: Semantic retrieval.

* AllTools: Full return.

* TagSearch: Tag retrieval.



**Name ** <span data-label="purple">string </span>`Sample value: name-ye7f6gd7nktv3gi6c***`

MCP toolset name.



**NetworkConfigurations ** <span data-label="purple">object[] </span>`Sample value: --`

Network configuration details of the MCP toolset.


**Endpoint ** <span data-label="purple">string </span>`Sample value: ***.apigateway-ap-southeast-1.volceapi.com`

Endpoint for access.



**NetworkType ** <span data-label="purple">string </span>`Sample value: Public`

The access type enabled. Valid values:


* Public: Public network access.

* Private: Access using private network



**VpcConfiguration ** <span data-label="purple">object </span>`Sample value: --`

VPC configuration information.


**SubnetIds ** <span data-label="purple">string[] </span>`Sample value: ["subnet-ye7s6jatq8rxg218****"]`

List of subnet IDs.



**VpcId ** <span data-label="purple">string </span>`Sample value: vpc-ye7s6jatq8rxg218****`

VPC ID.




**EnableSharedInternetAccess ** <span data-label="purple">boolean </span>`Sample value: false`

Specifies whether to enable shared public network access.


* false: Not enabled.

* true: Enabled.




**Path ** <span data-label="purple">string </span>`Sample value: /toolset`

Access path of the MCP toolset.



**ProjectName ** <span data-label="purple">string </span>`Sample value: default`

Project name of the MCP toolset.



**Status ** <span data-label="purple">string </span>`Sample value: Ready`

MCP toolset status. Value:


* Ready: Running.

* Creating: Being created.

* Updating: Being updated.

* Deleting: Being deleted.



**Tags ** <span data-label="purple">object[] </span>`Sample value: --`

MCP toolset tags.


**Key ** <span data-label="purple">string </span>`Sample value: k1`

The tag key.



**Type ** <span data-label="purple">string </span>`Sample value: env`

Tag type.



**Value ** <span data-label="purple">string </span>`Sample value: v1`

The tag value.




**UpdatedAt ** <span data-label="purple">string </span>`Sample value: 2006-01-02T15:04:05Z07:00`

Update time of the MCP toolset.



**GatewayInstanceName ** <span data-label="purple">string </span>`Sample value: exclusive-gateway`

The name of the dedicated gateway instance associated with the MCP toolset. This parameter is returned only when `GatewayMode `is` Exclusive`.



**GatewayInstanceId ** <span data-label="purple">string </span>`Sample value: gw-********`

The ID of the dedicated gateway instance associated with the MCP toolset. This parameter is returned only when` GatewayMode `is `Exclusive`.



**GatewayMode ** <span data-label="purple">string </span>`Sample value: Shared`

The gateway mode.


* Shared: Shared gateway.

* Exclusive: Dedicated gateway.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=GetMCPToolset&Version=2025-10-30 HTTP/1.1
Content-Type: application/json
{
    "MCPToolsetId": "mt-ye6xr60ikgq7oi5c***"
}

```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202106111445100102252431000052****",
    "Action": "GetMCPToolset",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "MCPToolset": {
      "MCPToolsetId": " mt-xxx",
      "Name": " my_mcp_toolset",
      "Status": " Ready",
      "Path": " /mcp",
      "NetworkConfigurations": [
        {
          "NetworkType": " Public",
          "Endpoint": " "
        }
      ],
      "AuthorizerConfiguration": {
        "AuthorizerType": " ApiKey",
        "Authorizer": {
          "KeyAuth": {
            "ApiKeys": [
              {
                "Key": " ",
                "Name": " "
              }
            ],
            "ApiKeyLocation": " HEADER"
          }
        }
      },
      "CreatedAt": " 2006-01-02T15:04:05Z07:00",
      "UpdatedAt": " 2006-01-02T15:04:05Z07:00",
      "MCPServices": [
        {
          "MCPServiceId": " mcp-xxx",
          "Name": " mcp-service-x",
          "Path": " /mcp",
          "Status": " Ready",
          "NetworkConfigurations": [
            {}
          ],
          "ProtocolType": " HTTP",
          "ProtocolConfiguration": {
            "ProtocolConvertConfiguration": " "
          },
          "CreatedAt": " 2006-01-02T15:04:05Z07:00",
          "UpdatedAt": " 2006-01-02T15:04:05Z07:00"
        }
      ]
    }
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |MissingParameter.MCPToolsetId |The required parameter MCPToolsetId is not supplied. |The parameter MCPToolsetId cannot be empty. |
|404 |InvalidResource.NotFound |The specified resource does not exist. |The specified resource does not exist. |

---
title: "GetMCPService - Queries MCP service details"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/GetMCPService_-_Queries_MCP_service_details"
---

You can call this operation to query MCP service details.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string</span><span data-api-tag="require|SaZ2EY">必选</span>  `Sample value: GetMCPService`

The action that you want to perform. Value: GetMCPService.



**Version**<span data-label="purple"> string </span><span data-api-tag="require|FqawFE">必选</span>`Sample value: 2025-10-30`

The API version. Value: 2025\-10\-30.



**MCPServiceId ** <span data-label="purple">string</span><span data-api-tag="require|FAkS5R">必选</span>  `Sample value: m-ye7f6gd7nktv3gi6c***`

MCP service ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**MCPService ** <span data-label="purple">object </span>`Sample value: --`

MCP service details.


**AssociatedMCPToolsets ** <span data-label="purple">object[] </span>`Sample value: --`

List of MCP toolsets associated with the MCP service.


**MCPToolsetId ** <span data-label="purple">string </span>`Sample value: mt-yefjsz5s0054ppxu****`

MCP toolset ID.



**Name ** <span data-label="purple">string </span>`Sample value: mcp_toolset_****`

MCP toolset name.




**RoleName ** <span data-label="purple">string </span>`Sample value: TestRoleForAgentKit`

Name of the IAM role associated with the MCP service.



**BackendConfiguration ** <span data-label="purple">object </span>`Sample value: --`

Details of backend service for the MCP service.


**CustomConfiguration ** <span data-label="purple">object </span>`Sample value: --`

Fixed domain name details.


**Domain ** <span data-label="purple">string </span>`Sample value: www.***.com`

Domain name.



**Port ** <span data-label="purple">integer </span>`Sample value: 80`

Port.



**ProtocolType ** <span data-label="purple">string </span>`Sample value: HTTP`

Protocol. Value:


* HTTP: Backend HTTP service.

* HTTPS: Backend HTTPS service.




**CustomMcpConfiguration ** <span data-label="purple">object </span>`Sample value: --`

Custom MCP Server configuration.


**EnableApmplus ** <span data-label="purple">boolean </span>`Sample value: true`

Whether to enable TLS. Valid values:


* true: Enabled.

* false: Disabled.



**FunctionId ** <span data-label="purple">string </span>`Sample value: faas-****`

ID of the created veFaaS Function (automatically populated by the system, no user input required).



**FunctionName ** <span data-label="purple">string </span>`Sample value: function-01`

Name of the created veFaaS Function (automatically populated by the system, no user input required).



**PrivatePackage ** <span data-label="purple">object </span>`Sample value: --`

Private package configuration.


**Command ** <span data-label="purple">string </span>`Sample value: ./run.sh`

Startup command. Default: ./run.sh



**Envs ** <span data-label="purple">object[] </span>`Sample value: --`

Environment variables.


**Key ** <span data-label="purple">string </span>`Sample value: k1`

Key.



**Value ** <span data-label="purple">string </span>`Sample value: v1`

Value.




**ImageUrl ** <span data-label="purple">string </span>`Sample value: http://****`

Image URL.




**PublicPackage ** <span data-label="purple">object </span>`Sample value: --`

Public package configuration.


**McpType ** <span data-label="purple">string </span>`Sample value: Stdio`

MCP service type. Value:


* Stdio: Standard input/output.

* Remote: Remote service.



**PackageManagerType ** <span data-label="purple">string </span>`Sample value: NPX`

Package manager type. Value: NPX or UVX.



**RawConfig ** <span data-label="purple">string </span>`Sample value: --`

The complete configuration of the MCP Server (JSON string) is stateless.





**EcsConfiguration ** <span data-label="purple">object </span>`Sample value: --`

The ECS details.


**Instances ** <span data-label="purple">object[] </span>`Sample value: --`

The list of ECS instances.


**InstanceId ** <span data-label="purple">string </span>`Sample value: i-yeattc3lkw****`

The ID of the ECS instance.



**Ip ** <span data-label="purple">string </span>`Sample value: 172.xx.xx.109`

The private IP address of the ECS instance.



**Port ** <span data-label="purple">integer </span>`Sample value: 80`

The port of the ECS instance.





**FunctionConfiguration ** <span data-label="purple">object </span>`Sample value: --`

veFaaS function details.


**FunctionId ** <span data-label="purple">string </span>`Sample value: 65a075a2`

veFaaS function ID.



**FunctionName ** <span data-label="purple">string </span>`Sample value: func-name-****`

veFaaS function name.




**VkeConfiguration ** <span data-label="purple">object </span>`Sample value: --`

The VKE details.


**ClusterId ** <span data-label="purple">string </span>`Sample value: cd59nk5v1a****`

The ID of the VKE cluster.



**Namespace ** <span data-label="purple">string </span>`Sample value: namespace01`

The VKE cluster namespace.



**Port ** <span data-label="purple">integer </span>`Sample value: 80`

The service port of the VKE cluster.



**ServiceName ** <span data-label="purple">string </span>`Sample value: service01`

The name of the VKE cluster service.





**BackendType ** <span data-label="purple">string </span>`Sample value: Function`

Type of backend service for the MCP service. Valid values:


* Function: veFaaS function.

* Domain: Fixed domain name.

* ECS: Elastic Compute Service (ECS).

* VKE: Vital Kubernetes Engine (VKE).

* CustomPublic: Public package (NPX/UVX).

* CustomPrivate: Private package (custom image).



**CreatedAt ** <span data-label="purple">string </span>`Sample value: 2006-01-02T15:04:05Z07:00`

Creation time of the MCP service.



**FailedLogFileUrl ** <span data-label="purple">string </span>`Sample value: https://xx.tos-s3-cn.volces.com/******`

URL to download the log file for a failed MCP service deployment.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">A return value is provided only when both of the following conditions are met: the MCP service status is unavailable (Status is "Error"), and the backend service is the newly created MCP service type (BackendType is "CustomPublic" or "CustomPrivate").</div>




**InboundAuthorizerConfiguration ** <span data-label="purple">object </span>`Sample value: --`

Inbound identity authentication information on the MCP service.


**Authorizer ** <span data-label="purple">object </span>`Sample value: --`

Authorizer configuration details.


**CustomJwtAuthorizer ** <span data-label="purple">object </span>`Sample value: --`

The OAuth JWT authentication configuration.


**AllowedClients ** <span data-label="purple">string[] </span>`Sample value: ["client1","client2"]`

List of allowed clients.



**DiscoveryUrl ** <span data-label="purple">string </span>`Sample value: https://example.com/.well-known/openid-configuration`

Authentication service address.




**IdentityAuthorizer ** <span data-label="purple">object </span>`Sample value: --`

The configuration of credential management when the backend service uses identity and permissions as outbound credentials.


**CredentialProviderName ** <span data-label="purple">string </span>`Sample value: Oauth2M2m01`

The name of credential management.



**ProviderType ** <span data-label="purple">string </span>`Sample value: Oauth2M2m`

The type of credential management. Valid values:


* ApiKey: Use API Key credentials.

* Oauth2M2m: Use OAuth Client.




**KeyAuth ** <span data-label="purple">object </span>`Sample value: --`

API Key authentication configuration.


**ApiKeyLocation ** <span data-label="purple">string </span>`Sample value: HEADER`

The location where the API Key is passed.



**ApiKeys ** <span data-label="purple">object[] </span>`Sample value: 8b02f2e2-ae83-11f0-b6e5-******&In`

API Key authentication configuration.


**Key ** <span data-label="purple">string </span>`Sample value: 65a075a2-aeff-11f0-****-00163e72f914`

The value of the API Key.



**Name ** <span data-label="purple">string </span>`Sample value: key-ye7f6gd7nktv3gi6c***`

API Key name.




**Parameter ** <span data-label="purple">string </span>`Sample value: Authorization`

The parameter name corresponding to the API Key carried in the request headers.





**AuthorizerType ** <span data-label="purple">string </span>`Sample value: ApiKey`

The type of inbound identity authentication for the MCP service. Valid values:


* ApiKey: API Key\-based authentication.

* CustomJWT: OAuth JWT\-based authentication.




**MCPServiceId ** <span data-label="purple">string </span>`Sample value: m-ye7f6gd7nktv3gi6c***`

MCP service ID.



**Name ** <span data-label="purple">string </span>`Sample value: mcp-name-***`

The name of the MCP service.



**NetworkConfigurations ** <span data-label="purple">object[] </span>`Sample value: --`

Network configuration details of the MCP service.


**Endpoint ** <span data-label="purple">string </span>`Sample value: ***.apigateway.com`

Endpoint for accessing the MCP service.



**NetworkType ** <span data-label="purple">string </span>`Sample value: Public`

Access type enabled for the MCP service. Value:


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




**OutboundAuthorizerConfiguration ** <span data-label="purple">object </span>`Sample value: --`

Outbound identity authentication configuration of the MCP service.


**Authorizer ** <span data-label="purple">object </span>`Sample value: --`

Authorizer configuration details.


**CustomJwtAuthorizer ** <span data-label="purple">object </span>`Sample value: --`

The OAuth JWT authentication configuration.


**AllowedClients ** <span data-label="purple">string[] </span>`Sample value: ["client1","client2"]`

List of allowed clients.



**DiscoveryUrl ** <span data-label="purple">string </span>`Sample value: https://example.com/.well-known/openid-configuration`

Authentication service address.




**IdentityAuthorizer ** <span data-label="purple">object </span>`Sample value: --`

The configuration of credential management when identity and permissions are used as outbound credentials.


**CredentialProviderName ** <span data-label="purple">string </span>`Sample value: Oauth2M2m01`

The name of credential management.



**ProviderType ** <span data-label="purple">string </span>`Sample value: Oauth2M2m`

The type of credential management. Valid values:


* ApiKey: Use API Key credentials.

* Oauth2M2m: Use OAuth Client.




**KeyAuth ** <span data-label="purple">object </span>`Sample value: --`

The configuration of API Key authentication when the API Key is used as outbound credentials.


**ApiKeyLocation ** <span data-label="purple">string </span>`Sample value: HEADER`

The location where the API Key is passed.



**ApiKeys ** <span data-label="purple">object[] </span>`Sample value: 8b02f2e2-ae83-11f0-b6e5-******&In`

API Key authentication configuration.


**Key ** <span data-label="purple">string </span>`Sample value: 65a075a2-aeff-11f0-****-00163e72f914`

The value of the API Key.



**Name ** <span data-label="purple">string </span>`Sample value: key-ye7f6gd7nktv3gi6c***`

API Key name.




**Parameter ** <span data-label="purple">string </span>`Sample value: Authorization`

The parameter name corresponding to the API Key carried in the request headers.





**AuthorizerType ** <span data-label="purple">string </span>`Sample value: ApiKey`

The type of outbound identity authentication for the MCP service. Valid values:


* ApiKey: API Key\-based authentication.

* Identity: Identity\-and\-permissions\-based authentication.




**Path ** <span data-label="purple">string </span>`Sample value: /mcp`

Access path of the MCP service.



**ProjectName ** <span data-label="purple">string </span>`Sample value: default`

Name of the project with which the MCP service is associated.



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


**Type ** <span data-label="purple">string </span>`Sample value: system`

Tag type.


* system: system tag

* custom: user tag



**Key ** <span data-label="purple">string </span>`Sample value: k1`

The tag key.



**Value ** <span data-label="purple">string </span>`Sample value: v1`

The tag value.




**UpdatedAt ** <span data-label="purple">string </span>`Sample value: 2006-01-02T15:04:05Z07:00`

Update time of the MCP service.



**GatewayInstanceName ** <span data-label="purple">string </span>`Sample value: exclusive-gateway`

The name of the dedicated gateway instance associated with the MCP service. This parameter is returned only when `GatewayMode` is `Exclusive`.



**BackendAccessType ** <span data-label="purple">string </span>`Sample value: Public`

The network type when the MCP service backend service uses a fixed domain name.


* Public: Public network.

* Private: Private network.



**GatewayMode ** <span data-label="purple">string </span>`Sample value: Shared`

The gateway mode.


* Shared: Shared gateway.

* Exclusive: Dedicated gateway.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=GetMCPService&Version=2025-10-30 HTTP/1.1
Content-Type: application/json
{
    "MCPServiceId":"m-ye70cet5ogtt****"
}

```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202106111445100102252431000052****",
    "Action": "GetMCPService",
    "Version": "2020-04-01",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "MCPService": {
      "MCPServiceId": " mcp-xxx",
      "Name": " mcp-service-x",
      "Path": " /mcp",
      "ProtocolType": " HTTP/MCP",
      "ProtocolConfiguration": {
        "ProtocolConvertConfiguration": " "
      },
      "NetworkConfigurations": [
        {
          "NetworkType": " Public",
          "Endpoint": " "
        }
      ],
      "InboundAuthorizerConfiguration": {
        "AuthorizerType": " ApiKey/CustomJWT",
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
      "OutboundAuthorizerConfiguration": {},
      "BackendConfiguration": {
        "FunctionConfiguration": {
          "FunctionId": " u3hyo****",
          "FunctionName": " my_function"
        },
        "CustomConfiguration": {
          "Domain": " api.example.com",
          "Port": " 80",
          "ProtocolType": " HTTP/HTTPS",
          "TlsSettings": {
            "Sni": " example.com",
            "TlsMode": " SIMPLE"
          }
        }
      },
      "BackendType": " Function/Domain",
      "CreatedAt": " 2006-01-02T15:04:05Z07:00",
      "UpdatedAt": " 2006-01-02T15:04:05Z07:00"
    }
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |MissingParameter.MCPServiceId |The required parameter MCPServiceId is not supplied. |The parameter MCPServiceId cannot be empty. |
|404 |InvalidResource.NotFound |The specified resource does not exist. |The specified resource does not exist. |

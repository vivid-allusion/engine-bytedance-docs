---
title: "CreateMCPService - Creates MCP service"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/CreateMCPService_-_Creates_MCP_services"
---

You can call this operation to create an MCP service. For operation instructions and precautions, refer to [MCP services](https://docs.byteplus.com/en/docs/agentkit/Tool_overview).

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action**<span data-label="purple"> string</span><span data-api-tag="require|KfueOU">必选</span>  `Sample value: CreateMCPService`

The action that you want to perform. Value: CreateMCPService.



**Version**<span data-label="purple"> string </span><span data-api-tag="require|eHJIA6">必选</span>`Sample value: 2025-10-30`

The API version. Value: 2025\-10\-30.



**BackendConfiguration.CustomConfiguration.Domain**<span data-label="purple"> string </span>`Optional Sample value: www.****.com`

The domain name of the backend service for the MCP service.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>BackendType</code> is set to Domain.</div>




**BackendConfiguration.CustomConfiguration.Port**<span data-label="purple"> integer </span>`Optional Sample value: 80`

The port of the backend service connected to the MCP service.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>BackendType</code> is set to Domain.</div>




**BackendConfiguration.CustomConfiguration.ProtocolType**<span data-label="purple"> string </span>`Optional Sample value: HTTP`

The protocol of the backend service connected to the MCP service. Value:


* HTTP: Backend HTTP service.

* HTTPS: Backend HTTPS service.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>BackendType</code> is set to Domain.</div>




**BackendConfiguration.FunctionConfiguration.FunctionId**<span data-label="purple"> string</span>` Optional Sample value: u3hyod8d`

ID of the veFaaS service.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>BackendType</code> is set to Function.</div>




**BackendConfiguration.CustomMcpConfiguration.FunctionId ** <span data-label="purple">string </span>`Optional Sample value: --`

ID of the created veFaaS Function (automatically populated by the system, no user input required).



**BackendConfiguration.CustomMcpConfiguration.EnableApmplus ** <span data-label="purple">boolean </span>`Optional` `Sample value: true`

Whether to enable TLS. Valid values:


* true (default): Enable.

* false: Disabled.



**BackendConfiguration.CustomConfiguration.TlsSettings.TlsMode**<span data-label="purple"> string </span> <span data-api-tag="require|Ko6toy">必选</span>`Sample value: DISABLE`

Select the TLS (Transport Layer Security) mode. This parameter is required when the backend service is of the fixed domain name type. Valid values:


* DISABLE: Disables TLS. Set to DISABLE when the backend protocol is HTTP.

* SIMPLE: Enables one\-way TLS. Set to SIMPLE when the backend protocol is HTTPS.



**BackendConfiguration.FunctionConfiguration.FunctionName ** <span data-label="purple">string </span>`Optional Sample value: vefaas01`

Name of the veFaaS service.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>BackendType</code> is set to Function.</div>




**BackendConfiguration.CustomMcpConfiguration.FunctionName ** <span data-label="purple">string </span>`Optional Sample value: --`

Name of the created veFaaS Function (automatically populated by the system, no user input required).



**BackendType**<span data-label="purple"> string</span><span data-api-tag="require|uwbDUN">必选</span>  `Sample value: Function`

Type of backend service for the MCP service. Valid values:


* Function: veFaaS function.

* Domain: Fixed domain name.

* ECS: Elastic Compute Service (ECS).

* VKE: Vital Kubernetes Engine (VKE).

* CustomPublic: Public package (NPX/UVX).

* CustomPrivate: Private package (custom image).



**BackendConfiguration.CustomMcpConfiguration.PrivatePackage.Command ** <span data-label="purple">string </span>`Optional Sample value: ./run.sh`

The startup command for the custom MCP service image, customized by the user based on the image. Default: ./run.sh.



**InboundAuthorizerConfiguration.Authorizer.CustomJwtAuthorizer.DiscoveryUrl**<span data-label="purple"> string</span><span data-api-tag="require|VtvTPZ">必选</span> ` Sample value: https://example.com/.well-known/openid-configuration`

The authentication service address used for inbound identity authentication by using OAuth JWT.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>Inbound****AuthorizerType</code> is set to CustomJWT.</div>




**ClientToken ** <span data-label="purple">string </span>`Optional` `Sample value: 333456899ff****`

The ClientToken is used to ensure request idempotency. The client can automatically generate a token, but you need to ensure that it is unique across requests. This prevents duplicate operations caused by multiple retries when the API request times out or an internal server error occurs.

Value: Only ASCII characters are supported. The length is no more than 64 ASCII characters.



**BackendConfiguration.CustomMcpConfiguration.PrivatePackage.Envs.N.Key ** <span data-label="purple">string[] </span>`Optional Sample value: k1`

Environment variable key for the custom MCP service image.



**InboundAuthorizerConfiguration.Authorizer.CustomJwtAuthorizer.AllowedClients.N ** <span data-label="purple">string[] </span>`Optional Sample value: client1`

The list of allowed clients when OAuth JWT is used for inbound identity authentication.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>Inbound****AuthorizerType</code> is set to CustomJWT.</div>




**InboundAuthorizerConfiguration.Authorizer.KeyAuth.ApiKeyLocation ** <span data-label="purple">string </span>`Optional Sample value: HEADER`

The location where the APIKey is passed when APIKey is used for inbound identity authentication. Valid values:


* HEADER: Currently, only HEADER is supported.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>Inbound****AuthorizerType</code> is set to ApiKey.</div>




**BackendConfiguration.CustomMcpConfiguration.PrivatePackage.Envs.N.Value ** <span data-label="purple">string[] </span>`Optional Sample value: v1`

Environment variable value for the custom MCP service image.



**InboundAuthorizerConfiguration.Authorizer.KeyAuth.ApiKeys.N.Name**<span data-label="purple"> string[] </span><span data-api-tag="require|wqrqgm">必选</span> `Sample value: ark-authkey`

The name of the APIKey when APIKey is used for inbound identity authentication.


* Parameter \- N: Indicates the serial number of the APIKey name. Value range: 1\-5. 

* Separate multiple field names with ampersands (&).

* A string of 4 to 64 characters.

* Consists of letters, numbers, hyphens (\-), and underscores (_).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>Inbound****AuthorizerType</code> is set to ApiKey.</div>




**BackendConfiguration.CustomMcpConfiguration.PrivatePackage.ImageUrl ** <span data-label="purple">string</span>` Optional Sample value: http://***`

The URL of the custom MCP service image.



**InboundAuthorizerConfiguration.Authorizer.KeyAuth.ApiKeys.N.Key ** <span data-label="purple">string[] </span>`Optional Sample value: 8b02f2e2-ae83-11f0-b6e5-******&In`

The value of the APIKey when the APIKey is used for inbound identity authentication. Valid values:


* Parameter \- N: Indicates the serial number of the API Key value. Value range: 1\-5.

* Separate multiple field names with ampersands (&).

* If not specified, a random string is generated by default.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>Inbound****AuthorizerType</code> is set to ApiKey.</div>




**BackendConfiguration.CustomMcpConfiguration.PublicPackage.McpType**<span data-label="purple"> string</span>` Optional Sample value: Stdio`

Custom MCP service type. Value:


* Stdio: Standard input/output.

* Remote: Remote service.



**InboundAuthorizerConfiguration.Authorizer.KeyAuth.Parameter**<span data-label="purple"> string </span>`Optional Sample value: Authorization`

The parameter name corresponding to the API Key carried in the request headers when the API Key is used for inbound identity authentication.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>Inbound****AuthorizerType</code> is set to CustomJWT.</div>




**BackendConfiguration.CustomMcpConfiguration.PublicPackage.PackageManagerType**<span data-label="purple"> string</span>` Optional Sample value: UVX`

Type of public package manager for the custom MCP service. Value:


* NPX.

* UVX.



**InboundAuthorizerConfiguration.AuthorizerType**<span data-label="purple"> string </span><span data-api-tag="require|lfE46F">必选</span>` Sample value: ApiKey`

The type of inbound identity authentication for the MCP service. Valid values:


* ApiKey: API Key\-based authentication.

* CustomJWT: OAuth JWT\-based authentication.



**BackendConfiguration.CustomMcpConfiguration.PublicPackage.RawConfig ** <span data-label="purple">string</span>` Optional Sample value: --`

Complete configuration (JSON string) of the custom MCP service.



**Name ** <span data-label="purple">string</span><span data-api-tag="require|ki99cE">必选</span> ` Sample value: MCP-001`

MCP service name. Value:


* A string of 4 to 64 characters.

* Consists of letters, numbers, hyphens (\-), and underscores (_).



**OutboundAuthorizerConfiguration.Authorizer.KeyAuth.ApiKeyLocation ** <span data-label="purple">string </span>`Optional Sample value: HEADER`

The location where the API Key is passed when the backend service uses the API Key as outbound credentials. Valid values:


* HEADER: Currently, only HEADER is supported.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>Outbound****.AuthorizerType</code> is set to ApiKey.</div>




**BackendConfiguration.EcsConfiguration.Instances.N.InstanceId ** <span data-label="purple">string[] </span>`Optional` `Sample value: i-yeattc3lkw****`

The ID of the ECS instance.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>BackendType</code> is set to ECS.</div>




**OutboundAuthorizerConfiguration.Authorizer.KeyAuth.ApiKeys.N.Key ** <span data-label="purple">string[]</span>` Optional Sample value: 3nr5ibubffg1s931eb5k5***`

The value of the API Key when the backend service uses the API Key as outbound credentials. Valid values:


* Parameter \- N: Indicates the serial number of the API Key value. Value range: 1\-5.

* Separate multiple field names with ampersands (&).

* If not specified, a random string is generated by default.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>Outbound****.AuthorizerType</code> is set to ApiKey.</div>




**BackendConfiguration.EcsConfiguration.Instances.N.Ip ** <span data-label="purple">string[] </span>`Optional` `Sample value: 172.xx.xx.109`

The private IP address of the ECS instance.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>BackendType</code> is set to ECS.</div>




**OutboundAuthorizerConfiguration.Authorizer.KeyAuth.Parameter**<span data-label="purple"> string</span>` Optional Sample value: Authorization`

The parameter name corresponding to the API Key carried in the request headers when the backend service uses the API Key as outbound credentials.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When the <code>Outbound****.AuthorizerType</code> parameter value is ApiKey, this parameter must be passed in.</div>




**BackendConfiguration.EcsConfiguration.Instances.N.Port ** <span data-label="purple">integer[] </span>`Optional` `Sample value: 80`

The port of the ECS instance.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>BackendType</code> is set to ECS.</div>




**OutboundAuthorizerConfiguration.AuthorizerType ** <span data-label="purple">string </span><span data-api-tag="require|wlWb97">必选</span> `Sample value: ApiKey`

The outbound credentials type of the backend service. Valid values:


* ApiKey: API Key\-based authentication.

* Identity: Identity\-and\-permissions\-based authentication.



**Path ** <span data-label="purple">string</span><span data-api-tag="require|zo9qnf">必选</span> ` Sample value: /mcp`

Access path of the MCP service.



**ProtocolConfiguration.HttpApiConfiguration.Configuration**<span data-label="purple"> string </span>`Optional Sample value: ewogICJzd2FnZ2VyIjogIjIuMCIsCiAgImluZm8iOiB7CiAgICAidGl0bGUi***`

API information of the MCP service, such as Swagger JSON, which must be Base64 encoded.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter needs to be configured only when the access method for the MCP service (ProtocolType) is "HTTP to MCP".</div>




**OutboundAuthorizerConfiguration.Authorizer.KeyAuth.ApiKeys.N.Name**<span data-label="purple"> string[]</span><span data-api-tag="require|sk23oz">必选</span>  `Sample value: api01`

The name of the API Key when the backend service uses the API Key as outbound credentials. Valid values:


* A string of 4 to 64 characters.

* Consists of letters, numbers, hyphens (\-), and underscores (_).

* Separate multiple field names with ampersands (&).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when the <code>Outbound****.AuthorizerType</code> parameter value is ApiKey.</div>




**BackendConfiguration.VkeConfiguration.ClusterId ** <span data-label="purple">string </span>`Optional` `Sample value: cd59nk5v1a****`

The ID of the VKE cluster.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>BackendType</code> is set to VKE.</div>




**ProtocolConfiguration.HttpApiConfiguration.Type ** <span data-label="purple">string </span>`Optional Sample value: Swagger`

The format of displaying the backend interface when the backend interface is based on HTTP. Value: Swagger.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>ProtocolType</code> is HTTP.</div>




**BackendConfiguration.VkeConfiguration.Namespace ** <span data-label="purple">string </span>`Optional` `Sample value: namespace01`

The name of the namespace in the VKE cluster.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>BackendType</code> is set to VKE.</div>




**ProtocolType**<span data-label="purple"> string</span><span data-api-tag="require|sULJoW">必选</span>  `Sample value: HTTP`

The access method for the MCP service. Valid values:


* HTTP: HTTP to MCP.

* MCP: Direct access to MCP.



**BackendConfiguration.VkeConfiguration.Port ** <span data-label="purple">integer </span>`Optional` `Sample value: 80`

The port of the VKE cluster.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>BackendType</code> is set to VKE.</div>




**BackendConfiguration.VkeConfiguration.ServiceName ** <span data-label="purple">string </span>`Optional` `Sample value: service01`

The name of the VKE cluster service.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>BackendType</code> is set to VKE.</div>




**NetworkConfiguration.EnablePrivateNetwork ** <span data-label="purple">boolean</span>` Optional Sample value: true`

Whether to enable private network access for the runtime. Value:


* true: Enabled.

* false (default): Disabled.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">One of the <code>EnablePrivateNetwork</code> or <code>EnablePublicNetwork</code> parameters must be provided.</div>




**NetworkConfiguration.EnablePublicNetwork ** <span data-label="purple">boolean </span>`Optional Sample value: true`

Whether to enable public network access for the runtime. Value:


* true (default): Enable.

* false: Disabled.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">One of the <code>EnablePrivateNetwork</code> or <code>EnablePublicNetwork</code> parameters must be provided.</div>




**NetworkConfiguration.VpcConfiguration.VpcId ** <span data-label="purple">string </span><span data-api-tag="require|kxmnqo">必选</span> `Sample value: vpc-ye7s6jatq8rxg218****`

VPC ID.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is required when <code>EnablePrivateNetwork</code> is set to true.</div>




**NetworkConfiguration.VpcConfiguration.SubnetIds.N ** <span data-label="purple">string[] </span>`Optional Sample value: SubnetIds.1=subnet-ye7s6jatq8rxg218****`

Subnet ID list. Only one Subnet ID can be specified for each availability zone.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is required when <code>EnablePrivateNetwork</code> is set to true.</div>




**ProjectName ** <span data-label="purple">string </span>`Optional` `Sample value: default`

The name of the associated project.



**OutboundAuthorizerConfiguration.Authorizer.IdentityAuthorizer.CredentialProviderName ** <span data-label="purple">string </span>`Optional` `Sample value: Oauth2M2m01`

The name of credential management when the backend service uses identity and permissions as outbound credentials.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>Outbound****.AuthorizerType</code> is set to Identity.</div>




**Tags.N.Key** <span data-label="purple">string[] </span><span data-api-tag="require|hxkEHx">必选</span>` Sample value: k1`

The tag key of the user tag to be added to the resource.


* Parameter \- N: Indicates the serial number of the tag key. Value range: 1–50.

* Separate multiple tag keys with ampersands (&).


Naming rules:


* It cannot start with` volc: `or `sys:` in any case form.

> Tag keys that start with `volc:` or `sys: `are reserved for the system. You cannot create tags starting with them.


* Only letters, digits, spaces, and the following symbols are allowed: "_", ".", ":", "/", "=", "+", "\-", and "@".

* It must be 1 to 128 characters in length.



**OutboundAuthorizerConfiguration.Authorizer.IdentityAuthorizer.ProviderType ** <span data-label="purple">string </span>`Optional` `Sample value: Oauth2M2m`

The type of credential management when the backend service uses identity and permissions as outbound credentials. Valid values:


* ApiKey: Use API Key credentials.

* Oauth2M2m: Use OAuth Client credentials.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when the <code>Outbound****.AuthorizerType</code> parameter value is Identity.</div>




**Tags.N.Value ** <span data-label="purple">string[] </span>`Optional Sample value: v1`

The tag value of the tag associated with the resource.


* Parameter \- N: Indicates the serial number of the tag value. Value range: 1\-50.

* Separate multiple tag values with &.


Naming rules:


* Only letters, digits, spaces, and the following symbols are allowed: "_", ".", ":", "/", "=", "+", "\-", and "@".

* It can be empty. Length limit: 0\-256 characters.



**RoleName ** <span data-label="purple">string </span>`Optional` `Sample value: TestRoleForAgentKit`

Name of the IAM role associated with the MCP service.



**Tags.N.Type ** <span data-label="purple">string[] </span>`Optional` `Sample value: system`

Tag type.


* system: system tag

* custom: user tag



**GatewayInstanceId ** <span data-label="purple">string </span>`Optional` `Sample value: gw-********`

The ID of the dedicated gateway instance associated with the MCP service.


* This parameter is required only when `GatewayMode` is set to `Exclusive`.

* You can obtain the dedicated gateway instance ID in the AgentKit console under "Gateway \> Gateway instance \> Dedicated gateway".



**BackendAccessType ** <span data-label="purple">string </span>`Optional` `Sample value: Public | Private`

The network type used by the dedicated gateway to access the backend service. Specify this parameter when GatewayMode is set to` Exclusive` and BackendType is set to `Domain`.


* Public: Public network access.

* Private: Access using private network



**GatewayMode ** <span data-label="purple">string </span>`Optional` `Sample value: Shared | Exclusive`

The gateway mode of the MCP service.


* Shared (default): Shared gateway.

* Exclusive: Dedicated gateway.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**MCPServiceId ** <span data-label="purple">string </span>`Sample value: m-ye7s6jatq8rxg218****`

MCP service ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=CreateMCPService&Version=2025-10-30 HTTP/1.1
Content-Type: application/json
{
    "Name": "mcp-***",
    "Path": "/mcp",
    "ProtocolType": "MCP",
    "NetworkConfigurations": [
        {
            "NetworkType": "Public"
        }
    ],
    "BackendType": "Function",
    "BackendConfiguration": {
        "FunctionConfiguration": {
            "FunctionId": "26fqb4gn"
        }
    },
    "InboundAuthorizerConfiguration": {
        "AuthorizerType": "ApiKey",
        "Authorizer": {
            "KeyAuth": {
                "ApiKeys": [
                    {
                        "Name": "***"
                    }
                ],
                "ApiKeyLocation": "HEADER"
            }
        }
    },
    "OutboundAuthorizerConfiguration": {
        "AuthorizerType": "ApiKey",
        "Authorizer": {
            "KeyAuth": {
                "ApiKeys": [
                    {
                        "Name": "***",
                        "Key": "usix-sixa-xxxx-***"
                    }
                ],
                "ApiKeyLocation": "HEADER"
            }
        }
    }
}

```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202106111445100102252431000052****",
    "Action": "CreateMCPService",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "MCPServiceId": " m-ye7s6jatq8rxg218****"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidApiKeyLocation.Malformed |The specified ApiKeyLocation is malformed. |The specified ApiKeyLocation is invalid. |
|400 |InvalidArgument |The specified argument is invalid. |The specified parameter is invalid. |
|400 |InvalidAuthorizerType.Malformed |The specified AuthorizerType is malformed. |The specified AuthorizerType is invalid. |
|400 |InvalidBackendType.Malformed |The specified BackendType is malformed. |The specified BackendType is invalid. |
|400 |InvalidFunction.NotFound |The specified FunctionId does not exist. |The specified function does not exist. |
|400 |InvalidMcpType.Malformed |The specified McpType is malformed. |The specified McpType is invalid. |
|400 |InvalidName.Malformed |The specified Name is malformed. |The specified Name is invalid. |
|400 |InvalidNetworkType.Malformed |The specified NetworkType is malformed. |The specified NetworkType is invalid. |
|400 |InvalidPackageManagerType.Malformed |The specified PackageManagerType is malformed. |The specified PackageManagerType is invalid. |
|400 |InvalidProtocolType.Malformed |The specified ProtocolType is malformed. |The specified ProtocolType is invalid. |
|400 |InvalidTlsMode.Malformed |The specified TlsMode is malformed. |The specified TlsMode is invalid. |
|400 |InvalidType.Malformed |The specified Type is malformed. |The specified value of Type is invalid. |
|400 |LimitExceeded.MaximumApiKeys |The specified ApiKeys exceeds the maximum limit. |The number of specified ApiKeys exceeds the upper limit. |
|400 |LimitExceeded.MaximumPort |The number of specified Port exceeds the maximum limit. |The number of specified ports exceeds the upper limit. |
|400 |LimitExceeded.MaximumSubnetIds |The number of specified SubnetIds exceeds the maximum limit. |The specified SubnetIds exceeds the upper limit. |
|400 |LimitExceeded.MinimumApiKeys |The number of specified ApiKeys exceeds the minimum limit. |The specified ApiKeys exceeds the lower limit. |
|400 |LimitExceeded.MinimumPort |The number of specified Port exceeds the minimum limit. |The number of specified ports is below the lower limit. |
|400 |LimitExceeded.MinimumSubnetIds |The number of specified SubnetIds exceeds the minimum limit. |The number of specified SubnetIds exceeds the lower limit. |
|400 |MissingParameter.ApiKeyLocation |The required parameter ApiKeyLocation is not supplied. |The parameter ApiKeyLocation cannot be empty. |
|400 |MissingParameter.ApiKeys |The required parameter ApiKeys is not supplied. |The parameter ApiKeys cannot be empty. |
|400 |MissingParameter.AuthorizerType |The required parameter AuthorizerType is not supplied. |The parameter AuthorizerType cannot be empty. |
|400 |MissingParameter.BackendConfiguration |The required parameter BackendConfiguration is not supplied. |The parameter BackendConfiguration cannot be empty. |
|400 |MissingParameter.BackendType |The required parameter BackendType is not supplied. |The parameter BackendType cannot be empty. |
|400 |MissingParameter.DiscoveryUrl |The required parameter DiscoveryUrl is not supplied. |The parameter DiscoveryUrl cannot be empty. |
|400 |MissingParameter.Domain |The required parameter Domain is not supplied. |The Domain cannot be empty. |
|400 |MissingParameter.FunctionId |The required parameter FunctionId is not supplied. |The parameter FunctionId cannot be left empty. |
|400 |MissingParameter.InboundAuthorizerConfiguration |The required parameter InboundAuthorizerConfiguration is not supplied. |The parameter InboundAuthorizerConfiguration cannot be empty. |
|400 |MissingParameter.Key |The required parameter Key is not supplied. |The parameter Key cannot be empty.  |
|400 |MissingParameter.Name |The required parameter Name is not supplied. |Name cannot be empty. |
|400 |MissingParameter.NetworkConfiguration |The required parameter NetworkConfiguration is not supplied. |The parameter NetworkConfiguration cannot be empty. |
|400 |MissingParameter.NetworkConfigurations |The required parameter NetworkConfigurations is not supplied. |The parameter NetworkConfigurations cannot be empty. |
|400 |MissingParameter.NetworkType |The required parameter NetworkType is not supplied. |The parameter NetworkType cannot be empty. |
|400 |MissingParameter.OutboundAuthorizerConfiguration |The required parameter OutboundAuthorizerConfiguration is not supplied. |The parameter OutboundAuthorizerConfiguration cannot be empty. |
|400 |MissingParameter.Parameter |The required parameter Parameter is not supplied. |The parameter Parameter cannot be empty. |
|400 |MissingParameter.Path |The required parameter Path is not supplied. |The parameter Path cannot be empty. |
|400 |MissingParameter.ProtocolType |The required parameter ProtocolType is not supplied. |Parameter ProtocolType cannot be empty. |
|400 |MissingParameter.TlsMode |The required parameter TlsMode is not supplied. |The parameter TlsMode cannot be empty. |
|400 |MissingParameter.VpcId |The required parameter VpcId is not supplied. |The parameter VpcId cannot be empty. |

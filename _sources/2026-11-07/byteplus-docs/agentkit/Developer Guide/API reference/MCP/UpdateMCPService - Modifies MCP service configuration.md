---
title: "UpdateMCPService - Modifies MCP service configuration"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/UpdateMCPService_-_Modifies_MCP_service_configuration"
---

You can call this operation to modify MCP service configuration.

<span id=".5L2_55So6K-05piO"></span>
## Usage notes

You cannot change the type of inbound identity authentication for an MCP service.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|yKyFgC">必选</span> `Sample value: UpdateMCPService`

The action that you want to perform. Value: UpdateMCPService.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|GD7aMC">必选</span> `Sample value: 2025-10-30`

The version of the API. Value: 2025\-10\-30.



**BackendConfiguration.CustomConfiguration.Domain ** <span data-label="purple">string </span>`Optional Sample value: www.***.com`

The domain name of the backend service for the MCP service.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>BackendType</code> is set to Domain.</div>




**BackendConfiguration.CustomConfiguration.Port ** <span data-label="purple">integer </span>`Optional Sample value: 443`

Port of the backend service connected to the MCP service.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>BackendType</code> is set to Domain.</div>




**BackendConfiguration.CustomConfiguration.ProtocolType**<span data-label="purple"> string </span>`Optional Sample value: HTTP`

The protocol of the backend service connected to the MCP service. Value:


* HTTP: Backend HTTP service.

* HTTPS: Backend HTTPS service.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>BackendType</code> is set to Domain.</div>




**BackendConfiguration.FunctionConfiguration.FunctionId ** <span data-label="purple">string</span>` Optional Sample value: fc65a****`

ID of the veFaaS service.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>BackendType</code> is set to Function.</div>




**BackendConfiguration.CustomMcpConfiguration.FunctionId ** <span data-label="purple">string </span>`Optional Sample value: --`

ID of the created veFaaS Function (automatically populated by the system, no user input required).



**BackendConfiguration.CustomConfiguration.TlsSettings.TlsMode ** <span data-label="purple">string </span><span data-api-tag="require|Eq7iFM">必选</span> `Sample value: SIMPLE`

Select the TLS (Transport Layer Security) mode. This parameter is required when the backend service is of the fixed domain name type. Valid values:


* DISABLE: Disables TLS. Set to DISABLE when the backend protocol is HTTP.

* SIMPLE: Enables one\-way TLS. Set to SIMPLE when the backend protocol is HTTPS.



**BackendConfiguration.FunctionConfiguration.FunctionName ** <span data-label="purple">string </span>`Optional Sample value: func-name-****`

Name of the veFaaS service.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>BackendType</code> is set to Function.</div>




**BackendConfiguration.CustomMcpConfiguration.FunctionName ** <span data-label="purple">string </span>`Optional Sample value: --`

Name of the created veFaaS Function (automatically populated by the system, no user input required).



**BackendConfiguration.CustomMcpConfiguration.EnableApmplus ** <span data-label="purple">boolean </span>`Optional` `Sample value: true`

Whether to enable the log service. Value:


* true: Enables.

* false: Disables.



**BackendType ** <span data-label="purple">string </span>`Optional Sample value: Function`

Type of backend service for the MCP service. Value:


* Function: veFaaS function.

* Domain: Fixed domain name.

* ECS: ECS.

* VKE: VKE.

* CustomPublic: public package (NPX/UVX).

* CustomPrivate: private package (custom image).



**BackendConfiguration.CustomMcpConfiguration.PrivatePackage.Command ** <span data-label="purple">string </span>`Optional Sample value: ./run.sh`

Startup command for the custom MCP service image, customized by the user based on the image. Default: ./run.sh



**InboundAuthorizerConfiguration.Authorizer.KeyAuth.ApiKeyLocation ** <span data-label="purple">string </span>`Optional Sample value: HEADER`

The location where the APIKey is passed when APIKey is used for inbound identity authentication. Value:


* HEADER: Currently, only HEADER is supported.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>Inbound****.AuthorizerType</code> is set to ApiKey.</div>




**BackendConfiguration.CustomMcpConfiguration.PrivatePackage.Envs.N.Key ** <span data-label="purple">string[] </span>`Optional Sample value: k1`

Environment variable key for the custom MCP service image.



**InboundAuthorizerConfiguration.Authorizer.KeyAuth.ApiKeys.N.Name ** <span data-label="purple">string[] </span><span data-api-tag="require|AwdXNw">必选</span> `Sample value: ark-authkey`

The name of the APIKey when APIKey is used for inbound identity authentication.


* Parameter \- N: Indicates the serial number of the APIKey name. Value range: 1\-5. 

* Separate multiple field names with ampersands (&).

* A string of 4 to 64 characters.

* Consists of letters, numbers, hyphens (\-), and underscores (_).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>Inbound****.AuthorizerType</code> is set to ApiKey.</div>




**BackendConfiguration.CustomMcpConfiguration.PrivatePackage.Envs.N.Value ** <span data-label="purple">string[] </span>`Optional Sample value: v1`

Environment variable value for the custom MCP service image.



**InboundAuthorizerConfiguration.Authorizer.KeyAuth.ApiKeys.N.Key ** <span data-label="purple">string[] </span>`Optional Sample value: 8b02f2e2-ae83-11f0-b6e5-******&In`

The value of the API Key when the API Key is used for inbound identity authentication. Value:


* Parameter \- N: Indicates the serial number of the API Key value. Value range: 1\-5.

* Separate multiple field names with ampersands (&).

* If not specified, a random string is generated by default.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>Inbound****.AuthorizerType</code> is set to ApiKey.</div>




**BackendConfiguration.CustomMcpConfiguration.PrivatePackage.ImageUrl ** <span data-label="purple">string</span>` Optional Sample value: http://***`

The URL of the custom MCP service image.



**InboundAuthorizerConfiguration.Authorizer.KeyAuth.Parameter**<span data-label="purple"> string </span>`Optional Sample value: Authorization`

The parameter name corresponding to the API Key carried in the request headers when the API Key is used for inbound identity authentication.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>Inbound****.AuthorizerType</code> is set to ApiKey.</div>




**BackendConfiguration.CustomMcpConfiguration.PublicPackage.McpType**<span data-label="purple"> string</span>` Optional Sample value: Stdio`

Custom MCP service type. Value:


* Stdio: Standard input/output.

* Remote: Remote service.



**InboundAuthorizerConfiguration.AuthorizerType ** <span data-label="purple">string </span><span data-api-tag="require|XGFnmZ">必选</span> `Sample value: ApiKey`

Inbound identity authentication for the MCP service. Value:


* ApiKey: API Key is used for authentication.

* CustomJWT: OAuth JWT\-based authentication.



**BackendConfiguration.CustomMcpConfiguration.PublicPackage.PackageManagerType**<span data-label="purple"> string</span>` Optional Sample value: UVX`

Type of public package manager for the custom MCP service. Value:


* NPX.

* UVX.



**MCPServiceId ** <span data-label="purple">string </span><span data-api-tag="require|TBV1a5">必选</span> `Sample value: m-ye7f6gd7nktv3gi6c***`

MCP service ID.



**BackendConfiguration.CustomMcpConfiguration.PublicPackage.RawConfig ** <span data-label="purple">string</span>` Optional Sample value: --`

Complete configuration (JSON string) of the custom MCP service.



**OutboundAuthorizerConfiguration.Authorizer.KeyAuth.ApiKeyLocation ** <span data-label="purple">string </span>`Optional Sample value: HEADER`

The location where the API Key is passed when the backend service uses the API Key as outbound credentials. Value:


* HEADER: Currently, only HEADER is supported.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>Outbound****.AuthorizerType</code> is set to ApiKey.</div>




**OutboundAuthorizerConfiguration.Authorizer.KeyAuth.ApiKeys.N.Name ** <span data-label="purple">string[] </span><span data-api-tag="require|wCj3XA">必选</span> `Sample value: name-ye7f6gd7nktv3gi6c***`

The name of the API Key when the backend service uses the API Key as outbound credentials. Valid values:


* A string of 4 to 64 characters.

* Consists of letters, numbers, hyphens (\-), and underscores (_).

* Separate multiple field names with ampersands (&).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>Outbound****.AuthorizerType</code> is set to ApiKey.</div>




**BackendConfiguration.EcsConfiguration.Instances.N.InstanceId ** <span data-label="purple">string[] </span>`Optional` `Sample value: i-yeattc3lkw****`

The ID of the ECS instance.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>BackendType</code> is set to ECS.</div>




**OutboundAuthorizerConfiguration.Authorizer.KeyAuth.ApiKeys.N.Key ** <span data-label="purple">string[]</span>` Optional Sample value: 3nr5ibubffg1s931eb5k5***`

The value of the API Key when the backend service uses the API Key as outbound credentials. Value:


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


<div data-tips="true" data-tips-type="tip">Required when <code>Outbound****.AuthorizerType</code> is set to ApiKey.</div>




**BackendConfiguration.EcsConfiguration.Instances.N.Port ** <span data-label="purple">integer[] </span>`Optional` `Sample value: 80`

The port of the ECS instance.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>BackendType</code> is set to ECS.</div>




**OutboundAuthorizerConfiguration.AuthorizerType ** <span data-label="purple">string </span><span data-api-tag="require|EeE6uz">必选</span> `Sample value: ApiKey`

The outbound credentials type of the backend service. Valid values:


* ApiKey: API Key\-based authentication.

* Identity: Use identity and permissions for authentication.



**InboundAuthorizerConfiguration.Authorizer.CustomJwtAuthorizer.DiscoveryUrl ** <span data-label="purple">string </span><span data-api-tag="require|x8a11v">必选</span> `Sample value: https://example.com/.well-known/openid-configuration`

Authentication service address.



**InboundAuthorizerConfiguration.Authorizer.CustomJwtAuthorizer.AllowedClients.N ** <span data-label="purple">string[] </span>`Optional Sample value: client1`

List of allowed clients.



**BackendConfiguration.VkeConfiguration.ClusterId ** <span data-label="purple">string </span>`Optional` `Sample value: cd59nk5v1a****`

The ID of the VKE cluster.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>BackendType</code> is set to VKE.</div>




**BackendConfiguration.VkeConfiguration.Namespace ** <span data-label="purple">string </span>`Optional` `Sample value: namespace01`

The name of the namespace in the VKE cluster.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>BackendType</code> is set to VKE.</div>




**BackendConfiguration.VkeConfiguration.Port ** <span data-label="purple">integer </span>`Optional` `Sample value: 80`

The port of the VKE cluster.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>BackendType</code> is set to VKE.</div>




**BackendConfiguration.VkeConfiguration.ServiceName ** <span data-label="purple">string </span>`Optional` `Sample value: service01`

The name of the VKE cluster service.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>BackendType</code> is set to VKE.</div>




**OutboundAuthorizerConfiguration.Authorizer.IdentityAuthorizer.CredentialProviderName ** <span data-label="purple">string </span>`Optional` `Sample value: Oauth2M2m01`

The name of credential management when the backend service uses identity and permissions as outbound credentials.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>Outbound****.AuthorizerType</code> is set to Identity.</div>




**OutboundAuthorizerConfiguration.Authorizer.IdentityAuthorizer.ProviderType ** <span data-label="purple">string </span>`Optional` `Sample value: Oauth2M2m01`

The type of credential management when the backend service uses identity and permissions as outbound credentials. Value:


* ApiKey: Use API Key credentials.

* Oauth2M2m: Use OAuth Client credentials.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>Outbound****.AuthorizerType</code> is set to Identity.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**MCPServiceId ** <span data-label="purple">string </span>`Sample value: m-ye7f6gd7nktv3gi6c***`

MCP service ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=UpdateMCPService&Version=2025-10-30 HTTP/1.1
Content-Type: application/json
{
    "MCPServiceId":"m-ye6xqypudcq7oi5c****",
    "BackendType": "Function",
    "BackendConfiguration": {
        "FunctionConfiguration": {
            "FunctionId": "j3t****"
        }
    },
        "InboundAuthorizerConfiguration": {
        "AuthorizerType": "ApiKey",
        "Authorizer": {
            "KeyAuth": {
                "ApiKeys": [
                    {
                        "Name": "****"
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
        "Action": "UpdateMCPService",
        "Version": "2025-10-30",
        "Service": "agentkit",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "MCPServiceId":" m-xxx"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidAuthorizerType.Malformed |The specified AuthorizerType is malformed. |The specified AuthorizerType is invalid. |
|400 |InvalidApiKeyLocation.Malformed |The specified ApiKeyLocation is malformed. |The specified ApiKeyLocation is invalid. |
|400 |InvalidBackendType.Malformed |The specified BackendType is malformed. |The specified BackendType is invalid. |
|400 |InvalidMcpType.Malformed |The specified McpType is malformed. |The specified McpType is invalid. |
|400 |InvalidNetworkType.Malformed |The specified NetworkType is malformed. |The specified NetworkType is invalid. |
|400 |InvalidPackageManagerType.Malformed |The specified PackageManagerType is malformed. |The specified PackageManagerType is invalid. |
|400 |MissingParameter.ApiKeyLocation |The required parameter ApiKeyLocation is not supplied. |The parameter ApiKeyLocation cannot be empty. |
|400 |InvalidProtocolType.Malformed |The specified ProtocolType is malformed. |The specified ProtocolType is invalid. |
|400 |InvalidTlsMode.Malformed |The specified TlsMode is malformed. |The specified TlsMode is invalid. |
|400 |LimitExceeded.MaximumApiKeys |The specified ApiKeys exceeds the maximum limit. |The number of specified ApiKeys exceeds the upper limit. |
|400 |LimitExceeded.MinimumApiKeys |The number of specified ApiKeys exceeds the minimum limit. |The specified ApiKeys exceeds the lower limit. |
|400 |LimitExceeded.MaximumPort |The number of specified Port exceeds the maximum limit. |The number of specified ports exceeds the upper limit. |
|400 |MissingParameter.AuthorizerType |The required parameter AuthorizerType is not supplied. |The parameter AuthorizerType cannot be empty. |
|400 |MissingParameter.ApiKeys |The required parameter ApiKeys is not supplied. |The parameter ApiKeys cannot be empty. |
|400 |MissingParameter.DiscoveryUrl |The required parameter DiscoveryUrl is not supplied. |The parameter DiscoveryUrl cannot be empty. |
|400 |MissingParameter.NetworkType |The required parameter NetworkType is not supplied. |The parameter NetworkType cannot be empty. |
|400 |LimitExceeded.MinimumPort |The number of specified Port exceeds the minimum limit. |The number of specified ports is below the lower limit. |
|400 |MissingParameter.MCPServiceId |The required parameter MCPServiceId is not supplied. |The parameter MCPServiceId cannot be empty. |
|400 |MissingParameter.Name |The required parameter Name is not supplied. |Name cannot be empty. |
|400 |MissingParameter.TlsMode |The required parameter TlsMode is not supplied. |The parameter TlsMode cannot be empty. |
|400 |MissingParameter.Parameter |The required parameter Parameter is not supplied. |The parameter Parameter cannot be empty. |
|400 |MissingParameter.Domain |The required parameter Domain is not supplied. |The parameter Domain cannot be empty. |
|400 |MissingParameter.BackendType |The required parameter BackendType is not supplied. |The parameter BackendType cannot be empty. |

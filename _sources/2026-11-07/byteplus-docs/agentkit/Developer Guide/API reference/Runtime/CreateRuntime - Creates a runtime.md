---
title: "CreateRuntime - Creates a runtime"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/CreateRuntime_-_Creates_a_runtime"
---

You can call this operation to create a runtime. For operation instructions and precautions, refer to [Creating runtime](https://docs.byteplus.com/en/docs/agentkit/Creating_agent_runtimes_in_console).

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|yeuXwM">必选</span> `Sample value: CreateRuntime`

The action that you want to perform. Value: CreateRuntime.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|FT6pEM">必选</span> `Sample value: 2025-10-30`

The API version. Value: 2025\-10\-30.



**AgentSpaceId ** <span data-label="purple">string </span>`Optional` `Sample value: as-yeh6q4a48****`

The ID of the associated A2A agent space.



**ApmplusEnable**<span data-label="purple"> boolean</span>` Optional Sample value: true`

Whether to enable APMPlus and log services to monitor the runtime and write logs. Valid values:


* true (default): Enable.

* false: Disabled.



**ArtifactType ** <span data-label="purple">string </span><span data-api-tag="require|htC76h">必选</span> `Sample value: image`

Image type. Valid values:


* image: Custom image.

* public_image: Public image.



**ArtifactUrl ** <span data-label="purple">string </span><span data-api-tag="require|qButrR">必选</span> `Sample value: cp-enterprise-ap-southeast-1.cr.volces.com/demo/agent:latest`

Image URL.


* The image URL in the `host/namespace/repo:tag` format.

* When the image type is set to public image, enter the image URL as `agentkit-prod-public-ap-southeast-1.cr.volces.com/template/financial:v1117_1`.



**AuthorizerConfiguration.CustomJwtAuthorizer.DiscoveryUrl ** <span data-label="purple">string </span><span data-api-tag="require|PtCrt0">必选</span> `Sample value: https://example.com/.well-known/openid-configuration`

The URL of the token signing key used for inbound identity authentication by using OAuth JWT.

This URL is used to obtain OpenID Connect configuration or authorization server metadata to verify the token passed in. Currently, only signature key URLs from the BytePlus identity service are supported.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For parameters with <code>KeyAuth</code> and <code>CustomJwtAuthorizer</code>, you must pass one of the two parameter sets.</div>




**AuthorizerConfiguration.CustomJwtAuthorizer.AllowedClients.N ** <span data-label="purple">string[] </span>`Optional` `Sample value: ["client1”, "client2"]`

The list of allowed clients when OAuth JWT is used for inbound identity authentication. If it is left empty, all clients are allowed to access.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For parameters with <code>KeyAuth</code> and <code>CustomJwtAuthorizer</code>, you must pass one of the two parameter sets.</div>




**AuthorizerConfiguration.KeyAuth.ApiKeyLocation**<span data-label="purple"> string </span>`Optional Sample value: Header`

The location where the API Key is passed when API Key is used for inbound identity authentication.


* Header: Currently, only Header is supported.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For parameters with <code>KeyAuth</code> and <code>CustomJwtAuthorizer</code>, you must pass one of the two parameter sets.</div>




**AuthorizerConfiguration.KeyAuth.ApiKeyName**<span data-label="purple"> string</span>` Optional Sample value: test-key`

The name of the passed API Key when API Key is used for inbound identity authentication. Valid values:


* When this parameter is passed in, it cannot be empty. The parameter value is a string containing 4 to 64 characters.

* Consists of letters, numbers, hyphens (\-), and underscores (_).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For parameters with <code>KeyAuth</code> and <code>CustomJwtAuthorizer</code>, you must pass one of the two parameter sets.</div>




**ClientToken ** <span data-label="purple">string </span>`Optional` `Sample value: 23fa21A8823nfasd7f****`

The ClientToken is used to ensure request idempotency. The client can automatically generate a token, but you need to ensure that it is unique across requests. This prevents duplicate operations caused by multiple retries when the API request times out or an internal server error occurs.

Value: Only ASCII characters are supported. The length is no more than 64 ASCII characters.



**CpuMilli ** <span data-label="purple">integer </span>`Optional` `Sample value: 2000`

The vCPU specification of the instance. Unit: milli cpu.


* Valid range: 250\-16000.

* Default value: 2000.



**Description ** <span data-label="purple">string </span>`Optional` `Sample value: Agent-001`

Runtime description.


* The text length cannot exceed 1000 Unicode characters.

* If left blank, the parameter defaults to an empty value.



**Envs.N.Key ** <span data-label="purple">string[] </span><span data-api-tag="require|zkI87Q">必选</span> `Sample value: DATABASE_MEM0_BASE_URL`

Key of the runtime environment variable.


* It can contain only letters, digits, and underscores, and must start with an underscore or letter. It must be 1 to 63 characters in length.

* Each Key must be unique under one runtime.



**Envs.N.Value ** <span data-label="purple">string[] </span>`Optional` `Sample value: mem0-cnlfjzigaku8gc****.mem0.volces.com:8000`

Value of the runtime environment variable.



**KnowledgeId ** <span data-label="purple">string </span>`Optional` `Sample value: kb-ye9g****`

ID of the associated knowledge base.



**MCPToolsetId ** <span data-label="purple">string </span>`Optional` `Sample value: mt-3tigy72q3u3vj0x2****`

ID of the associated MCP toolset.



**MaxConcurrency ** <span data-label="purple">integer </span>`Optional` `Sample value: 100`

The maximum number of concurrent requests for the instance.


* Valid range: 10\-1000.

* Default value: 100.



**MaxInstance ** <span data-label="purple">integer </span>`Optional` `Sample value: 10`

The maximum number of instances.


* Valid range: 1\-10.

* Default: 10.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To increase the upper limit for the maximum number of instances, go to the <a href="https://console.byteplus.com/quota/productList/ParameterList?ProviderCode=agentkit">Quota Center</a> to apply for a higher runtime/instance quota limit.</div>




**MemoryId ** <span data-label="purple">string </span>`Optional` `Sample value: mem-1763997****`

ID of the associated memory.



**MemoryMb ** <span data-label="purple">integer </span>`Optional` `Sample value: 2048`

The memory specification of the instance. Unit: MiB.


* Valid range: 512\-131072.

* Default value: 4096.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Values must be specified in increments of 512, such as 512, 1024, 1536, and 2048.</div>




**MinInstance ** <span data-label="purple">integer </span>`Optional` `Sample value: 1`

The minimum number of instances.


* Valid range: 0\-MaxInstance.

* Default value: 0.



**ModelAgentName ** <span data-label="purple">string </span>`Optional` `Sample value: doubao-seed-1.6`

The access point for the inference model.



**Name ** <span data-label="purple">string </span><span data-api-tag="require|GTE9UQ">必选</span> `Sample value: test-runtime`

Runtime name.


* A string of 4 to 64 characters.

* Consists of letters, numbers, hyphens (\-), and underscores (_).



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




**NetworkConfiguration.VpcConfiguration.VpcId ** <span data-label="purple">string </span><span data-api-tag="require|UdSQaP">必选</span> `Sample value: vpc-257gqcdfvx6n****`

VPC ID.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when NetworkConfiguration.EnablePrivateNetwork is set to true.</div>




**NetworkConfiguration.VpcConfiguration.EnableSharedInternetAccess ** <span data-label="purple">boolean </span>`Optional` `Sample value: true`

The public network egress configuration. Valid values:


* true (default): Enabled. This value indicates that the runtime uses the public network egress provided by the platform to access the public network.

* false: Not enabled. This value indicates that the runtime uses the public network NAT gateway egress configured in the private network to access the public network.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is valid only when <code>NetworkConfiguration.EnablePrivateNetwork</code> is set to true.</div>




**NetworkConfiguration.VpcConfiguration.SubnetIds.N ** <span data-label="purple">string[] </span>`Optional` `Sample value: ["subnet-1234567890"]`

Subnet ID list. Only one Subnet ID can be specified for each availability zone.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is required when <code>EnablePrivateNetwork</code> is set to true.</div>




**ProjectName ** <span data-label="purple">string </span>`Optional` `Sample value: default`

The name of the associated project.



**RoleName ** <span data-label="purple">string </span><span data-api-tag="require|LhPzSu">必选</span> `Sample value: AgentKit_Runtime_Default_ServiceRole_****`

Name of the IAM role associated with the runtime.



**RequestModifierConfig.FunctionId ** <span data-label="purple">string </span>`Optional` `Sample value: fn-2abcxxxx`

veFaaS function ID. You can call [GetFunction](https://docs.byteplus.com/en/docs/faas/GetFunction) to obtain the function ID.



**SessionStoreId ** <span data-label="purple">string </span>`Optional` `Sample value: ss-yefjbwgpa8c1kdto****`

Associated session resource ID.



**RequestModifierConfig.Path ** <span data-label="purple">string </span>`Optional` `Sample value: /hello`

The custom path for accessing the HTTP server. Specifies the request path to which the request modifier applies.



**Tags.N.Key ** <span data-label="purple">string[] </span><span data-api-tag="require|gvBdo2">必选</span> `Sample value: Tags.1.Key=k1`

The key of the tag associated with the resource.


* Parameter \- N: Indicates the serial number of the tag key. Valid range: 1–20.

* Separate multiple tag keys with ampersands (&).


Naming rules:


* It cannot start with` volc: `or `sys:` in any case form.

> Tag keys that start with `volc:` or `sys: `are reserved for the system. You cannot create tags starting with them.


* Only letters, digits, spaces, and the following symbols are allowed: "_", ".", ":", "/", "=", "+", "\-", and "@".

* It must be 1 to 128 characters in length.



**Tags.N.Type ** <span data-label="purple">string[] </span>`Optional` `Sample value: custom`

The type of the tag associated with the resource.


* system: system tag

* custom: user tag



**Tags.N.Value**<span data-label="purple"> string[] </span>`Optional` `Sample value: Tags.1.Value=v1`

The value of the tag associated with the resource.


* Parameter \- N: specifies the serial number of the tag value. Valid range: 1–20.

* Separate multiple tag values with &.


Naming rules:


* Only letters, digits, spaces, and the following symbols are allowed: "_", ".", ":", "/", "=", "+", "\-", and "@".

* It can be empty. Length limit: 0\-256 characters.



**ToolId ** <span data-label="purple">string </span>`Optional` `Sample value: t-dascxxxxx`

Associated tool ID.



**TosMountConfig.Credentials.AccessKeyId ** <span data-label="purple">string </span>`Optional` `Sample value: GY2OGJiOTdl****`

Enter the Access Key ID of the BytePlus platform.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>TosMountConfig.EnableTos</code> is set to true.</div>




**TosMountConfig.Credentials.SecretAccessKey ** <span data-label="purple">string </span>`Optional` `Sample value: emRoTnpVNU5HU****`

Enter the Secret Access Key ID of the BytePlus platform.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>TosMountConfig.EnableTos</code> is set to true.</div>




**TosMountConfig.EnableTos ** <span data-label="purple">boolean </span>`Optional` `Sample value: false`

Whether to enable TOS mounting. After mounting, the data generated in the corresponding directory of the runtime instance will be stored in the TOS service. Valid values:


* true: Enabled.

* false (default): Disabled.



**TosMountConfig.MountPoints.N.BucketName ** <span data-label="purple">string[] </span>`Optional` `Sample value: bucket01`

The TOS bucket name.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>TosMountConfig.EnableTos</code> is set to true.</div>




**TosMountConfig.MountPoints.N.BucketPath ** <span data-label="purple">string[] </span>`Optional` `Sample value: http://tos-ap-southeast-1.ivolces.com`

The TOS bucket path.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>TosMountConfig.EnableTos</code> is set to true.</div>




**TosMountConfig.MountPoints.N.Endpoint ** <span data-label="purple">string[] </span>`Optional` `Sample value: tmp/abc`

The TOS bucket subdirectory.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>TosMountConfig.EnableTos</code> is set to true.</div>




**TosMountConfig.MountPoints.N.LocalMountPath ** <span data-label="purple">string[] </span>`Optional` `Sample value: /home/app`

The local directory of the runtime instance to be mounted.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>TosMountConfig.EnableTos</code> is set to true.</div>




**TosMountConfig.MountPoints.N.ReadOnly ** <span data-label="purple">boolean[] </span>`Optional` `Sample value: false`

Specifies the access permissions for the local directory of the runtime instance to be mounted. Valid values:


* true: Read\-only permission.

* false (default): Read/write permissions.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>TosMountConfig.EnableTos</code> is set to true.</div>




**GatewayMode ** <span data-label="purple">string </span>`Optional` `Sample value: Shared`

The gateway mode. Valid values:


* Shared (default): Shared gateway.

* Exclusive: Dedicated gateway.



**GatewayInstanceId ** <span data-label="purple">string </span>`Optional` `Sample value: g-dab8me4bbg9nb6j6****`

The ID of the dedicated gateway instance.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is required when <code>GatewayMode</code> is set to "Exclusive".</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RuntimeId ** <span data-label="purple">string </span>`Sample value: r-ye7agye1a8cr38iu****`

ID of the runtime.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=CreateRuntime&Version=2025-10-30 HTTP/1.1
Content-Type: application/json
{
    "Name": "my-126663mx9****",
    "ArtifactType": "image",
    "ArtifactUrl": "agentkit-center-test-ap-southeast-1.cr.volces.com/agentkit/simple-app:1.0",
    "RoleName": "TestRoleForAgentKit",
    "AuthorizerConfiguration": {
        "KeyAuth": {
            "ApiKeyName": "xxi4256666623****",
            "ApiKeyLocation": "Header"
        }
    },
    "Envs": [
        {
            "Key": "MODEL_AGENT_API_KEY",
            "Value": "38484cc0-29ab-****-99b1-*****"
        },
        {
            "Key": "OBSERVABILITY_OPENTELEMETRY_APMPLUS_API_KEY",
            "Value": "78ed39eee6fa12824042a6b2359****"
        },
        {
            "Key": "OBSERVABILITY_OPENTELEMETRY_APMPLUS_ENDPOINT",
            "Value": "http://apmplus-ap-southeast-1.volces.com:4317"
        },
        {
            "Key": "OBSERVABILITY_OPENTELEMETRY_APMPLUS_SERVICE_NAME",
            "Value": "veadk_tracing"
        }
    ],
    "ApmplusEnable": true
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202106111445100102252431000052****",
    "Action": "CreateRuntime",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "RuntimeId": " r-3thhlu***"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidDescription.Malformed |The specified Description is malformed. |The format of the specified description is invalid. |
|400 |InvalidKey.Malformed |The specified Key is malformed. |The specified Key is invalid. |
|400 |InvalidName.Malformed |The specified Name is malformed. |The specified Name is invalid. |
|400 |InvalidParameter.ArtifactType |The specified ArtifactType is invalid. |The ArtifactType parameter is invalid. |
|400 |InvalidParameter.ArtifactUrl |The specified parameter ArtifactUrl is invalid. |The specified ArtifactUrl is invalid. |
|400 |InvalidParameter.ConflictingAuthorizerConfiguration |The AuthorizerConfiguration contains conflicting configurations. |The AuthorizerConfiguration parameter is invalid. |
|400 |InvalidParams.MaxConcurrency |MaxConcurrency should be in range [10, 1000] |The MaxConcurrency value is invalid. It must be in the range [10, 1000]. |
|400 |LimitExceeded.MaximumSubnetIds |The number of specified SubnetIds exceeds the maximum limit. |The specified SubnetIds exceeds the upper limit. |
|400 |LimitExceeded.MinimumSubnetIds |The number of specified SubnetIds exceeds the minimum limit. |The number of specified SubnetIds exceeds the lower limit. |
|400 |MissingParameter.ArtifactType |The required parameter ArtifactType is not supplied. |The parameter ArtifactType cannot be empty. |
|400 |MissingParameter.ArtifactUrl |The required parameter ArtifactUrl is not supplied. |The parameter ArtifactUrl cannot be empty. |
|400 |MissingParameter.AuthorizerConfiguration |The required parameter AuthorizerConfiguration is not supplied. |The parameter AuthorizerConfiguration cannot be empty. |
|400 |MissingParameter.DiscoveryUrl |The required parameter DiscoveryUrl is not supplied. |The parameter DiscoveryUrl cannot be empty. |
|400 |MissingParameter.EnableLog |The required parameter EnableLog is not supplied. |The EnableLog parameter cannot be empty. |
|400 |MissingParameter.Key |The required parameter Key is not supplied. |The parameter Key cannot be empty.  |
|400 |MissingParameter.Name |The required parameter Name is not supplied. |Name cannot be empty. |
|400 |MissingParameter.NetworkConfiguration |The required parameter NetworkConfiguration is not supplied. |The parameter NetworkConfiguration cannot be empty. |
|400 |MissingParameter.RoleName |The required parameter RoleName is not supplied. |The parameter RoleName cannot be empty. |
|400 |MissingParameter.VpcId |The required parameter VpcId is not supplied. |The parameter VpcId cannot be empty. |
|400 |QuotaExceeded.Runtime |You've reached the limit on the number of runtime that you can create, please submit ticket or sign\-on to the Console to request an increase in [runtime] quota. |The runtime quota has been exceeded. |
|403 |AccessDenied.Unauthorized |The specified action on the resource is denied. |The specified operation is rejected. The role permissions are insufficient. |
|409 |InvalidParameter.DuplicateName |The specified name already exists. |The name already exists. |

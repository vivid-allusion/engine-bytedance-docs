---
title: "UpdateRuntime - Modifies runtime configuration"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/UpdateRuntime_-_Modifies_runtime_configuration"
---

You can call this operation to modify runtime configuration.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|Lur3xe">必选</span> `Sample value: UpdateRuntime`

The action that you want to perform. Value: UpdateRuntime.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|V82KfD">必选</span> `Sample value: 2025-10-30`

The API version. Value: 2025\-10\-30.



**AgentSpaceId ** <span data-label="purple">string </span>`Optional` `Sample value: as-yeh6q4a48****`

The ID of the associated A2A agent space.



**ApmplusEnable**<span data-label="purple"> boolean</span>` Optional Sample value: true`

Whether to enable APMPlus and log services to provide observability for the runtime and write logs. Valid values:


* true: Enabled.

* false: Disabled.



**ArtifactType ** <span data-label="purple">string </span>`Optional` `Sample value: image`

Image type. Valid values:


* image: Custom image.

* public_image: Public image.



**ArtifactUrl ** <span data-label="purple">string </span>`Optional` `Sample value: cp-enterprise-ap-southeast-1.cr.volces.com/demo/agent:latest`

Image URL.


* The image URL in the `host/namespace/repo:tag` format.

* When the image type is set to public image, enter the image URL as `agentkit-prod-public-ap-southeast-1.cr.volces.com/template/financial:v1117_1`.



**CpuMilli ** <span data-label="purple">integer </span>`Optional` `Sample value: 2000`

The vCPU specification of the instance. Unit: milli cpu.

Valid range: 250\-16000.



**Description ** <span data-label="purple">string </span>`Optional` `Sample value: Agent-001`

Runtime description.


* The text length cannot exceed 1000 Unicode characters.



**Envs.N.Key ** <span data-label="purple">string[] </span><span data-api-tag="require|rnheeb">必选</span> `Sample value: DATABASE_MEM0_BASE_URL`

Key of the runtime environment variable.


* It can contain only letters, digits, and underscores, and must start with an underscore or letter. It must be 1 to 63 characters in length.

* Each Key must be unique under one runtime.



**Envs.N.Value ** <span data-label="purple">string[] </span>`Optional` `Sample value: mem0-cnlfjzigaku8gc****.mem0.volces.com:8000`

Value of the runtime environment variable.



**KnowledgeId ** <span data-label="purple">string </span>`Optional` `Sample value: kb-xxxx`

ID of the associated knowledge base.



**LlmshieldAppId ** <span data-label="purple">string </span>`Optional` `Sample value: app-d65v55avi7p8hpl3****`

Associated large model Guardrails asset ID.



**LlmshieldStatus ** <span data-label="purple">integer </span>`Optional` `Sample value: 1`

Whether the Guardrails service for the large model is enabled.


* 1: Enabled.

* 0: Not enabled.



**MCPToolsetId ** <span data-label="purple">string </span>`Optional` `Sample value: mt-3tigy72q3u3vj0x2****`

The ID of the associated MCP toolset.



**MaxConcurrency ** <span data-label="purple">integer </span>`Optional` `Sample value: 100`

The maximum number of concurrent requests for the instance. Valid range: 10\-1000.



**MaxInstance ** <span data-label="purple">integer </span>`Optional` `Sample value: 10`

The maximum number of instances. Valid range: 1\-10.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To increase the upper limit for the maximum number of instances, go to the <a href="https://console.byteplus.com/quota/productList/ParameterList?ProviderCode=agentkit">Quota Center</a> to apply for a higher runtime/instance quota limit.</div>




**MemoryId ** <span data-label="purple">string </span>`Optional` `Sample value: mem-xxxx`

ID of the associated memory.



**MemoryMb ** <span data-label="purple">integer </span>`Optional` `Sample value: 4096`

The memory specification of the instance. Unit: MiB. Valid range: 512\-131072.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Values must be specified in increments of 512, such as 512, 1024, 1536, and 2048.</div>




**MinInstance ** <span data-label="purple">integer </span>`Optional` `Sample value: 1`

The minimum number of instances. Valid range: 0\-MaxInstance.



**ModelAgentName ** <span data-label="purple">string </span>`Optional` `Sample value: doubao-seed-1.6`

The access point for the inference model.



**ReleaseEnable ** <span data-label="purple">boolean </span>`Optional` `Sample value: true`

Whether to publish immediately after the update. Valid values:


* true: Publish immediately.

* false: Do not publish immediately.



**RuntimeId ** <span data-label="purple">string </span><span data-api-tag="require|P3MsKH">必选</span> `Sample value: r-ye7agye1a8cr38iu****`

ID of the runtime.



**RequestModifierConfig.FunctionId ** <span data-label="purple">string </span>`Optional` `Sample value: wrwsk****`

veFaaS function ID. You can call [GetFunction](https://docs.byteplus.com/en/docs/faas/GetFunction) to obtain the function ID.



**SessionStoreId ** <span data-label="purple">string </span>`Optional` `Sample value: ss-yefjbwgpa8c1kdto****`

Associated session resource ID.



**RequestModifierConfig.Path ** <span data-label="purple">string </span>`Optional` `Sample value: /hello`

The custom path for accessing the HTTP server. Specifies the request path to which the request modifier applies.



**Tags.N.Key ** <span data-label="purple">string[] </span><span data-api-tag="require|qDlrnr">必选</span> `Sample value: Tags.1.Value=v1`

The tag key of the user tag to be added to the resource.


* Parameter \- N: Indicates the serial number of the tag key. Valid range: 1–20.

* Separate multiple tag keys with ampersands (&).


Naming rules:


* It cannot start with` volc: `or `sys:` in any case form.

> Tag keys that start with `volc:` or `sys: `are reserved for the system. You cannot create tags starting with them.


* Only letters, digits, spaces, and the following symbols are allowed: "_", ".", ":", "/", "=", "+", "\-", and "@".

* It must be 1 to 128 characters in length.



**Tags.N.Type ** <span data-label="purple">string[] </span>`Optional` `Sample value: custom`

Tag type.


* system: system tag

* custom: user tag



**Tags.N.Value**<span data-label="purple"> string[] </span>`Optional` `Sample value: Tags.1.Value=v1`

The tag value of the tag associated with the resource.


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

* false: Disabled.



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

* false: Read/write permissions.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>TosMountConfig.EnableTos</code> is set to true.</div>




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
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=UpdateRuntime&Version=2025-10-30 HTTP/1.1
Content-Type: application/json
{
    "RuntimeId": "r-ye6hflyl1c598vs****",
    "Description": "Agent-001"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202106111445100102252431000052****",
    "Action": "UpdateRuntime",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "Id": "r-ye6hflyl1c598vs****"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidDescription.Malformed |The specified Description is malformed. |The format of the specified description is invalid. |
|400 |InvalidKey.Malformed |The specified Key is malformed. |The specified Key is invalid. |
|400 |InvalidParams.MaxInstance |MaxInstance should be in range [MinInstance, runtime.quota] |The configured maximum instance count is invalid. |
|400 |InvalidParams.MinInstance |MinInstance should be in range [0, MaxInstance] |The configured minimum instance count is invalid. |
|400 |InvalidResourceStatus |The status of the specified resource does not support this request. |The current status of the resource does not support this operation. |
|400 |MissingParameter.DiscoveryUrl |The required parameter DiscoveryUrl is not supplied. |The parameter DiscoveryUrl cannot be empty. |
|400 |MissingParameter.Key |The required parameter Key is not supplied. |The parameter Key cannot be empty.  |
|400 |MissingParameter.RuntimeId |The required parameter RuntimeId is not supplied. |The parameter RuntimeId cannot be empty. |
|400 |InvalidParameter.MemoryId |The specified parameter MemoryId is invalid. |The MemoryId parameter is invalid. |
|400 |InvalidEnvKey.Malformed |The environment variable key must start with an underscore or a letter, contain only letters, digits, or underscores, and be at most 63 characters long. |The environment variable Key is invalid. |
|400 |InvalidParameter.ArtifactUrl |The specified parameter ArtifactUrl is invalid. |The ArtifactUrl parameter is invalid. |
|400 |InvalidParameter.KnowledgeIds |The specified parameter KnowledgeIds is invalid. |The KnowledgeIds parameter is invalid. |
|400 |InvalidParams.CpuMilli |CpuMilli should be in range [1000, 1250, 1500, 2000, 4000, 8000, 16000] |The value of the CpuMilli parameter must be one of the following: [1000, 1250, 1500, 2000, 4000, 8000, 16000]. |
|404 |InvalidAgentKitRuntime.NotFound |The specified AgentKitRuntime does not exist. |The resource does not exist. |

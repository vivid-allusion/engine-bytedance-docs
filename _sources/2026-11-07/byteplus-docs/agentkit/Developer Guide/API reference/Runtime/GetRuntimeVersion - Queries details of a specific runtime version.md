---
title: "GetRuntimeVersion - Queries details of a specific runtime version"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/GetRuntimeVersion_-_Queries_details_of_a_specific_runtime_version"
---

You can call this operation to query details of a specific runtime version.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|Mf95cV">必选</span> `Sample value: GetRuntimeVersion`

The action that you want to perform. Value: GetRuntimeVersion.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|EO4hOO">必选</span> `Sample value: 2025-10-30`

The API version. Value: 2025\-10\-30.



**RuntimeId ** <span data-label="purple">string </span><span data-api-tag="require|c64Jdr">必选</span> `Sample value: r-ye7agye1a8cr38iu****`

ID of the runtime.



**VersionNumber ** <span data-label="purple">integer </span>`Optional` `Sample value: 1`

Runtime version number. If not specified, the default value is 0, which indicates the latest version.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**ApmplusEnable ** <span data-label="purple">boolean </span>`Sample value: true`

Whether to enable APMPlus and log services to provide observability for the runtime and write logs. Including:


* true: Enabled.

* false: Disabled.



**ArtifactType ** <span data-label="purple">string </span>`Sample value: image`

Image type. Valid values:


* image: Custom image.

* public_image: Public image.



**ArtifactUrl ** <span data-label="purple">string </span>`Sample value: cp-enterprise-ap-southeast-1.cr.volces.com/demo/agent:latest`

URL of the runtime image.



**AuthorizerConfiguration ** <span data-label="purple">object </span>`Sample value: --`

The inbound identity authentication information. Currently, the API Key and OAuth JWT authentication configurations are supported.


**CustomJwtAuthorizer ** <span data-label="purple">object </span>`Sample value: --`

The OAuth JWT authentication configuration.


**AllowedClients ** <span data-label="purple">string[] </span>`Sample value: ["client1"]`

List of allowed clients. If it is left empty, all clients are allowed to access.



**DiscoveryUrl ** <span data-label="purple">string </span>`Sample value: https://example.com/.well-known/openid-configuration`

URL of token signature key. This URL is used to obtain OpenID Connect configuration or authorization server metadata to verify the token passed in. Currently, only signature key URLs from the BytePlus identity service are supported.




**KeyAuth ** <span data-label="purple">object </span>`Sample value: --`

API Key authentication configuration.


**ApiKey ** <span data-label="purple">string </span>`Sample value: 22243eefff**`

The value of the API Key.



**ApiKeyLocation ** <span data-label="purple">string </span>`Sample value: Header`

Location of the API Key. Valid values:


* Header, currently only Header is supported.



**ApiKeyName ** <span data-label="purple">string </span>`Sample value: test-key`

The name of the API Key.





**Command ** <span data-label="purple">string </span>`Sample value: ./run.sh`

Runtime startup command.



**CpuMilli ** <span data-label="purple">integer </span>`Sample value: 1000`

Maximum CPU per instance. Unit: milli cpu.



**CreatedAt ** <span data-label="purple">string </span>`Sample value: 2025-10-20T16:02:15+08:00`

Creation time of the version.



**Description ** <span data-label="purple">string </span>`Sample value: runtime01`

Runtime description.



**Endpoint ** <span data-label="purple">string </span>`Sample value: http://sd3qupshmeps3v7l9****.apigateway-ap-southeast-1.volceapi.com`

Domain name of the runtime.



**Envs ** <span data-label="purple">object[] </span>`Sample value: --`

Runtime environment variables.


**Key ** <span data-label="purple">string </span>`Sample value: test-key`

The Key of the environment variable.



**Value ** <span data-label="purple">string </span>`Sample value: test-value`

The Value of the environment variable.




**LinkedResources ** <span data-label="purple">object[] </span>`Sample value: --`

The list of associated component resources.


**Id ** <span data-label="purple">string </span>`Sample value: mem-yefiu7g5q8c1kdto****`

Resource ID.



**Name ** <span data-label="purple">string </span>`Sample value: viking_g6q3nnk`

The resource name.



**Type ** <span data-label="purple">string </span>`Sample value: Memory`

Resource type. Including:


* Knowledge: knowledge base.

* Memory: memory.

* MCPToolset: MCP toolset.

* BuiltInTool: tool.

* SessionStore: session resource.




**LlmshieldAppId ** <span data-label="purple">string </span>`Sample value: app-d65v55avi7p8hpl3****`

Associated large model Guardrails asset ID.



**LlmshieldStatus ** <span data-label="purple">integer </span>`Sample value: 1`

The status of the Guardrails service for the large model.


* 1: Enabled.

* 0: Not enabled.



**MaxConcurrency ** <span data-label="purple">integer </span>`Sample value: 5`

The maximum number of concurrent requests for the instance.



**MemoryMb ** <span data-label="purple">integer </span>`Sample value: 2048`

Maximum memory per instance, in MB.



**ModelAgentName ** <span data-label="purple">string </span>`Sample value: doubao-seed-1.6`

The access point for the inference model.



**Name ** <span data-label="purple">string </span>`Sample value: my-agent`

Runtime name.



**ProjectName ** <span data-label="purple">string </span>`Sample value: default`

The name of the project associated with the runtime.



**RoleName ** <span data-label="purple">string </span>`Sample value: MyTestRole`

Name of the IAM role associated with the runtime.



**RuntimeId ** <span data-label="purple">string </span>`Sample value: r-22ddsc***`

ID of the runtime.



**Status ** <span data-label="purple">string </span>`Sample value: Ready`

Runtime status. Valid values:


* Creating: Being created.

* Error: Error.

* Releasing: Being published.

* Ready: Running.

* Deleting: Being deleted.

* Deleted: Deleted.

* Updating: Being updated.

* UnReleased: Not published.



**Tags ** <span data-label="purple">object[] </span>`Sample value: --`

Runtime tags.


**Key ** <span data-label="purple">string </span>`Sample value: k1`

The tag key.



**Type ** <span data-label="purple">string </span>`Sample value: system`

Tag type.


* system: system tag

* custom: user tag



**Value ** <span data-label="purple">string </span>`Sample value: v1`

The tag value.




**TosMountConfig ** <span data-label="purple">object </span>`Sample value: --`

The TOS mounting configuration.


**Credentials ** <span data-label="purple">object </span>`Sample value: --`

The TOS credentials.


**AccessKeyId ** <span data-label="purple">string </span>`Sample value: GY2OGJiOTdl****`

The Access Key ID of the BytePlus platform.



**SecretAccessKey ** <span data-label="purple">string </span>`Sample value: emRoTnpVNU5HU****`

The Secret Access Key ID of the BytePlus platform.




**EnableTos ** <span data-label="purple">boolean </span>`Sample value: true`

Whether to enable TOS mounting. After mounting, the data generated in the corresponding directory of the runtime instance will be stored in the TOS service. Valid values:


* true: Enabled.

* false: Disabled.



**MountPoints ** <span data-label="purple">object[] </span>`Sample value: --`

The list of TOS mount points.


**BucketName ** <span data-label="purple">string </span>`Sample value: bucket01`

The TOS bucket name.



**BucketPath ** <span data-label="purple">string </span>`Sample value: http://tos-ap-southeast-1.ivolces.com`

The TOS bucket path.



**Endpoint ** <span data-label="purple">string </span>`Sample value: tmp/abc`

The TOS bucket subdirectory.



**LocalMountPath ** <span data-label="purple">string </span>`Sample value: /home/app`

The local directory of the runtime instance to be mounted.



**ReadOnly ** <span data-label="purple">boolean </span>`Sample value: false`

The access permission of the runtime instance to be mounted. Valid values:


* true: Read\-only permission.

* false: Read/write permissions.





**UpdatedAt ** <span data-label="purple">string </span>`Sample value: 2025-10-20T16:02:15+08:00`

Update time of the version.



**VersionNumber ** <span data-label="purple">integer </span>`Sample value: 1`

Runtime version number.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=GetRuntimeVersion&Version=2025-10-30 HTTP/1.1
Content-Type: application/json
{
    "RuntimeId": "r-ye6xzwchkwoaroxxxxxx",
    "versionNumber": "1"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202106111445100102252431000052****",
    "Action": "GetAgentKitRuntimeVersion",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "RuntimeId": "r-ye7******",
    "Name": "runtime******",
    "Description": "agentkit",
    "ArtifactType": "image",
    "ArtifactUrl": "agentkit******/******/******",
    "AuthorizerConfiguration": {
      "KeyAuth": {
        "ApiKey": "Dht******",
        "ApiKeyLocation": "Header",
        "ApiKeyName": "dsfy******"
      },
    },
    "Envs": [
      {
        "Key": "test",
        "Value": "test-value"
      }
    ],
    "RoleName": "TestRoleForAgentKit",
    "ApmplusEnable": true,
    "Command": "python3 my_agent.py",
    "Status": "Ready",
    "ProjectName": "default",
    "Endpoint": "http://sd3qupshmeps3v7l9****.apigateway-ap-southeast-1.volceapi.com",
    "CpuMilli": 1000,
    "MemoryMb": 2048,
    "VersionNumber": 1,
    "CreatedAt": "2025-10-23T20:35:07+08:00",
    "UpdatedAt": "2025-10-23T20:36:21+08:00",
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |MissingParameter.RuntimeId |The required parameter RuntimeId is not supplied. |The parameter RuntimeId cannot be empty. |
|404 |InvalidResource.NotFound |The specified resource does not exist. |The resource does not exist. |

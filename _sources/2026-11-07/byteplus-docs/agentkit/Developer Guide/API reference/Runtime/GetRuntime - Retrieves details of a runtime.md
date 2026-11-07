---
title: "GetRuntime - Retrieves details of a runtime"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/GetRuntime_-_Queries_runtime_details"
---

You can call this operation to query the details of a runtime.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|AgXiNP">必选</span> `Sample value: GetRuntime`

The action that you want to perform. Value: GetRuntime.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|Od6SUz">必选</span> `Sample value: 2025-10-30`

The API version. Value: 2025\-10\-30.



**RuntimeId ** <span data-label="purple">string </span><span data-api-tag="require|xYURri">必选</span> `Sample value: r-ye7agye1a8cr38iu****`

ID of the runtime.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**Endpoint ** <span data-label="purple">string </span>`Sample value: https://xxxxiqpabcr6dormd12.apigateway-ap-southeast-1.volceapi.com`

The domain name for accessing the agent.



**AgentSpaceId ** <span data-label="purple">string </span>`Sample value: as-yeh6q4a48****`

The ID of the associated A2A agent space.



**ApmplusEnable ** <span data-label="purple">boolean </span>`Sample value: true`

Whether to enable APMPlus and log services to provide observability for the runtime and write logs. Including:


* true: Enabled.

* false: Disabled.



**ArtifactType ** <span data-label="purple">string </span>`Sample value: image`

Image type. Valid values:


* image: Custom image.

* public_image: Public image.



**ArtifactUrl ** <span data-label="purple">string </span>`Sample value: cp-enterprise-ap-southeast-1.cr.volces.com/demo/agent:latest`

Image URL. Image address in the format <host/namespace/repo:tag\>.



**AuthorizerConfiguration ** <span data-label="purple">object </span>`Sample value: --`

The inbound identity authentication information. Currently, the API Key and OAuth JWT authentication configurations are supported.


**CustomJwtAuthorizer ** <span data-label="purple">object </span>`Sample value: --`

The OAuth JWT authentication configuration.


**AllowedClients ** <span data-label="purple">string[] </span>`Sample value: ["client1"]`

List of allowed clients. If it is left empty, all clients are allowed to access.



**DiscoveryUrl ** <span data-label="purple">string </span>`Sample value: https://example.com/.well-known/openid-configuration`

URL of token signature key. This URL is used to obtain OpenID Connect configuration or authorization server metadata to verify the token passed in.




**KeyAuth ** <span data-label="purple">object </span>`Sample value: --`

API Key authentication configuration.


**ApiKey ** <span data-label="purple">string </span>`Sample value: 22243eefff**`

The value of the API Key.



**ApiKeyLocation ** <span data-label="purple">string </span>`Sample value: Header`

The location where the API Key is passed. Currently, only Header is supported.



**ApiKeyName ** <span data-label="purple">string </span>`Sample value: test-key`

API Key name.





**Command ** <span data-label="purple">string </span>`Sample value: ./run.sh`

Runtime startup command.



**CpuMilli ** <span data-label="purple">integer </span>`Sample value: 1000`

Maximum CPU per instance. Unit: milli cpu.



**CreatedAt ** <span data-label="purple">string </span>`Sample value: 2025-10-20T16:02:15+08:00`

Creation time of the runtime.



**CurrentVersionNumber ** <span data-label="purple">integer </span>`Sample value: 1`

Number of the current effective version.



**Description ** <span data-label="purple">string </span>`Sample value: runtime01`

Runtime description.



**Envs ** <span data-label="purple">object[] </span>`Sample value: --`

Runtime environment variables.


**Key ** <span data-label="purple">string </span>`Sample value: test-key`

The Key of the environment variable.



**Value ** <span data-label="purple">string </span>`Sample value: test-value`

The Value of the environment variable.




**FailedLogFileUrl ** <span data-label="purple">string </span>`Sample value: https://xx.tos-s3-cn.volces.com/release_failed_instance_logs/******`

The address for downloading the log file for a runtime deployment failure.



**KnowledgeId ** <span data-label="purple">string </span>`Sample value: kb-ye9g****`

ID of the associated knowledge base.



**MCPToolsetId ** <span data-label="purple">string </span>`Sample value: mt-3tigy72q3qddxxxx`

ID of the associated MCP toolset.



**MaxConcurrency ** <span data-label="purple">integer </span>`Sample value: 100`

The maximum number of concurrent requests for the instance.



**MaxInstance ** <span data-label="purple">integer </span>`Sample value: 10`

The maximum number of instances.



**MemoryId ** <span data-label="purple">string </span>`Sample value: mem-1763997****`

ID of the associated memory.



**MemoryMb ** <span data-label="purple">integer </span>`Sample value: 2048`

Maximum memory per instance, in MB.



**MinInstance ** <span data-label="purple">integer </span>`Sample value: 1`

The minimum number of instances.



**ModelAgentName ** <span data-label="purple">string </span>`Sample value: doubao-seed-1.6`

The access point for the inference model.



**Name ** <span data-label="purple">string </span>`Sample value: my-agent`

Runtime name.



**NetworkConfigurations ** <span data-label="purple">object[] </span>`Sample value: --`

Access information for the runtime, including public network and VPC.


**Endpoint ** <span data-label="purple">string </span>`Sample value: https://sd3p0u******.apigateway-ap-southeast-1.volceapi.com`

Domain name of the runtime.



**NetworkType ** <span data-label="purple">string </span>`Sample value: public`

Access type. Value:


* public: Access using public network

* private: Access using private network



**VpcConfiguration ** <span data-label="purple">object </span>`Sample value: --`

VPC configuration.


**EnableSharedInternetAccess ** <span data-label="purple">boolean </span>`Sample value: true`

The public network egress configuration. Valid values:


* true: Enabled. This value indicates that the runtime uses the public network egress provided by the platform to access the public network.

* false: Not enabled. This value indicates that the runtime uses the public network NAT gateway egress configured in the private network to access the public network.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is returned only when network access is set to Private network.</div>




**SecurityGroupIds ** <span data-label="purple">string[] </span>`Sample value: ["sg-w08tvkc3e****"]`

List of security group IDs.



**SubnetIds ** <span data-label="purple">string[] </span>`Sample value: ["subnet-1234567890"]`

List of subnet IDs.



**VpcId ** <span data-label="purple">string </span>`Sample value: vpc-257gqcdfvx6n****`

VPC ID.





**ProjectName ** <span data-label="purple">string </span>`Sample value: default`

The name of the project associated with the runtime.



**RequestModifierConfig ** <span data-label="purple">object </span>`Sample value: --`

The request rewrite configuration.


**FunctionId ** <span data-label="purple">string </span>`Sample value: wrwsk****`

veFaaS function ID. You can call [GetFunction](https://docs.byteplus.com/en/docs/faas/GetFunction) to obtain the function ID.



**Path ** <span data-label="purple">string </span>`Sample value: /hello`

The path for accessing the HTTP server. Specifies the request path to which the request modifier applies.




**RoleName ** <span data-label="purple">string </span>`Sample value: MyTestRole`

Name of the IAM role associated with the runtime.



**RuntimeId ** <span data-label="purple">string </span>`Sample value: r-22ddsc***`

ID of the runtime.



**SessionStoreId ** <span data-label="purple">string </span>`Sample value: ss-yefjbwgpa8c1kdto****`

Associated session resource ID.



**Status ** <span data-label="purple">string </span>`Sample value: Ready`

Runtime status. Value:


* Creating: Being created.

* Error: Error.

* Releasing: Being published.

* Ready: Running.

* Deleting: Being deleted.

* Deleted: Deleted.

* Updating: Being updated.

* UnReleased: Not published.



**StatusMessage ** <span data-label="purple">string </span>`Sample value: release finished successfully`

Detailed information of the current status, as a supplement to the release status. For example, the cause of a startup failure.



**Tags ** <span data-label="purple">object[] </span>`Sample value: --`

Runtime tags.


**Key ** <span data-label="purple">string </span>`Sample value: k1`

The tag key.



**Type ** <span data-label="purple">string </span>`Sample value: custom`

Tag type.


* system: system tag

* custom: user tag



**Value ** <span data-label="purple">string </span>`Sample value: v1`

The tag value.




**ToolId ** <span data-label="purple">string </span>`Sample value: t-dasc*****`

Associated tool ID.



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

Update time of the runtime.



**GatewayMode ** <span data-label="purple">string </span>`Sample value: Shared`

The gateway mode. Valid values:


* Shared: Shared gateway.

* Exclusive: Dedicated gateway.



**GatewayInstanceId ** <span data-label="purple">string </span>`Sample value: g-dab8me4bbg9nb6j6****`

The ID of the dedicated gateway instance.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is returned only when <code>GatewayMode</code> is set to "Exclusive".</div>




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=GetRuntime&Version=2025-10-30 HTTP/1.1
Content-Type: application/json
{
    "RuntimeId": "r-ye6xzwchkwoaroxxxxxx"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202106111445100102252431000052****",
    "Action": "GetRuntime",
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
      "CustomJwtAuthorizer": null
    },
    "Envs": [
      {
        "Key": "test-key",
        "Value": "test-value"
      }
    ],
    "Tags": [],
    "RoleName": "TestRoleForAgentKit",
    "ApmplusEnable": true,
    "Command": "python3 my_agent.py",
    "Status": "Ready",
    "ProjectName": "default",
    "Endpoint": "http://sd3qupshmeps3v7l9****.apigateway-ap-southeast-1.volceapi.com",
    "CpuMilli": 1000,
    "MemoryMb": 2048,
    "CurrentVersionNumber": 1,
    "CreatedAt": "2025-10-23T20:35:07+08:00",
    "UpdatedAt": "2025-10-23T20:36:21+08:00",
    "StatusMessage": ""
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |MissingParameter.RuntimeId |The required parameter RuntimeId is not supplied. |The parameter RuntimeId cannot be empty. |
|404 |InvalidAgentKitRuntime.NotFound |The specified AgentKitRuntime does not exist. |The resource does not exist. |

---
title: "ListRuntimes - Batch queries runtime details"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/ListRuntimes_-_Batch_queries_runtime_details"
---

You can query details of multiple runtimes using custom filter conditions.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|0limRQ">必选</span> `Sample value: ListRuntimes`

The action that you want to perform. Value: ListRuntimes.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|gv5Y4s">必选</span> `Sample value: 2025-10-30`

The API version. Value: 2025\-10\-30.



**CreateTimeAfter ** <span data-label="purple">string </span>`Optional Sample value: 2006-01-02T15:04:05Z07:00`

Filter runtimes created after this time point. (RFC3339 format)



**CreateTimeBefore ** <span data-label="purple">string </span>`Optional Sample value: 2006-01-02T15:04:05Z07:00`

Filter runtimes created before this time point. (RFC3339 format)



**Filters.N.Name ** <span data-label="purple">string[] </span>`Optional Sample value: Name`

Field name used for exact filtering. Value: 


* Parameter \- N: Indicates the serial number of the filter condition. Value range: 1–10.

* Separate multiple field names with ampersands (&), representing an "Or" relationship.

* Valid values:

   * Id: ID of the runtime.

   * Name: Runtime name.

   * Description: Runtime description.

   * Status: Runtime status.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When <code>Filters.N.Name</code> and <code>Filters.N.NameContains</code> are both passed in, only <code>Filters.N.Name</code> takes effect.</div>




**Filters.N.NameContains ** <span data-label="purple">string[] </span>`Optional` `Sample value: Name`

Field name used for fuzzy filtering. Values: 


* Parameter \- N: Indicates the serial number of the filter condition. Value range: 1–10.

* Separate multiple field names with ampersands (&), representing an "Or" relationship.

* Valid values:

   * Id: ID of the runtime.

   * Name: Runtime name.

   * Description: Runtime description.

   * Status: Runtime status.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When <code>Filters.N.Name</code> and <code>Filters.N.NameContains</code> are both passed in, only <code>Filters.N.Name</code> takes effect.</div>




**Filters.N.Values.N ** <span data-label="purple">string[]</span>` Optional Sample value: Ready`

Value of the filter field.


* Parameter \- N: Indicates the serial number of the filter condition. Value range: 1–10.

* Separate multiple field names with ampersands (&).


When the filter field is Status, the values are:


* Creating: Being created.

* Error: Unavailable.

* Releasing: Being published.

* Ready: Running.

* Deleting: Being deleted.

* Deleted: Deleted.

* Updating: Being updated.

* UnReleased: Not published.



**MaxResults ** <span data-label="purple">integer </span>`Optional Sample value: 10`

The number of entries returned on each page in a pagination query.


* Minimum value: 1.

* Maximum value: 100. 

* Default value: 10.



**NextToken ** <span data-label="purple">string </span>`Optional` `Sample value: dC15ZTdjZ2xlM3VvYzFrZHRvcn***`

Pagination token marking the query position. Omit this parameter for initial API requests. In the next query, set the `NextToken` parameter to the value returned by the previous API call.



**ProjectName ** <span data-label="purple">string </span>`Optional` `Sample value: default`

The name of the associated project.



**TagFilters.N.Key ** <span data-label="purple">string[] </span>`Optional` `Sample value: TagFilters.1.Key=k1`

Tag key specified when querying resources by tag. Each tag key must be unique.


* Parameter \- N: specifies the serial number of the tag key. Value range: 1–10.

* Separate multiple tag keys with ampersands (&).



**TagFilters.N.Values.N ** <span data-label="purple">string[] </span>`Optional` `Sample value: TagFilters.1.Values.1=v1&TagFilters.1.Values.2=v2`

The tag value specified when resources are queried based on tags.


* The first N: specifies the serial number of the tag key. Valid range: 1–10.

* The second N: specifies the serial number of the tag value. Valid range: 1\-3. That is, you can query up to three tag values of the same tag key.

* Separate multiple tag values with &.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">To pass in this parameter, pass in TagFilters.N.Key first.</div>


* <div data-tips="true" data-tips-type="tip">If you do not pass in this parameter, all tag values under the same tag key are queried.</div>


* <div data-tips="true" data-tips-type="tip">If you specify an empty string, you query tags with an empty tag value.</div>




**UpdateTimeAfter ** <span data-label="purple">string </span>`Optional Sample value: 2006-01-02T15:04:05Z07:00`

Filter runtimes updated after this time point. (RFC3339 format)



**UpdateTimeBefore ** <span data-label="purple">string</span>` Optional Sample value: 2006-01-02T15:04:05Z07:00`

Filter runtimes updated before this time point. (RFC3339 format)



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**AgentKitRuntimes ** <span data-label="purple">object[] </span>`Sample value: --`

Details of the runtimes that meet the conditions.


**RequestModifierConfig ** <span data-label="purple">object </span>`Sample value: --`

The request rewrite configuration.


**FunctionId ** <span data-label="purple">string </span>`Sample value: fn-2abcxxxx`

veFaaS function ID. You can call [GetFunction](https://docs.byteplus.com/en/docs/faas/GetFunction) to obtain the function ID.



**Path ** <span data-label="purple">string </span>`Sample value: /hello`

The custom path for accessing the HTTP server. Used to specify the effect of the request modifier.




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





**AgentSpaceId ** <span data-label="purple">string </span>`Sample value: as-yeh6q4a48****`

The ID of the associated A2A agent space.



**ApmplusEnable ** <span data-label="purple">boolean </span>`Sample value: true`

Whether to enable APMPlus and log services to provide observability for the runtime and write logs. Including:


* true: Enabled.

* false: Disabled.



**ArtifactType ** <span data-label="purple">string </span>`Sample value: image`

Runtime image type. Valid values:


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

The location where the API Key is passed. Valid values:


* Header: Currently, only Header is supported.



**ApiKeyName ** <span data-label="purple">string </span>`Sample value: test-key`

API Key name.





**Command ** <span data-label="purple">string </span>`Sample value: ./run.sh`

Runtime startup command.



**CpuMilli ** <span data-label="purple">integer </span>`Sample value: 1000`

Maximum CPU per instance. Unit: milli cpu.



**CreatedAt ** <span data-label="purple">string </span>`Sample value: 2025-10-20T16:02:15+08:00`

Creation time of the runtime version.



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




**KnowledgeId ** <span data-label="purple">string </span>`Sample value: kb-ye9g****`

ID of the associated knowledge base.



**MCPToolsetId ** <span data-label="purple">string </span>`Sample value: mt-3tigy72q3u3vj0x2****`

ID of the associated MCP toolset.



**MemoryId ** <span data-label="purple">string </span>`Sample value: mem-1763997****`

ID of the associated memory.



**MemoryMb ** <span data-label="purple">integer </span>`Sample value: 2048`

Maximum memory per instance, in MB.



**Name ** <span data-label="purple">string </span>`Sample value: my-agent`

Runtime name.



**NetworkConfigurations ** <span data-label="purple">object[] </span>`Sample value: --`

The network access information of the runtime.


**Endpoint ** <span data-label="purple">string </span>`Sample value: http://sd3qupshmeps3v7l9****.apigateway-ap-southeast-1.volceapi.com`

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



**RoleName ** <span data-label="purple">string </span>`Sample value: MyTestRole`

Name of the IAM role associated with the runtime.



**RuntimeId ** <span data-label="purple">string </span>`Sample value: r-daf******`

ID of the runtime.



**SessionStoreId ** <span data-label="purple">string </span>`Sample value: ss-yefjbwgpa8c1kdto****`

Associated session resource ID.



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



**Type ** <span data-label="purple">string </span>`Sample value: custom`

Tag type.


* system: system tag

* custom: user tag



**Value ** <span data-label="purple">string </span>`Sample value: v1`

The tag value.




**ToolId ** <span data-label="purple">string </span>`Sample value: t-dascxxxxx`

ID of the tool associated with the runtime.



**UpdatedAt ** <span data-label="purple">string </span>`Sample value: 2025-10-20T16:02:15+08:00`

Update time of the runtime version.



**GatewayMode ** <span data-label="purple">string </span>`Sample value: Shared`

The gateway mode. Valid values:


* Shared: Shared gateway.

* Exclusive: Dedicated gateway.



**GatewayInstanceId ** <span data-label="purple">string </span>`Sample value: g-dab8me4bbg9nb6j6****`

The ID of the dedicated gateway instance.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is returned only when <code>GatewayMode</code> is set to "Exclusive".</div>





**NextToken ** <span data-label="purple">string </span>`Sample value: bHpwdXJja2RxemU1eG5sb3NzdGcW1-RCEq****`

The pagination token returned by this call. If this value is empty, the current page is the last page.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=ListRuntimes&Version=2025-10-30 HTTP/1.1
Content-Type: application/json
{
    "Filters": [
        {
            "Name": "Name",
            "Values": [
                ""
            ]
        }
    ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20251027221557619118028A455F3C0C79",
    "Action": "ListRuntimes",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "AgentKitRuntimes": [
      {
        "RuntimeId": "r-ye7t******",
        "Name": "agent1******",
        "Description": "",
        "Status": "Error",
        "CreateTime": "2025-10-27T21:19:19+08:00",
        "UpdateTime": "2025-10-27T21:20:52+08:00",
        "ArtifactType": "",
        "ArtifactUrl": "",
        "AuthorizerConfiguration": null,
        "Envs": [],
        "Tags": [],
        "RoleName": "",
        "ApmplusEnable": false,
        "Command": "",
        "Endpoint": "",
        "CpuMilli": 0,
        "MemoryMb": 0,
        "CurrentVersionNumber": 1,
        "CreatedAt": "2025-10-27T21:19:19+08:00",
        "UpdatedAt": "2025-10-27T21:20:52+08:00"
      },
      {
        "RuntimeId": "r-ye******",
        "Name": "simple******",
        "Description": "AgentKit",
        "Status": "Ready",
        "CreateTime": "2025-10-27T17:09:37+08:00",
        "UpdateTime": "2025-10-27T17:10:52+08:00",
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
        "Envs": [],
        "RoleName": "test-xxx",
        "ApmplusEnable": false,
        "Command": "run.sh",
        "Endpoint": "http://sd3qupshmeps3v7l9****.apigateway-ap-southeast-1.volceapi.com",
        "CpuMilli": 1000,
        "MemoryMb": 2048,
        "CurrentVersionNumber": 1,
        "CreatedAt": "2025-10-27T17:09:37+08:00",
        "UpdatedAt": "2025-10-27T17:10:52+08:00"
      }
    ]
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

To learn more about error codes, see [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).

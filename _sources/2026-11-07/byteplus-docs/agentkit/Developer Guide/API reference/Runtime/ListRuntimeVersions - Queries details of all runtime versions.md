---
title: "ListRuntimeVersions - Queries details of all runtime versions"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/ListRuntimeVersions_-_Queries_details_of_all_runtime_versions"
---

You can call this operation to query details of all runtime versions.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|wMAv0Q">必选</span> `Sample value: ListRuntimeVersions`

The action that you want to perform. Value: ListRuntimeVersions.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|Q8CUTq">必选</span> `Sample value: 2025-10-30`

The API version. Value: 2025\-10\-30.



**MaxResults ** <span data-label="purple">integer </span>`Optional Sample value: 10`

The number of entries returned on each page in a pagination query.


* Minimum value: 1.

* Maximum value: 100. 

* Default value: 10.



**NextToken ** <span data-label="purple">string </span>`Optional` `Sample value: 3da3332e**`

Pagination token marking the query position. Omit this parameter for initial API requests. In the next query, set the `NextToken` parameter to the value returned by the previous API call.



**RuntimeId ** <span data-label="purple">string </span><span data-api-tag="require|AmZaQp">必选</span> `Sample value: r-ye7agye1a8cr38iu****`

ID of the runtime.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**AgentKitRuntimeVersions ** <span data-label="purple">object[] </span>`Sample value: --`

Details of all runtime versions.


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

The OAuth JWT authentication method.


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

The name of the API Key.





**Command ** <span data-label="purple">string </span>`Sample value: ./run.sh`

Runtime startup command.



**CpuMilli ** <span data-label="purple">integer </span>`Sample value: 1000`

Maximum CPU per instance. Unit: milli cpu.



**CreatedAt ** <span data-label="purple">string </span>`Sample value: 2025-10-20T16:02:15+08:00`

Creation time of the runtime version.



**Description ** <span data-label="purple">string </span>`Sample value: runtime01`

Runtime description.



**Envs ** <span data-label="purple">object[] </span>`Sample value: --`

Runtime environment variables.


**Key ** <span data-label="purple">string </span>`Sample value: test-key`

The Key of the environment variable.



**Value ** <span data-label="purple">string </span>`Sample value: test-value`

The Value of the environment variable.




**MemoryMb ** <span data-label="purple">integer </span>`Sample value: 2048`

Maximum memory per instance, in MB.



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



**UpdatedAt ** <span data-label="purple">string </span>`Sample value: 2025-10-20T16:02:15+08:00`

Update time of the runtime version.



**VersionNumber ** <span data-label="purple">integer </span>`Sample value: 1`

The version number.




**NextToken ** <span data-label="purple">string </span>`Sample value: bHpwdXJja2RxemU1eG5sb3NzdGcW1-RCEq****`

The pagination token returned by this call. If this value is empty, the current page is the last page.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=ListRuntimeVersions&Version=2025-10-30 HTTP/1.1
Content-Type: application/json
{
    "RuntimeId": "r-ye6xzwchkwoaroxxxxxx",
    "MaxResults": "10",
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202510272157150B50CD9A1448B0289A80",
    "Action": "ListRuntimeVersions",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "AgentKitRuntimeVersions": [
      {
        "RuntimeId": "rv-ye7******",
        "Description": "AgentKit project",
        "VersionNumber": 1,
        "CreatedAt": "2025-10-27T17:04:53+08:00",
        "UpdatedAt": "2025-10-27T17:05:20+08:00",
        "ArtifactType": "image",
        "ArtifactUrl": "agentkit-cli-******",
        "AuthorizerConfiguration": {
          "KeyAuth": {
            "ApiKey": "dsdsds******",
            "ApiKeyLocation": "Header",
            "ApiKeyName": "API-KEY-******"
          },
        },
        "Envs": [
          {
            "Key": "MODEL_AGENT_API_KEY",
            "Value": "38484******"
          }
        ],
        "Command": "",
        "RoleName": "AgentKit-Runtime******",
        "Status": "Ready",
        "CpuMilli": 1000,
        "MemoryMb": 2048,
        "ApmplusEnable": true
      },
      {
        "RuntimeId": "rv-ye7s******",
        "Description": "AgentKit project",
        "VersionNumber": 0,
        "CreatedAt": "2025-10-27T17:04:04+08:00",
        "UpdatedAt": "2025-10-27T17:04:04+08:00",
        "ArtifactType": "image",
        "ArtifactUrl": "agentkit-******",
        "AuthorizerConfiguration": {
          "KeyAuth": {
            "ApiKey": "dsdd******",
            "ApiKeyLocation": "Header",
            "ApiKeyName": "API-KEY-******"
          },
        },
        "Envs": [
          {
            "Key": "MODEL_AGENT_API_KEY",
            "Value": "38484******"
          }
        ],
        "Command": "",
        "RoleName": "AgentKit******",
        "Status": "Creating",
        "CpuMilli": 0,
        "MemoryMb": 0,
        "ApmplusEnable": true,
      }
    ],
    "NextToken": "dC15ZTdjZ2xlM3VvYzFrZHRvcn****",
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |MissingParameter.RuntimeId |The required parameter RuntimeId is not supplied. |The parameter RuntimeId cannot be empty. |
|404 |InvalidAgentKitRuntime.NotFound |The specified AgentKitRuntime does not exist. |The specified runtime does not exist. |

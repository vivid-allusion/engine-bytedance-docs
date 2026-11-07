---
title: "CreateSession - Creates tool session instance"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/CreateSession_-_Creates_tool_session_instance"
---

You can call this operation to create a session instance for a tool.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|UUTDB9">必选</span> `Sample value: CreateSession`

The action that you want to perform. Value: CreateSession.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|PZzvBl">必选</span> `Sample value: 2025-10-30`

The API version. Value: 2025\-10\-30.



**ToolId ** <span data-label="purple">string </span><span data-api-tag="require|CKbsiA">必选</span> `Sample value: t-3tigy72q3u3vj0x2****`

Tool ID.



**Envs.N.Key ** <span data-label="purple">string[] </span><span data-api-tag="require|Zskrjv">必选</span> `Sample value: LOG_LEVEL`

The Key of the environment variable.


* It can only contain letters, numbers, and underscores, and must start with an underscore or a letter.

* It can be 1 to 63 characters in length.



**Ttl**<span data-label="purple"> integer </span>`Optional Sample value: 1800`

TTL of the session instance, that is, the period during which the tool preserves the user state and operation context within a single user\-tool interactive session. After the session expires, log in again or restart the operation.


* Unit: seconds.

* Value range: 60–86400.

* Default value: 1800.



**TosMountPoints.N.BucketName ** <span data-label="purple">string[] </span>`Optional` `Sample value: bucket01`

The TOS bucket name.



**Envs.N.Value ** <span data-label="purple">string[] </span>`Optional` `Sample value: info`

The value of the environment variable. It can contain up to 8192 characters.



**TtlUnit ** <span data-label="purple">string </span>`Optional Sample value: second`

The unit for TTL. Value:


* minute: minute.

* second (default): second.



**TosMountPoints.N.BucketPath ** <span data-label="purple">string[] </span>`Optional` `Sample value: http://tos-ap-southeast-1.ivolces.com`

The TOS bucket path.



**ImageInfo.Command ** <span data-label="purple">string </span><span data-api-tag="require|iTekwh">必选</span> `Sample value: python app.py`

The command to be executed at startup.



**UserSessionId ** <span data-label="purple">string</span>` Optional Sample value: session01`

User session information.


* Can contain uppercase and lowercase English letters, numbers, hyphens (\-), and underscores (_).

* Length limit: 0–200 characters.



**TosMountPoints.N.LocalMountPath ** <span data-label="purple">string[] </span>`Optional` `Sample value: /home/app`

The local directory of the tool instance to be mounted.



**ImageInfo.Image ** <span data-label="purple">string </span><span data-api-tag="require|5PzLCw">必选</span> `Sample value: registry.example.com/my-app:v1.0.0`

The complete URL of the image, including the version number of the image.



**ImageInfo.Port ** <span data-label="purple">integer </span><span data-api-tag="require|m4oVYN">必选</span> `Sample value: 8080`

The port number (integer) exposed externally by the image.



**Metadata.N.Key ** <span data-label="purple">string[] </span><span data-api-tag="require|Px39ft">必选</span> `Sample value: env`

The tag key of the metadata, such as env, version, and other custom identifiers.


* Parameter \- N: Indicates the sequence number of the tag key. Value range: 1–10.

* The maximum length of a single key is 128 characters.

* Separate multiple field names with ampersands (&). Duplicate field names are not allowed.



**Metadata.N.Type ** <span data-label="purple">string[] </span>`Optional` `Sample value: String`

The tag type of the metadata, used to declare the data type of the tag value, such as String and Int.


* Parameter \- N: Indicates the sequence number of the tag type. Value range: 1–10.

* Separate multiple field names with ampersands (&).



**Metadata.N.Value ** <span data-label="purple">string[] </span>`Optional` `Sample value: production`

The tag value of the metadata.


* Parameter \- N: Indicates the sequence number of the tag value. Value range: 1–10.

* The maximum length of a single value is 256 characters. Separate multiple field names with ampersands (&).



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**Endpoint ** <span data-label="purple">string </span>`Sample value: https://sd391h67itqkq7brr****.apigateway-ap-southeast-1.volceapi.com`

The public endpoint for accessing the session.



**InternalEndpoint ** <span data-label="purple">string </span>`Sample value: https://sd391h67itqkq7brr****.apigateway-ap-southeast-1-inner.volceapi.com`

The private endpoint for accessing the session.



**SessionId ** <span data-label="purple">string </span>`Sample value: s-3tigy72q3u3vj0x2****`

Session ID.



**UserSessionId ** <span data-label="purple">string </span>`Sample value: session1`

Session information.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=CreateSession&Version=2025-10-30 HTTP/1.1
Content-Type: application/json
{
    "ToolId": "t-ye6xzwchkwoaroxxxxxx",
    "Ttl": 1440
}

```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20251027144356FBC64212879D5D3A****",
    "Action": "CreateSession",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "SessionId": "s-ye7sfdm2o0c1kdto****",
    "UserSessionId": "",
    "Endpoint": "http://sd3s4ng567ui2e1ad****.apigateway-ap-southeast-1.volceapi.com/?faasInstanceName=vefaas-bf5xfrv4-qa6b0ee7db-d3vh9b033fo44gohgrj0-sandbox",
    "InternalEndpoint": ""
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidKey.Malformed |The specified Key is malformed. |The specified key is invalid. |
|400 |InvalidUserSessionId.Malformed |The specified UserSessionId is malformed. |The specified UserSessionId is invalid. |
|400 |MissingParameter.Command |The required parameter Command is not supplied. |The parameter Command cannot be empty. |
|400 |MissingParameter.Image |The required parameter Image is not supplied. |The Image parameter cannot be empty. |
|400 |MissingParameter.Key |The required parameter Key is not supplied. |The parameter Key cannot be empty.  |
|400 |MissingParameter.Port |The required parameter Port is not supplied. |The parameter Port cannot be empty. |
|400 |MissingParameter.ToolId |The required parameter ToolId is not supplied. |The parameter ToolId cannot be empty. |
|400 |InvalidParameter.DuplicateUserSessionId |The specified user_session_id already exists. |The session information already exists. |
|400 |InvalidParameter.Ttl |The specified parameter Ttl is invalid. |The specified Ttl parameter is invalid. |
|400 |InvalidResourceStatus |The status of the specified resource does not support this request. |The current status of the resource does not support this operation. |
|400 |ErrCreateSessionFail |Session start fail, please check console log. |Failed to create a session. Check the console logs for troubleshooting. |
|400 |QuotaExceeded.ToolSessions |You've reached the limit on the session number of tool that you can create, please submit ticket or sign\-on to the Console to request an increase in [tool/sessions] quota. |The tool quota has been exceeded. Go to the Quota Center to apply for a tool or session quota increase. |
|404 |InvalidResource.NotFound |The specified resource does not exist. |The resource does not exist. |

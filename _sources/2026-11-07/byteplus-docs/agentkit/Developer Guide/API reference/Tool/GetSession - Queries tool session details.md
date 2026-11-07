---
title: "GetSession - Queries tool session details"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/GetSession_-_Queries_tool_session_details"
---

You can call this operation to query tool session details.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|wUPavB">必选</span> `Sample value: GetSession`

The action that you want to perform. Value: GetSession.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|3JK5yw">必选</span> `Sample value: 2025-10-30`

The API version. Value: 2025\-10\-30.



**SessionId ** <span data-label="purple">string </span><span data-api-tag="require|BiCbOt">必选</span> `Sample value: s-3tigy72q3u3vj0x2****`

Session ID.



**ToolId ** <span data-label="purple">string </span><span data-api-tag="require|l1MVjJ">必选</span> `Sample value: t-3tigy72q3u3vj0x2****`

Tool ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**Metadata ** <span data-label="purple">object[] </span>`Sample value: --`

The session label metadata.


**Key ** <span data-label="purple">string </span>`Sample value: env`

The tag key of the metadata.



**Type ** <span data-label="purple">string </span>`Sample value: String`

The tag type of the metadata, used to declare the data type of the tag value.



**Value ** <span data-label="purple">string </span>`Sample value: production`

The tag value of the metadata.




**CreatedAt ** <span data-label="purple">string </span>`Sample value: 2006-01-02T15:04:05Z07:00`

Creation time of the session.



**Endpoint ** <span data-label="purple">string </span>`Sample value: https://sd391h67itqkq7brr****.apigateway-ap-southeast-1.volceapi.com`

The public endpoint for accessing the session.



**ExpireAt ** <span data-label="purple">string </span>`Sample value: 2006-01-02T15:04:05Z07:00`

Expiration time of the session.



**InternalEndpoint ** <span data-label="purple">string </span>`Sample value: https://sd391h67itqkq7brr****.apigateway-ap-southeast-1-inner.volceapi.com`

The private endpoint for accessing the session.



**Name ** <span data-label="purple">string </span>`Sample value: session-test`

Session name.



**SessionId ** <span data-label="purple">string </span>`Sample value: s-3tigy72q3u3vj0x2****`

Session ID.



**SessionMeta ** <span data-label="purple">object </span>`Sample value: --`

Session metadata.


**VncUrl ** <span data-label="purple">string </span>`Sample value: http://sd3s4ng567ui2e1ad****.apigateway-ap-southeast-1.volceapi.com/terminal?faasInstanceName=vefaas-bf5xfrv4-qa6b0ee7db-d3vh9b033fo44goh****-sandbox`

The access URL of the session VNC.



**WebshellUrl ** <span data-label="purple">string </span>`Sample value: http://sd3s4ng567ui2e1ad****.apigateway-ap-southeast-1.volceapi.com/vnc/index.html?faasInstanceName=vefaas-bf5xfrv4-qa6b0ee7db-d3vh9b033fo44goh****-sandbox`

Webshell link of the session.




**Status ** <span data-label="purple">string </span>`Sample value: Ready`

Session status. Values:


* Starting: Starting.

* Ready: Running.

* Failed: Failed to start.

* Terminating: Terminating.



**ToolType ** <span data-label="purple">string </span>`Sample value: All-in-one`

Tool type. Valid values:


* All\-in\-one: An integrated toolset, i.e., the preset tool AIO Sandbox.

* Skill: Skill tool image, which is the preset tool Skills Sandbox.

* PersonalAssistant: preset tool OpenClaw.

* Private: Custom tool.



**TosMountPoints ** <span data-label="purple">object[] </span>`Sample value: --`

TOS mount point information of the session instance.


**BucketName ** <span data-label="purple">string </span>`Sample value: bucket01`

The TOS bucket name.



**BucketPath ** <span data-label="purple">string </span>`Sample value: http://tos-ap-southeast-1.ivolces.com`

The TOS bucket path.



**LocalMountPath ** <span data-label="purple">string </span>`Sample value: /home/app`

The local directory of the tool instance to be mounted.




**UserSessionId ** <span data-label="purple">string </span>`Sample value: session01`

User session information.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=GetSession&Version=2025-10-30 HTTP/1.1
Content-Type: application/json
{
    "ToolId": "t-ye6xzwchkwoaroxxxxxx",
    "SessionId": "s-ye6xzwchkwoaroxxxxxx"
}

```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202510271450109FD029A85C12E74BE556",
    "Action": "GetSession",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "SessionId": "s-ye7sfdm2o0c1kdto****",
    "Status": "Ready",
    "UserSessionId": "",
    "Endpoint": "http://sd3s4ng567ui2e1ad****.apigateway-ap-southeast-1.volceapi.com/?faasInstanceName=vefaas-bf5xfrv4-qa6b0ee7db-d3vh9b033fo44goh****-sandbox",
    "InternalEndpoint": "",
    "ToolType": "All-in-one",
    "UserSessionId": "session01",
    "SessionMeta": {
      "WebshellUrl": "http://sd3s4ng567ui2e1ad****.apigateway-ap-southeast-1.volceapi.com/terminal?faasInstanceName=vefaas-bf5xfrv4-qa6b0ee7db-d3vh9b033fo44goh****-sandbox",
      "VncUrl": "http://sd3s4ng567ui2e1ad****.apigateway-ap-southeast-1.volceapi.com/vnc/index.html?faasInstanceName=vefaas-bf5xfrv4-qa6b0ee7db-d3vh9b033fo44goh****-sandbox"
    },
    "CreatedAt": "2025-10-27T14:44:12+08:00",
    "ExpireAt": "2025-10-28T14:44:12+08:00"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |MissingParameter.SessionId |The required parameter SessionId is not supplied. |The SessionId cannot be empty. |
|400 |MissingParameter.ToolId |The required parameter ToolId is not supplied. |The parameter ToolId cannot be empty. |
|404 |InvalidResource.NotFound |The specified resource does not exist. |The specified resource does not exist. |

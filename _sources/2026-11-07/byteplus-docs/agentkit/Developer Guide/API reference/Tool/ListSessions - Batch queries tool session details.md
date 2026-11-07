---
title: "ListSessions - Batch queries tool session details"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/ListSessions_-_Batch_queries_tool_session_details"
---

You can batch query tool session details using custom filter conditions.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|SsQOnF">必选</span> `Sample value: ListSessions`

The action that you want to perform. Value: ListSessions.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|ORWef1">必选</span> `Sample value: 2025-10-30`

The API version. Value: 2025\-10\-30.



**CreateTimeAfter ** <span data-label="purple">string </span>`Optional Sample value: 2006-01-02T15:04:05Z07:00`

Filter sessions created after this time point. (RFC3339 format)



**CreateTimeBefore ** <span data-label="purple">string </span>`Optional Sample value: 2006-01-02T15:04:05Z07:00`

Filter sessions created before this time point. (RFC3339 format)



**ExpireTimeAfter**<span data-label="purple"> string</span>` Optional Sample value: 2006-01-02T15:04:05Z07:00`

Filter sessions updated after this time point. (RFC3339 format)



**ExpireTimeBefore ** <span data-label="purple">string </span>`Optional Sample value: 2006-01-02T15:04:05Z07:00`

Filter sessions updated before this time point. (RFC3339 format)



**Filters.N.Name ** <span data-label="purple">string[] </span>`Optional Sample value: UserSessionId`

Field name used for exact filtering.


* Parameter \- N: Indicates the serial number of the filter condition. Value range: 1–10.

* Separate multiple field names with ampersands (&), representing an "Or" relationship.

* Valid values:

   * Id: Session ID.

   * UserSessionId: Session information.

   * Status: Session status.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When <code>Filters.N.Name</code> and <code>Filters.N.NameContains</code> are both passed in, only <code>Filters.N.Name</code> takes effect.</div>




**Filters.N.NameContains ** <span data-label="purple">string[] </span>`Optional Sample value: Status`

Field name used for fuzzy filtering. Values: 


* Parameter \- N: Indicates the serial number of the filter condition. Value range: 1–10.

* Separate multiple field names with ampersands (&), representing an "Or" relationship.

* Valid values:

   * Id: Session ID.

   * UserSessionId: Session information.

   * Status: Session status.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When <code>Filters.N.Name</code> and <code>Filters.N.NameContains</code> are both passed in, only <code>Filters.N.Name</code> takes effect.</div>




**Filters.N.Values.N ** <span data-label="purple">string[]</span>` Optional Sample value: Ready`

Value of the filter field.


* Parameter \- N: Indicates the serial number of the filter condition. Value range: 1–10.

* Separate multiple field names with ampersands (&).


When the filter field is Status, the values are:


* Starting: Starting.

* Ready: Running.

* Failed: Failed to start.

* Terminating: Terminating.



**MaxResults ** <span data-label="purple">integer </span>`Optional Sample value: 10`

The number of entries returned on each page in a pagination query.


* Minimum value: 1.

* Maximum value: 100. 

* Default value: 100.



**NextToken ** <span data-label="purple">string </span>`Optional Sample value: unique-token`

Pagination token marking the query position. Omit this parameter for initial API requests. In the next query, set the `NextToken` parameter to the value returned by the previous API call.



**Metadata.N.Key ** <span data-label="purple">string[] </span><span data-api-tag="require|Z3DpFu">必选</span> `Sample value: env`

The tag key of the metadata, such as env, version, and other custom identifiers.


* Parameter \- N: Indicates the sequence number of the tag key. Value range: 1–10.

* The maximum length of a single key is 128 characters.

* Separate multiple field names with ampersands (&). Duplicate field names are not allowed.



**ToolId ** <span data-label="purple">string </span><span data-api-tag="require|BZRLnV">必选</span> `Sample value: t-3tigy72q3u3vj0x2****`

Tool ID.



**Metadata.N.Value ** <span data-label="purple">string[] </span>`Optional` `Sample value: production`

The tag value of the metadata.


* Parameter \- N: Indicates the sequence number of the tag value. Value range: 1–10.

* The maximum length of a single value is 256 characters. Separate multiple field names with ampersands (&).



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**NextToken ** <span data-label="purple">string </span>`Sample value: bHpwdXJja2RxemU1eG5sb3NzdGcW1-RCEq******`

The pagination token returned by this call. If this value is empty, the current page is the last page.



**SessionInfos ** <span data-label="purple">object[] </span>`Sample value: --`

The information of the instances that meet the query conditions.


**CreatedAt ** <span data-label="purple">string </span>`Sample value: 2006-01-02T15:04:05Z07:00`

Creation time of the session.



**Endpoint ** <span data-label="purple">string </span>`Sample value: https://sd391h67itqkq7brr****.apigateway-ap-southeast-1.volceapi.com`

The public endpoint for accessing the session.



**ExpireAt ** <span data-label="purple">string </span>`Sample value: 2006-01-02T15:04:05Z07:00`

Expiration time of the session.



**InternalEndpoint ** <span data-label="purple">string </span>`Sample value: https://sd391h67itqkq7brr****.apigateway-ap-southeast-1.volceapi.com`

The private endpoint for accessing the session.



**Metadata ** <span data-label="purple">object[] </span>`Sample value: --`

The metadata information.


**Key ** <span data-label="purple">string </span>`Sample value: evn`

The metadata key.



**Type ** <span data-label="purple">string </span>`Example: String`

The metadata type.



**Value ** <span data-label="purple">string </span>`Sample value: production`

The value of the metadata.




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
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=ListSessions&Version=2025-10-30 HTTP/1.1
Content-Type: application/json
{
    "ToolId": "t-ye6xzwchkwoaroxxxxxx",
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
    "RequestId": "202510271421540541FD6FB0976A53AC40",
    "Action": "ListSessions",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "SessionInfos": [
      {
        "SessionId": "s-ye7sfdm2o0c1kdto****",
        "Status": "Ready",
        "UserSessionId": "",
        "Endpoint": "http://sd3s4ng567ui2e1ad****.apigateway-ap-southeast-1.volceapi.com/?faasInstanceName=vefaas-bf5xfrv4-qa6b0ee7db-d3vh9b033fo44goh****-sandbox",
        "InternalEndpoint": "",
        "ToolType": "All-in-one",
        "UserSessionId": "session01",
        "CreatedAt": "2025-10-27T14:44:12+08:00",
        "ExpireAt": "2025-10-28T14:44:12+08:00"
      }
    ],
    "NextToken": "dC15ZTdpdnliMm04YzFrZHRvc2****=="
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |LimitExceeded.MaximumFilters |The number of specified Filters exceeds the maximum limit. |The specified Filters exceeds the upper limit. |
|400 |MissingParameter.Key |The required parameter Key is not supplied. |The parameter Key cannot be empty.  |
|400 |MissingParameter.ToolId |The required parameter ToolId is not supplied. |The parameter ToolId cannot be empty. |
|404 |InvalidResource.NotFound |The specified resource does not exist. |The resource does not exist. |

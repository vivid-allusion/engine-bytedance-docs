---
title: "DeleteTrafficMirrorSession - Deleting a traffic mirror session instance"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/DeleteTrafficMirrorSession"
---

Call the DeleteTrafficMirrorSession API to delete the traffic mirror session.

## Instructions

* Releasing the mirror source network interface will automatically delete its associated mirror session.

* DeleteTrafficMirrorSession is an asynchronous API; when a request ID is returned, the system is still deleting in the background. You can call the [DescribeTrafficMirrorSessions](https://docs.byteplus.com/en/docs/vpc/DescribeTrafficMirrorSessions) API to check the status of a mirror session. A status of Deleting indicates it is being deleted, and a failed query indicates the deletion is complete.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteTrafficMirrorSession&serviceCode=vpc&version=2020-04-01&groupName=)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information is available in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** String必选 `Example value: DeleteTrafficMirrorSession`

The interface name. The current API name is `DeleteTrafficMirrorSession`.

**Version ** String 必选`Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.

**TrafficMirrorSessionId ** String必选 `Example value: tms-j6cmls82xnc86vtpe****`

ID of the traffic mirror session.

You can call the [DescribeTrafficMirrorSessions](https://docs.byteplus.com/en/docs/vpc/DescribeTrafficMirrorSessions) API to query the Traffic Mirror Session ID.

## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** String`Example value: 2021062415303301022514515207C4****`

Request ID.

## Request examples

```JSON
GET /?Action=DeleteTrafficMirrorSession&Version=2020-04-01&TrafficMirrorSessionId=tms-j6cmls82xnc86vtpe**** HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "DeleteTrafficMirrorSession",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021062415303301022514515207C4****"
    }
}
```

## Error codes

|**Status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |InvalidTrafficMirrorSession.InvalidStatus |The specified traffic mirror session is not in the correct status for the request. |The specified traffic mirror session is in a state that cannot process this request. |
|400 |OrderError |Failed to create an order in one step. |Failed to create and pay for the order. |
|404 |InvalidTrafficMirrorSession.NotFound |The specified traffic mirror session does not exist. |The specified traffic mirror session does not exist. |

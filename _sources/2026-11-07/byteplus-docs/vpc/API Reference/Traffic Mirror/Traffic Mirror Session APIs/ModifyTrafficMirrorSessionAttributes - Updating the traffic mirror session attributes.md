---
title: "ModifyTrafficMirrorSessionAttributes - Updating the traffic mirror session attributes"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/ModifyTrafficMirrorSessionAttributes"
---

Call the ModifyTrafficMirrorSessionAttributes API to modify the traffic mirror session.

## Instructions

* If the following optional parameters are not configured, the existing configurations will be preserved.

* ModifyTrafficMirrorSessionAttributes is an asynchronous API. When a request ID is returned, the system is still configuring in the background. You can call [DescribeTrafficMirrorSessions](https://docs.byteplus.com/en/docs/vpc/DescribeTrafficMirrorSessions) to check the status of a Traffic Mirror Session. Pending indicates being created, and Active indicates the modification is complete.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyTrafficMirrorSessionAttributes&serviceCode=vpc&version=2020-04-01&groupName=)

## Request parameters

The table below lists only the request parameters unique to this interface and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** String必选 `Example: ModifyTrafficMirrorSessionAttributes`

Interface name. The current API name is `ModifyTrafficMirrorSessionAttributes`.

**Version ** String必选 `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.

**TrafficMirrorSessionName ** String`optional` `Example: TM_Session_1`

Name of the Traffic Mirror Session.

* Length limit: 1 to 128 characters.

* Must start with a letter, Chinese character, or number. May include periods (.), underscores (_), and hyphens (\-).

**Description ** String`optional` `Example: TM_Session_1_Description`

Description of the traffic mirror session.

* Length limit: 0 to 255 characters.

* Must start with a letter, Chinese character, or number. May include commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas (，), and full\-width periods (。).

**TrafficMirrorSessionId ** String必选 `Example: tms-j6cmls82xnc86vtpe****`

The ID of the Traffic Mirror Session.

You can call the [DescribeTrafficMirrorSessions](https://docs.byteplus.com/en/docs/vpc/DescribeTrafficMirrorSessions) API to query the mirror session ID.

**TrafficMirrorTargetId ** String`optional` `Example: tmt-35bvae1r7rv283dy2w2ll****`

ID of the Traffic Mirror Target.

You can call the [DescribeTrafficMirrorTargets](https://docs.byteplus.com/en/docs/vpc/DescribeTrafficMirrorTargets) API to query the ID of the Traffic Mirror Target.

**TrafficMirrorFilterId** String `optional` `Example: tmf-bp1opxu1zkhn00123****`

ID of the traffic mirror filter.

You can call the [DescribeTrafficMirrorFilters](https://docs.byteplus.com/en/docs/vpc/DescribeTrafficMirrorFilters) API to query the Mirror Filter ID.

**VirtualNetworkId ** Integer`optional` `Example: 2`

VNI of Traffic Mirror Session. Used for the mirror target to distinguish traffic from different mirror sessions.

* Value range: **1**~**16777215.**

* If not specified, one is assigned randomly.

**Priority ** Integer`optional` `Example: 1`

The priority of the traffic mirror session ranges from **1** to **32766**.

* A lower priority value indicates higher precedence.

* The priorities of mirror sessions created by the same account in the same region must be unique.

**PacketLength** Integer `optional` `Example: 1450`

Data packet size of the traffic mirror session. The minimum range is 64 bytes, and the recommended range is 64 to 1450 bytes. Default is 1500 bytes.

> **tip**

> If the set packet size is ≤ the MTU of the mirror site or \> 1450, some packets may be truncated and the truncated content discarded. To ensure packets are not truncated, it is recommended to set the ENI's MTU value according to the following relationship:

> The MTU of the mirror site ≤ the packet size set in the mirror session ≤ the MTU of the Mirror Target \- 50, and the packet size set in the mirror session must be ≤ 1450.

**Enabled ** Boolean`optional` `Example: true`

Start traffic mirror session.

* true: Start

* false: Stop

## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** String`Example: 2021062415303301022514515207C4****`

Request ID.

## Request example

```json
GET /?Action=ModifyTrafficMirrorSessionAttributes&Version=2020-04-01&TrafficMirrorSessionId=tms-j6cmls82xnc86vtpe****&TrafficMirrorSessionName=TM_Session_1 HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ModifyTrafficMirrorSessionAttributes",
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

|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The specified description format is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The specified description format is invalid. The description cannot exceed 255 characters. |
|400 |InvalidEni.InvalidStatus |The specified elastic network interface is not in the correct status for the request. |The specified ENI is not in a status that can respond to this request. |
|400 |InvalidName.Malformed |The specified name is malformed. |The specified name format is invalid. Correct the name format and try again. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The specified name format is invalid. A name cannot exceed 128 characters. |
|400 |InvalidPacketLength.Malformed |The specified MTU is malformed. |The specified MTU is invalid. |
|400 |InvalidPriority.Malformed |The specified priority is malformed. |The specified priority is invalid. |
|400 |InvalidTrafficMirrorFilter.InvalidStatus |The specified traffic mirror filter is not in the correct status for the request. |The specified traffic mirror filter is in a state that cannot process this request. |
|400 |InvalidTrafficMirrorSession.InvalidBusinessStatus |The specified traffic mirror session is not in the correct status for the request. The specified traffic mirror session is frozen. |The specified traffic mirror session is in a state that cannot respond to this request. The current traffic mirror session is frozen. |
|400 |InvalidTrafficMirrorSession.InvalidStatus |The specified traffic mirror session is not in the correct status for the request. |The specified traffic mirror session is in a state that cannot respond to this request. |
|400 |InvalidTrafficMirrorTarget.InvalidInstance |The specified traffic mirror target has an invalid instance for the request. |The instance associated with the specified traffic mirror target cannot process this request. |
|400 |InvalidTrafficMirrorTarget.InvalidStatus |The specified traffic mirror target is not in the correct status for the request. |The specified traffic mirror target is in a state that cannot respond to the request. |
|400 |InvalidVirtualNetworkId.Malformed |The specified VNI is malformed. |The specified VNI is invalid. |
|400 |QuotaExceeded.TrafficMirrorFilterSession |You've reached the limit on the number of traffic mirror sessions per filter that you can create. |The maximum number of mirror sessions that can be associated with each mirror filter has been reached. |
|400 |QuotaExceeded.TrafficMirrorTargetSession |You've reached the limit on the number of traffic mirror sessions per target that you can create. |The maximum number of mirror sessions that can be associated with each mirror target has been reached. |
|400 |QuotaExceeded.TrafficMirrorTargetSource |You've reached the limit on the number of traffic mirror sources per target that you can create. |The maximum number of mirror sites that can be associated with each mirror target has been reached. |
|404 |InvalidTrafficMirrorFilter.NotFound |The specified traffic mirror filter does not exist. |The specified Traffic Mirror Filter does not exist. |
|404 |InvalidTrafficMirrorSession.NotFound |The specified traffic mirror session does not exist. |The specified traffic mirror session does not exist. |
|404 |InvalidTrafficMirrorTarget.NotFound |The specified traffic mirror target does not exist. |The specified traffic mirror target does not exist. |
|409 |InvalidTrafficMirrorSessionPriority.Conflict |The specified priority conflicts with another in your traffic mirror session. |The specified mirror session has a priority conflict with another session under its parent traffic mirror session. |

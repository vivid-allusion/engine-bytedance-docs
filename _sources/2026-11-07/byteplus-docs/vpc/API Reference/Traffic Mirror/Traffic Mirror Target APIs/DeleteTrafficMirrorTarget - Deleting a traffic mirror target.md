---
title: "DeleteTrafficMirrorTarget - Deleting a traffic mirror target"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/DeleteTrafficMirrorTarget"
---

Call the DeleteTrafficMirrorTarget API to delete the mirror target.

## Instructions

The traffic mirror target is not associated with any traffic mirror session. If associated, delete [Mirror Session](https://docs.byteplus.com/en/docs/vpc/Managing-a-Traffic-Mirror-session#.5Yig6Zmk6ZWc5YOP5Lya6K-d).

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteTrafficMirrorTarget&serviceCode=vpc&version=2020-04-01&groupName=)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information is available in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** String必选 `Example value: DeleteTrafficMirrorTarget`

The interface name. The current API name is `DeleteTrafficMirrorTarget`.

**Version ** String 必选`Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.

**TrafficMirrorTargetId ** String 必选`Example value: tmt-35bvae1r7rv283dy2w2ll****`

ID of the Traffic Mirror Target.

You can call the [DescribeTrafficMirrorTargets](https://docs.byteplus.com/en/docs/vpc/DescribeTrafficMirrorTargets) API to query the Traffic Mirror Target ID.

## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** String`Example value: 2021062415303301022514515207C4****`

Request ID.

## Request examples

```JSON
GET /?Action=DeleteTrafficMirrorTarget&Version=2020-04-01&TrafficMirrorTargetId=tmt-35bvae1r7rv283dy2w2ll**** HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DeleteTrafficMirrorTarget",
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

|**Status code** |**Error codes** |**Error message** |**Explain** |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |InvalidTrafficMirrorTarget.InUse |The specified traffic mirror target is in use. |The specified Traffic Mirror Target is currently in use. |
|404 |InvalidTrafficMirrorTarget.NotFound |The specified traffic mirror target does not exist. |The specified Traffic Mirror Target does not exist. |

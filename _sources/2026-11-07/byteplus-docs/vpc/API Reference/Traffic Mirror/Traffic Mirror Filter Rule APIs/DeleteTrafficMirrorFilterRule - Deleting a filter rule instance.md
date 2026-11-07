---
title: "DeleteTrafficMirrorFilterRule - Deleting a filter rule instance"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/DeleteTrafficMirrorFilterRule"
---

Call the DeleteTrafficMirrorFilterRule API to delete the traffic mirror filter rule instance.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteTrafficMirrorFilterRule&serviceCode=vpc&version=2020-04-01&groupName=)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information is available in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** String必选 `Example value: DeleteTrafficMirrorFilterRule`

The interface name. The current API name is `DeleteTrafficMirrorFilterRule`.

**Version ** String必选 `Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.

**TrafficMirrorFilterRuleId ** String 必选 `Example value: tmr-j6cmls82xnc86vtpe****`

ID of the filter rule.

You can call the [DescribeTrafficMirrorFilters](https://docs.byteplus.com/en/docs/vpc/DescribeTrafficMirrorFilters) API to query the filter rule IDs within the traffic mirror filters.

## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** String`optional` `Example value: 2021062415303301022514515207C4****`

Request ID.

## Request examples

```JSON
GET /?Action=DeleteTrafficMirrorFilterRule&Version=2020-04-01&TrafficMirrorFilterRuleId=tmr-j6cmls82xnc86vtpe**** HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DeleteTrafficMirrorFilterRule",
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
|404 |InvalidTrafficMirrorFilterRule.NotFound |The specified traffic mirror filter rule does not exist. |The specified traffic mirror filter rule does not exist. |

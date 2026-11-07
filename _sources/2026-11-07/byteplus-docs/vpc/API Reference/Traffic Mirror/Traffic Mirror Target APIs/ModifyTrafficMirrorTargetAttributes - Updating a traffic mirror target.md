---
title: "ModifyTrafficMirrorTargetAttributes - Updating a traffic mirror target"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/ModifyTrafficMirrorTargetAttributes"
---

Call the ModifyTrafficMirrorTargetAttributes API to modify the name and description of the traffic mirror target.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyTrafficMirrorTargetAttributes&serviceCode=vpc&version=2020-04-01&groupName=)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information is available in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** String必选 `Example value: ModifyTrafficMirrorTargetAttributes`

The interface name. The current API name is `ModifyTrafficMirrorTargetAttributes`.

**Version ** String必选 `Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.

**TrafficMirrorTargetId ** String必选 `Example value: tmt-35bvae1r7rv283dy2w2ll****`

ID of the traffic mirror target.

You can call the [DescribeTrafficMirrorTargets](https://docs.byteplus.com/en/docs/vpc/DescribeTrafficMirrorTargets) API to query the traffic mirror target ID.

**TrafficMirrorTargetName ** String `optional` `Example value: TM_Target_1`

Name of the traffic mirror target.

* Must be 1 to 128 characters.

* Must start with a letter, Chinese character, or number. May include periods (.), underscores (_), and hyphens (\-).

**Description ** String`optional` `Example value: TM_Target_1_Description`

Description of the traffic mirror target.

* Must be 0 to 255 characters.

* Must start with a letter, Chinese character, or number. May include commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas (，), and full\-width periods (。).

## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** String`Example value: 2021062415303301022514515207C4****`

Request ID.

## Request examples

```JSON
GET /?Action=ModifyTrafficMirrorTargetAttributes&Version=2020-04-01&TrafficMirrorTargetId=tmt-35bvae1r7rv283dy2w2ll****&TrafficMirrorTargetName=TM_Target_1 HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ModifyTrafficMirrorTargetAttributes",
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
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format of specified description is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The format of specified description is invalid. A description must not exceed 255 characters. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format of the specified name is invalid. Correct the name format and retry. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The format of specified name is invalid. A name must not exceed 128 characters. |
|400 |InvalidTrafficMirrorTarget.InvalidStatus |The specified traffic mirror target is not in the correct status for the request. |The specified traffic mirror target is in a state that cannot respond to the request. |
|404 |InvalidTrafficMirrorTarget.NotFound |The specified traffic mirror target does not exist. |The specified traffic mirror target does not exist. |

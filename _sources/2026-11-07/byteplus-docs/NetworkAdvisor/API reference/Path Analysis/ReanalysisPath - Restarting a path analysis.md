---
title: "ReanalysisPath - Restarting a path analysis"
product: "Network Advisor"
product_code: "NetworkAdvisor"
source: "https://docs.byteplus.com/en/docs/NetworkAdvisor/ReanalysisPath"
---

Call the ReanalysisPath API to restart the path analysis.

## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=ReanalysisPath&groupName=%E8%B7%AF%E5%BE%84%E5%88%86%E6%9E%90&serviceCode=na&version=2020-04-01)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** string必选 `Example: ReanalysisPath`

Action to execute. Set the value to ReanalysisPath.

**Version ** string必选 `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.

**PathId ** string必选 `Example: pa-3ogfsspk3cf0g6****`

Network path ID.

## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**PathId ** string`Example: pa-4ogfsspk3cf0g6****`

Network path ID.

**PathReportId ** string`Example: par-ak4v00jduk1s3r****`

Path analysis report ID.

## Request example

```text
GET /?Action=ReanalysisPath&Version=2020-04-01&PathId=pa-3ogfsspk3cf0g6****
Host: na.byteplusapi.com
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/na/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```text
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ReanalysisPath",
        "Version": "2020-04-01",
        "Service": "na",
        "Region": "cn-beijing"
    },
    "Result": {
        "PathId": "pa-4ogfsspk3cf0g6****",
        "PathReportId": "par-ak4v00jduk1s3r****"
    }
}
```

## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |InvalidAllPublicIP |The specified source ip and target ip are public ip. |When the source is public IPs, the destination must be an EIP. |
|400 |InvalidAnalysisPath.NotFound |The specified analysis path is not found. |The specified analysis path is not found. |
|400 |InvalidIPv4 |The specified ipv4 is not invalid. |The specified IPv4 is invalid. |
|400 |InvalidPathAnalysisEndType |The specified end type is invalid. |The specified end type is invalid. |
|400 |InvalidPort |The specified port is invalid. |The specified port number is invalid. |
|400 |InvalidProtocol |The specified protocol is invalid. |The specified protocol type is invalid. |
|400 |InvalidSourceTarget |The specified source and target should not be same. |The specified source and destination cannot be the same. |

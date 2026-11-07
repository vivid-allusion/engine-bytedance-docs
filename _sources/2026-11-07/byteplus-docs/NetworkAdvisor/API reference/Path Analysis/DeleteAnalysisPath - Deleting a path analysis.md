---
title: "DeleteAnalysisPath - Deleting a path analysis"
product: "Network Advisor"
product_code: "NetworkAdvisor"
source: "https://docs.byteplus.com/en/docs/NetworkAdvisor/DeleteAnalysisPath"
---

Call the DeleteAnalysisPath API to delete the specified path analysis.

## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DeleteAnalysisPath&groupName=%E8%B7%AF%E5%BE%84%E5%88%86%E6%9E%90&serviceCode=na&version=2020-04-01)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** string必选 `Example: DeleteAnalysisPath`

Action to execute. Set the value to DeleteAnalysisPath.

**Version ** string必选 `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.

**PathId ** string必选 `Example: pa-3ogfsspk3cf0g6****`

Network path ID.

## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

## Request example

```text
GET /?Action=DeleteAnalysisPath&Version=2020-04-01&PathId=pa-3ogfsspk3cf0g6****
Host: na.byteplusapi.com
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/na/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```text
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DeleteAnalysisPath",
        "Version": "2020-04-01",
        "Service": "na",
        "Region": "cn-beijing"
    }
}
```

## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |InvalidAnalysisPath.NotFound |The specified analysis path is not found. |The specified analysis path is not found. |

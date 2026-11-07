---
title: "DeleteAnalysisPathReport - Deleting a path analysis report"
product: "Network Advisor"
product_code: "NetworkAdvisor"
source: "https://docs.byteplus.com/en/docs/NetworkAdvisor/DeleteAnalysisPathReport"
---

Call DeleteAnalysisPathReport API to delete the path analysis report.

## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DeleteAnalysisPathReport&groupName=%E8%B7%AF%E5%BE%84%E5%88%86%E6%9E%90&serviceCode=na&version=2020-04-01)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** string必选 `Example: DeleteAnalysisPathReport`

Action to execute. Set the value to DeleteAnalysisPathReport.

**Version ** string必选 `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.

**PathReportId ** string必选 `Example: par-ak3v00jduk1s3r****`

Path analysis report ID.

## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

## Request example

```text
GET /?Action=DeleteAnalysisPathReport&Version=2020-04-01&PathReportId=par-ak3v00jduk1s3r****
Host: na.byteplusapi.com
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/na/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DeleteAnalysisPathReport",
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
|400 |InvalidAnalysisPathReport.NotFound |The specified analysis path report is not found. |The specified path analysis report is not found. |

---
title: "DescribeHistoryDiagnosis - Viewing the instance history diagnosis"
product: "Network Advisor"
product_code: "NetworkAdvisor"
source: "https://docs.byteplus.com/en/docs/NetworkAdvisor/DescribeHistoryDiagnosis"
---

Call the DescribeHistoryDiagnosis API to view all historical diagnosis records for a resource instance.

## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeHistoryDiagnosis&groupName=%E4%B8%80%E9%94%AE%E8%AF%8A%E6%96%AD&serviceCode=na&version=2020-04-01)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** string必选 `Example: DescribeHistoryDiagnosis`

Action to execute. Set the value to DescribeHistoryDiagnosis.

**Version ** string必选 `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.

**ResourceInstanceId ** string必选 `Example: eip-12b8n3mdsl4hs17q7****`

Resource instance ID.

## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**HistoryDiagnosis ** object[]`Example: --`

Instance diagnosis history.

**Created on ** string`Example: 2025-12-31T11:41:30+08:00`

Creation time.

**DiagnosisInstanceId ** string`Example: di-12b8n3mdsl4hs17q7y2bp****`

Instance diagnosis ID.

**DiagnosisInstanceStatus ** string`Example: Normal`

Instance diagnosis status.

* Running

* Pass

* Hint

* Normal

* Serious

* Fatal

## Request example

```text
GET /?Action=DescribeHistoryDiagnosis&Version=2020-04-01&ResourceInstanceId=eip-12b8n3mdsl4hs17q7****
Host: na.byteplusapi.com
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/na/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeHistoryDiagnosis",
        "Version": "2020-04-01",
        "Service": "na",
        "Region": "cn-beijing"
    },
    "Result": {
        "HistoryDiagnosis": [
            {
                "CreationTime": "2025-12-31T11:41:30+08:00",
                "DiagnosisInstanceId": "di-12b8n3mdsl4hs17q7y2bp****",
                "DiagnosisInstanceStatus": "Hint"
            }
        ]
    }
}
```

## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |InvalidPaging.Malformed |The specified PageNumber or PageSize is malformed. |The format specified for pagination parameter is invalid. |
|400 |InvalidDiagResourceType.NotSupported |The specified resource type is not supported. |The specified resource type is not supported. |

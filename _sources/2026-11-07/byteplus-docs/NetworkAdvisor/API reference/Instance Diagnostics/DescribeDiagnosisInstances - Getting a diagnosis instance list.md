---
title: "DescribeDiagnosisInstances - Getting a diagnosis instance list"
product: "Network Advisor"
product_code: "NetworkAdvisor"
source: "https://docs.byteplus.com/en/docs/NetworkAdvisor/DescribeDiagnosisInstances"
---

Call the DescribeDiagnosisInstances API to get the diagnosis instance list.

## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeDiagnosisInstances&groupName=%E4%B8%80%E9%94%AE%E8%AF%8A%E6%96%AD&serviceCode=na&version=2020-04-01)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** string必选`Example: DescribeDiagnosisInstances`

Action to execute. Set the value to DescribeDiagnosisInstances.

**Version ** string必选 `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.

**ResourceType ** string`optional` `Example: EIP`

The resource type. Valid values:

* EIP

* NAT: NAT gateway.

* CLB: Classic Load Balancer.

* VPN: VPN gateway.

* TR: Transit Router.

* PL: PrivateLink.

* DC: Direct Connect Gateway.

**ResourceInstanceId ** string`optional` `Example: eip-12b8n3mdsl4hs17q****`

Resource instance ID.

**PageNumber ** integer`optional` `Example: 1`

Page number of the list. Default: 1.

**PageSize ** integer`optional` `Example: 10`

The number of entries per page in a paginated query. Maximum: 100. Default: 10.

## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**DiagnosisInstances ** object[]`Example: --`

Information of the diagnosis instance.

**Count ** integer`Example: 3`

Number of historical diagnostic reports.

**CreationTime ** string`Example: 2025-12-31T11:41:30+08:00`

Creation time.

**Resource type ** string`Example: EIP`

Resource type.

**ResourceRegion ** string`Example: cn-beijing`

Region of the resource.

**ResourceDeleted ** boolean`Example: false`

Is the resource deleted.

* true

* false

**ResourceInstanceId ** string`Example: eip-12b8n3mdsl4hsq****`

Resource instance ID.

**DiagnosisInstanceId ** string`Example: di-12b8n3mdsl4hsq****`

Instance diagnosis ID.

**ResourceInstanceName ** string`Example: eip-12b8n3mdsl4hsq****`

Name of the resource instance.

**DiagnosisInstanceStatus ** string`Example: Pass`

Instance diagnosis status.

* Running

* Pass

* Hint

* Normal

* Serious

* Fatal

**RequestId ** string`Example: 0ED8D006-F706-4D23-88ED-E11ED28DCAC0`

Request ID

**PageNumber ** integer`Example: 1`

Current page number.

**PageSize ** integer`Example: 2`

The number of rows on the current page.

**TotalCount ** integer`Example: 2`

Total number of instance diagnoses that match the criteria.

## Request example

```text
GET /?Action=DescribeDiagnosisInstances&Version=2020-04-01&ResourceType=EIP&ResourceInstanceId=eip-12b8n3mdsl4hs17q****&PageNumber=10&PageSize=10
Host: na.byteplusapi.com
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/na/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeDiagnosisInstances",
        "Version": "2020-04-01",
        "Service": "na",
        "Region": "cn-beijing"
    },
    "Result": {
        "DiagnosisInstances": [
            {
                "Count": 3,
                "CreationTime": "2025-12-31T11:41:30+08:00",
                "ResourceType": "EIP",
                "ResourceRegion": "cn-beijing",
                "ResourceDeleted": true,
                "ResourceInstanceId": "eip-12b8n3mdsl4hsq****",
                "DiagnosisInstanceId": "di-12b8n3mdsl4hsq****",
                "ResourceInstanceName": "eip-12b8n3mdsl4hsq****",
                "DiagnosisInstanceStatus": "Pass"
            }
        ],
        "PageNumber": 1,
        "PageSize": 2,
        "TotalCount": 2
    }
}
```

## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |ErrDataUnmarshalFailed |Data unmarshal failed. |Failed to parse the request. |
|400 |InvalidDiagResourceType.NotSupported |The specified resource type is not supported. |The specified resource type is not supported. |
|400 |InvalidPaging.Malformed |The specified PageNumber or PageSize is malformed. |The format specified for pagination parameter is invalid. |

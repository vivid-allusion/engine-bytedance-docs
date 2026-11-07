---
title: "DescribeDiagnosisInstanceDetail - Getting the details of diagnosis instance"
product: "Network Advisor"
product_code: "NetworkAdvisor"
source: "https://docs.byteplus.com/en/docs/NetworkAdvisor/DescribeDiagnosisInstanceDetail"
---

Call the DescribeDiagnosisInstanceDetail API to get diagnosis instance details.

## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeDiagnosisInstanceDetail&groupName=%E4%B8%80%E9%94%AE%E8%AF%8A%E6%96%AD&serviceCode=na&version=2020-04-01)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** string必选 `Example: DescribeDiagnosisInstanceDetail`

Action to execute. Set the value to DescribeDiagnosisInstanceDetail.

**Version ** string必选 `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.

**DiagnosisInstanceId ** string必选 `Example: di-2ziwb7ujxscd****`

Instance diagnosis ID.

## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**CreationTime ** string`Example: 2025-12-31T11:41:30+08:00`

Creation time.

**RequestId ** string`Example: 0ED8D006-F706-4D23-88ED-E11ED28DCAC0`

Request ID

**DiagnosisCategoryItems ** object[]`Example: --`

Information of the diagnostic items.

**DiagnosisItems ** object[]`Example: --`

Diagnostic items.

**ItemName ** string`Example: Check whether the instance is in arrears`

Diagnostic item name (in Chinese).

For details, see [diagnostic item description in the diagnostic item table](https://docs.byteplus.com/en/docs/NetworkAdvisor/EIP_diagnostic_items).

**ItemStatus ** string`Example: Normal`

Diagnosis status of the diagnostic items.

* Running

* Pass

* Hint

* Normal

* Serious

* Fatal

**AbnormalResult ** string`Example: The instance is in arrears but has not been suspended`

Abnormal result information (in Chinese).

For details, see [Diagnostic conditions from the diagnostic items table](https://docs.byteplus.com/en/docs/NetworkAdvisor/EIP_diagnostic_items).

**Recommendation ** string`The account is in arrears. Please recharge in time to ensure normal resource usage + Recharge link in the Billing Center [Billing Center - Account Recharge] (https://console.byteplus.com/finance/fund/recharge)`

Resolution suggestion (in Chinese).

See [Repair suggestions in the diagnostic item table](https://docs.byteplus.com/en/docs/NetworkAdvisor/EIP_diagnostic_items).

**ItemCategoryName ** string`Example: Arrears alert`

Diagnostic category name (in Chinese). [Corresponding diagnostic items]

See [Diagnostic items in the diagnostic items table](https://docs.byteplus.com/en/docs/NetworkAdvisor/EIP_diagnostic_items).

**DiagnosisInstanceId ** string`Example: di-2ziwb7ujxscd****`

Instance diagnosis ID.

**DiagnosisInstanceStatus ** string`Example: Pass`

Instance diagnosis status.

* Running

* Pass

* Hint

* Normal

* Serious

* Fatal

**ResourceDeleted ** boolean`Example: true`

Indicates whether the diagnosed resource has been deleted.

* `true`: Resource has been deleted.

* `false`: Resource has not been deleted.

**ResourceInstanceId ** string`Example: eip-2ziwb7ujxscd****`

The unique identifier of the resource instance, used to identify the specific resource instance being diagnosed.

**ResourceInstanceName ** string`Example: eip-12b8n3mdsl4****`

Name of the resource instance.

**ResourceRegion ** string`Example: cn-beijing`

Region of the resource.

**ResourceType ** string`Example: EIP`

Resource type.

* EIP

* NAT: NAT gateway.

* CLB: Classic Load Balancer.

* VPN: VPN gateway.

* TR: Transit Router.

* PL: PrivateLink.

* DC: Direct Connect.

## Request example

```text
GET /?Action=DescribeDiagnosisInstanceDetail&Version=2020-04-01&DiagnosisInstanceId=di-2ziwb7ujxscd****
Host: na.byteplusapi.com
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/na/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```text
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeDiagnosisInstanceDetail",
        "Version": "2020-04-01",
        "Service": "na",
        "Region": "cn-beijing"
    },
    "Result": {
        "CreationTime": "2025-12-31T11:41:30+08:00",
        "DiagnosisCategoryItems": [
            {
                "DiagnosisItems": [
                    {
                        "ItemName": "检查实例是否欠费",
                        "ItemStatus": "Serious",
                        "AbnormalResult": "实例已欠费未关停",
                        "Recommendation": "账户已欠费，请及时充值确保资源正常使用+费用中心充值链接 [费用中心-账户充值](https://console.byteplus.com/finance/fund/recharge)"
                    }
                ],
                "ItemCategoryName": "欠费告警"
            }
        ],
        "DiagnosisInstanceId": "di-2ziwb7ujxscd****",
        "DiagnosisInstanceStatus": "Pass",
        "ResourceDeleted": true,
        "ResourceInstanceId": "eip-2ziwb7ujxscd****",
        "ResourceInstanceName": "eip-12b8n3mdsl4hs17",
        "ResourceRegion": "cn-beijing",
        "ResourceType": "EIP"
    }
}
```

## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |ErrDataUnmarshalFailed |Data unmarshal failed. |Failed to parse the request. |
|400 |InvalidDiagnosisInstance.NotFound |The specified diagnosis instance is not found. |The specified diagnosis instance is not found. |

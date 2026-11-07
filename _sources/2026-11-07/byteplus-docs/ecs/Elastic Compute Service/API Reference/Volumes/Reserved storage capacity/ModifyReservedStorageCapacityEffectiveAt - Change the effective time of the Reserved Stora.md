---
title: "ModifyReservedStorageCapacityEffectiveAt - Change the effective time of the Reserved Storage Capacity package"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/ModifyReservedStorageCapacityEffectiveAt"
---

Call the ModifyReservedStorageCapacityEffectiveAt API to change the effective time of the Reserved Storage Capacity package.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

Only applies to changing the effective time for Reserved Storage Capacity packages that have not taken effect. If the Reserved Storage Capacity package has already taken effect, you cannot change its effective time through this API.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=ModifyReservedStorageCapacityEffectiveAt&groupName=RSC&serviceCode=storage_ebs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## request parameters

Below are request parameters specific to this API and some common parameters. For more information, see [Public Parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|WAlmHE">必选</span> `Example: ModifyReservedStorageCapacityEffectiveAt`

Action to be performed: ModifyReservedStorageCapacityEffectiveAt



**Version ** <span data-label="purple">string </span><span data-api-tag="require|3rPqU3">必选</span> `Example value: 2020-04-01`

The version of the API is: 2020\-04\-01.



**RSCId ** <span data-label="purple">string </span><span data-api-tag="require|JnuvZh">必选</span> `Example value: rsc-3vpnts78dk3x35cj****`

Reserved storage capacity package ID.



**EffectiveAt ** <span data-label="purple">string </span>`Optional` `Example value: 2025-03-29T17:50:00+08:00`

The effective time for the Reserved Storage Capacity package. The date format follows the ISO 8601 standard. The default value is empty, which means immediate effect. If a non\-integer\-hour effective time is specified, it takes effect at the corresponding whole hour. For instance, if specified time is 2024\-11\-25 21:50:05, the actual effective time would be 2024\-11\-25 21:00:00.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response Parameters

This API does not have unique response parameters. For more information, see [Response Structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
POST /?Action=ModifyReservedStorageCapacityEffectiveAt&Version=2020-04-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20251125T080645Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251125/ap-southeast-1/storage_ebs/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "EffectiveAt": "2025-03-29T17:50:00+08:00",
 "RSCId": "rsc-3vpnts78dk3x35cj****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Back to example

```json
{
  "ResponseMetadata": {
    "RequestId": "202511251606571820061410479B****",
    "Action": "ModifyReservedStorageCapacityEffectiveAt",
    "Version": "2020-04-01",
    "Service": "storage_ebs",
    "Region": "ap-southeast-1"
  },
  "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## error code

The following table lists all error codes related to this API and its business logic. For common error codes, refer to the [Public Error Code](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) documentation.


|Status code |error code |error message |Create Volume |
|---|---|---|---|
|400 |ErrInvalidAccountId |account id invalid |Account ID is invalid. |
|400 |RscMissingRscId |Missing Rsc id. |Missing RSC ID. |
|400 |InvalidEffectiveTime |Invalid effective time. |Invalid effective time. |
|400 |RscIdInvalid |The Rsc id is invalid. |Invalid RSC ID. |
|400 |RscInvalidStatus |The RSC status is invalid. |Invalid RSC status. |

---
title: "PurchaseReservedStorageCapacity - Purchase Reserved Storage Capacity Package"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Purchasereservedstoragecapacity"
---

Use the PurchaseReservedStorageCapacity interface to purchase a reserved storage capacity package.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* The reserved storage capacity package can only offset the pay\-as\-you\-go cloud disk.

* Only the cloud disks in the same region and availability zone as the reserved storage capacity package can be offset.

* It can only offset the cloud disk bills of the same specification as the reserved storage capacity package. For example, a reserved storage capacity package of ESSD PL0 specification cannot offset the cloud disk bill of ESSD FlexPL specification.


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=PurchaseReservedStorageCapacity&groupName=RSC&serviceCode=storage_ebs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## request parameters

The following lists request parameters specific to this interface and some common parameters. For more information, see [Public Parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|nPhW4w">必选</span> `Example value: PurchaseReservedStorageCapacity`

The action to perform. Value: PurchaseReservedStorageCapacity.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|rLnwpF">必选</span> `Example: 2020-04-01`

The version of the API is: 2020\-04\-01.



**ReservedStorageCapacityName ** <span data-label="purple">string </span>`Optional` `Example value: RSC`

Name of the reserved storage capacity package.



**ZoneId ** <span data-label="purple">string </span>`Optional` `Example value: ap-southeast-1-a`

The availability zone where the reserved storage capacity package is located.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The default region for the reserved storage capacity package is the Region specified in the request, i.e., the Region in the Header.</div>




**VolumeType ** <span data-label="purple">string </span>`Optional` `Example value: ESSD_PL0`

Specifications for the reserved storage capacity in cloud volumes, are defined as follows:


* ESSD_PL0: Extreme\-Speed SSD volume, PL0 specification

* ESSD_FlexPL: Extreme\-Speed SSD volume, FlexPL specification



**PeriodUnit ** <span data-label="purple">string </span>`optional` `Example: monthly`

The purchase duration unit for the reserved storage capacity package only supports the value "monthly," indicating that the purchase duration is measured in months.



**ClientToken ** <span data-label="purple">string </span>`Optional` `Example value: 333456899ff****`

Ensure request idempotence. The client generates a unique parameter value automatically to ensure uniqueness across different requests, preventing duplicate operations when the client retries multiple times due to API timeouts or internal server errors.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Only supports ASCII characters and cannot exceed 64 characters.</div>




**Period ** <span data-label="purple">integer </span>`Optional` `Example value: 1`

The number of months to purchase for the reserved storage capacity package ranges from 1 to 36.



**ReservedCapacity** <span data-label="purple">integer</span> `Optional` `Example: 50`

Reserved storage capacity package size, in GiB/hour.



**EffectiveAt ** <span data-label="purple">string </span>`Optional` `Example value: 2025-11-26 21:44:05`

Effective time for Reserved Storage Capacity. Follow the ISO 8601 date format. Default is empty, which means it takes effect immediately. If a non\-integer\-hour effective time is specified, it takes effect at the corresponding whole hour. For instance, if specified time is 2024\-11\-25 21:50:05, the actual effective time would be 2024\-11\-25 21:00:00.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Return parameters

Below are the return parameters specific to this API. For more information, see [Response Structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**OrderNumber ** <span data-label="purple">string </span>`Example: Order738395864274233****`

Order number.



**ReservedStorageCapacityId ** <span data-label="purple">string </span>`Example value: rsc-3vpnts78dk3x35cj****`

Reserved storage capacity package ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
GET /?Action=PurchaseReservedStorageCapacity&Version=2020-04-01&Period=1&PeriodUnit=monthly&ZoneId=ap-southeast-1-a&ReservedStorageCapacityName=RSC01&VolumeType=ESSD_PL0&ReservedCapacity=20 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
ServiceName: storage_ebs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Back to example

```json
{
  "ResponseMetadata": {
    "RequestId": "202511251604150541181320966C****",
    "Action": "PurchaseReservedStorageCapacity",
    "Version": "2020-04-01",
    "Service": "storage_ebs",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "OrderNumber": "Order738395864274233****",
    "ReservedStorageCapacityId": "rsc-3vpnts78dk3x35cj****"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## error code

The following table lists error codes related to this API and its business logic. For public error codes, refer to the [Public Error Codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) documentation.


|Status code |error code |error message |Create Volume |
|---|---|---|---|
|400 |ErrorRscVolumeTypeNoSupport |This volume type does not support creating RSC (additional performance package). |This volume type does not support RSC creation. |
|400 |ErrorRscSizeInvalid |The RSC capacity is not within the allowed range. |RSC capacity is out of the allowed range. |
|400 |ErrorRscZoneInvalid |Please provide a correct zone ID. |Provide a valid zone ID. |
|400 |ErrorRscNameInvalid |Please provide a correct RSC name. |Enter the correct RSC name. |
|400 |ErrorRscCheckQuotaFailed |The total capacity of the created RSC exceeds the quota limit. |The total purchased RSC capacity exceeds the Quota limit for this volume specification. |
|400 |ErrorRscInvalidPeriodUnit |The RSC billing cycle unit is invalid, please provide a valid billing cycle unit. |This RSC purchase period is invalid. Please provide a valid purchase period. |
|400 |ErrorRscInvalidPeriod |The RSC billing cycle is invalid, only 1\-36 months are supported. |This RSC purchase cycle is invalid; only cycles from 1 to 36 months are supported. |

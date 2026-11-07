---
title: "CalculatePriceV2 - Pricing API V2"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/CalculatePriceV2"
---

Call the CalculatePriceV2 API to query the volume price.

## Instructions

When a sub\-account uses the CalculatePriceV2 API to query the volume price, the query result includes the original price, payable price, and discount price by default. You can configure a permission policy to hide the discount price and grant it to the sub\-account, so that the sub\-account can only view the original price and payable price, but not the discount price. The permission policy to hide the discount price is as follows:

```json
{
  "Statement": [
    {
      "Effect": "Deny",
      "Action": [
        "billing:QueryDiscountPrice"
      ],
      "Resource": [
        "*"
      ]
    }
  ]
}
```

## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=CalculatePriceV2&groupName=%E4%BA%91%E7%9B%98&serviceCode=storage_ebs&version=2020-04-01)

## request parameters

Below are the unique request parameters for this API and some common parameters. For more information, see [Common Parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** string必选 `Example: CalculatePriceV2`

Action to be performed: CalculatePriceV2.

**Version ** string必选 `Example: 2020-04-01`

The version of the API is: 2020\-04\-01.

**AccountId ** long`Optional` `Example value: 210000****`

Account ID.

**CalculatePriceInfos ** object[]`Optional` `Example: -`

Inquiry information.

**Count ** long`Optional` `Example: 1`

The number of volumes, default is 1.

**PurchaseTime ** long`Optional` `Example value: 2023-11-06T06:38:51+08:00`

Purchase time.

**Size ** float`Optional` `Example: 40`

Volume capacity, unit GiB.

> **warning**

> Before performing actions such as creating a volume, expanding a volume, changing the volume billing mode, or changing the volume specifications, the Size parameter is required when inquiring about the price.

**VolumeType ** string`Optional` `Example: ESSD_FlexPL`

Volume specifications, values are as follows:

* PTSSD: Performance SSD.

* ESSD_PL0: High\-speed SSD volume of PL0 specification.

* Extreme Speed SSD Cloud volume, FlexPL specification.

* TSSD_TL0: Throughput SSD volume.

**Action ** string`Optional` `Example: extend`

The operations for pricing conversion are insensitive to case, and the value description is as follows:

* create: Inquire about pricing before creating a volume.

* Extend: Inquire before expanding the volume.

* ModifyChargeType: Change the billing model, such as changing from a yearly or monthly billed volume to a pay\-as\-you\-go volume.

* ModifyType: Inquire before changing the volume specifications, for example, changing from ESSD PL0 to ESSD FlexPL.

* Renew: Inquire before renewal.

* Terminate: Inquire before unsubscribing.

> **warning**

> Pay\-as\-you\-go volumes do not support Renew (inquiry for renewal) and Terminate (inquiry to unsubscribe).

**Period ** string`Optional` `Example: hourly`

Description of volume purchase cycle types:

* monthly: Purchase by the month. Annual and monthly packages only support monthly.

* hourly: Purchase by the hour. Pay\-as\-you\-go only supports hourly.

> **tip**

> Period and Times parameters must be provided together.

**Times ** integer`Optional` `Example value: 2`

Duration of volume purchase. For example, if Period is set to monthly and Time is set to 2, it indicates the purchase of the volume for 2 months.

> **tip**

> Times and Period parameters must be entered together.

**EndTime** integer `Optional` `Example: 1748361599`

The expiration deadline of the volume is converted based on the timestamp.

> **warning**

* > Only annual or monthly volumes support setting the EndTime parameter.

* > The unsubscription scenario does not support the EndTime parameter.

* > If both EndTime and Times are set, EndTime is given priority.

**VolumeKind ** string`Optional` `Example value: system`

Volume type. Value descriptions are as follows:

* data: Data disk

* system: System disk

Default is data disk.

**VolumeID ** string`Optional` `Example value: vol-ikbsisshogcrntuo****`

Volume ID.

> **warning**

> Before creating a volume, there is no need to enter this parameter; in other scenarios, it must be entered.

**Region ** string`Optional` `Example value: cn-beijing`

Region. Defaults to the requested region.

**ExtraPerformances** object[] `Optional` `Example value: -`

Additional performance package.

**ExtraPerformanceType** string `Optional` `Example value: IOPS`

Type of additional performance. The available values are as follows:

* Balance: Balanced type.

* IOPS: IOPS type.

* Throughput: Throughput type.

**ExtraPerformanceValue ** integer`Optional` `Example value: 20`

The performance size of the additional performance package.

**InstanceID ** string`Optional` `Example value: i-yci7p7t660awmay7****`

ECS instance ID. After setting InstanceID, the expiration time of the ECS instance will be used as the deadline for the volume, eliminating the need to set EndTime.

> **warning**

* > Only subscription volumes support setting InstanceID parameter.

* > InstanceID and EndTime parameters are mutually exclusive. Inputting both InstanceID and EndTime parameters will result in an error.

* > If InstanceID and Times are both provided, the expiration time of the instance corresponding to InstanceID will be prioritized.

**ChargeType ** string`Optional` `Example value: PostPaid`

The payment models for cloud volume, explained as follows:

* PostPaid: Pay\-as\-you\-go

* PrePaid: Subscription based

## Return parameters

The table below lists the return parameters specific to this API. For more details, see [Return structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**OriginalAmount ** string`Example value: 40`

Total original price of all volumes.

**DiscountAmount ** string`Example value: 40`

Total discount price for all volumes.

**PayableAmount ** string`Example value: 40`

Total payable price for all volumes.

> **tip**

* > When querying the price of pay\-as\-you\-go volumes, PayableAmount returns as 0.

* > If it is a subscription cancellation scenario, which supports refunds for cancellation, volume specification modification, or downgrading extra performance packages, and at this time PayableAmount shows a negative balance, this negative balance indicates the refund amount.

**ConfigItems**object[]`Example value: -`

Detailed pricing information.

**DiscountAmount ** stringExample: 40

An operation of CalculatePriceInfo structure corresponds to the total discount price of the volume.

**Product ** stringExample: volume

The product name corresponding to the volume, only returns volume.

**OriginalAmount ** string`Example value: 40`

An operation of a CalculatePriceInfo structure corresponds to the total original cost of the cloud volume.

**PayableAmount**string`Example value: 40`

One operation on a CalculatePriceInfo structure corresponds to the total payable price for the volume.

> **tip**

> When querying the price of pay\-as\-you\-go volumes, PayableAmount returns as 0.

**ChargeItems ** object[]`Example: -`

List of billing items.

**ChargeItemCode ** string`Example: data-EBS_ESSD_PL0_cn-beijing`

Billing item code.

**OriginalAmount ** string`Example value: 40`

The original price of each billing item.

**DiscountAmount ** string`Example: 40`

Discounted price for each billing item.

**PayableAmount ** string`Example value: 40`

The payable price for each billing item.

> **tip**

> When querying the price for usage\-based billing volumes, PayableAmount returns as 0.

**ConfigurationCode ** string`Example value: data-EBS_ESSD_PL0.month`

Billing item category.

## Request example

```JSON
POST /?Action=CalculatePriceV2&Version=2020-04-01 HTTP/1.1
Host: open.volcengineapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20240903T084538Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240903/cn-beijing/storage_ebs/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
{
"CalculatePriceInfos": [
      {
        "VolumeType": "ESSD_PL0",
        "Size": 40,
        "Action": "create",
        "ChargeType": "PrePaid",
        "VolumeKind": "data",
        "Period": "monthly",
        "Times": 2
      }
    ]
  }
```

## Back to example

```JSON
{
  "ResponseMetadata": {
    "RequestId": "20240903164751104004150048BA****",
    "Action": "CalculatePrice",
    "Version": "2020-04-01",
    "Service": "storage_ebs",
    "Region": "cn-beijing"
  },
   "Result": {
    "ConfigItems": [
      {
        "ChargeItems": [
          {
            "ChargeItemCode": "data-EBS_ESSD_PL0_cn-beijing",
            "DiscountAmount": "40",
            "OriginalAmount": "40",
            "PayableAmount": "40"
          }
        ],
        "ConfigurationCode": "data-EBS_ESSD_PL0.month",
        "DiscountAmount": "40",
        "OriginalAmount": "40",
        "PayableAmount": "40",
        "Product": "volume",
        "Quantity": 1
      }
    ],
    "DiscountAmount": "40",
    "OriginalAmount": "40",
    "PayableAmount": "40",
    "Quantity": 1,
    "Visible": true
  }
}
```

## error code

The following table lists error codes related to API and business logic. For common error codes, see the [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) documentation.

|Status code |error code |error message |Create Volume |
|---|---|---|---|
|400 |InvalidVolumeSize |Invalid volume size. |The volume size is invalid. |
|412 |InvalidInstanceExpireTime |Failed to retrieve the expiration time of the instance or the instance has already expired. |Either the instance expiration time was not found, or the instance has expired. |

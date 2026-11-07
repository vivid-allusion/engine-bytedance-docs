---
title: "SetCenBandwidthPackageRenewal - Updating the renewal type of bandwidth packages"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/SetCenBandwidthPackageRenewal"
---

Call the SetCenBandwidthPackageRenewal API to configure the renewal type for a subscription bandwidth package.

## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=SetCenBandwidthPackageRenewal&groupName=%E5%B8%A6%E5%AE%BD%E5%8C%85&serviceCode=cen&version=2020-04-01)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** string必选 `Example: SetCenBandwidthPackageRenewal`

Action to execute. Set the value to SetCenBandwidthPackageRenewal.

**Version ** string必选 `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.

**CenBandwidthPackageId ** string必选 `Example: cbp-bp1o94dp5****`

ID of the bandwidth package.

You can call the [DescribeCenBandwidthPackages](https://docs.byteplus.com/en/docs/cen/DescribeCenBandwidthPackages) API to get the bandwidth package ID.

**RenewType ** string必选 `Example: Auto`

Renewal type of the bandwidth package instance. Valid values:

* Manual: Manual renewal.

* Auto: Automatic renewal.

* NoRenew: Non\-renewal.

**RenewPeriod ** integer`optional` `Example: 1`

The period for a single automatic renewal, in month.

Valid values: 1–3, 6, and 12. Default: 1.

**RemainRenewTimes ** integer`optional` `Example: 1`

The number of automatic renewals.

Values include \-1 and 1 to 100. The default is \-1, meaning unlimited automatic renewals.

## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

## Request examples

```text
GET /?Action=SetCenBandwidthPackageRenewal&Version=2020-04-01&CenBandwidthPackageId=cbp-bp1o94dp5****&RenewType=Auto HTTP/1.1
Host: cen.byteplusapi.com
X-Date: 20260109T085002Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260109/cn-beijing/cen/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```

## Response examples

```json
{
  "ResponseMetadata": {
    "RequestId": "202508151702371242552322078E0948",
    "Action": "SetCenBandwidthPackageRenewal",
    "Version": "2020-04-01",
    "Service": "cen",
    "Region": "cn-beijing"
  },
  "Result": {}
}
```

## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |InvalidParameter |A parameter specified in the request is not valid, is unsupported or cannot be used. |The request contains invalid or unsupported parameters. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request. |This request does not contain required parameters. Ensure all required parameters are provided when initiating the request. |
|400 |InvalidCenBandwidthPackage.RenewTypeMalformed |The specified RenewType is invalid. |The specified renewal type is invalid. |
|400 |UnsupportedOperation.CrossBorderBandwidthPackage |The specified request is denied because the bandwidth package is a cross\-border bandwidth package. |The specified bandwidth package is a cross\-border bandwidth package and does not support this operation. |
|400 |FailedOperation |Failed to obtain CEN bandwidth package billing information. |Failed to retrieve the billing information of the bandwidth package. |
|400 |InvalidCenBandwidthPackage.BillingTypeMalformed |The specified BillingType is invalid. |The specified billing method is invalid. |
|400 |InvalidCenBandwidthPackage.ModifyRenewalSettings |Modify renewal settings failed. |Failed to modify automatic renewal settings. |
|400 |InvalidCenBandwidthPackage.RemainRenewTimesMalformed |The specified RemainRenewTimes is invalid. |The specified remaining automatic renewals is invalid. |
|400 |InvalidCenBandwidthPackage.RenewPeriodMalformed |The specified RenewPeriod is invalid. |The specified renewal cycle is invalid. |
|404 |InvalidCenBandwidthPackage.NotFound |The bandwidth package of the specified geographic regions does not exist. |The specified bandwidth package does not exist. |
|500 |InternalError |Request failed with internal server error. |Internal system error. |

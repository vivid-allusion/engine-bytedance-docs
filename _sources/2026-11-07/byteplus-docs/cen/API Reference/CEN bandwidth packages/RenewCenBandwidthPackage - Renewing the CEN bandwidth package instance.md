---
title: "RenewCenBandwidthPackage - Renewing the CEN bandwidth package instance"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/RenewCenBandwidthPackage"
---

Call the RenewCenBandwidthPackage API to renew a subscription bandwidth package.

## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=RenewCenBandwidthPackage&groupName=%E5%B8%A6%E5%AE%BD%E5%8C%85&serviceCode=cen&version=2020-04-01)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** string必选 `Example: RenewCenBandwidthPackage`

Action to execute. Set the value to RenewCenBandwidthPackage.

**Version ** string必选 `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.

**PeriodUnit ** string`optional` `Example: Month`

Billing cycle of the bandwidth package instance. Valid values:

* Month (default): Billing by month.

* Year: Billing by year.

**Period ** integer`optional` `Example: 1`

The purchase duration for the bandwidth package instance, with a default value of 1.

* When `PeriodUnit` is set to "Month", valid values are 1 to 9, 12, 24, and 36.

* When `PeriodUnit` is set to "Year", valid values are 1 to 3.

**CenBandwidthPackageId ** string必选 `Example: cbp-bp1o94dp5****`

ID of the CEN bandwidth package.

You can call the [DescribeCenBandwidthPackages](https://docs.byteplus.com/en/docs/cen/DescribeCenBandwidthPackages) API to query the bandwidth package ID.

## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

## Request examples

```text
GET /?Action=RenewCenBandwidthPackage&Version=2020-04-01&CenBandwidthPackageId=cbp-bp1o94dp5**** HTTP/1.1
Host: cen.byteplusapi.com
X-Date: 20260109T090525Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260109/cn-beijing/cen/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```

## Response examples

```json
{
  "ResponseMetadata": {
    "RequestId": "2025081517035701304815223459B895",
    "Action": "RenewCenBandwidthPackage",
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
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request. |This request does not contain required parameters. Ensure all required parameters are provided when initiating the request. |
|400 |InvalidParameter |A parameter specified in the request is not valid, is unsupported or cannot be used. |The request contains invalid or unsupported parameters. |
|400 |InvalidCenCrossBorderBandwidthPackage.FrozenStatus |The specified request is denied because your account has been frozen for cross\-border. Please wait for the Service Provider to unfreeze it. |The cross\-border service under your account is suspended. Proceed after the line operator reactivates your service. |
|400 |InvalidCenBandwidthPackage.InvalidStatus |Specified CEN bandwidth package is being operated now. |The specified bandwidth package is in a status that cannot respond to this request. Retry later. |
|400 |InvalidCenBandwidthPackage.PeriodUnitMalformed |The specified PeriodUnit is invalid. |The specified billing cycle is invalid. |
|400 |InvalidCenBandwidthPackage.PeriodMalformed |The specified Period is invalid. |The specified purchase duration is invalid. |
|400 |InvalidBandwidthPackage.OrderConflict |The specified Bandwidth package has unpaid order. |The specified bandwidth package has an unpaid order. Please complete the payment for the previous order or wait for it to time out after 24 hours. |
|400 |FailedOperation |Failed to obtain CEN bandwidth package billing information. |Failed to retrieve the billing information of the bandwidth package. |
|400 |InvalidCenBandwidthPackage.BillingTypeMalformed |The specified BillingType is invalid. |The specified billing method is invalid. |
|400 |InvalidCenBandwidthPackage.OperationMalformed |The specified renew operation is invalid. You can renew within 30 days of expired time. |The specified operation is invalid. Renewal must be completed within 30 days before the expiration date. |
|400 |OrderError |Failed to create an order. |Order placement failed. |
|400 |UnsupportedOperation |The request on the specified instance is denied due to the account in arrears status. |The action request on this instance is denied because the account is in arrears. |
|400 |UnsupportedOperation |The payment failed due to the account balance is not enough for this order. |Insufficient account balance. Order payment failed. |
|404 |InvalidCenBandwidthPackage.NotFound |The bandwidth package of the specified geographic regions does not exist. |The specified bandwidth package does not exist. |
|500 |InternalError |Request failed with internal server error. |Internal system error. |

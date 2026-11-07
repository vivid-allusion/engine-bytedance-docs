---
title: "ModifyCenInterRegionBandwidthAttributes - Modifying the bandwidth of a specified CEN inter-region bandwidth"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/ModifyCenInterRegionBandwidthAttributes"
---

Call the ModifyCenInterRegionBandwidthAttributes API to modify the bandwidth size of a specified inter\-region bandwidth.

## Instructions

If a bandwidth package is used, the sum of all inter\-region bandwidths within the same bandwidth package must not exceed the bandwidth upper limit of the bandwidth package.

## Debug

[去调试](https://api.volcengine.com/tools/api-explorer/?action=ModifyCenInterRegionBandwidthAttributes&groupName=%E5%9F%9F%E9%97%B4%E5%B8%A6%E5%AE%BD&serviceCode=cen&version=2020-04-01)

## Request parameters

The table below lists only the request parameters unique to this interface and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** string必选 `Example: ModifyCenInterRegionBandwidthAttributes`

Action to execute. Set the value to ModifyCenInterRegionBandwidthAttributes.

**Version ** string必选 `Example: 2020-04-01`

Current API version is 2020\-04\-01.

**Bandwidth ** integer`optional` `Example: 1000`

The peak bandwidth of the CEN inter\-region bandwidth. Unit: Mbps.

* This parameter is required only when inter\-region bandwidth is allocated through a bandwidth package.

* The value cannot exceed the available bandwidth size of the associated bandwidth package.

**CenBandwidthPackageId ** string`optional` `Example: cbp-4c2zaavbvh5fx****`

Bandwidth package ID.

**InterRegionBandwidthId ** string必选 `Example: cirb-3tex2x1cwd4c6c0v****`

ID of the CEN inter\-region bandwidth.

**BandwidthType ** string`optional` `Example: BandwidthPackage`

Bandwidth usage method.

* BandwidthPackage: Subscription bandwidth package.

* CloudDataTransfer: Pay\-by\-traffic billing, i.e., billing for traffic between regions. It is already integrated with Cloud Data Transfer (CDT). For more information, see [Cloud Data Transfer](https://docs.byteplus.com/en/docs/Cloud_Data_Transfer/What_is_Cloud_Data_Transfer).

**LineOperator ** string`optional` `Example: ChinaUnicom`

Line operator. This parameter is required only in cross\-border scenarios.

* ChinaUnicom: China Unicom.

* ChinaTelecom: China Telecom.

## Response parameters

This API has no unique response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

## Request example

```text
GET /?Action=ModifyCenInterRegionBandwidthAttributes&Version=2020-04-01&InterRegionBandwidthId=cirb-3tex2x1cwd4c6c0v**** HTTP/1.1
Host: cen.byteplusapi.com
X-Date: 20260109T083258Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260109/cn-beijing/cen/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```

## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "20250815172413026070072180A25A2F",
    "Action": "ModifyCenInterRegionBandwidthAttributes",
    "Version": "2020-04-01",
    "Service": "cen",
    "Region": "cn-beijing"
  },
  "Result": {}
}
```

## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).

|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InstanceCreateOrderError |Failed to create cdt instance order. |The order placement failed. |
|400 |InvalidBandwidthPackageId.MissMatchBandwidthType |The specified bandwidth package ID does not match the bandwidth type. |The specified bandwidth package ID does not match the bandwidth allocation method. |
|400 |InvalidBandwidthType.NotSupported |The specified bandwidth type is not supported. |The specified bandwidth allocation method is not supported. |
|400 |InvalidCenCrossBorderBandwidthPackage.FrozenStatus |The specified request is denied because your account has been frozen for cross\-border. Please wait for the Service Provider to unfreeze it. |Your account is currently in a cross\-border suspension state. Please wait until the carrier lifts the suspension before performing the action. |
|400 |InvalidInterRegionBandwidth.BillingTypeMissmatch |The billing type of specified inter\-region bandwidth and bandwidth package are different. |The billing method of the specified inter\-region bandwidth is inconsistent with that of the bandwidth package. |
|400 |InvalidInterRegionBandwidth.CenMissmatch |The associated cen of specified inter\-region bandwidth and bandwidth package are different. |The specified inter\-region bandwidth is not associated with the same CEN instance as the bandwidth package. |
|400 |InvalidInterRegionBandwidth.GeographicRegionSetIDMissmatch |The regions of specified inter\-region bandwidth do not match the geographic region set ID of the bandwidth package. |The interconnected regions of the specified inter\-region bandwidth do not match the interconnection areas of the bandwidth package. |
|400 |InvalidLineOperator.MissMatchBandwidthType |The specified line operator does not match the bandwidth type. |The specified line operator does not match the bandwidth allocation method. |
|400 |InvalidParameter |A parameter specified in the request is not valid, is unsupported or cannot be used. |This request contains an invalid or unsupported parameter. |
|400 |LimitExceeded.InterRegionBandwidth |The specified inter\-region bandwidth exceeds the lower limit. |The specified bandwidth size exceeds the minimum limit for inter\-region bandwidth. |
|400 |LimitExceeded.InterRegionBandwidth |The specified inter\-region bandwidth exceeds the range of bandwidth package. |The specified inter\-region bandwidth size exceeds the allocatable bandwidth of the bandwidth package. |
|400 |LimitExceeded.InterRegionBandwidthOfCloudDataTransfer |The specified inter\-region bandwidth exceeds the range of cloud data transfer. |The specified pay\-by\-traffic inter\-region bandwidth size exceeds the allocatable bandwidth. |
|400 |LimitExceeded.PhysicalLineBandwidth |You’ve reached the bandwidth limit on the number of physical line. |The allocatable bandwidth upper limit of the DC Connection has been reached. |
|400 |MainAccountNotSupportPaypalErr |You are requested to contact the main account to provide an alternative payment method other than Paypal before enabling the pay\-as\-you\-go products in BytePlus. |The postpaid product in this order does not support PayPal payment. Please contact the root user to add another payment method. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request. |This request is missing a required parameter. Ensure all required parameters are provided when initiating the request. |
|400 |NotSupportPaypalErr |You are requested to provide an alternative payment method other than Paypal before enabling the pay\-as\-you\-go products in BytePlus. |The postpaid product in this order does not support PayPal payment. Please add another payment method. |
|400 |UnsupportedOperation |The request on the specified bandwidth package is denied because the bandwidth package is expired. |The specified bandwidth package has expired, and the current action is not supported. |
|400 |UnsupportedOperation |The request on the specified bandwidth package is denied because the bandwidth package is shut down due to arrears. |The specified bandwidth package is suspended due to arrears, and the current action is not supported. |
|400 |UnsupportedOperation |The request on the specified instance is denied due to the account in arrears status. |The request on the specified instance is denied because the account is in arrears. |
|403 |Forbidden.CrossBorderApprovalNotApplied |You cannot create cross\-border resources because you have not applied for cross\-border audit yet. |Cross\-border qualification review has not been submitted, so cross\-border resources cannot be created. |
|403 |Forbidden.CrossBorderApprovalPending |The specified request is denied because your cross\-border audit application is pending approval. |Your cross\-border application is still under review. Please wait for the business qualification to be approved before creating cross\-border resources. |
|403 |Forbidden.CrossBorderApprovalRejected |You cannot create cross\-border resources because your cross\-border audit application has been rejected. |The cross\-border qualification review was rejected, so cross\-border resources cannot be created. |
|403 |Forbidden.CrossBorderUserFrozen |The specified request is denied because your account has been frozen for cross\-border. Please wait for the Service Provider to unfreeze it. |Your account is currently in a cross\-border suspension state. Please wait until the carrier lifts the suspension before performing the action. |
|404 |InvalidCenBandwidthPackage.NotFound |The bandwidth package of the specified geographic regions does not exist. |The specified bandwidth package does not exist. |
|404 |InvalidInterRegionBandwidth.NotFound |The specified inter\-region bandwidth does not exist. |The specified inter\-region bandwidth does not exist. |
|409 |InvalidCen.InvalidStatus |The specified CEN instance is not in the correct status for the request. |The specified CEN instance is in a state that cannot process the request. Please try again later. |
|500 |InternalError |Request failed with internal server error. |Internal system error. |

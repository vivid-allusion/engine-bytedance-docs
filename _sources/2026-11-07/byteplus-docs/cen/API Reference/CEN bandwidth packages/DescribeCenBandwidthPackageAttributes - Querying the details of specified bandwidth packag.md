---
title: "DescribeCenBandwidthPackageAttributes - Querying the details of specified bandwidth package instance"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/DescribeCenBandwidthPackageAttributes"
---

Call the DescribeCenBandwidthPackageAttributes API to view the details of the specified bandwidth package.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeCenBandwidthPackageAttributes&groupName=%E5%B8%A6%E5%AE%BD%E5%8C%85&serviceCode=cen&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|7zO0TV">必选</span>`Example: DescribeCenBandwidthPackageAttributes`

Action to execute. Set the value to DescribeCenBandwidthPackageAttributes.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|9nqwor">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**CenBandwidthPackageId ** <span data-label="purple">string </span><span data-api-tag="require|Ezohrn">必选</span> `Example: cbp-bp1o94dp5****`

Bandwidth package ID.

You can call the [DescribeCenBandwidthPackages](https://docs.byteplus.com/en/docs/cen/DescribeCenBandwidthPackages) API to query the bandwidth package ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**CenBandwidthPackageId** <span data-label="purple">string</span> `Example: cbp-bp1o94dp5****`

Bandwidth package ID.



**CenBandwidthPackageName ** <span data-label="purple">string </span>`Example: cbp-test`

Bandwidth package name.



**Description ** <span data-label="purple">string </span>`Example: testdesc`

Bandwidth package description.



**LocalGeographicRegionSetId** <span data-label="purple">string</span> `Example: China`

Local geographic region ID for interconnection.



**PeerGeographicRegionSetId ** <span data-label="purple">string </span>`Example: China`

Peer geographic region ID for interconnection.



**Bandwidth** <span data-label="purple">integer</span> `Example: 20`

Bandwidth size. Unit: Mbps



**RemainingBandwidth ** <span data-label="purple">integer </span>`Example: 10`

Remaining bandwidth. Unit: Mbps



**CenIds ** <span data-label="purple">string[] </span>`Example: cen-7qthudw0ll6jmc****`

List of associated CEN instance IDs.



**Status ** <span data-label="purple">string </span>`Example: Available`

Status of the bandwidth package.


* Creating

* Deleting

* Pending: Action in progress​.

* Available: Unbound.

* InUse: Bound.



**CreationTime ** <span data-label="purple">string </span>`Example: 2018-04-18T15:02:37+08:00`

Creation time of the bandwidth package.



**AccountId ** <span data-label="purple">string </span>`Example: 210000****`

The ID of the account that owns the TR bandwidth package.



**BusinessStatus ** <span data-label="purple">string </span>`Example: Normal`

The frozen status of the bandwidth package.


* Normal

* FinancialLocked: Locked.



**BillingType ** <span data-label="purple">integer </span>`Example: 1`

Billing methods for the bandwidth package.


* 1: Subscription.

* 4: Pay\-as\-you\-go \- Pay\-by\-95\-peak.



**ExpiredTime ** <span data-label="purple">string </span>`Example: 2021-05-07 23:59:59`

Expiration time of the bandwidth package.



**DeletedTime ** <span data-label="purple">string </span>`Example: 2021-05-22 00:00:00`

Deletion time of the bandwidth package.



**ProjectName ** <span data-label="purple">string </span>`Example: default`

Name of the project to which the bandwidth package belongs.



**Tags ** <span data-label="purple">object[] </span>`Example: --`

Tag information of the bandwidth package.


**Value ** <span data-label="purple">string </span>`Example: v1`

The tag value.



**Key ** <span data-label="purple">string </span>`Example: k1`

The tag key.




**UpdateTime ** <span data-label="purple">string </span>`Example: 2018-04-18T15:02:37+08:00`

Update time of bandwidth package.



**LineOperator ** <span data-label="purple">string </span>`Example: ChinaUnicom`

The provider of cross\-border bandwidth package.


* ChinaTelecom: China Telecom.

* ChinaUnicom: China Unicom.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=DescribeCenBandwidthPackageAttributes&Version=2020-04-01&CenBandwidthPackageId=cbp-bp1o94dp5**** HTTP/1.1
Host: cen.byteplusapi.com
X-Date: 20260109T085330Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260109/cn-beijing/cen/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
  "ResponseMetadata": {
    "RequestId": "20250818110000064099205009C7D798",
    "Action": "DescribeCenBandwidthPackageAttributes",
    "Version": "2020-04-01",
    "Service": "cen",
    "Region": "cn-beijing"
  },
  "Result": {
    "CenBandwidthPackageId": "cbp-bp1o94dp5****",
    "CenBandwidthPackageName": "cbp-test",
    "Description": "testdesc",
    "LocalGeographicRegionSetId": "China",
    "PeerGeographicRegionSetId": "China",
    "Bandwidth": 20,
    "RemainingBandwidth": 10,
    "CenIds": [
      "cen-7qthudw0ll6jmc****"
    ],
    "Status": "Available",
    "CreationTime": "2018-04-18T15:02:37+08:00",
    "AccountId": "210000****",
    "BusinessStatus": "Normal",
    "BillingType": 1,
    "ExpiredTime": "2021-05-07 23:59:59",
    "DeletedTime": "2021-05-22 00:00:00",
    "ProjectName": "default",
    "Tags": [
      {
        "Value": "v1",
        "Key": "k1"
      }
    ],
    "UpdateTime": "2018-04-18T15:02:37+08:00",
    "LineOperator": "ChinaUnicom"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request. |This request does not contain required parameters. Ensure all required parameters are provided when initiating the request. |
|400 |InvalidParameter |A parameter specified in the request is not valid, is unsupported or cannot be used. |The request contains invalid or unsupported parameters. |
|404 |InvalidCenBandwidthPackage.NotFound |The bandwidth package of the specified geographic regions does not exist. |The specified bandwidth package does not exist. |
|500 |InternalError |Request failed with internal server error. |Internal system error. |

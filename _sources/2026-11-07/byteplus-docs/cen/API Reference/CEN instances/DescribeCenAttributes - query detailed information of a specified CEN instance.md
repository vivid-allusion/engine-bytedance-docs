---
title: "DescribeCenAttributes - query detailed information of a specified CEN instance"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/DescribeCenAttributes"
---

Call the DescribeCenAttributes API to view details of a specified CEN instance

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeCenAttributes&groupName=%E4%BA%91%E4%BC%81%E4%B8%9A%E7%BD%91%E5%AE%9E%E4%BE%8B&serviceCode=cen&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|Os3MLN">必选</span> `Example: DescribeCenAttributes`

The action to perform. Value: DescribeCenAttributes.



Version string Example: 2020\-04\-01

The API version. Value: 2020\-04\-01.



**CenId ** <span data-label="purple">string </span><span data-api-tag="require|wo3VtO">必选</span> `Example: cen-7qthudw0ll6jmc****`

The ID of the CEN instance to view.

You can call the [DescribeCens](https://docs.byteplus.com/en/docs/cen/DescribeCens) interface to query the CEN instance ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**CenId ** <span data-label="purple">string </span>`Example value: cen-7qthudw0ll6jmc****`

ID of the CEN instance.



**CenName ** <span data-label="purple">string </span>`Example: cen-test`

Name of the CEN instance.



**AccountId ** <span data-label="purple">string </span>`Example: 210000****`

Account ID of the CEN instance owner.



**Description ** <span data-label="purple">string </span>`Example value: ThisIsAsSampleDescription`

Description of the CEN instance.



**CreationTime ** <span data-label="purple">string </span>`Example value: 2021-04-09T08:36:47+08:00`

Time when the CEN instance was created.



**UpdateTime ** <span data-label="purple">string </span>`Example value: 2021-04-10T09:18:28+08:00`

Time when the CEN instance was updated.



**Status ** <span data-label="purple">string </span>`Example: Available`

Status of the CEN instance.


* Creating

* Deleting

* Pending: In the configuring process.

* Available



**CenBandwidthPackageIds ** <span data-label="purple">string[] </span>`Example value: cbp-4c2zaavbvh5fx****`

Bandwidth Package ID.



**ProjectName ** <span data-label="purple">string </span>`Example: default`

Name of the project to which the CEN instance belongs.



**Tags ** <span data-label="purple">object[] </span>`Example value: --`

Tag information.


**Value ** <span data-label="purple">string </span>`Example: v1`

The tag value.



**Key ** <span data-label="purple">string </span>`Example: k1`

The tag key.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=DescribeCenAttributes&Version=2020-04-01&CenId=cen-7qthudw0ll6jmc**** HTTP/1.1
Host: cen.byteplusapi.com
X-Date: 20260109T084652Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260109/cn-beijing/cen/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
  "ResponseMetadata": {
    "RequestId": "20250818104331112082171033289258",
    "Action": "DescribeCenAttributes",
    "Version": "2020-04-01",
    "Service": "cen",
    "Region": "cn-beijing"
  },
  "Result": {
    "CenId": "cen-7qthudw0ll6jmc****",
    "CenName": "cen-test",
    "AccountId": "210000****",
    "Description": "ThisIsAsSampleDescription",
    "CreationTime": "2021-04-09T08:36:47+08:00",
    "UpdateTime": "2021-04-10T09:18:28+08:00",
    "Status": "Available",
    "CenBandwidthPackageIds": [
      "cbp-4c2zaavbvh5fx****"
    ],
    "ProjectName": "default",
    "Tags": [
      {
        "Value": "v1",
        "Key": "k1"
      }
    ]
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For more information, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error codes |Error message |Explanation |
|---|---|---|---|
|400 |InvalidParameter |A parameter specified in the request is not valid, is unsupported or cannot be used. |The request contains invalid or unsupported parameters. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request. |This request does not contain required parameters. Ensure all required parameters are provided when initiating the request. |
|404 |InvalidCen.NotFound |The specified CEN does not exist. |The specified Cloud Enterprise Network (CEN) instance does not exist. |
|500 |InternalError |Request failed with internal server error. |Internal system error. |

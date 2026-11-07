---
title: "DescribePlacementGroupDetails - Query placement group volumes"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Describeplacementgroupdetails"
---

Call DescribePlacementGroupDetails to query information about volumes attached to the storage placement group.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribePlacementGroupDetails&groupName=%E5%AD%98%E5%82%A8%E6%94%BE%E7%BD%AE%E7%BB%84&serviceCode=storage_ebs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## request parameters

Only interface\-specific request parameters and some common parameters are listed below. For more information, see [Common Parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|qYSK69">必选</span> `Example value: DescribePlacementGroupDetails`

Action to be performed: DescribePlacementGroupDetails.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|2HBWAq">必选</span> `Example: 2020-04-01`

The version of the API is: 2020\-04\-01.



**PlacementGroupId ** <span data-label="purple">string </span><span data-api-tag="require|9FGF6e">必选</span> `Example: pg-bp67acfmxazb4ph****`

Storage placement group ID.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can call the DescribePlacementGroups API operation to query storage placement group IDs.</div>




**VolumeIds.N ** <span data-label="purple">string[] </span>`Optional` `Example: vol-jv4gkgfal98bv6pz****`

Volume ID.



**PlacementSubgroupNumbers.N ** <span data-label="purple">integer[] </span>`Optional` `Example: 2`

Storage placement subgroup number.



**PageNumber ** <span data-label="purple">integer </span>`Optional` `Example: 1`

Starting page number, default is 1.



**PageSize ** <span data-label="purple">integer </span>`Optional` `Example: 15`

Page size, up to 100, default is 15.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response Parameters

Only interface\-specific response parameters are listed below. For more information, see [Response Structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**Volumes ** <span data-label="purple">object[] </span>`Example: 1`

Volume information.


**VolumeId ** <span data-label="purple">string </span>`Example: vol-jv4gkgfal98bv6pz****`

Volume ID.



**VolumeName ** <span data-label="purple">string </span>`Example: test-vol`

Cloud disk name.



**VolumeType ** <span data-label="purple">string </span>`Example: ESSD_PL0`

Cloud disk type, with the following values:


* ESSD_PL0: High\-speed SSD volume of PL0 specification.

* Extreme Speed SSD Cloud volume, FlexPL specification.



**ZoneId ** <span data-label="purple">string </span>`Example: ap-southeast-1-a`

The available zone where the volume is located.



**PlacementGroupId ** <span data-label="purple">string </span>`Example: pg-bp67acfmxazb4ph****`

Storage placement group ID.



**SubgroupNumber ** <span data-label="purple">integer </span>`Example value: 3`

Storage subgroup number.



**CreatedAt ** <span data-label="purple">string </span>`Example: 2023-07-05T15:48:58+08:00`

Volume creation time.



**UpdatedAt ** <span data-label="purple">string </span>`Example: 2023-07-05T15:48:58+08:00`

Volume modification time.




**PageNumber ** <span data-label="purple">integer </span>`Example: 1`

Number of Pages.



**PageSize ** <span data-label="purple">integer </span>`Example value: 100`

Page Size.



**TotalCount ** <span data-label="purple">integer </span>`Example value: 2`

Number of volumes



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
POST /?Action=DescribePlacementGroupDetails&Version=2020-04-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20250730T085401Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250730/ap-southeast-1/storage_ebs/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "PlacementGroupId": "1"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Back to example

```json
{
  "ResponseMetadata": {
    "RequestId": "2025073016540703420501617025****",
    "Action": "DescribePlacementGroupDetails",
    "Version": "2020-04-01",
    "Service": "storage_ebs",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "Volumes": [
      {
        "VolumeId": "vol-jv4gkgfal98bv6pz****",
        "VolumeName": "test-vol",
        "VolumeType": "ESSD_PL0",
        "ZoneId": "ap-southeast-1-a",
        "PlacementGroupId": "pg-bp67acfmxazb4ph****",
        "SubgroupNumber": 3,
        "CreatedAt": "2023-07-05T15:48:58+08:00",
        "UpdatedAt": "2023-07-05T15:48:58+08:00"
      }
    ],
    "PageNumber": 1,
    "PageSize": 100,
    "TotalCount": 1
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## error code

The following table lists error codes related to this API and its business logic. For public error codes, refer to the [Public Error Codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) documentation.


|Status code |error code |error message |Create Volume |
|---|---|---|---|
|404 |InvalidPlacementGroup.NotFound |placement group not found |Anti\-affinity group does not exist. |

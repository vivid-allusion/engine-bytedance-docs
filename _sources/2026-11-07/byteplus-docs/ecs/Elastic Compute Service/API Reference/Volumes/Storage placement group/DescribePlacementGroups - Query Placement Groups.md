---
title: "DescribePlacementGroups - Query Placement Groups"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Describeplacementgroups"
---

Call the DescribePlacementGroups API to query information about storage placement groups.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribePlacementGroups&groupName=%E5%AD%98%E5%82%A8%E6%94%BE%E7%BD%AE%E7%BB%84&serviceCode=storage_ebs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## request parameters

Below are the unique request parameters for this API and some common parameters. For more information, see [Common Parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|SgtYtr">必选</span> `Example: DescribePlacementGroups`

The operation to be performed is: DescribePlacementGroups.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|3SLol4">必选</span> `Example: 2020-04-01`

The version of the API is: 2020\-04\-01.



**ZoneId ** <span data-label="purple">string </span>`Optional` `Sample value: ap-southeast-1-a`

The availability zone where the storage placement group belongs.



**Ids.N ** <span data-label="purple">string[] </span>`Optional` `Example: pg-bp67acfmxazb4ph****`

Storage placement group ID.



**Name ** <span data-label="purple">string </span>`Optional` `Example: test-pg`

Enter the name of the placement group. Fuzzy search is supported.



**PageNumber ** <span data-label="purple">integer </span>`Optional` `Example: 1`

Starting page number, default is 1.



**PageSize ** <span data-label="purple">integer </span>`Optional` `Example: 15`

Page size, maximum is 100, default is 15.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response Parameters

Below are the unique response parameters for this API. For more information, see [Response Structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**PlacementGroups ** <span data-label="purple">object[] </span>`Example: -`

Store the placement group information


**Id ** <span data-label="purple">string </span>`Example: pg-bp67acfmxazb4ph****`

Storage Placement Group ID.



**Name ** <span data-label="purple">string </span>`Sample value: test-pg`

Storage Placement Group Name



**Description ** <span data-label="purple">string </span>`Example: testDescription`

Placement group description.



**ZoneId ** <span data-label="purple">string </span>`Example value: cn-beijing-a`

Store the zone to which the placement group belongs.



**SubgroupCount ** <span data-label="purple">integer </span>`Example: 2`

Number of storage sub\-placement groups.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The system automatically numbers placement groups in ascending order, starting at 1 and ending at the total number of placement groups.</div>




**AutoAssign ** <span data-label="purple">boolean </span>`Example value: true`

Enable the automatic assignment of storage sub\-placement groups for the volume. When this feature is enabled, the placement group is bound when you create a volume, and storage sub\-placement groups will be automatically assigned. Value descriptions are as follows:


* true: Enable automatic assignment.

* false: Do not enable automatic assignment.



**CreatedAt ** <span data-label="purple">string </span>`Example: 2023-07-05T15:48:58+08:00`

Storage placement group creation time.



**UpdatedAt ** <span data-label="purple">string </span>`Example: 2023-07-05T15:48:58+08:00`

Placement group update time.




**PageNumber ** <span data-label="purple">integer </span>`Example: 1`

Number of Pages.



**PageSize ** <span data-label="purple">integer </span>`Sample value: 100`

Page Size.



**TotalCount ** <span data-label="purple">integer </span>`Example: 3`

Number of storage placement groups.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
POST /?Action=DescribePlacementGroups&Version=2020-04-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20250730T083129Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250730/ap-southeast-1/storage_ebs/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

```


<span id=".6L-U5Zue56S65L6L"></span>
## Back to example

```json
{
  "ResponseMetadata": {
    "RequestId": "202507301631361960900521012C****",
    "Action": "DescribePlacementGroups",
    "Version": "2020-04-01",
    "Service": "storage_ebs",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "PlacementGroups": [
      {
        "Id": "pg-bp67acfmxazb4ph****",
        "Name": "test",
        "Description": "qx9xJc3zQkW",
        "ZoneId": "ap-southeast-1-a",
        "SubgroupCount": 2,
        "AutoAssign": true,
        "CreatedAt": "2023-07-05T15:48:58+08:00",
        "UpdatedAt": "2023-07-05T15:48:58+08:00"
      }
    ],
    "PageNumber": 1,
    "PageSize": 100,
    "TotalCount": 3
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## error code

The table below lists the error codes related to this interface and its business logic. For public error codes, refer to the [Public Error Code](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) documentation.


|Status code |error code |error message |Create Volume |
|---|---|---|---|
|500 |ErrUnknown |unknown error |Unknown error. |

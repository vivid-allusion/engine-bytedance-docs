---
title: "DescribeAutoSnapshotPolicy - Query automatic snapshot policy"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Describeautosnapshotpolicy"
---

Call the DescribeAutoSnapshotPolicy API to query all created automatic snapshot policies that match your criteria in a specific region.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeAutoSnapshotPolicy&groupName=%E8%87%AA%E5%8A%A8%E5%BF%AB%E7%85%A7%E7%AD%96%E7%95%A5&serviceCode=storage_ebs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## request parameters

Only unique request parameters and some common parameters for this API are listed below. For more information, see [Common Parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|v7ZeUg">必选</span> `Example: DescribeAutoSnapshotPolicy`

Operation to perform: DescribeAutoSnapshotPolicy.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|HrC4TC">必选</span> `Example value: 2020-04-01`

The version of the API is: 2020\-04\-01.



**PageSize ** <span data-label="purple">integer </span>`Optional` `Example: 10`

Page size, maximum 100; the default is 15.



**PageNumber ** <span data-label="purple">integer </span>`Optional` `Example: 1`

Starting page number, default is 1.



**TagFilters.N.Key ** <span data-label="purple">string[] </span>`Optional` `Example value: TagFilters.1.Key=tag`

Specifying the tag key when querying resources by tags. Description as follows:


* TagFilters.N.Key: `N` indicates the index number of the tag key. Value range: 1~10.

* Separate multiple tag keys using `&`. Duplicate entries are not allowed.

* If this parameter is not provided, it implies querying all tags.

* When an empty string is passed, the error code `InvalidTagFilterKey.Malformed` is returned.



**TagFilters.N.Values.N ** <span data-label="purple">string[] </span>`Optional` `Example: TagFilters.1.Values.1=tag&TagFilters.1.Values.2=test`

Specifies the tag value when querying resources by tags. Description as follows:


* TagFilters.N.Values.N: The first `N` indicates the sequence number of the tag key. Value range: 1~10.

* TagFilters.N.Values.N: The second `N` indicates the sequence number of the tag value. Value range: 1 to 3.

* Separate multiple tag values with `&`.

* If this parameter is passed in, you must first pass in `TagFilters.N.Key`.

* Not providing this parameter means querying all tag values under the same tag key.

* When an empty string is entered, it means querying tags with empty tag values.



**AutoSnapshotPolicyIds.N ** <span data-label="purple">string[] </span>`Optional` `Example: AutoSnapshotPolicyIds.1=asp-anj249wubz9kakc8**** AutoSnapshotPolicyIds.2=asp-ancejlwubz9kakc8****`

List of automatic snapshot policy IDs to query.



**ProjectName ** <span data-label="purple">string </span>`Optional` `Example: default`

The project associated with the auto snapshot policy.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response Parameters

Only unique response parameters for this API are listed below. For more information, see [Response Structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**PageSize ** <span data-label="purple">integer </span>`Example value: 15`

Page size.



**PageNumber ** <span data-label="purple">integer </span>`Example: 1`

Page number.



**TotalCount ** <span data-label="purple">integer </span>`Example value: 3`

Total number of automatic snapshot policies.



**AutoSnapshotPolicies ** <span data-label="purple">object[] </span>`Example: -`

List of automatic snapshot policies.


**AutoSnapshotPolicyId ** <span data-label="purple">string </span>`Example: asp-anj249wubz9kakc8****`

Auto snapshot policy ID.



**Status ** <span data-label="purple">string </span>`Example: /`

Reserved parameter.



**RepeatDays ** <span data-label="purple">integer </span>`Example value: 2`

Create snapshots on a daily interval, that is, create snapshots every specified number of days



**UpdatedAt ** <span data-label="purple">string </span>`Example value: 2021-06-28T15:10:47+08:00`

Last updated time of the automatic snapshot policy



**CreatedAt ** <span data-label="purple">string </span>`Example: 2021-06-28T15:10:47+08:00`

Creation time of the automatic snapshot policy



**ProjectName ** <span data-label="purple">string </span>`Example: default`

Project to which the automatic snapshot policy belongs.



**TimePoints ** <span data-label="purple">string[] </span>`Example: "2", "8", "9"`

Creation time points for automatic snapshots.



**RepeatWeekdays ** <span data-label="purple">string[] </span>`Example values: "3", "5", "7"`

Create snapshots on a weekly basis by selecting one or more days between Monday and Sunday.



**RetentionDays ** <span data-label="purple">integer </span>`Example value: 50`

The retention period for automatic snapshots, measured in days, is defined as follows:


* \-1: Save permanently.

* 1~65536: Specify the number of days to retain.



**VolumeNums ** <span data-label="purple">integer </span>`Example: 1`

Total number of volumes.



**AutoSnapshotPolicyName ** <span data-label="purple">string </span>`Example: testName`

Name of the automatic snapshot policy.



**Tags ** <span data-label="purple">object[] </span>`Example: /`

Tag.


**Key ** <span data-label="purple">string </span>`Example value: tag`

Tag key for the automatic snapshot policy.



**Value ** <span data-label="purple">string </span>`Example: test`

Tag values for automatic snapshot policy.





&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
GET /?Action=DescribeAutoSnapshotPolicy&Version=2020-04-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
ServiceName: storage_ebs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Back to example

```text
{
    "ResponseMetadata": {
        "RequestId": "2022050518000501021206303202BF****",
        "Action": "DescribeAutoSnapshotPolicy",
        "Version": "2020-04-01",
        "Service": "storage_ebs",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "AutoSnapshotPolicies": [
            {
                "AccountId": "200000****",
                "AutoSnapshotPolicyId": "asp-anj1nuju6w9gsaqi****",
                "AutoSnapshotPolicyName": "modify_****autosanpshot_policy",
                "CreatedAt": "2022-04-28T18:46:36+08:00",
                "ProjectName": "default",
                "RepeatWeekdays": [
                    "3",
                    "5",
                    "7"
                ],
                "RetentionDays": 50,
                "Status": "",
                "TimePoIntegers": [
                    "2",
                    "8",
                    "9"
                ],
                "UpdatedAt": "2022-04-28T18:46:37+08:00",
                "VolumeNums": 0
            },
            {
                "AccountId": "200000****",
                "AutoSnapshotPolicyId": "asp-anj2a9gwj49gsbso****",
                "AutoSnapshotPolicyName": "****test",
                "CreatedAt": "2022-04-28T14:49:01+08:00",
                "ProjectName": "",
                "RepeatWeekdays": [
                    "1"
                ],
                "RetentionDays": -1,
                "Status": "",
                "TimePoIntegers": [
                    "0"
                ],
                "UpdatedAt": "2022-04-28T14:49:01+08:00",
                "VolumeNums": 0
            }
        ],
        "PageNumber": 1,
        "PageSize": 10,
        "RequestId": "2022050518000501021206303202BFE158-cc****",
        "TotalCount": 2
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## error code

The table below lists the error codes related to business logic for this API. For public error codes, see the [Public Error Codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) documentation.


|Status code |error code |error message |Create Volume |
|---|---|---|---|
|400 |InvalidRequest |The operation is not permitted due to the request is invalid. |Invalid request. |
|400 |ErrMaximumTagFilterKeys |too many tag filter keys |The tag filter key exceeds the limit |
|400 |ErrTagFilterKeyConflict |tag filter key conflict |Label filter key conflict. |
|400 |ErrInvalidTagFilterKey |tag filter key invalid |Tag filter key is invalid |
|400 |ErrMaximumTagFilterValues |too many tag filter value |Tag filter value exceeds the limit |
|400 |ErrInvalidTagFilterValue |tag filter value invalid |Tag filter value is invalid. |
|400 |ErrInvalidAccountId |account id invalid |Account ID is invalid |

---
title: "DescribeSnapshotsUsage - Query snapshot usage"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DescribeSnapshotsUsage"
---

Call the DescribeSnapshotsUsage API to query snapshot usage.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeSnapshotsUsage&groupName=%E5%BF%AB%E7%85%A7&serviceCode=storage_ebs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## request parameters

Only unique request parameters for this API and some common parameters are listed below. For more information, see [Common Parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|rbjTnH">必选</span> `Example value: DescribeSnapshotsUsage`

The action to be performed: DescribeSnapshotsUsage.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|VYWd4i">必选</span> `Example value: 2020-04-01`

The version of the API is: 2020\-04\-01.



**RegionId ** <span data-label="purple">string </span><span data-api-tag="require|DBLDXy">必选</span> `Example value: cn-beijing`

ID of the region to query.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the unique response parameters for this API are listed below. For more information, see [Response Structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**SnapshotSize ** <span data-label="purple">long </span>`Example value: 264960475136`

Total snapshot capacity, measured in bytes.



**SnapshotCount ** <span data-label="purple">integer </span>`Example value: 5`

Total number of snapshots.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
GET /?Action=DescribeSnapshotsUsage&Version=2020-04-01&RegionId=ap-southeast-1 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
ServiceName: storage_ebs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Back to example

```json
{
  "ResponseMetadata": {
    "RequestId": "20260107162925096024223194DB****",
    "Action": "DescribeSnapshotsUsage",
    "Version": "2020-04-01",
    "Service": "storage_ebs",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "SnapshotSize": 264960475136,
    "SnapshotCount": 5
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## error code

The following table lists error codes related to this API and its business logic. For common error codes, see the [Public Error Codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) documentation.


|Status code |error code |error message |Create Volume |
|---|---|---|---|
|400 |InvalidParameters |The request has invalid parameters. |The request contains invalid parameters. |
|400 |ErrInvalidAccountId |account id invalid |Account ID is invalid. |
|400 |SnapshotServiceNonactivated |Snapshot service is nonactivated, need activate snapshot service from user console. |Snapshot service is not activated. Please activate it in the user console. |
|500 |InternalError |An internal error has occurred. |Internal error. Please try again. If multiple attempts fail, submit a ticket. |

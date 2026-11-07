---
title: "DescribeSnapshotChains - Query snapshot chains"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Describesnapshotchains"
---

Call the DescribeSnapshotChains API to query snapshot chains.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeSnapshotChains&groupName=%E5%BF%AB%E7%85%A7&serviceCode=storage_ebs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## request parameters

Below are request parameters unique to this API and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|4Fy9da">必选</span>`Example value: DescribeSnapshotChains`

The action to be performed: DescribeSnapshotChains.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|axCwGb">必选</span> `Example value: 2020-04-01`

The version of the API is: 2020\-04\-01.



**PageSize ** <span data-label="purple">integer </span>`Optional` `Example: 10`

Page size, default is 10.



**PageNumber ** <span data-label="purple">integer </span>`Optional` `Example value: 1`

Starting page, default is 1.



**VolumeIds.N ** <span data-label="purple">string[] </span>`Optional` `Example value: VolumeIds.1=vol-3tiz8tg97u3vj0x0****`

Volume ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Below are response parameters unique to this API. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**PageSize ** <span data-label="purple">integer </span>`Example: 1`

Page Size.



**PageNumber ** <span data-label="purple">integer </span>`Example value: 10`

Page number.



**TotalCount ** <span data-label="purple">integer </span>`Example value: 1`

Total number of snapshot chains.



**SnapshotChains ** <span data-label="purple">object[] </span>`Example: -`

Snapshot chain details.


**SnapshotChainId ** <span data-label="purple">string </span>`Example: sc-3w7fo5l5e24l9237****`

Snapshot chain ID.



**VolumeId ** <span data-label="purple">string </span>`Example value: vol-lqoao69a4kg9jt24****`

The volume ID associated with the snapshot chain.



**SnapshotSize ** <span data-label="purple">long </span>`Example value: 100`

Total snapshot capacity in the chain, measured in bytes.



**SnapshotCount ** <span data-label="purple">integer </span>`Example: 1`

Total number of snapshots in the snapshot chain.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
GET /?Action=DescribeSnapshotChains&VolumeIds.1=vol-xxx&Version=2020-04-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
ServiceName: storage_ebs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Back to example

```json
{
  "ResponseMetadata": {
    "RequestId": "20260107162356005087167215E****",
    "Action": "DescribeSnapshotChains",
    "Version": "2020-04-01",
    "Service": "storage_ebs",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "PageSize": 10,
    "PageNumber": 1,
    "TotalCount": 1,
    "SnapshotChains": [
      {
        "SnapshotChainId": "sc-3w7fo5l5e24l9237****",
        "VolumeId": "vol-xxx",
        "SnapshotSize": 100,
        "SnapshotCount": 1
      }
    ]
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## error code

The table below lists error codes related to this API and its business logic. For common error codes, see the [public error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) documentation.


|Status code |error code |error message |Create Volume |
|---|---|---|---|
|400 |InvalidRequest |The operation is not permitted due to the request is invalid. |Invalid request. |
|400 |AccountIdNotMatched |The specified account ID does not match. |User ID does not match. |
|403 |OperationNotAllowed |The operation is not allowed. |This operation is not allowed. |
|404 |VolumeNotFound |The specified volume does not exist. |Volume does not exist. |

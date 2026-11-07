---
title: "DeleteAutoSnapshotPolicy - Delete automatic snapshot policy"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Deleteautosnapshotpolicy"
---

Use the DeleteAutoSnapshotPolicy API to delete an automatic snapshot policy.

<span id=".5rOo5oSP5LqL6aG5"></span>
## precautions


* If the target automatic snapshot policy has been applied to volumes, deleting the policy stops those volumes from executing it.

* After deleting the automatic snapshot policy, existing automatic snapshots are not affected.


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DeleteAutoSnapshotPolicy&groupName=%E8%87%AA%E5%8A%A8%E5%BF%AB%E7%85%A7%E7%AD%96%E7%95%A5&serviceCode=storage_ebs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## request parameters

Only the unique request parameters for this API and some common parameters are listed below. For more information, see [Common Parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|m1YcAH">必选</span>`Example value: DeleteAutoSnapshotPolicy`

The operation to perform: DeleteAutoSnapshotPolicy.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|8nsnoV">必选</span> `Example value: 2020-04-01`

The version of the API is: 2020\-04\-01.



**AutoSnapshotPolicyId ** <span data-label="purple">string </span><span data-api-tag="require|0bd4YE">必选</span> `Example value: asp-anj249wubz9kakc8****`

The automatic snapshot policy ID to be deleted.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response Parameters

This API does not have specific return parameters. For more information, see [Return Structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
GET /?Action=DeleteAutoSnapshotPolicy&AutoSnapshotPolicyId=asp-anj249wubz9kakc8****&Version=2020-04-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
ServiceName: storage_ebs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Back to example

```json
{
    "ResponseMetadata": {
        "RequestId": "2022050519544301021215003413BD****",
        "Action": "DeleteAutoSnapshotPolicy",
        "Version": "2020-04-01",
        "Service": "storage_ebs",
        "Region": "ap-southeast-1"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## error code

The table below lists error codes related to this API and business logic. For common error codes, see the [Public Error Codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) documentation.


|Status code |error code |error message |Create Volume |
|---|---|---|---|
|400 |InvalidRequest |The operation is not permitted due to the request is invalid. |Invalid request. |
|400 |AccountIdNotMatched |The specified account ID does not match. |User ID does not match. |
|500 |InternalError |An internal error has occurred. |Internal error. Try again. If the problem persists after multiple attempts, submit a ticket. |

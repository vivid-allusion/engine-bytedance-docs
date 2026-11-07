---
title: "DeleteSnapshotGroup - Delete snapshot consistency group"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DeleteSnapshotGroup"
---

Call the DeleteSnapshotGroup interface to delete a snapshot consistency group.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DeleteSnapshotGroup&groupName=%E5%BF%AB%E7%85%A7%E4%B8%80%E8%87%B4%E6%80%A7%E7%BB%84&serviceCode=storage_ebs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## request parameters

The section below lists only request parameters specific to this interface and some common parameters. For more information, see [Common Parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|h8IeVU">必选</span>`Example: DeleteSnapshotGroup`

The operation to perform is: DeleteSnapshotGroup.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|4Q1O4f">必选</span> `Example value: 2020-04-01`

The version of the API is: 2020\-04\-01.



**SnapshotGroupId**<span data-label="purple">string</span><span data-api-tag="require|axWPe8">必选</span>`Example: sg-bp1s5fnvk4gn2****`

Snapshot Consistency Group ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response Parameters

This interface does not have any specific response parameters. For more information, see [Response Structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
GET /?Action=DeleteSnapshotGroup&Version=2020-04-01&SnapshotGroupId=sg-bp1s5fnvk4gn2**** HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
ServiceName: storage_ebs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Back to example

```json
{
    "ResponseMetadata": {
        "RequestId": "2022050520060001021207006918C1****",
        "Action": "DeleteSnapshotGroup",
        "Version": "2020-04-01",
        "Service": "storage_ebs",
        "Region": "ap-southeast-1"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## error code

The table below lists error codes related to the interface and business logic. For public error codes, see the [Public Error Codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) documentation.


|Status code |error code |error message |Create Volume |
|---|---|---|---|
|400 |IncorrectSnapshotStatus |The specified snapshot status is invalid. |The specified snapshot status is invalid. |
|400 |SnapshotGroupCRRCopying |The snapshot consistency group is being replicated across region and cannot be deleted. |The snapshot consistency group is being replicated across regions and cannot be deleted. |
|403 |SnapshotBindingImageForbiddenDelete |The snapshot is bound to a mirror and cannot be deleted. |This snapshot is associated with an image and cannot be deleted. |
|403 |SnapshotGroupBindingImageForbiddenDelete |The snapshot consistency group is bound to a mirror and cannot be deleted. |This snapshot consistency group is associated with an image and cannot be deleted. |
|404 |InvalidSnapshotGroup.NotFound |The specified snapshot group does not exist. |Snapshot group does not exist. |
|500 |InternalError |An internal error has occurred. |Internal error. Try again. If multiple attempts fail, submit a ticket. |

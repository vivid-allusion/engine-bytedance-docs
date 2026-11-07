---
title: "ModifySnapshotGroup - Modify snapshot consistency group properties"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/ModifySnapshotGroup"
---

Call the ModifySnapshotGroup interface to edit the snapshot consistency group.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=ModifySnapshotGroup&groupName=%E5%BF%AB%E7%85%A7%E4%B8%80%E8%87%B4%E6%80%A7%E7%BB%84&serviceCode=storage_ebs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## request parameters

Only parameters specific to this interface and selected common parameters are listed below. For more information, see [Common Parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|5X6qz8">必选</span> `Example value: ModifySnapshotGroup`

The operation to perform: ModifySnapshotGroup.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|xKI6vM">必选</span> `Example value: 2020-04-01`

The version of the API is: 2020\-04\-01.



**SnapshotGroupId ** <span data-label="purple">string </span><span data-api-tag="require|kXztWT">必选</span> `Example value: sg-bp1s5fnvk4gn2tws0****`

Snapshot Consistency Group ID.



**Name**<span data-label="purple">string</span>`Optional` `Example value: testSnapshotName`

Snapshot consistency group name, description as follows:


* It can only start with Chinese characters, letters, or an underscore (_).

* Only Chinese characters, letters, numbers, underscores (_), hyphens (\-), and periods (.) are allowed.

* The length limit is 1 to 128 characters.



**Description ** <span data-label="purple">string </span>`Optional` `Example value: testDescription`

Description of the snapshot consistency group is as follows:


* It can only start with Chinese characters, letters, or an underscore (_).

* Only Chinese characters, letters, numbers, underscores (_), hyphens (\-), and periods (.) are allowed.

* The length limit is 1 to 255 characters.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response Parameters

This interface does not have specific response parameters. For more information, see [Response Structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
GET /?Action= ModifySnapshotGroup&Version=2020-04-01&SnapshotGroupId=sg-7e2gbxchg89jwlcg****&Name=test-name&Description=test-desc HTTP/1.1
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
        "Action": "ModifySnapshotGroup",
        "Version": "2020-04-01",
        "Service": "storage_ebs",
        "Region": "ap-southeast-1"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## error code

The following table lists the error codes related to the interface and business logic. For public error codes, see the [Public Error Codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) document.


|Status code |error code |error message |Create Volume |
|---|---|---|---|
|400 |InvalidRequest |The operation is not permitted due to the request is invalid. |Invalid request. |
|403 |InvalidParameter.Name |The specified name is invalid. |The specified name format is invalid. |
|403 |InvalidParameter.Description |The specified description is invalid. |Specified description format is invalid. |
|404 |InvalidSnapshotGroup.NotFound |The specified snapshot group does not exist. |The snapshot group does not exist. |
|500 |InternalError |An internal error has occurred. |Internal error. Try again. If you continue to experience issues, submit a ticket. |

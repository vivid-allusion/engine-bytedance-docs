---
title: "ModifySnapshotAttribute - Modify snapshot properties"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Modifysnapshotattribute"
---

Use the ModifySnapshotAttribute API to change snapshot properties. You can currently update the snapshot name, description, and retention period.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=ModifySnapshotAttribute&groupName=%E5%BF%AB%E7%85%A7&serviceCode=storage_ebs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## request parameters

Below are the request parameters specific to this API, along with some public parameters. For more information, see [public parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|c5NLYU">必选</span> `Example value: ModifySnapshotAttribute`

Action to perform: ModifySnapshotAttribute.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|3CnMG7">必选</span> `Example value: 2020-04-01`

The version of the API is: 2020\-04\-01.



**SnapshotName ** <span data-label="purple">string </span>`Optional` `Example value: testSnapshotName`

Snapshot naming rules are as follows:


* Length must be between 1 to 128 characters.

* Only Chinese characters, letters, numbers, underscores (_), hyphens (\-), and periods (.) are allowed.

* To avoid conflicts with the names of automatic snapshots, the name cannot start with "auto".



**Description ** <span data-label="purple">string </span>`Optional` `Example value: testDescription`

Snapshot description, length 0–255 characters.



**RetentionDays ** <span data-label="purple">integer </span>`optional` `Example value: 10`

Extend the snapshot retention period. The snapshot retention period can only be extended, not shortened. The valid range is N+1 to 65,536, where N is the retention period set when the snapshot was created.



**SnapshotId ** <span data-label="purple">string </span><span data-api-tag="require|dft9bi">必选</span> `Example value: snap-31akybwsxi8rudc6****`

ID of the snapshot to be updated.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have any unique response parameters. For more information, see [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
GET /?Action=ModifySnapshotAttribute&Description=testDescription&SnapshotId=snap-31akybwsxi8rudc6****&SnapshotName=testSnapshotName&Version=2020-04-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
ServiceName: storage_ebs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Back to example

```text
{
        "ResponseMetadata": {
                "RequestId": "20220308180931010225243139000DF***",
                "Action": "ModifySnapshotAttribute",
                "Version": "2020-04-01",
                "Service": "storage_ebs",
                "Region": "ap-southeast-1"
        },
        "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## error code

The following table lists error codes related to this API and its business logic. For general error codes, refer to the [Public Error Codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) documentation.


|Status code |error code |error message |Create Volume |
|---|---|---|---|
|400 |InvalidParameter |The parameter {{param}} is invalid. |Parameter {{param}} is invalid. |
|400 |NotAllowed.PermanentSnapshot |This operation is not supported for permanent snapshots. |Permanently saved snapshots do not support this operation. |
|409 |LessThanCurrent.RetentionDays |The retention days should be greater than the current value. |The retention period must be greater than the current value. |

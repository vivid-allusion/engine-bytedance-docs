---
title: "ModifyAutoSnapshotPolicy - Edit automatic snapshot policy attributes"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Modifyautosnapshotpolicy"
---

Call the ModifyAutoSnapshotPolicy operation to update an automatic snapshot policy. After modifying the automatic snapshot policy, the volumes previously using this policy will immediately switch to the updated automatic snapshot policy.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=ModifyAutoSnapshotPolicy&groupName=%E8%87%AA%E5%8A%A8%E5%BF%AB%E7%85%A7%E7%AD%96%E7%95%A5&serviceCode=storage_ebs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## request parameters

Below are the request parameters specific to this operation, along with some common parameters. For more information, see [Public Parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|l8Qikl">必选</span> `Example value: ModifyAutoSnapshotPolicy`

Operation to perform: ModifyAutoSnapshotPolicy.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|1zhwB4">必选</span> `Example value: 2020-04-01`

The version of the API is: 2020\-04\-01.



**AutoSnapshotPolicyName ** <span data-label="purple">string </span>`optional` `Example value: testName`

Auto snapshot policy name. Naming guidelines are as follows:


* The first character can only be a Chinese character, letter, or underscore (_).

* Can contain Chinese characters, letters, numbers, underscores (_), or hyphens (\-).

* The length must be between 1 and 128 characters.



**TimePoints.N ** <span data-label="purple">string[] </span>`Optional` `Example value: TimePoIntegers.1=0&TimePoIntegers.2=1`

Automatic snapshot creation times are described as follows:


* Use UTC+8; the unit is hour.

* Valid values: 0~23, representing 00:00 to 23:00. For example, `1` means 01:00.

* If you need to create automatic snapshots multiple times in a day, you can provide multiple time points, up to 24.



**RepeatWeekdays.N ** <span data-label="purple">string[] </span>`Optional` `Example value: RepeatWeekdays.1=1&RepeatWeekdays.2=7`

Create snapshots on a repeating weekly schedule by selecting one or more days from Monday to Sunday. Description as follows:


* The value ranges from 1 to 7. For example, 1 represents Monday.

* If you need to create multiple automatic snapshots in one week, you can enter several time points, up to a maximum of 7.



**RepeatDays ** <span data-label="purple">integer </span>`Optional` `Example value: 2`

Create snapshots at daily intervals, with a specified number of days between each snapshot, ranging from 1 to 30.

After you change the `RepeatDays` of an automatic snapshot policy, the day the change is made is considered day one.



**RetentionDays ** <span data-label="purple">integer </span>`Optional` `Example value: 30`

The retention period for automatic snapshots, measured in days. Changing the retention period will not affect historical snapshots and only applies to new snapshots.

Value descriptions are as follows:


* \-1: Permanently retained.

* 1~65536: Specifies the number of days to retain.



**AutoSnapshotPolicyId ** <span data-label="purple">string </span><span data-api-tag="require|qRpUqy">必选</span> `Example value: asp-anj249wubz9kakc8****`

ID of the automatic snapshot policy to modify.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response Parameters

This operation does not have unique response parameters. For more information, see [Response Structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
GET /?Action=ModifyAutoSnapshotPolicy&AutoSnapshotPolicyId=asp-anj249wubz9kakc8****&AutoSnapshotPolicyName=testName&Version=2020-04-01&TimePoints.1=0&TimePoints.2=1&RepeatWeekdays.1=1&RepeatWeekdays.2=7 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
ServiceName: storage_ebs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Back to example

```json
{
    "ResponseMetadata": {
        "RequestId": "2022050519574501021219921217C2****",
        "Action": "ModifyAutoSnapshotPolicy",
        "Version": "2020-04-01",
        "Service": "storage_ebs",
        "Region": "ap-southeast-1"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## error code

The table below lists error codes related to the interface and business logic. For common error codes, refer to the [Public Error Codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) documentation.


|Status code |error code |error message |Create Volume |
|---|---|---|---|
|400 |InvalidParameters |The request has invalid parameters. |The request contains invalid parameters. |
|400 |InvalidSnapshotPolicyNameLen |The length of the automatic snapshot policy name is invalid. |The automatic snapshot policy name length is invalid. |
|400 |InvalidSnapshotPolicyNameFormat |The format of the automatic snapshot policy name is invalid. |The format of the automatic snapshot policy name is invalid. |
|400 |ErrInvalidTimePoints |The specified time point is invalid. |The specified time point is invalid. |
|400 |InvalidRepeatDays |The specified period days is invalid. |The specified recurrence period is invalid. |
|400 |ErrInvalidRepeatWeekDays |The specified repeat weekdays is invalid. |The specified recurrence period is invalid. |

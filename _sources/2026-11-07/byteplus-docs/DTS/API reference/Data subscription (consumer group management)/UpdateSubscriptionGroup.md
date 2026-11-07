---
title: "UpdateSubscriptionGroup"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/updatesubscriptiongroup"
---

Call the UpdateSubscriptionGroup API to modify subscription consumer group name information.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|TaskId |String |Yes |4ddec6d036384248a25862fb\*\*\*\*\*\*\*\* |Task ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/DTS/describetransmissiontasks">DescribeTransmissionTasks</a> API to query the task ID.</div><br> |
|GroupName |String |Yes |testgroup |Consumer group name<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/DTS/describesubscriptiongroups">DescribeSubscriptionGroups</a> API to query the subscription consumer group list.</div><br> |
|Username |String |Yes |testname |Set the consumer group account. Naming rules:<br><br><br>* The length must be between 2 and 16 characters.<br><br>* The name must start with a letter and end with a letter or a digit.<br><br>* It consists of numbers, uppercase letters, lowercase letters, and underscores (_). |
|Password |String |Yes |Admin@123\*\*\* |Set the account and password of consumer group. Password rule:<br><br><br>* The length must be between 8 and 32 characters.<br><br>* It contains at least three of the following: uppercase letters, lowercase letters, digits, and special characters. Special characters are `_#!@$%^&*()+=-`. |
|Description |String |No |Description |The description of the consumer group helps you identify the purpose of the consumer group. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
POST /?Action=UpdateSubscriptionGroup&Version=2022-10-01 HTTP/1.1
Content-Type: application/json
Host: dts.cn-beijing.byteplusapi.com.cn
X-Date: 20221001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20221001/cn-beijing/dts/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "TaskId": "9863318d02ed4a6f88f14c03a2*****",
    "GroupName": "9863318d02ed4a6f88f14c03a28c5b6c:test****123",
    "Username": "test****123",
    "Password": "Admin123"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230320110450E791F4A3C770E90E5239",
        "Action": "UpdateSubscriptionGroup",
        "Version": "2022-10-01",
        "Service": "dts",
        "Region": "cn-beijing"
    },
    "Result": null
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/DTS/error_codes).

---
title: "AddTagsToResource"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/addtagstoresource"
---

Call AddTagsToResource to add tags to a task.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|TaskIds |Array of String |Yes |[ "18064de5e9d345dc965ee45217\*\*\*\*\*\*" ] |The task ID that needs to add a tag.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You can call <a href="https://docs.byteplus.com/en/docs/DTS/describetransmissiontasks">DescribeTransmissionTasks</a> API to view the task ID.</div><br><br><br>* <div data-tips="true" data-tips-type="default">You can specify multiple instance IDs, separated by commas (,). You can specify up to 20 instance IDs at a time.</div><br> |
|Tags |Array of [TagObject](https://docs.byteplus.com/en/docs/57/15981#tagobject) |Yes |```json```<br>```[```<br>```    {```<br>```        "Key":"key1",```<br>```        "Value":"value1"```<br>```    }```<br>```]```<br> |Tag list information.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You can specify multiple tag key\-value pairs, and separate by commas (,).</div><br><br><br>* <div data-tips="true" data-tips-type="default">You can specify up to 20 tag keys at a time. A maximum of 50 tags can be associated with a single task.</div><br> |


<span id="tagobject"></span>
### TagObject


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|Key |String |Yes |key1 |Tag key information. The configuration specifications are as follows:<br><br><br>* Supports any language, characters, numbers, spaces, or symbols (`_.:/=+-@`).<br><br>* Case\-sensitive, and the length is 1 to 128 characters.<br><br>* In UTF\-8 encoded Unicode format.<br><br>* Keys cannot start with any form of `volc:`, such as `Volc:` or `VOLC:`. |
|Value |String |Yes |value1 |Tag value information. The configuration specifications are as follows:<br><br><br>* Supports any language, character, digit, space, or symbol (`_.:/=+-@`).<br><br>* Case\-sensitive, and the length is 0 to 256 characters.<br><br>* In UTF\-8 encoded Unicode format. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Return parameters

Null.

null

<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
POST /?Action=AddTagsToResource&Version=2022-10-01 HTTP/1.1
Content-Type: application/json
Host: dts.cn-beijing.byteplusapi.com.cn
X-Date: 20221001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20221001/cn-beijing/dts/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "TaskIds": [
        "18064de5e9d345dc965ee45217******"
    ],
    "Tags": [
        {
            "Key": "key1",
            "Value": "value1"
        }
    ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230414161942CD08B59CEB1E16301017",
        "Action": "AddTagsToResource",
        "Version": "2022-10-01",
        "Service": "dts",
        "Region": "cn-beijing"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/DTS/error_codes).

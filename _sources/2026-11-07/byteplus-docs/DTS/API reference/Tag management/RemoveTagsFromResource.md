---
title: "RemoveTagsFromResource"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/removetagsfromresource"
---

Call the RemoveTagsFromResource API to disassociate the task tag.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|TaskIds |Array of String |Yes |[ "18064de5e9d345dc965ee45217\*\*\*\*\*\*" ] |List of task ID information. A maximum of 20 task IDs can be passed in at one time. |
|TagKeys |Array of String |Yes |["key1"] |The list information of the key to be deleted.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can specify multiple tag keys, separated by commas (,). You can specify up to 20 tag keys at a time.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
POST /?Action=RemoveTagsFromResource&Version=2022-10-01 HTTP/1.1
Content-Type: application/json
Host: dts.cn-beijing.byteplusapi.com.cn
X-Date: 20221001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20221001/cn-beijing/dts/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "TaskIds": [
        "18064de5e9d345dc965ee45217******"
    ],
    "TagKeys": [
        "key1"
    ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202304141636586F57F2F8F23AD2301B10",
        "Action": "RemoveTagsFromResource",
        "Version": "2022-10-01",
        "Service": "dts",
        "Region": "cn-shanghai"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/DTS/error_codes).

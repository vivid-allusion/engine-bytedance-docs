---
title: "DescribeTagsByResource"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/describetagsbyresource"
---

Call DescribeTagsByResource to query the tags of a task.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|TaskIds |Array of String |Yes |[ "18064de5e9d345dc965ee45217\*\*\*\*\*\*" ] |List of task ID information. You can specify up to 20 task IDs at a time. |
|PageNumber |Integer |No |1 |Page number. The value range is 1 to 1000, with a default of 1. |
|PageSize |Integer |No |10 |Number of records per page. The value range is 1 to 1000, with a default of 10. |
|TagFilters |Array of [TagFilterObject](https://docs.byteplus.com/en/docs/57/15980#tagfilterobject) |No |```json```<br>```[```<br>```    {```<br>```        "Key":"key1",```<br>```        "Value":"value1"```<br>```    }```<br>```]```<br> |Task tag information.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">When this parameter is set, the tag information of the specified tag under the specified task will be returned.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If this parameter is not set, all tag information under the specified task is returned by default.</div><br> |


<span id="tagfilterobject"></span>
### TagFilterObject


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|Key |String |Yes |key1 |Tag keys for querying and filtering.<br><br><br>* This parameter is required if you want to use tags to query and filter instances.<br><br>* Duplicate tag keys are allowed.<br><br>* A maximum of 10 tags can be passed in for query and filter at one time. |
|Value |String |No |value1 |Tag value corresponding to the tag key used for query filtering.<br><br><br>* If this parameter is left empty, it means that there is no restriction on the tag value, and all instances bound to the specified tag key will be filtered.<br><br>* If an empty string is passed in, it means filtering instances with empty tag values under the corresponding tag key. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Return parameters

Null.


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Total |Integer |1 |Total number of tags. |
|ResourceTags |Array of [ResourceTag](https://docs.byteplus.com/en/docs/57/15980#resourcetag) |```json```<br>```[```<br>```    {```<br>```        "Key":"key1",```<br>```        "TaskId":"18064de5e9d345dc965ee45217******",```<br>```        "Value":"value1"```<br>```    }```<br>```]```<br> |Task tag list information. |


<span id="resourcetag"></span>
### ResourceTag


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|TaskId |String |18064de5e9d345dc965ee45217\*\*\*\*\*\* |Task ID of the task bound with the tag specified by key and value. |
|Key |String |key1 |The tag Key bound to the task. |
|Value |String |value1 |The tag value bound to the task. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
POST /?Action=DescribeTagsByResource&Version=2022-10-01 HTTP/1.1
Content-Type: application/json
Host: dts.cn-beijing.byteplusapi.com.cn
X-Date: 20221001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20221001/cn-beijing/dts/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "TaskIds": ["18064de5e9d345dc965ee45217******"],
    "TagFilters": [
    {
      "Key": "key1",
      "Value": "value1"
    }
  ],
    "PageNumber":1,
    "PageSize":10
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2023041416325819C8523905F879303A46",
        "Action": "DescribeTagsByResource",
        "Version": "2022-10-01",
        "Service": "dts",
        "Region": "cn-shanghai"
    },
    "Result": {
        "ResourceTags": [
            {
                "Key": "key1",
                "TaskId": "18064de5e9d345dc965ee45217******",
                "Value": "value1"
            }
        ],
        "Total": 1
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/DTS/error_codes).

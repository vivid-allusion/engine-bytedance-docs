---
title: "AddTagsToResource"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/AddTagsToResource"
---

Call the AddTagsToResource to associate tags to one or more instances.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=AddTagsToResource&serviceCode=vedbm&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceIds |Array of String |Yes |["vedbm\-r3xq0zdl\*\*\*\*"] |The ID of the instance to add a tag to.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances">DescribeDBInstances</a> API to query the basic information of all instances in the target region, including their instance IDs.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Each time, you can pass up to 20 instance IDs simultaneously, and each instance can bind up to 50 tags.</div><br> |
|Tags |Array of [TagObject](https://docs.byteplus.com/en/docs/265/57363#tagobject) |Yes |See the request example. |An array object of tag keys and tag values to be bound.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">A single request supports up to 20 tag key\-value pairs, and a single instance can be bound with a maximum of 50 tags.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The tag key value must meet certain setting rules. For details, please refer to the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/Tag_overview#.5qCH562-6K6-572u6KeE5YiZ">Tag setting rules</a>.</div><br> |


<span id="tagobject"></span>
### TagObject


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|Key |String |Yes |department |Tag key bound to the instance. |
|Value |String |No |game |Tag value bound to the instance. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```JSON
POST /?Action=AddTagsToResource&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host:vedbm.cn-beijing.byteplusapi.com.cn
X-Date: 20220101T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20220101/cn-beijing/vedbm/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "InstanceIds": [
        "vedbm-d6rjf5ln****"
    ],
    "Tags": [
        {
            "Key": "chargetype",
            "Value": "prepaid"
        },
        {
            "Key": "instancetype",
            "Value": "cluster"
        }
    ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2023080110185134A93678651E064D4350",
        "Action": "AddTagsToResource",
        "Version": "2022-01-01",
        "Service": "vedbm",
        "Region": "cn-beijing"
    },
    "Result": null
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Error_codes).

---
title: "RemoveTagsFromResource"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/RemoveTagsFromResource"
---

Call the RemoveTagsFromResource to disassociate tags from one or more instances.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=RemoveTagsFromResource&serviceCode=vedbm&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceIds |Array of String |Yes |["vedbm\-r3xq0zdl\*\*\*\*"] |The instance ID for which the tag needs to be removed.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances">DescribeDBInstances</a> API to query the basic information of all instances in the target region, including their instance IDs.</div><br><br><br>* <div data-tips="true" data-tips-type="default">A maximum of 20 instance IDs can be passed in at a time.</div><br> |
|TagKeys |Array of String |No |["instancetype", "chargetype"] |The tag keys to remove.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">A single request can include a maximum of 20 tag keys.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When <code>InstanceIds</code> contains multiple instance IDs, tags with the provided tag keys will be removed from all of them. Proceed with caution.</div><br> |
|All |Boolean |No |false |Whether to remove all tags on the specified instance. Value range:<br><br><br>* `true`: remove all tags from the specified instance.<br><br>* `false`: do not remove all tags from the specified instance (default).<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The <code>All</code> parameter takes effect only when <code>TagKeys</code> is empty.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```JSON
POST /?Action=RemoveTagsFromResource&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host:vedbm.cn-beijing.byteplusapi.com.cn
X-Date: 20220101T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20220101/cn-beijing/vedbm/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "InstanceIds": [
        "vedbm-d6rjf5ln****"
    ],
    "TagKeys": [
        "chargetype",
        "instancetype"
    ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2023080110134234A93678651E064CCD04",
        "Action": "RemoveTagsFromResource",
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

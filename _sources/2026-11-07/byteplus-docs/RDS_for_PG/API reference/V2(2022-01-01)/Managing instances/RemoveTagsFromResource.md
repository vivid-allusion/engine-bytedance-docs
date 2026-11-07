---
title: "RemoveTagsFromResource"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/removetagsfromresource"
---

Call the RemoveTagsFromResource API to remove tags from an instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|InstanceIds |Array of String |Yes |["postgres\-da8f12d3\*\*\*\*", "postgres\-6b40e576\*\*\*\*"] |Instance IDs that need to remove tag.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can specify up to 20 instance IDs at a time.</div><br> |
|TagKeys |Array of String |No |["key1", "key2"] |Key of the tag to be removed.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">It supports passing in the keys of multiple tags at once for batch unbinding. Remove up to 20 tags at a time.</div><br> |
|All |Boolean |No |false |Whether to remove all tags from the resource. Range:<br><br><br>* `true`: remove all tags.<br><br>* `false`: default value, do not remove all tags.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is valid only when TagKeys is empty in the request.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=RemoveTagsFromResource&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceIds": [
        "postgres-50a3c0b2****",
        "postgres-f696c2b4****"
    ],
    "All": true
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20231113171752F4AD50C8C5F898DB6725",
        "Action": "RemoveTagsFromResource",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": null
}
```

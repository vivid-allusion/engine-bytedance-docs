---
title: "AddTagsToResource"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/addtagstoresource"
---

Call the AddTagsToResource API to add tags to an instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|InstanceIds |Array of String |Yes |["postgres\-da8f12d3\*\*\*\*", "postgres\-6b40e576\*\*\*\*"] |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Multiple instance IDs can be passed, with a maximum of 20 instance IDs per request and a maximum of 50 tags bound to a single instance.</div><br> |
|Tags |Array of [TagObject](https://docs.byteplus.com/en/docs/61/15768#tagobject) |Yes |Refer to the request example. |An array object of tag keys and tag values to be bound.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">It supports passing multiple sets of tag key\-value pairs at once. A maximum of 20 sets of tag key\-value pairs can be passed per request, with up to 50 tags bound per instance.</div><br> |


<span id="tagobject"></span>
### TagObject


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|Key |String |Yes |abc |Tag key. Naming rules are as follows:<br><br><br>* It cannot start with any case\-insensitive variation of the prefix `volc:`. `volc:` is a system\-reserved tag key and is forbidden to use.<br><br>* It can only contain language characters, numbers, spaces, and English symbols (`_`, `.`, `:`, `/`, `=`, `+`, `-`, and `@`).<br><br>* The length must be between 1 and 128 characters.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The number of tags created at one time cannot exceed 20.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Tag keys cannot be duplicated under a single instance.</div><br> |
|Value |String |No |3 |Tag value. The naming rules are as follows:<br><br><br>* It can only contain language characters, numbers, spaces, and English symbols (`_`, `.`, `:`, `/`, `=`, `+`, `-`, and `@`).<br><br>* Nullable. Length must be between 0 and 256 characters. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

null

<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=AddTagsToResource&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceIds": [
        "postgres-50a3c0b248b5"
    ],
    "Tags": [
        {
            "Key": "Key1",
            "Value": "Value1"
        },
        {
            "Key": "Key2",
            "Value": "Value2"
        }
    ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2023080211144634754706651E8FD70549",
        "Action": "AddTagsToResource",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": null
}
```

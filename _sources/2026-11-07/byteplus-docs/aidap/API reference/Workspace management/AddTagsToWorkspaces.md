---
title: "AddTagsToWorkspaces"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/AddTagsToWorkspaces"
---

Call the AddTagsToWorkspaces API to add tags to the workspace.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Is it required?**  |**Sample value** |**Description** |
|---|---|---|---|---|
|WorkspaceIds |Array of String |Yes |["goody\-birch\-84a1\*\*\*\*", "dandy\-pansy\-4514\*\*\*\*"] |ID of the workspace to which tags will be associated with.<br><br><div data-tips="true" data-tips-type="default">Decscription</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Up to 20 tags can be associated with a workspace in a single call.</div><br><br><br>* <div data-tips="true" data-tips-type="default">A workspace can associate with up to 50 tags.</div><br> |
|Tags |Array of [TagOption](https://docs.byteplus.com/en/docs/330/84404#tagoption) |Yes |Refer to the sample request. |An array object of tag keys and tag values to be associated with.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Up to 20 tags can be associated with a workspace in a single call.</div><br> |


<span id="tagoption"></span>
### TagOption


|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Key |String |Yes |Tag_key |Key of the workspace tag. The rules for defining tag keys are as follows:<br><br><br>* In UTF\-8 encoded Unicode format.<br><br>* Cannot start with `volc:` or `sys` in any case. `volc:` and `sys` are system\-reserved tag keys and are forbidden to use.<br><br>* Can only contain language characters, digits, spaces, and English symbols `_`, `.`, `:`, `/`, `=`, `+`, `-`, and `@`.<br><br>* The length must be between 1 and 128 characters.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Tag keys are case\-sensitive<strong>.</strong></div><br><br><br>* <div data-tips="true" data-tips-type="default">The number of tags created at one time cannot exceed 20.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Tag keys within a single workspace cannot be duplicated.</div><br><br><br>* <div data-tips="true" data-tips-type="default">A tag key can only have one tag value within a single workspace.</div><br> |
|Value |String |No |Tag_value |The value of the workspace tag. The rules for the tag value are as follows:<br><br><br>* In UTF\-8 encoded Unicode format.<br><br>* It can only contain language characters, numbers, spaces, and English symbols (`_`, `.`, `:`, `/`, `=`, `+`, `-`, and `@`).<br><br>* Allow empty, length limit between 0 and 256 characters.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The tag value is case\-sensitive.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```JSON
POST /?Action=AddTagsToWorkspaces&Version=2025-10-01 HTTP/1.1
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "WorkspaceIds": [
        "goody-birch-84a1****",
        "dandy-pansy-4514****"
    ],
    "Tags": [
        {
            "Key": "Tag1_key",
            "Value": "Tag1_value"
        },
        {
            "Key": "Tag2_key",
            "Value": "Tag2_value"
        }
    ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "AddTagsToWorkspaces",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).

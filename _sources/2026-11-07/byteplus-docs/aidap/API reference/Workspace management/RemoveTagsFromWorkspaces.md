---
title: "RemoveTagsFromWorkspaces"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/RemoveTagsFromWorkspaces"
---

Call the RemoveTagsFromWorkspaces API to remove tags from the workspace.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|WorkspaceIds |Array of String |Yes |["goody\-birch\-84a1\*\*\*\*", "dandy\-pansy\-4514\*\*\*\*"] |ID of the workspace whose tag is to be disassociated with.<br><br><div data-tips="true" data-tips-type="default">Decscription</div><br><br><br><div data-tips="true" data-tips-type="default">Up to 20 workspaces can have tags disassociated with simultaneously in a single call.</div><br> |
|TagKeys |Array of String |Yes |Refer to the sample request. |Array object of tag keys and tag values for the tags to be unbound.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Up to 20 tags can be associated with a workspace in a single call.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

null

<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```JSON
POST /?Action=RemoveTagsFromWorkspaces&Version=2025-10-01 HTTP/1.1
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "WorkspaceIds": [
        "goody-birch-84a1****",
        "dandy-pansy-4514****"
    ],
    "TagKeys": [
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
        "Action": "RemoveTagsFromWorkspaces",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).

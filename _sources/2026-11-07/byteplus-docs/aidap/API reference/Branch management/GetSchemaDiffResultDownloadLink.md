---
title: "GetSchemaDiffResultDownloadLink"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/GetSchemaDiffResultDownloadLink"
---

Call GetSchemaDiffResultDownloadLink API to obtain the download link for the branch compare result.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

This API can only be used to operate a workspace using the PostgreSQL engine or Supabase engine.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Is it required?**  |**Sample value** |**Description** |
|---|---|---|---|---|
|WorkspaceId |String |Yes |perky\-bean\-1459\*\*\*\* |ID of the workspace. |
|SchemaDiffJobId |String |Yes |schema\-diff\-7cf8b8402a17426f8bcef50f62db\*\*\*\* |The ID of the branch comparison task. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|DownloadLink |String |https://sinlar\-schema\-diff.tos\-cn\-beijing.volces.com/sinlar\-schema\-diff/2026\-05\-11/schema\-diff\-ae59511330534b218ca31f547aa0\*\*\*\*/schema\-diff\-ae59511330534b218ca31f547aa0\*\*\*\*_SourceSchema_DestinationSchema_20260511T122157.zip?X\-Tos\-Algorithm=TOS4\-HMAC\-SHA256&X\-Tos\-Credential=AKLTMDcyNTA4YzIwYWUxNDkzNDhmYzRkNDU1NmUwZGU\*\*\*\*%2F20260511%2Fcn\-beijing%2Ftos%2Frequest&X\-Tos\-Date=20260511T045306Z&X\-Tos\-Expires=7200&X\-Tos\-Signature=1ce28f5184499aa98ac7110c225f63cca50f7101d090db59d6ab970ef284\*\*\*\*&X\-Tos\-SignedHeaders=host |Download link for branch comparison results.<br><br><div data-tips="true" data-tips-type="default">Decscription</div><br><br><br><div data-tips="true" data-tips-type="default">This address is valid for 7 days.</div><br> |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```JSON
POST /?Action=GetSchemaDiffResultDownloadLink&Version=2025-10-01
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "WorkspaceId": "perky-bean-1459****",
    "SchemaDiffJobId": "schema-diff-7cf8b8402a17426f8bcef50f62db****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetSchemaDiffResultDownloadLink",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {
        "DownloadLink": "https://sinlar-schema-diff.tos-cn-beijing.volces.com/sinlar-schema-diff/2026-05-11/schema-diff-ae59511330534b218ca31f547aa0****/schema-diff-ae59511330534b218ca31f547aa0****_SourceSchema_DestinationSchema_20260511T122157.zip?X-Tos-Algorithm=TOS4-HMAC-SHA256&X-Tos-Credential=AKLTMDcyNTA4YzIwYWUxNDkzNDhmYzRkNDU1NmUwZGU****%2F20260511%2Fcn-beijing%2Ftos%2Frequest&X-Tos-Date=20260511T045306Z&X-Tos-Expires=7200&X-Tos-Signature=1ce28f5184499aa98ac7110c225f63cca50f7101d090db59d6ab970ef284****&X-Tos-SignedHeaders=host"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).

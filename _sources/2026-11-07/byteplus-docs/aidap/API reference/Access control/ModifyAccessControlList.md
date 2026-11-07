---
title: "ModifyAccessControlList"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/ModifyAccessControlList"
---

Call the ModifyAccessControlList API to modify the Workspace\-bound IP allowlist.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

This API can only be used to operate the workspace using the Supabase engine.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Is it required?**  |**Sample value** |**Description** |
|---|---|---|---|---|
|WorkspaceId |String |Yes |noble\-heath\-3a48\*\*\*\* |ID of the workspace. |
|AccessControlListName |String |Yes |acl\-default |Allowlist name.<br><br><div data-tips="true" data-tips-type="default">Decscription</div><br><br><br><div data-tips="true" data-tips-type="default">Currently, each workspace can have only one IP allowlist, named <code>acl-default</code>.</div><br> |
|ModifyMode |String |Yes |Cover |Modify an allowlist method. Values:<br><br><br>* `Cover`: cover, which means replacing the original allowlist with the IP addresses in the request parameter IPList.<br><br>* `Append`: append, which means adding the IP addresses in the request parameter IPList to the original allowlist.<br><br>* `Delete`: delete, which means removing the IP addresses in the request parameter IPList from the original allowlist. |
|IPList |Array of String |Yes |["2.\*\*\*.\*\*\*.1/32"] |IP address list.<br><br><br>* If the allowlist does not contain any IP address, the workspace allows access from all IP addresses.<br><br>* If the allowlist only contains the `127.0.0.1` address, the workspace denies access.<br><br>* CIDR\-format IP segments can be included in the allowlist, such as `192.168.0.0/24`, meaning the workspace allows access from IP addresses within this subnet.<br><br>* A maximum of 300 IP addresses or CIDR\-format IP segments can be added to one allowlist. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

null

<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```JSON
POST /?Action=ModifyAccessControlList&Version=2025-10-01 HTTP/1.1
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "WorkspaceId": "noble-heath-3a48****",
    "AccessControlListName": "acl-default",
    "ModifyMode": "Cover",
    "IPList": [
        "2.***.***.1/32"
    ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ModifyAccessControlList",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": null
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).

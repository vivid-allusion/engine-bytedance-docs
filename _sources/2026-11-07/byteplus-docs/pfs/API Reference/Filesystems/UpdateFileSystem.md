---
title: "UpdateFileSystem"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/UpdateFileSystem"
---

Call the UpdateFileSystem interface to update file system information.

<span id="request-parameters"></span>
## Request parameters


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|FileSystemId |String |Yes |vepfs\-apse1dfff3e96\*\*\*\* |File system ID. |
|FileSystemName |String |No |test |File system name. The naming convention is as follows:<br><br><br>* Cannot start with a number or a dash (\-).<br><br>* Can only contain Chinese, letters, numbers, underscores (_) and underscores (\-).<br><br>   The length should be between 1 and 128 characters. |
|Description |String |No |Just\-for\-test |File system description information, 0 to 120 characters in length. |
|Project |String |No |default |The project to which the file system belongs, defaults to `dafault`. |
|Tags |Array of [Tag](https://docs.byteplus.com/en/docs/92/25013#tag) |No |See the request example for details |Label information to be added.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The label information of the file system needs to meet certain rules. For details, please refer to <a href="https://docs.byteplus.com/en/docs/pfs/Binding-or-adding-tags">Tag Setup Rules</a>.</div><br> |


<span id="tag"></span>
### Tag


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|Key |String |Yes |tag_00 |Label key. |
|Type |String |Yes |Custom |The label type is described as follows:<br><br><br>* `Custom`: user\-defined labels.<br><br>* `System`: System label. |
|Value |String |Yes |tag_value00 |Label value. |


<span id="response-parameters"></span>
## Response parameters

Empty.

<span id="sample-request"></span>
## Sample request

```json
POST /?Action=UpdateFileSystem&Version=2022-01-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/vepfs/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
{
    "FileSystemId": "vepfs-apse1dfff3e96****",
    "FileSystemName": "test",
    "Description": "Just-for-test",
    "Project": "default",
    "Tags": [
        {
            "Key": "tag_00",
            "Type": "Custom",
            "Value": "tag_value00"
        }
    ]
}
```


<span id="sample-response"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "UpdateFileSystem",
        "Region": "ap-southeast-1",
        "Service": "vepfs",
        "Version": "2022-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {}
}
```

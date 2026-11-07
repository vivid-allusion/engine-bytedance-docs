---
title: "CreateFileSystem"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/CreateFileSystem"
---

Call the CreateFileSystem interface to create the file system.

<span id="request-parameters"></span>
## Request parameters


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|FileSystemName |String |Yes |test |File system name. The naming convention is as follows:<br><br><br>* Cannot start with a number or a dash (\-).<br><br>* Can only contain Chinese, letters, numbers, underscores (\ _) and underscores (\-).<br><br>   The length should be between 1 and 128 characters. |
|ZoneId |String |Yes |ap\-southeast\-1a |Availability zone ID. |
|FileSystemType |String |Yes |Extreme |File system type. The value selection description is as follows:<br><br>`Extreme`: NAS Extreme Speed. |
|ProtocolType |String |Yes |NFS |File system protocol type. The value selection description is as follows:<br><br>`NFS`: NFS protocol, often used Linux client side. |
|ChargeType |String |Yes |PayAsYouGo |Billing type. The value selection description is as follows:<br><br>`PayAsYouGo`: Billing by volume. |
|ProjectName |String |No |default |Project name. |
|Description |String |No |Just\-for\-test |Describe the information. |
|Capacity |Integer |No |100 |Extremely fast file system capacity. |
|SnapshotId |String |No |snap\-123456 |The snapshot ID to use when creating. Once this parameter is passed, the snapshot will be used to create a new file system.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/nas/DescribeSnapshots">DescribeSnapshots</a> interface to view the snapshot ID.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter can only be used if <code>FileSystemType</code> is <code>Extreme</code>.</div><br> |
|ClientToken |String |No |123456\-789\-0 |Request the idempotence parameter. |
|Tags |Array of [Tag](https://docs.byteplus.com/en/docs/91/24980#tag) |No |[{<br><br>"Key": "tagkey",<br><br>"Type": "Customs",<br><br>"Value": "tagValue"<br><br>}] |Tag information for the file system. |


<span id="tag"></span>
### Tag


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|Key |String |Yes |tagkey |Label key. |
|Type |String |Yes |Custom |The label type is described as follows:<br><br><br>* `Custom`: user\-defined labels.<br><br>* `System`: System label. |
|Value |String |Yes |tagvalue |Label value. |


<span id="response-parameters"></span>
## Response parameters


|Name |Type |Example |Description |
|---|---|---|---|
|FileSystemId |String |enas\-8d820ea7\*\*\*\* |The file system ID created. |
|OrderNo |String |Order724371858305511\*\*\*\* |Order number. |


<span id="sample-request"></span>
## Sample request

```json
POST /?Action=CreateFileSystem&Version=2022-01-01 HTTP/1.1
Host: filenas.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/filenas/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
{
    "FileSystemName": "test",
    "ZoneId": "ap-southeast-1a",
    "Description": "Just-for-test",
    "ChargeType": "PayAsYouGo",
    "FileSystemType": "Extreme",
    "StoreType": "Standard",
    "ProtocolType": "NFS",
    "ProjectName": "default",
    "Capacity": 100
}
```


<span id="sample-response"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "CreateFileSystem",
        "Region": "ap-southeast-1",
        "Service": "filenas",
        "Version": "2022-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "FileSystemId": "enas-8d820ea7****",
        "OrderNo": "Order724371858305511****"
    }
}
```

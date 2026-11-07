---
title: "ExpandFileSystem"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/ExpandFileSystem"
---

Call the ExpandFileSystem interface to expand the file system.

<span id="request-parameters"></span>
## Request parameters


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|FileSystemId |String |Yes |vepfs\-apse1dfff3e96\*\*\*\* |The file system ID that needs to be expanded. |
|Capacity |Integer |Yes |200 |The expanded file system capacity, in TiB. |
|EnableRestripe |Boolean |No |undefined |Whether to open data equalization after expansion, the value selection description is as follows:<br><br><br>* `true`: Enable data equalization immediately after scaling.<br><br>* `false`: Data balancing is not turned on after expansion.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="warning">Since the data balancing process consumes the network and disk bandwidth of the storage node, the performance of the file system is degraded, so it needs to be turned on carefully. In addition, the time of data balancing is mainly affected by the amount of stored data.</div><br> |


<span id="response-parameters"></span>
## Response parameters


|Name |Type |Example |Description |
|---|---|---|---|
|OrderNO |String |Order714380929892930\*\*\*\* |Order ID. |


<span id="sample-request"></span>
## Sample request

```json
POST /?Action=ExpandFileSystem&Version=2022-01-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/vepfs/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
{
    "FileSystemId": "vepfs-apse1dfff3e96****",
    "Capacity": 200
}
```


<span id="sample-response"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "ExpandFileSystem",
        "Region": "ap-southeast-1",
        "Service": "vepfs",
        "Version": "2022-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "OrderNO": "Order714380929892930****"
    }
}
```

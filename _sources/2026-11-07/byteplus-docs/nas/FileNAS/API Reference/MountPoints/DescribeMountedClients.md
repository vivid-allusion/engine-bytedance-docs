---
title: "DescribeMountedClients"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/DescribeMountedClients"
---

The call DescribeMountedClients interface enumerates client side information mounted on the file system.

<span id="request-parameters"></span>
## Request parameters


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|FileSystemId |String |Yes |enas\-18bcb923\*\*\*\* |File system ID. |
|MountPointId |String |No |mount\-cb17\*\*\*\* |Mount Point ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/nas/DescribeMountPoints">DescribeMountPoints</a> interface to query the mount point ID of the specified file system.</div><br> |


<span id="response-parameters"></span>
## Response parameters


|Name |Type |Example |Description |
|---|---|---|---|
|TotalCount |Integer |1 |Number of client sides. |
|Clients |Array of [Client](https://docs.byteplus.com/en/docs/91/24988#client) |See the return example for details |Client side information. |


<span id="client"></span>
### Client


|Name |Type |Example |Description |
|---|---|---|---|
|Ip |String |192.168. **.**  |The client's private network IP address. |
|VpcName |String |NAStest |Private network name. |
|ProtocolVersion |String |NFSv3 |Mount the protocol version number. |


<span id="sample-request"></span>
## Sample request

```json
POST /?Action=DescribeMountedClients&Version=2022-01-01 HTTP/1.1
Host: filenas.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/filenas/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
{
    "FileSystemId": "enas-18bcb923****t",
    "MountPointId": "mount-cb17****"
}
```


<span id="sample-response"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "DescribeMountedClients",
        "Region": "ap-southeast-1",
        "Service": "filenas",
        "Version": "2022-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "TotalCount": 1,
        "Clients": [
            {
                "Ip": "192.168.**.**",
                "VpcName": "NAStest",
                "ProtocolVersion": "NFSv3"
            }
        ]
    }
}
```

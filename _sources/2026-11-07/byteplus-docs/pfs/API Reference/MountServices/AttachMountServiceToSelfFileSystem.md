---
title: "AttachMountServiceToSelfFileSystem"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/AttachMountServiceToSelfFileSystem"
---

Call AttachMountServiceToSelfFileSystem interface to mount the service binding storage instance.

<span id="note"></span>
## Note


|Restrictions |Description |
|---|---|
|Quantity limit |* A single PFS instance can bind up to 5 mount services.<br><br>* A single mount service can bind 2 instances. |
|vePFS Instances |* If your PFS instance needs to bind multiple mount services, all mount services must be in the same VPC.<br><br>* For an optimal performance experience, it is recommended that the PFS instance be in the same Availability Zone as the mount service.<br><br>* A mount service does not support access to multiple Smart Edition instances via RDMA.<br><br>* The instance cannot perform binding\-related operations when it is in other states such as expansion, deletion, etc.<br><br>* The state of all nodes in the mounted service cluster must be active during the binding instance operation, and the key file is not destroyed, otherwise the binding operation cannot be performed. |
|Mount Service |After creating the mount service, the system will automatically create 3 ECS instances for managing the client side cluster. Do not modify the initial password of the management node and ensure that the instance can log in normally. |


<span id="request-parameters"></span>
## Request parameters


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|MountServiceId |String |Yes |mount\-75a6\*\*\*\* |The mount service ID that needs to be bound. |
|FileSystemId |String |Yes |vepfs\-apse1dfff3e96\*\*\*\* |The file system ID to bind to. |
|CustomerPath |String |No |/vepfs\-test |Custom mount directory, if left blank, defaults to file system ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you need to set a custom mount path, the parent directory must be an existing directory and the child directory has not been created.</div><br> |


<span id="response-parameters"></span>
## Response parameters

Empty.

<span id="sample-request"></span>
## Sample request

```json
POST /?Action=AttachMountServiceToSelfFileSystem&Version=2022-01-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/vepfs/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
{
    "MountServiceId": "mount-75a6****",
    "FileSystemId": "vepfs-apse1dfff3e96****",
    "CustomerPath": "/vepfs-test"
}
```


<span id="sample-response"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "AttachMountServiceToSelfFileSystem",
        "Region": "ap-southeast-1",
        "Service": "vepfs",
        "Version": "2022-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {}
}
```

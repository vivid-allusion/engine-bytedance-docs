---
title: "CreateSnapshot"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/CreateSnapshot"
---

Call the CreateSnapshot interface to create a file system snapshot.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* Only Extreme Speed NAS supports snapshot creation.

* The current snapshot is in the public beta state, and there is no charge for the time being. During the free period, an extremely fast NAS file system can create up to 128 manual snapshots.

* It takes a certain amount of time to create a snapshot, and there will be minutes of data that cannot be written. It is recommended that you choose a business low\-peak operation. During the creation period, you can mount the file system, but you cannot delete or expand the file system.

   A single file system cannot create two snapshots simultaneously.

   The same account cannot create snapshots of multiple file systems simultaneously.

* Manual snapshots are permanently retained after creation and cannot be automatically deleted. If you need to delete a snapshot, see [DeleteSnapshot](https://docs.byteplus.com/en/docs/nas/DeleteSnapshot) for specific steps.


<span id="request-parameters"></span>
## Request parameters


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|FileSystemId |String |Yes |enas\-01961fc437\*\*\*\* |The file system ID that needs to create the snapshot. |
|SnapshotName |String |Yes |testcreate |Snapshot name. The naming convention is as follows:<br><br><br>* Cannot start with a number or a dash (\-).<br><br>* Can only contain Chinese, letters, numbers, underscores (_) and underscores (\-).<br><br>   The length should be between 1 and 128 characters.<br><br>* Cannot start with `auto`. |
|Description |String |No |test |Snapshot description information, 0 to 120 characters in length. |


<span id="response-parameters"></span>
## Response parameters


|Name |Type |Example |Description |
|---|---|---|---|
|SnapshotId |String |snap\-472a716f\*\*\*\* |Generated snapshot ID. |


<span id="sample-request"></span>
## Sample request

```json
POST /?Action=CreateSnapshot&Version=2022-01-01 HTTP/1.1
Host: filenas.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/filenas/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
{
    "FileSystemId": "enas-01961fc437****",
    "SnapshotName": "testcreate",
    "Description": "test"
}
```


<span id="sample-response"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "CreateSnapshot",
        "Region": "ap-southeast-1",
        "Service": "filenas",
        "Version": "2022-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "SnapshotId": "snap-472a716f****"
    }
}
```

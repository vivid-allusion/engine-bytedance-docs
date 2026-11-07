---
title: "DeleteAutoSnapshotPolicy"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/DeleteAutoSnapshotPolicy"
---

Call DeleteAutoSnapshotPolicy interface to remove the automatic snapshot policy.

<span id="requirements"></span>
## Requirements


* Before deleting an automatic snapshot policy, ensure that the policy does not have an associated file storage instance, otherwise the deletion will fail.

* After the policy is deleted, it cannot be restored. Please delete it with caution.

* When you remove the automatic snapshot policy, if an instance is creating an automatic snapshot, that snapshot will continue to be created, but subsequent automatic snapshots will no longer be created.


<span id="request-parameters"></span>
## Request parameters


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|AutoSnapshotPolicyId |String |Yes |asp\-15c19547\*\*\*\* |The automatic snapshot policy ID that needs to be deleted. |


<span id="response-parameters"></span>
## Response parameters

Empty.

<span id="sample-request"></span>
## Sample request

```json
POST /?Action=DeleteAutoSnapshotPolicy&Version=2022-01-01 HTTP/1.1
Host: filenas.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/filenas/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
{
    "AutoSnapshotPolicyId": "asp-15c19547****"
}
```


<span id="sample-response"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "DeleteAutoSnapshotPolicy",
        "Region": "ap-southeast-1",
        "Service": "filenas",
        "Version": "2022-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {}
}
```

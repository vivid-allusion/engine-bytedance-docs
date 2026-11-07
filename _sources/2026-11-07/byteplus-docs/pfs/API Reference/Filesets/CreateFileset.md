---
title: "CreateFileset"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/CreateFileset"
---

Call the CreateFileset interface to create a Fileset.

<span id="request-parameters"></span>
## Request parameters


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|FileSystemId |String |Yes |vepfs\-apse1dfff3e96\*\*\*\* |File system ID. |
|FilesetName |String |Yes |fileset1 |Fileset name, the naming convention is as follows:<br><br><br>* You can only start with English and Chinese.<br><br>* Can only contain Chinese, letters, numbers, underscores (\ _) and underscores (\-).<br><br>* The length is from 1 to 128 characters. |
|FilesetPath |String |Yes |/fileset1/ |The path of Fileset in the vePFS filesystem is constrained as follows:<br><br>Enter the absolute path of the directory in the file system, starting and ending with `/`.<br><br>The path format should be `/< parent directory >/< subdirectory >/`, where:<br><br>The parent directory must be an existing directory.<br><br><br>* Subdirectory is the directory name that needs to be created when creating Fileset this time. This directory corresponds to Fileset and is automatically created by the system.<br><br>* Example directory: `/dir/Filesetdir/`.<br><br>   The maximum path depth is 8 layers.<br><br>   The length is between 1 and 255 characters. |


<span id="response-parameters"></span>
## Response parameters


|Name |Type |Example |Description |
|---|---|---|---|
|FilesetId |String |fset\-413b\*\*\*\* |The created Fileset ID. |


<span id="sample-request"></span>
## Sample request

```json
POST /?Action=CreateFileset&Version=2022-01-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/vepfs/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
{
    "FileSystemId": "vepfs-apse1dfff3e96****",
    "FilesetName": "fileset1",
    "FilesetPath": "/fileset1/"
}
```


<span id="sample-response"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "CreateFileset",
        "Region": "ap-southeast-1",
        "Service": "vepfs",
        "Version": "2022-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "FilesetId": "fset-413b****"
    }
}
```

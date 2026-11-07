---
title: "DescribeFilesets"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/DescribeFilesets"
---

Call the DescribeFilesets interface to query the Fileset list.

<span id="request-parameters"></span>
## Request parameters


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|FileSystemId |String |Yes |vepfs\-apse1dfff3e96\*\*\*\* |File system ID. |
|Filters |Array of [FilesetFilter](https://docs.byteplus.com/en/docs/92/25026#filesetfilter) |No |{<br><br>"Key": "FilesetName",<br><br>"Value": "fileset1"<br><br>} |Fileset query filter. |
|OrderBy |String |No |CreateTimeDesc |Fileset list sorting method, value selection description is as follows:<br><br><br>* `CreateTimeDesc`: Descending by time, default sorting.<br><br>* `CreateTimeAsc`: in ascending chronological order.<br><br>* `NameDesc`: Descending by Fileset name.<br><br>* `NameAsc`: In ascending order by Fileset name. |
|PageSize |Integer |No |10 |Number of records per page, the default is 10. |
|PageNumber |Integer |No |1 |The page number of the list, up to the maximum value of the Integer data type, starting at 1. |


<span id="filesetfilter"></span>
### FilesetFilter


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|Key |String |Yes |FilesetName |Filters the Fileset for the specified feature based on the feature. The parameters that support filtering are as follows:<br><br><br>* `FilesetName`: Filter by Fileset name, fuzzy match.<br><br>* `FilesetId`: Filter precisely by Fileset ID.<br><br>* `FilesetPath`: Filter by path in the file system, fuzzy match.<br><br>* `Status`: Filter by Fileset status. |
|Value |String |Yes |filset1 |Filter the value of the item. |


<span id="response-parameters"></span>
## Response parameters


|Name |Type |Example |Description |
|---|---|---|---|
|TotalCount |Integer |2 |Number of Filesets. |
|Filesets |Array of [Fileset](https://docs.byteplus.com/en/docs/92/25026#fileset) |See the return example for details |Fileset details. |
|PageSize |Integer |10 |Number of Filesets per page. |
|PageNumber |Integer |1 |The paginated page number of the Fileset list. |


<span id="fileset"></span>
### Fileset


|Name |Type |Example |Description |
|---|---|---|---|
|Status |String |Running |Fileset status, value selection description is as follows:<br><br><br>* `Creating`: Creating<br><br>* `CreateError`: Failed to create<br><br>* `Running`: running<br><br>* `Updating`: Updating<br><br>* `UpdateError`: update failed<br><br>* `Deleting`: Deleting<br><br>* `DeleteError`: Delete failed<br><br>* `Deleted`: deleted<br><br>* `Error`: error |
|IOPSQos |Integer |0 |IOPS QoS. |
|FileUsed |Long |3 |Number of files used. |
|FileLimit |Long |0 |Quota for the number of files or directories. |
|FilesetId |String |fset\-5fa4\*\*\*\* |Fileset ID. |
|CreateTime |String |2023\-08\-17 T14:49:37 + 08:00 |Fileset creation time. |
|FilesetName |String |fileset1 |Fileset name. |
|FilesetPath |String |/aaa |Fileset absolute path. |
|MaxInodeNum |Long |10000000 |Maximum number of Fileset Inodes. |
|BandwidthQos |Integer |0 |Bandwidth QoS. |
|CapacityUsed |Integer |156 |Used capacity, in GiB. |
|FileSystemId |String |vepfs\-apse1dfff3e96\*\*\*\* |File system ID. |
|CapacityLimit |Integer |500 |Capacity quota limit, in gibs. |


<span id="sample-request"></span>
## Sample request

```json
POST /?Action=DescribeFilesets&Version=2022-01-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/vepfs/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
{
    "FileSystemId": "vepfs-apse1dfff3e96****",
    "OrderBy": "CreateTimeDesc",
    "PageSize": 10,
    "PageNumber": 1
}
```


<span id="sample-response"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "DescribeFilesets",
        "Region": "ap-southeast-1",
        "Service": "vepfs",
        "Version": "2022-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "TotalCount": 2,
        "Filesets": [
            {
                "Status": "Running",
                "IOPSQos": 0,
                "FileUsed": 3,
                "FileLimit": 0,
                "FilesetId": "fset-5fa4****",
                "CreateTime": "2023-08-17T14:49:37+08:00",
                "FilesetName": "fileset1",
                "FilesetPath": "/aaa",
                "MaxInodeNum": 10000000,
                "BandwidthQos": 0,
                "CapacityUsed": 156,
                "FileSystemId": "vepfs-apse1dfff3e96****",
                "CapacityLimit": 500
            }
        ],
        "PageSize": 10,
        "PageNumber": 1
    }
}
```

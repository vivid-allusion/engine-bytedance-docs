---
title: "DescribeMountServices"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/DescribeMountServices"
---

Call DescribeMountServices interface to query the mount service details.

<span id="request-parameters"></span>
## Request parameters


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|Filters |Array of [MountServiceFilter](https://docs.byteplus.com/en/docs/92/25017#mountservicefilter) |No |See the request example for details |Mount the service query filter. |
|OrderBy |String |No |CreateTimeDesc |The mount service sorting method, the value selection description is as follows:<br><br><br>* `CreateTimeDesc`: in descending order of creation time.<br><br>* `CreateTimeAsc`: in descending order by creation time.<br><br>* `NameDesc`: named in ascending order by the system on which the service is mounted.<br><br>* `NameAsc`: named in ascending order by the system on which the service is mounted. |
|PageSize |Integer |No |10 |The number of mounted services contained in each pagination, the value is `1` to `100`, and the default is `10`. |
|PageNumber |Integer |No |1 |The page number to mount the service information list, up to the maximum value of the Integer data type, starting at 1. |
|Project |String |No |default |Project name. |


<span id="mountservicefilter"></span>
### MountServiceFilter


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|Key |String |Yes |Status |Filters instances of the specified feature based on the feature. The parameters that support filtering are as follows:<br><br><br>* `Status`: Precise filtering according to the status of the mount service, supports multiple selection, and is separated by English commas (,).<br><br>* `FileSystemId`: Filter precisely by file system ID.<br><br>* `MountServiceName`: Fuzzy filtering based on mount service name, multiple selection is not supported.<br><br>* `MountServiceId`: Filter precisely based on the mount service ID. |
|Value |String |Yes |Running |Filter the value of the item. |


<span id="response-parameters"></span>
## Response parameters


|Name |Type |Example |Description |
|---|---|---|---|
|TotalCount |Integer |2 |Number of mounted services. |
|MountServices |Array of [MountService](https://docs.byteplus.com/en/docs/92/25017#mountservice) |See the return example for details |Mount point details. |
|PageSize |Integer |10 |The number of mount services per page. |
|PageNumber |Integer |1 |The page number to mount the service information list. |


<span id="mountservice"></span>
### MountService


|Name |Type |Example |Description |
|---|---|---|---|
|Nodes |Array of [MountServiceManagerNode](https://docs.byteplus.com/en/docs/92/25017#mountservicemanagernode) |See the return example for details |The client side manages the node list. |
|VpcId |String |vpc\-13fz0iip9nlds3n6nu4fi\*\*\*\* |Private network ID. |
|Status |String |Running |Mount service status, described as follows:<br><br><br>* `Creating`: Creating<br><br>* `CreateError`: Failed to create<br><br>* `Running`: running<br><br>* `Updating`: Updating<br><br>* `UpdateError`: update failed<br><br>* `Deleting`: Deleting<br><br>* `DeleteError`: Delete failed<br><br>* `Deleted`: deleted<br><br>* `Attaching`: binding<br><br>* `AttachError`: binding failed<br><br>* `Detaching`: unbinding<br><br>* `DetachError`: Unbinding failed<br><br>* `Stopped`: shutdown<br><br>* `Error`: error |
|ZoneId |String |ap\-southeast\-1a |Availability zone ID. |
|Project |String |default |Mount the item to which the service belongs. |
|RegionId |String |ap\-southeast\-1 |Geographical information. |
|SubnetId |String |subnet\-13fz1bsbrsw743n6nu47c\*\*\*\* |Subnet ID. |
|ZoneName |String |Asia Pacific (Johor) A |Availability zone name. |
|AccountId |String |210015\*\*\*\* |User ID. |
|CreateTime |String |2023\-07\-18 T17:10:03 + 08:00 |Creation time. |
|MountServiceId |String |mount\-94eb\*\*\*\* |Mount service ID. |
|SecurityGroupId |String |sg\-mioirewk8zcw5smt1ba8\*\*\*\* |Client side network interface card security group ID. |
|MountServiceName |String |mountservice |Mount service name. |
|AttachFileSystems |Array of [AttachFileSystem](https://docs.byteplus.com/en/docs/92/25017#attachfilesystem) |See the return example for details |Mount instance information. |


<span id="mountservicemanagernode"></span>
### MountServiceManagerNode


|Name |Type |Example |Description |
|---|---|---|---|
|NodeId |String |i\-yclmdnskx838df3y\*\*\*\* |ECS instance ID. |
|DefaultPassword |String |948E4 = 9@2Jbq \*\*\*\* |ECS instance initial login password. |


<span id="attachfilesystem"></span>
### AttachFileSystem


|Name |Type |Example |Description |
|---|---|---|---|
|Status |String |Attached |The binding status is described as follows:<br><br><br>* `Attaching`: binding<br><br>* `AttachError`: binding failed<br><br>* `Attached`: bound<br><br>* `Detaching`: unbinding<br><br>* `DetachError`: Unbinding failed |
|AccountId |String |210015\*\*\*\* |Byteplus account ID. |
|CustomerPath |String |/vepfs\-test |User mount path. |
|FileSystemId |String |vepfs\-apse1dfff3e96\*\*\*\* |File system ID. |
|FileSystemName |String |lltest |File system name. |


<span id="sample-request"></span>
## Sample request

```json
POST /?Action=DescribeMountServices&Version=2022-01-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/vepfs/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
{
    "Filters": [
        {
            "Key": "Status",
            "Value": "Running"
        }
    ],
    "OrderBy": "CreateTimeDesc",
    "PageSize": 10,
    "PageNumber": 1,
    "Project": "default"
}
```


<span id="sample-response"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "DescribeMountServices",
        "Region": "ap-southeast-1",
        "Service": "vepfs",
        "Version": "2022-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "TotalCount": 2,
        "MountServices": [
            {
                "Nodes": [
                    {
                        "NodeId": "i-yclmdnskx838df3y****",
                        "DefaultPassword": "948E4=9@2Jbq****"
                    }
                ],
                "VpcId": "vpc-13fz0iip9nlds3n6nu4fi****",
                "Status": "Running",
                "Project": "default",
                "RegionId": "ap-southeast-1",
                "SubnetId": "subnet-13fz1bsbrsw743n6nu47c****",
                "AccountId": "210015****",
                "TradeInfo": {
                    "IsTest": false,
                    "Identity": "pulling",
                    "AccountId": "remembers"
                },
                "CreateTime": "2023-07-18T17:10:03+08:00",
                "MountServiceId": "mount-94eb****",
                "SecurityGroupId": "sg-mioirewk8zcw5smt1ba8****",
                "MountServiceName": "mountservice",
                "AttachFileSystems": [
                    {
                        "Status": "Attached",
                        "AccountId": "210015****",
                        "CustomerPath": "/vepfs-test",
                        "FileSystemId": "vepfs-apse1dfff3e96****",
                        "FileSystemName": "lltest"
                    }
                ],
                "MountServiceGrafanaUrl": "commenced"
            }
        ],
        "PageSize": 10,
        "PageNumber": 1
    }
}
```

---
title: "DescribeDBInstances"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances"
---

Call the DescribeDBInstances to query the instance list.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeDBInstances&serviceCode=vedbm&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|DBEngineVersion |String |No |MySQL_8_0 |The compatible version of the instance. Value range:<br><br><br>* `MySQL_8_0`: Compatible with MySQL version 8.0.<br><br>* `MySQL_5_7`: Compatible with MySQL version 5.7. |
|InstanceId |String |No |vedbm\-d4mx2akm\*\*\*\* |Instance ID. |
|InstanceName |String |No |test |Instance name. Fuzzy search is supported. |
|InstanceStatus |String |No |Running |Instance status.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For a detailed description of the instance state, refer to <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/Instance_status_description">Instance state description</a>.</div><br> |
|CreateTimeStart |String |No |2022\-06\-21T07:57:26Z |The start time to create the instance, in YYYY\-MM\-DDTHH:MM:SSZ format (UTC time). |
|CreateTimeEnd |String |No |2022\-06\-21T07:57:26Z |The end time for creating the instance, in the format: YYYY\-MM\-DDTHH:MM:SSZ (UTC time).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When both the <code>CreateTimeStart</code> and <code>CreateTimeEnd</code> parameters are specified, the end time must be later than the start time.</div><br> |
|ZoneId |String |No |cn\-beijing\-a |The ID of the availability zone where the instance is located.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeAvailabilityZones">DescribeAvailabilityZones</a> API to query the availability zones supported by the instance.</div><br> |
|StorageType |String |No |IOOptimizedStorage |Storage type. Value range:<br><br><br>* `IOOptimizedStorage`: IO performance type.<br><br>* `SmartCompressedStorage`: Intelligent compression type. |
|ChargeType |String |No |PostPaid |Calculate billing type. The valid values are:<br><br><br>* `PostPaid`: Pay\-as\-you\-go.<br><br>* `PrePaid`: Yearly or monthly subscription. |
|NodeSpec |String |No |vedb.mysql.x4.xlarge |The node specification of the instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For detailed information on instance node specifications, refer to <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/Product_specifications">Product specifications</a>.</div><br> |
|TagFilters |Array of [TagFilterObject](https://docs.byteplus.com/en/docs/265/57343#tagfilterobject) |No |See the request example. |An array of tag key\-value pairs for querying and filtering.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Up to 10 tag key\-value pairs can be passed in at a time for querying and filtering.</div><br> |
|ProjectName |String |No |default |The name of the project to which the instance belongs. |
|PageSize |Integer |No |10 |Number of records per page. The value range is 1 to 500, with a default of 10. |
|PageNumber |Integer |No |1 |The page number, which must be greater than or equal to 1 and not exceed the maximum value of an Integer. The default is 1. |


<span id="tagfilterobject"></span>
### TagFilterObject


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|Key |String |No |department |Tag key for query filtering. |
|Value |String |No |game |Tag value for querying and filtering.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is required for filtering if a tag value is set when adding the tag.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|Name |Type |Example |Description |
|---|---|---|---|
|Total |Integer |1 |The number of instances that meet the query conditions. |
|Instances |Array of [InstanceObject](https://docs.byteplus.com/en/docs/265/57343#instanceobject) |Refer to the Sample response. |Instance list. |


<span id="instanceobject"></span>
### InstanceObject


|Name |Type |Example |Description |
|---|---|---|---|
|InstanceId |String |vedbm\-d4mx2akm\*\*\*\* |Instance ID. |
|InstanceName |String |test |Instance name. |
|InstanceStatus |String |Running |Instance status.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For a detailed description of the instance state, refer to <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/Instance_status_description">Instance state description</a>.</div><br> |
|CreateTime |String |2022\-06\-21T07:54:05Z |Instance creation time, in the format YYYY\-MM\-DDTHH:MM:SSZ (UTC). |
|DBEngineVersion |String |MySQL_8_0 |The compatible version of the instance. Value range:<br><br><br>* `MySQL_8_0`: Compatible with MySQL version 8.0.<br><br>* `MySQL_5_7`: Compatible with MySQL version 5.7. |
|ProjectName |String |vedb_project |The project to which the instance belongs.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">A project is a virtual concept that includes a set of resources, users, and roles. A project allows you to view and manage a group of resources in a unified manner and control the permissions of users and roles to these resources.</div><br> |
|ZoneIds |String |cn\-beijing\-a |The availability zone of the instance. |
|VpcId |String |vpc\-3ajzohyfaru9s340jz1rp\*\*\*\* |Virtual private cloud (VPC) ID. |
|TimeZone |String |UTC +08:00 |The time zone of the instance. The default time zone for all regions in China is `UTC + 08:00`. |
|StorageChargeType |String |PostPaid |Storage billing type. The valid values are:<br><br><br>* `PostPaid`: Pay\-as\-you\-go.<br><br>* `PrePaid`: Yearly or monthly subscription. |
|PrePaidStorageInGB |Integer |50 |Total capacity of the prepaid storage in GiB. |
|StorageUsedGiB |Double |0.44 |The used storage space in GiB. |
|ChargeDetail |Object of [ChargeDetailObject](https://docs.byteplus.com/en/docs/265/57343#chargedetailobject) |Refer to the Sample response. |Billing information. |
|RegionId |String |cn\-beijing |Region ID. |
|SubnetId |String |subnet\-1g15j13jtzgu88ibuxwqp\*\*\*\* |Subnet ID. The subnet must belong to the selected availability zone. |
|Nodes |Array of [NodeObject](https://docs.byteplus.com/en/docs/265/57343#nodeobject) |Refer to the Sample response. |Details of the instance node. |
|Tags |Array of [TagObject](https://docs.byteplus.com/en/docs/265/57343#tagobject) |Refer to the Sample response. |An array object of tag keys and tag values bound to the instance. |
|DeletionProtection |String |enabled |Whether deletion protection is enabled for the instance. Value range:<br><br><br>* `enabled`: Enable.<br><br>* `disabled`: Disable. |
|DBRevisionVersion |String |3.0.2.1 |The kernel version of the instance. For a detailed description of kernel version numbers, see [Version management](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Version_number_management). |
|SpecFamily |String |Exclusive |Instance specification type. The valid values are:<br><br><br>* `General`: General type.<br><br>* `Exclusive`: Exclusive type. |
|LowerCaseTableNames |String |1 |Whether table names are case sensitive. Value range:<br><br><br>* `0`: table names are stored as is and are case\-sensitive.<br><br>* `1`: table names are stored in lowercase and are case\-insensitive. |
|StorageType |String |IOOptimizedStorage |Storage type. Value range:<br><br><br>* `IOOptimizedStorage`: IO performance type.<br><br>* `SmartCompressedStorage`: Intelligent compression type. |


<span id="chargedetailobject"></span>
### ChargeDetailObject


|Name |Type |Example |Description |
|---|---|---|---|
|ChargeType |String |PostPaid |Calculate billing type. The valid values are:<br><br><br>* `PostPaid`: Pay\-as\-you\-go.<br><br>* `PrePaid`: Yearly or monthly subscription. |
|ChargeStatus |String |Normal |Payment status:<br><br><br>* `Normal`: Normal.<br><br>* `Overdue`: Overdue.<br><br>* `Shutdown`: Shut down. |
|OverdueReclaimTime |String |2022\-09\-27T06:09:20Z |The estimated release time for a shutdown due to an overdue payment, in yyyy\-MM\-ddTHH:mm:ssZ format (UTC time). |
|OverdueTime |String |2022\-10\-04T07:50:22Z |The shutdown time for an overdue instance, in yyyy\-MM\-ddTHH:mm:ssZ format (UTC time). |
|AutoRenew |Boolean |true |Specifies whether to enable Due Automatic renewal for prepaid instances. Value:<br><br><br>* `true`: enables auto\-renewal.<br><br>* `false`: no automatic renewal. |
|ChargeStartTime |String |2023\-09\-22T08:08:35Z |The time when billing starts. Format: yyyy\-MM\-ddTHH:mm:ssZ (UTC time). |
|ChargeEndTime |String |2023\-09\-22T08:08:35Z |The expiration time for subscription billing, in yyyy\-MM\-ddTHH:mm:ssZ format (UTC time). |


<span id="nodeobject"></span>
### NodeObject


|Name |Type |Example |Description |
|---|---|---|---|
|NodeId |String |vedbm\-h441603c68aaa\*\*\*\*\-\*\* |Node ID. |
|ZoneId |String |cn\-beijing\-a |Availability zone ID. |
|NodeType |String |Primary |Node type. Value:<br><br><br>* `Primary`: Primary node.<br><br>* `ReadOnly`: Read\-only node. |
|vCPU |Integer |8 |CPU size. For example, a value of 1 indicates a CPU size of 1U. |
|Memory |Integer |32 |Memory size. Unit is GiB. |
|NodeSpec |String |vedb.mysql.x4.xlarge |The node specification of the instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For detailed information on instance node specifications, refer to <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/Product_specifications">Product specifications</a>.</div><br> |
|FailoverPriority |Integer |5 |The priority of the node for switching to primary. The value ranges from 0 to 15. The larger the value, the higher the priority. |


<span id="tagobject"></span>
### TagObject


|Name |Type |Example |Description |
|---|---|---|---|
|Key |String |department |Tag key bound to the instance. |
|Value |String |game |The tag value associated with the instance. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```json
POST /?Action=DescribeDBInstances&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host:vedbm.cn-beijing.byteplusapi.com.cn
X-Date: 20220101T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20220101/cn-beijing/vedbm/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "PageSize": 10,
    "PageNumber": 1,
    "ChargeType": "PostPaid",
    "InstanceStatus": "Running",
    "CreateTimeEnd": "2023-07-24T06:09:36Z",
    "TagFilters": [
        {
            "Key": "project",
            "Value": "default"
        }
    ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20230801111540C54F0E53A01BAA61D62A",
        "Action": "DescribeDBInstances",
        "Version": "2022-01-01",
        "Service": "vedbm",
        "Region": "cn-beijing"
    },
    "Result": {
        "Instances": [
            {
                "ChargeDetail": {
                    "ChargeStatus": "Normal",
                    "ChargeType": "PostPaid",
                    "OverdueReclaimTime": "",
                    "OverdueTime": ""
                },
                "CreateTime": "2023-07-24T06:09:36Z",
                "DBEngineVersion": "MySQL_8_0",
                "DBRevisionVersion": "3.0.2.1",
                "DeletionProtection": "disabled",
                "InstanceId": "vedbm-d6rjf5ln****",
                "InstanceName": "vedb_test",
                "InstanceStatus": "Running",
                "LowerCaseTableNames": "0",
                "Nodes": [
                    {
                        "Memory": 32,
                        "NodeId": "vedbm-d6rjf5ln****-0",
                        "NodeSpec": "vedb.mysql.x4.xlarge",
                        "NodeType": "ReadOnly",
                        "ZoneId": "cn-beijing-b",
                        "vCPU": 8
                    },
                    {
                        "Memory": 32,
                        "NodeId": "vedbm-d6rjf5ln****-1",
                        "NodeSpec": "vedb.mysql.x4.xlarge",
                        "NodeType": "Primary",
                        "ZoneId": "cn-beijing-b",
                        "vCPU": 8
                    }
                ],
                "PrePaidStorageInGB": 50,
                "ProjectName": "default",
                "RegionId": "cn-beijing",
                "SpecFamily": "Exclusive",
                "StorageChargeType": "PostPaid",
                "StorageType": "IOOptimizedStorage",
                "StorageUsedGiB": 235.16,
                "SubnetId": "subnet-3jh4l05leg6ww3pncmeyb****",
                "Tags": [
                    {
                        "Key": "hhhh",
                        "Value": ""
                    },
                    {
                        "Key": "project",
                        "Value": "default"
                    }
                ],
                "TimeZone": "UTC +08:00",
                "VpcId": "vpc-30uw0duznqt4w7r2qr0un****",
                "ZoneIds": "cn-beijing-b"
            }
        ],
        "Total": 1
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Error_codes).

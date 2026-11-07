---
title: "DescribeInstanceNodes"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/DescribeInstanceNodes"
---

Call DescribeInstanceNodes to query detailed information on member nodes of a specified instance, such as the node type, running status, and resource configurations.

<span id="967d50c9"></span>
## Request Description


* Request method: POST

* Request URL: /?Action=DescribeInstanceNodes&Version=2023\-01\-01 HTTP/1.1


<span id="a266f231"></span>
## Request parameters

<span id="39c13ad5"></span>
### Query


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`DescribeInstanceNodes` |The action that you want to perform. Value: `DescribeInstanceNodes`. |
|Version |String |Yes |`2023-01-01` |The version of the API. Value: `2023-01-01`. |


<span id="5e14b4dc"></span>
### Body


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |o\-00k\*\*\*ko718 |The ID of the instance for which you want to query the node information. |


<span id="512cfd8e"></span>
## Response parameters


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Nodes |Array of [ESNodeInfo](https://docs.byteplus.com/docs/cloudsearch/DescribeInstanceNodes#b25ce44c) |N/A |Details of nodes in the instance, including the node type, running status, and resource configurations. |


<span id="b25ce44c"></span>
### ESNodeInfo


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|IsHot |Boolean |false |Whether the node is a data node of the instance.<br><br><br>* true: The node is a data node.<br><br>* false: The node is not a data node. |
|IsCold |Boolean |false |Whether the node is a cold data node of the instance.<br><br><br>* true: The node is a cold data node.<br><br>* false: The node is not a cold data node. |
|Status |String |Running |The status of the node.<br><br>Valid values: Running, Error, and Warn. |
|IsKibana |Boolean |true |Whether the node is a Kibana node of the instance. Valid values:<br><br><br>* true: The node is a Kibana node.<br><br>* false: The node is not a Kibana node. |
|IsMaster |Boolean |false |Whether the node is a master node of the instance.<br><br><br>* true: The node is a master node.<br><br>* false: The node is not a master node. |
|NodeName |String |es\-coordinator\-00k\*\*\*718\-0 |The node name. |
|StartTime |String |2023\-10\-20 17:17:12 |The last start time of the node. |
|InstanceId |String |o\-00k\*\*\*718 |The instance ID. |
|StorageSpec |Object of [StorageSpec](https://docs.byteplus.com/docs/cloudsearch/DescribeInstanceNodes#7dd71aa0) | |The storage specification details of the node. |
|ResourceSpec |Object of [ResourceSpec](https://docs.byteplus.com/docs/cloudsearch/DescribeInstanceNodes#dfa47548) | |The instance type details of the node. |
|IsCoordinator |Boolean |true |Whether the node is a coordinator node of the instance.<br><br><br>* true: The node is a coordinator node.<br><br>* false: The node is not a coordinator node. |
|RestartNumber |Integer |0 |The number of restart times of the node since creation. |
|NodeDisplayName |String |es\-master\-0 |The display name of the node. |
|IsWarm |Boolean |false |Whether the node is a Warm node of the instance. Valid values:<br><br><br>* true: The node is a Warm node.<br><br>* false: The node is not a Warm node. |


<span id="7dd71aa0"></span>
### StorageSpec


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Description |String |High Performance Cloud Storage\-pl0 |The description of the storage specification. |
|DisplayName |String |ESSD\-PL0 |The display name of the storage specification. |
|MaxSize |Integer |10000 |The maximum size defined by the storage specification. Unit: GiB. |
|MinSize |Integer |20 |The minimum size defined by the storage specification. Unit: GiB. |


<span id="dfa47548"></span>
### ResourceSpec


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Description |String |Standard\-2Core4GiB Node |The description of the instance type. |
|DisplayName |String |2Core4GiB |The display name of the instance type. |
|Memory |Integer |4 |The memory capacity defined by the instance type. Unit: GiB. |
|CPU |Integer |2 |The CPU resources defined by the instance type. Unit: cores. |


<span id="9c7549b6"></span>
## Sample request

```HTTP
POST https://open.ap-southeast-1.byteplusapi.com/?Action=DescribeInstanceNodes&Version=2023-01-01
Content-Type: application/json
X-Date: 20231003T104027Z
Authorization: HMAC-SHA256 
Credential=AKLTMjI2ODVlYzI3ZGY1NGU4ZjhjYWRjMTlmNTM5OTZ****/20231003/ap-southeast-1/ESCloud/request, SignedHeaders=content-type;host;x-date, Signature=88dd0a9ea555d8609ec83eb46054b52f6cd4f79b8d5094fa784c66fa3f2b****
{
    "InstanceId": "o-0080**iu98"
}
```


<span id="f28245e4"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20231020*****7E32DB23E961997AD",
        "Action": "DescribeInstanceNodes",
        "Version": "2023-01-01",
        "Service": "ESCloud",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Nodes": [
            {
                "InstanceId": "o-00k****718",
                "NodeName": "es-coordinator-00k****718-0",
                "NodeDisplayName": "es-coordinator-0",
                "Status": "Running",
                "StartTime": "2023-10-19 17:22:53",
                "RestartNumber": 0,
                "IsMaster": false,
                "IsHot": false,
                "IsCoordinator": true,
                "IsWarm": false,
                "IsCold": false,
                "IsKibana": false,
                "ResourceSpec": {
                    "Description": "",
                    "DisplayName": "",
                    "Memory": 2,
                    "CPU": 1
                },
                "StorageSpec": {
                    "Description": "",
                    "DisplayName": "",
                    "MinSize": 0,
                    "MaxSize": 0,
                    "Type": "",
                    "Size": 0
                }
            },
            {
                "InstanceId": "o-00****o718",
                "NodeName": "es-coordinator-00k****718-1",
                "NodeDisplayName": "es-coordinator-1",
                "Status": "Running",
                "StartTime": "2023-10-19 17:22:53",
                "RestartNumber": 0,
                "IsMaster": false,
                "IsHot": false,
                "IsCoordinator": true,
                "IsWarm": false,
                "IsCold": false,
                "IsKibana": false,
                "ResourceSpec": {
                    "Description": "",
                    "DisplayName": "",
                    "Memory": 2,
                    "CPU": 1
                },
                "StorageSpec": {
                    "Description": "",
                    "DisplayName": "",
                    "MinSize": 0,
                    "MaxSize": 0,
                    "Type": "",
                    "Size": 0
                }
            },
            {
                "InstanceId": "o-00****o718",
                "NodeName": "es-custom-00****o718-cold-0",
                "NodeDisplayName": "es-cold-0",
                "Status": "Running",
                "StartTime": "2023-10-19 17:22:54",
                "RestartNumber": 0,
                "IsMaster": false,
                "IsHot": false,
                "IsCoordinator": false,
                "IsWarm": false,
                "IsCold": true,
                "IsKibana": false,
                "ResourceSpec": {
                    "Description": "",
                    "DisplayName": "",
                    "Memory": 2,
                    "CPU": 1
                },
                "StorageSpec": {
                    "Description": "",
                    "DisplayName": "",
                    "MinSize": 0,
                    "MaxSize": 0,
                    "Type": "ESSD-PL0",
                    "Size": 100
                }
            },
            {
                "InstanceId": "o-00****o718",
                "NodeName": "es-custom-00****o718-cold-1",
                "NodeDisplayName": "es-cold-1",
                "Status": "Running",
                "StartTime": "2023-10-19 17:22:54",
                "RestartNumber": 0,
                "IsMaster": false,
                "IsHot": false,
                "IsCoordinator": false,
                "IsWarm": false,
                "IsCold": true,
                "IsKibana": false,
                "ResourceSpec": {
                    "Description": "",
                    "DisplayName": "",
                    "Memory": 2,
                    "CPU": 1
                },
                "StorageSpec": {
                    "Description": "",
                    "DisplayName": "",
                    "MinSize": 0,
                    "MaxSize": 0,
                    "Type": "ESSD-PL0",
                    "Size": 100
                }
            },
            {
                "InstanceId": "o-00****o718",
                "NodeName": "es-custom-00****o718-cold-2",
                "NodeDisplayName": "es-cold-2",
                "Status": "Running",
                "StartTime": "2023-10-19 17:22:54",
                "RestartNumber": 0,
                "IsMaster": false,
                "IsHot": false,
                "IsCoordinator": false,
                "IsWarm": false,
                "IsCold": true,
                "IsKibana": false,
                "ResourceSpec": {
                    "Description": "",
                    "DisplayName": "",
                    "Memory": 2,
                    "CPU": 1
                },
                "StorageSpec": {
                    "Description": "",
                    "DisplayName": "",
                    "MinSize": 0,
                    "MaxSize": 0,
                    "Type": "ESSD-PL0",
                    "Size": 100
                }
            },
            {
                "InstanceId": "o-00****o718",
                "NodeName": "es-data-00****o718-0",
                "NodeDisplayName": "es-data-0",
                "Status": "Running",
                "StartTime": "2023-10-19 17:22:53",
                "RestartNumber": 0,
                "IsMaster": false,
                "IsHot": true,
                "IsCoordinator": false,
                "IsWarm": false,
                "IsCold": false,
                "IsKibana": false,
                "ResourceSpec": {
                    "Description": "",
                    "DisplayName": "",
                    "Memory": 2,
                    "CPU": 1
                },
                "StorageSpec": {
                    "Description": "",
                    "DisplayName": "",
                    "MinSize": 0,
                    "MaxSize": 0,
                    "Type": "ESSD-PL0",
                    "Size": 20
                }
            },
            {
                "InstanceId": "o-00****o718",
                "NodeName": "es-data-00****o718-1",
                "NodeDisplayName": "es-data-1",
                "Status": "Running",
                "StartTime": "2023-10-19 17:22:53",
                "RestartNumber": 0,
                "IsMaster": false,
                "IsHot": true,
                "IsCoordinator": false,
                "IsWarm": false,
                "IsCold": false,
                "IsKibana": false,
                "ResourceSpec": {
                    "Description": "",
                    "DisplayName": "",
                    "Memory": 2,
                    "CPU": 1
                },
                "StorageSpec": {
                    "Description": "",
                    "DisplayName": "",
                    "MinSize": 0,
                    "MaxSize": 0,
                    "Type": "ESSD-PL0",
                    "Size": 20
                }
            },
            {
                "InstanceId": "o-00****o718",
                "NodeName": "es-data-00****o718-2",
                "NodeDisplayName": "es-data-2",
                "Status": "Running",
                "StartTime": "2023-10-19 17:22:54",
                "RestartNumber": 0,
                "IsMaster": false,
                "IsHot": true,
                "IsCoordinator": false,
                "IsWarm": false,
                "IsCold": false,
                "IsKibana": false,
                "ResourceSpec": {
                    "Description": "",
                    "DisplayName": "",
                    "Memory": 2,
                    "CPU": 1
                },
                "StorageSpec": {
                    "Description": "",
                    "DisplayName": "",
                    "MinSize": 0,
                    "MaxSize": 0,
                    "Type": "ESSD-PL0",
                    "Size": 20
                }
            },
            {
                "InstanceId": "o-00****o718",
                "NodeName": "es-master-00****o718-0",
                "NodeDisplayName": "es-master-0",
                "Status": "Running",
                "StartTime": "2023-10-19 17:22:53",
                "RestartNumber": 0,
                "IsMaster": true,
                "IsHot": false,
                "IsCoordinator": false,
                "IsWarm": false,
                "IsCold": false,
                "IsKibana": false,
                "ResourceSpec": {
                    "Description": "",
                    "DisplayName": "",
                    "Memory": 2,
                    "CPU": 1
                },
                "StorageSpec": {
                    "Description": "",
                    "DisplayName": "",
                    "MinSize": 0,
                    "MaxSize": 0,
                    "Type": "ESSD-PL0",
                    "Size": 20
                }
            },
            {
                "InstanceId": "o-00****o718",
                "NodeName": "es-master-00****o718-1",
                "NodeDisplayName": "es-master-1",
                "Status": "Running",
                "StartTime": "2023-10-19 17:22:53",
                "RestartNumber": 0,
                "IsMaster": true,
                "IsHot": false,
                "IsCoordinator": false,
                "IsWarm": false,
                "IsCold": false,
                "IsKibana": false,
                "ResourceSpec": {
                    "Description": "",
                    "DisplayName": "",
                    "Memory": 2,
                    "CPU": 1
                },
                "StorageSpec": {
                    "Description": "",
                    "DisplayName": "",
                    "MinSize": 0,
                    "MaxSize": 0,
                    "Type": "ESSD-PL0",
                    "Size": 20
                }
            },
            {
                "InstanceId": "o-00****o718",
                "NodeName": "es-master-00****o718-2",
                "NodeDisplayName": "es-master-2",
                "Status": "Running",
                "StartTime": "2023-10-19 17:22:54",
                "RestartNumber": 0,
                "IsMaster": true,
                "IsHot": false,
                "IsCoordinator": false,
                "IsWarm": false,
                "IsCold": false,
                "IsKibana": false,
                "ResourceSpec": {
                    "Description": "",
                    "DisplayName": "",
                    "Memory": 2,
                    "CPU": 1
                },
                "StorageSpec": {
                    "Description": "",
                    "DisplayName": "",
                    "MinSize": 0,
                    "MaxSize": 0,
                    "Type": "ESSD-PL0",
                    "Size": 20
                }
            },
            {
                "InstanceId": "o-00****o718",
                "NodeName": "kibana-00****o718",
                "NodeDisplayName": "kibana",
                "Status": "Running",
                "StartTime": "2023-10-19 17:22:54",
                "RestartNumber": 0,
                "IsMaster": false,
                "IsHot": false,
                "IsCoordinator": false,
                "IsWarm": false,
                "IsCold": false,
                "IsKibana": true,
                "ResourceSpec": {
                    "Description": "",
                    "DisplayName": "",
                    "Memory": 2,
                    "CPU": 1
                },
                "StorageSpec": {
                    "Description": "",
                    "DisplayName": "",
                    "MinSize": 0,
                    "MaxSize": 0,
                    "Type": "",
                    "Size": 0
                }
            }
        ]
    }
}
```

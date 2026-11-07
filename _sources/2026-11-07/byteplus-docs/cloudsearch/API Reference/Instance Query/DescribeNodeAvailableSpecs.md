---
title: "DescribeNodeAvailableSpecs"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/DescribeNodeAvailableSpecs"
---

Call DescribeNodeAvailableSpecs to query the available node types, instance types, and storage specifications as well as the billing configuration code.

<span id="f1b62825"></span>
## Request Description


* Request method: POST

* Request URL: /?Action=DescribeNodeAvailableSpecs&Version=2023\-01\-01 HTTP/1.1


<span id="463bd052"></span>
## Request parameters

<span id="4dc2a7ca"></span>
### Query


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`DescribeNodeAvailableSpecs` |The action that you want to perform. Value: `DescribeNodeAvailableSpecs`. |
|Version |String |Yes |`2023-01-01` |The version of the API. Value: `2023-01-01`. |


<span id="bb6a3b4c"></span>
### Body


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |No |o\-00k\*\*\*\*718 |The ID of the instance to be queried. |


<span id="6cf7535f"></span>
## Response parameters


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|ConfigurationCode |String |es.standard |The configuration code for billing. |
|NodeAvailableSpecs |Array of [NodeAvailableSpecs](https://docs.byteplus.com/docs/cloudsearch/DescribeNodeAvailableSpecs#a8343f41) | |The list of available nodes, which are categorized by node type. |
|ResourceSpecs |Array of [ResourceSpecs](https://docs.byteplus.com/docs/cloudsearch/DescribeNodeAvailableSpecs#d334388a) | |The list of available instance types for nodes. |
|StorageSpecs |Array of [StorageSpecs](https://docs.byteplus.com/docs/cloudsearch/DescribeNodeAvailableSpecs#6307c7f9) | |The list of available storage specifications. |
|AZAvailableSpecsSoldOut |Array of AZAvailableSpecsSoldOut | **{** <br><br>"ap\-southeast\-1": "1"<br><br> **}**  |The list of available Availability Zones in the current Region. |


<span id="a8343f41"></span>
### NodeAvailableSpecs


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|ResourceSpecNames |Array of String |```JSON```<br>```[```<br>```"es.x4.small",```<br>```"es.x2.medium",```<br>```"es.x4.medium",```<br>```"es.x8.medium",```<br>```......```<br>```]```<br> |The name of the instance type. Different instance types define different numbers of CPU cores and different memory sizes. For more information, refer to [instance types](https://docs.byteplus.com/en/docs/cloudsearch/specifications). |
|StorageSpecNames |Array of String |`["es.volume.essd.pl0"]` |The name of the storage specification. Valid value:<br><br><br>* `es.volume.essd.pl0`: Standard\-High Performance Cloud Storage\-pl0<br><br>* `es.volume.essd.flexpl-standard`: Standard\-High Performance Cloud Storage\-flexpl |
|Type |String |`Master` |The node type. Valid values:<br><br><br>* Master: master node.<br><br>* Kibana: Kibana node.<br><br>* Hot: data node.<br><br>* Coordinator: coordinator node.<br><br>* Cold: cold data node.<br><br>* Warm: warm data node. |


<span id="d334388a"></span>
### ResourceSpecs


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Description |String |Standard\-2C4G Node |The description of the instance type. |
|DisplayName |String |2Core4GiB |The display name of the instance type. |
|Memory |Integer |4 |The memory capacity defined by the instance type. Unit: GiB. |
|CPU |Integer |2 |The CPU resources defined by the instance type. Unit: cores. |
|Name |String |`es.x2.medium` |The instance type of the node. For more information on the types and details of instance types, refer to [instance types](https://docs.byteplus.com/en/docs/cloudsearch/specifications). |


<span id="6307c7f9"></span>
### StorageSpecs


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Description |String |High Performance Cloud Storage\-pl0 |The description of the storage specification. |
|DisplayName |String |ESSD\-PL0 |The display name of the storage specification. |
|MaxSize |Integer |10000 |The maximum size defined by the storage specification. Unit: GiB. |
|MinSize |Integer |20 |The minimum size defined by the storage specification. Unit: GiB. |
|Name |String |es.volume.essd.pl0 |The name of the storage specification. Valid value:<br><br><br>* `es.volume.essd.pl0`: High Performance Cloud Storage\-pl0<br><br>* `es.volume.essd.flexpl-standard`: High Performance Cloud Storage\-flexpl |


<span id="191a63eb"></span>
## Sample request

```HTTP
POST https://open.ap-southeast-1.byteplusapi.com/?Action=DescribeNodeAvailableSpecs&Version=2023-01-01 HTTP/1.1
Content-Type: application/json
X-Date: 20231003T104027Z
Authorization: HMAC-SHA256 
Credential=AKLTMjI2ODVlYzI3ZGY1NGU4ZjhjYWRjMTlmNTM5OTZ****/20231003/ap-southeast-1/ESCloud/request, SignedHeaders=content-type;host;x-date, Signature=88dd0a9ea555d8609ec83eb46054b52f6cd4f79b8d5094fa784c66fa3f2b****
{
    "InstanceId": "o-00k04h**"
}
```


<span id="0e5c32ff"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2023102317***B8FC2F8D8122",
        "Action": "DescribeNodeAvailableSpecs",
        "Version": "2023-01-01",
        "Service": "ESCloud",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "ConfigurationCode": "es.standard",
        "NodeAvailableSpecs": [
            {
                "ResourceSpecNames": [
                    "es.x4.small",
                    "es.x2.medium",
                    "es.x4.medium",
                    "es.x2.large",
                    "es.x4.large",
                    "es.x2.xlarge",
                    "es.x4.xlarge",
                    "es.x2.2xlarge",
                    "es.x4.2xlarge",
                    "es.x2.2.5xlarge",
                    "es.x4.2.5xlarge",
                    "es.x2.3xlarge"
                ],
                "StorageSpecNames": [
                    "es.volume.essd.pl0"
                ],
                "Type": "Master"
            },
            {
                "ResourceSpecNames": [
                    "kibana.x2.small"
                ],
                "Type": "Kibana"
            },
            {
                "ResourceSpecNames": [
                    "es.x4.small",
                    "es.x2.medium",
                    "es.x4.medium",
                    "es.x2.large",
                    "es.x4.large",
                    "es.x2.xlarge",
                    "es.x4.xlarge",
                    "es.x2.2xlarge",
                    "es.x4.2xlarge",
                    "es.x2.2.5xlarge",
                    "es.x4.2.5xlarge",
                    "es.x2.3xlarge",
                    "es.x4.3xlarge"
                ],
                "StorageSpecNames": [
                    "es.volume.essd.pl0",
                    "es.volume.essd.flexpl"
                ],
                "Type": "Hot"
            },
            {
                "ResourceSpecNames": [
                    "es.x4.small",
                    "es.x2.medium",
                    "es.x4.medium",
                    "es.x2.large",
                    "es.x4.large",
                    "es.x2.xlarge",
                    "es.x4.xlarge",
                    "es.x2.2xlarge",
                    "es.x4.2xlarge",
                    "es.x2.2.5xlarge",
                    "es.x4.2.5xlarge",
                    "es.x2.3xlarge"
                ],
                "StorageSpecNames": [
                    "es.volume.essd.pl0"
                ],
                "Type": "Coordinator"
            },
            {
                "ResourceSpecNames": [
                    "es.x4.small",
                    "es.x2.medium",
                    "es.x4.medium",
                    "es.x2.large",
                    "es.x4.large",
                    "es.x2.xlarge",
                    "es.x4.xlarge",
                    "es.x2.2xlarge",
                    "es.x4.2xlarge",
                    "es.x2.2.5xlarge",
                    "es.x4.2.5xlarge",
                    "es.x2.3xlarge",
                    "es.x4.3xlarge"
                ],
                "StorageSpecNames": [
                    "es.volume.essd.pl0"
                ],
                "Type": "Cold"
            }
        ],
        "ResourceSpecs": [
            {
                "Description": "Kibana-1Core2GiB Node",
                "DisplayName": "1Core2GiB",
                "Memory": 2,
                "Name": "kibana.x2.small",
                "CPU": 1
            },
            {
                "Description": "Standard-1Core4GiB Node",
                "DisplayName": "1Core4GiB",
                "Memory": 4,
                "Name": "es.x4.small",
                "CPU": 1
            },
            {
                "Description": "Standard-2Core4GiB Node",
                "DisplayName": "2Core4GiB",
                "Memory": 4,
                "Name": "es.x2.medium",
                "CPU": 2
            },
            {
                "Description": "Standard-2Core8GiB Node",
                "DisplayName": "2Core8GiB",
                "Memory": 8,
                "Name": "es.x4.medium",
                "CPU": 2
            },
            {
                "Description": "Standard-4Core8GiB Node",
                "DisplayName": "4Core8GiB",
                "Memory": 8,
                "Name": "es.x2.large",
                "CPU": 4
            },
            {
                "Description": "Standard-4Core16GiB Node",
                "DisplayName": "4Core16GiB",
                "Memory": 16,
                "Name": "es.x4.large",
                "CPU": 4
            },
            {
                "Description": "Standard-8Core16GiB Node",
                "DisplayName": "8Core16GiB",
                "Memory": 16,
                "Name": "es.x2.xlarge",
                "CPU": 8
            },
            {
                "Description": "Standard-8Core32GiB Node",
                "DisplayName": "8Core32GiB",
                "Memory": 32,
                "Name": "es.x4.xlarge",
                "CPU": 8
            },
            {
                "Description": "Standard-16Core32GiB Node",
                "DisplayName": "16Core32GiB",
                "Memory": 32,
                "Name": "es.x2.2xlarge",
                "CPU": 16
            },
            {
                "Description": "Standard-16Core64GiB Node",
                "DisplayName": "16Core64GiB",
                "Memory": 64,
                "Name": "es.x4.2xlarge",
                "CPU": 16
            },
            {
                "Description": "Standard-24Core48GiB Node",
                "DisplayName": "24Core48GiB",
                "Memory": 48,
                "Name": "es.x2.2.5xlarge",
                "CPU": 24
            },
            {
                "Description": "Standard-24Core96GiB Node",
                "DisplayName": "24Core96GiB",
                "Memory": 96,
                "Name": "es.x4.2.5xlarge",
                "CPU": 24
            },
            {
                "Description": "Standard-32Core64GiB Node",
                "DisplayName": "32Core64GiB",
                "Memory": 64,
                "Name": "es.x2.3xlarge",
                "CPU": 32
            },
            {
                "Description": "Standard-32Core128GiB Node",
                "DisplayName": "32Core128GiB",
                "Memory": 128,
                "Name": "es.x4.3xlarge",
                "CPU": 32
            }
        ],
        "StorageSpecs": [
            {
                "Description": "Standard-High Performance Cloud Storage-pl0",
                "DisplayName": "ESSD-PL0",
                "MaxSize": 10000,
                "MinSize": 20,
                "Name": "es.volume.essd.pl0",
                "Size": 0,
                "Type": ""
            },
            {
                "Description": "Standard-High Performance Cloud Storage-flexpl",
                "DisplayName": "FlexPL",
                "MaxSize": 10000,
                "MinSize": 20,
                "Name": "es.volume.essd.flexpl",
                "Size": 0,
                "Type": ""
            }
        ],
        "AZAvailableSpecsSoldOut": {
            "ap-southeast-1": "1"
        }
    }
}
```

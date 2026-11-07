---
title: "ModifyNodeSpecInOneStep"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/ModifyNodeSpecInOneStep"
---

Call ModifyNodeSpecInOneStep to upgrade or downgrade the node configurations of an instance in one step.

<span id="e7d38561"></span>
## Precautions

When upgrading or downgrading instance configurations, pay attention to the following points:


* In a downgrade request, you can only downgrade the instance type of each node.

* In an upgrade request, you can upgrade the instance type and increase the number of nodes and storage capacity for each type of node. Upgrade specifics vary depending on the node type.

* Only instances in the **Running** state (indicated by green) can be upgraded. Instances in other states cannot be upgraded.

* Upgrading the instance type triggers an instance restart. We recommend that you perform this operation during off\-peak hours. If an upgrade request only increases the storage capacity or the number of nodes, the change takes effect without an instance restart.


<span id="fd6b9db2"></span>
## Request Description


* Request method: POST

* Request URL: /?Action=ModifyNodeSpecInOneStep&Version=2023\-01\-01 HTTP/1.1


<span id="bea45bae"></span>
## Request parameters

<span id="fd563369"></span>
### Query


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`ModifyNodeSpecInOneStep` |The action that you want to perform. Value: `ModifyNodeSpecInOneStep`. |
|Version |String |Yes |`2023-01-01` |The version of the API. Value: `2023-01-01`. |


<span id="56fb99d0"></span>
### Body


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |o\-0080\*\*iu98 |The ID of the instance whose node configurations you want to change. |
|NodeSpecsAssigns |Array of [EsNodeSpecAssign](https://docs.byteplus.com/docs/cloudsearch/ModifyNodeSpecInOneStep#d152ade8) |Yes | |The node type and other configuration details.<br><br>The following node types support configuration changes: Kibana, Master, Hot, Coordinator, Warm, and Cold. |


<span id="d152ade8"></span>
### EsNodeSpecAssign


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|Type |String |Yes |Hot |The type of the node whose configurations you want to change.<br><br><br>* Master: master node.<br><br>* Hot: data node.<br><br>* Warm: warm data node.<br><br>* Cold: cold data node.<br><br>* Kibana: Kibana node.<br><br>* Coordinator: coordinator node.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For any node configuration changes, the configuration information for both master and data nodes must be included within an array structure.</div><br> |
|Number |Integer |Yes |2 |The number of nodes.<br><br><br>* For upgrades, you can increase the number of nodes for all node types except for Kibana and dedicated master nodes.<br><br>* For downgrades, you can decrease the number of nodes only for coordinator nodes. |
|StorageSize |Integer |Yes |100 |The storage capacity. Unit: GiB. The value must be a multiple of 10.<br><br><br>* For upgrades, you can increase the storage capacity only for data nodes and cold nodes.<br><br>* For downgrades, you cannot decrease the storage capacity for all node types. |
|ResourceSpecName |String |Yes |es.x4.medium |The name of the instance type. The instance type can be changed for all node types.<br><br>To get a list of available instance types for nodes, call [DescribeNodeAvailableSpecs](https://docs.byteplus.com/docs/cloudsearch/DescribeNodeAvailableSpecs). Alternatively, refer to [Specifications](https://docs.byteplus.com/en/docs/cloudsearch/specifications) for details of the instance types for nodes. |
|StorageSpecName |String |Yes |es.volume.essd.pl0 |The name of the storage specification.<br><br><br>* `es.volume.essd.pl0`: High Performance Cloud Storage\-pl0.<br><br>* `es.volume.essd.flexpl-standard`: High Performance Cloud Storage\-flexpl<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For Kibana nodes, leave the <strong>StorageSpecName</strong> parameter blank, that is, <code>"StorageSpecName": ""</code>.</div><br> |


<span id="609dc42d"></span>
## Response parameters


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|InstanceId |String |o\-0080\*\*iu98 |The instance ID returned after the node configurations are changed. |


<span id="f5f7d223"></span>
## Sample request

```HTTP
POST https://open.ap-southeast-1.byteplusapi.com/?Action=ModifyNodeSpecInOneStep&Version=2023-01-01
Content-Type: application/json
X-Date: 20231003T104027Z
Authorization: HMAC-SHA256 
Credential=AKLTMjI2ODVlYzI3ZGY1NGU4ZjhjYWRjMTlmNTM5OTZ****/20231003/ap-southeast-1/ESCloud/request, SignedHeaders=content-type;host;x-date, Signature=88dd0a9ea555d8609ec83eb46054b52f6cd4f79b8d5094fa784c66fa3f2b****
{
    "InstanceId": "o-0080**iu98",
    "NodeSpecsAssigns": [
        {
            "Number": 2,
            "ResourceSpecName": "es.x4.medium",
            "StorageSize": 100,
            "StorageSpecName": "es.volume.essd.pl0",
            "Type": "Hot"
        }
    ]
}
```


<span id="9f804a2d"></span>
## Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20231116113434C***959520",
        "Action": "ModifyNodeSpecInOneStep",
        "Version": "2023-01-01",
        "Service": "escloud",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "InstanceId": "o-00***iu98"
    }
}
```

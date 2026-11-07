---
title: "ListVirtualNodes"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/ListVirtualNodes"
---

Query the list and details of virtual nodes that meet the specified criteria.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">[<a href="https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features"><strong>Beta · Apply for Trial</strong></a>]: APIs related to virtual nodes are in the <strong>beta</strong> phase. To use these APIs, submit an application.</div>


<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point for your business region.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=ListVirtualNodes&Version=2022\-05\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table describes the API request parameters. You also need to use public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters).


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |ListVirtualNodes |The API name. The name of the current API is `ListVirtualNodes`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|Filter |Object of [VirtualNodesFilter](https://docs.byteplus.com/en/docs/vke/ListVirtualNodes#virtualnodesfilter) |no |\- |The criteria used for querying virtual nodes. |
|PageNumber |Integer |no |1 |The starting page number when querying. The default number is 1. |
|PageSize |Integer |no |10 |The number of results per page:<br><br><br>* Minimum value: 1<br><br>* Maximum value: 100<br><br>* Default value: 10 |


&nbsp;


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |ListVirtualNodes |The API name. The name of the current API is `ListVirtualNodes`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|Filter |Object of [VirtualNodesFilter](https://docs.byteplus.com/en/docs/vke/ListVirtualNodes#virtualnodesfilter) |no |\- |The criteria used for querying virtual nodes. |
|PageNumber |Integer |no |1 |The starting page number when querying. The default number is 1. |
|PageSize |Integer |no |10 |The number of results per page:<br><br><br>* Minimum value: 1<br><br>* Maximum value: 100<br><br>* Default value: 10 |


<span id="virtualnodesfilter"></span>
### VirtualNodesFilter


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Ids |Array of String |no |["v73mhao7vj0g58ozfe53xxxx"] |The list of virtual node IDs.<br><br>You can enter up to 10 virtual node IDs each time. |
|Name |String |no |node\-1 |The name of the virtual node. Fuzzy matching is supported.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If this parameter is left empty, the information about all virtual nodes in the specified region will be returned.</div><br> |
|Statuses |Array of [VirtualNodeStatusFilterRequest](https://docs.byteplus.com/en/docs/vke/ListVirtualNodes#virtualnodestatusfilterrequest) |no |\- |The status of the virtual node.<br><br>You can enter up to 15 elements in the array at a time. The logic **OR** relationship is applied to multiple states. |


<span id="virtualnodestatusfilterrequest"></span>
### VirtualNodeStatusFilterRequest


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Phase |String |no |Running |The status of the virtual node. Valid values:<br><br><br>* **Creating**<br><br>* **Running**<br><br>* **Deleting**<br><br>* **Failed**<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For valid combinations of <strong>Phase</strong> and <strong>Conditions.Type</strong>, see <a href="https://docs.byteplus.com/en/docs/vke/Resource-status-description">Resource status description</a>.</div><br> |
|Conditions.Type |String |no |Ok |The condition under which the virtual node enters the primary status. You can specify multiple conditions. Valid values:<br><br><br>* **Progressing**<br><br>* **Ok**<br><br>* **Unavailable**<br><br>* **CreateFailed**<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For valid combinations of <strong>Phase</strong> and <strong>Conditions.Type</strong>, see <a href="https://docs.byteplus.com/en/docs/vke/Resource-status-description">Resource status description</a>.</div><br> |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST /?Action=ListVirtualNodes&Version=2022-05-12 HTTP/1.1
Content-Type:application/json
{
    "Filter": {
        "Ids": ["vck4gdidlemc3ou******"]
    },
    "PageNumber": 1,
    "PageSize": 10
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following table contains the response parameters of this API. See [Response results](https://docs.byteplus.com/en/docs/vke/Response) for details about public response parameters.


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Items |Array of [VirtualNode](https://docs.byteplus.com/en/docs/vke/ListVirtualNodes#virtualnode) |\- |The virtual node list. |
|PageNumber |Integer |1 |The current page number. |
|PageSize |Integer |10 |The number of virtual nodes displayed on each page. |
|TotalCount |Integer |11 |The total number of virtual nodes that meet the criteria. |


<span id="virtualnode"></span>
### VirtualNode


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Id |String |v73mhao7vj\*\*\*\*\*\*\*\* |The ID of the virtual node. |
|CreateClientToken |String |BC028527\-33B9\-4990\-A633\-84E9F9\*\*\*\*\*\* |The client token returned upon successful creation. The client token is a string that ensures the idempotency of the request. This string is provided by the caller. |
|Name |String |vci\-vnode\-cn\-beijing\-1 |The name of the virtual node. |
|VirtualNodeConfig |Object of [VirtualNodeConfig](https://docs.byteplus.com/en/docs/vke/ListVirtualNodes#virtualnodeconfig) |\- |The configuration information of the virtual node. |
|KubernetesConfig |Object of [VirtualNodeKubernetesConfigResponse](https://docs.byteplus.com/en/docs/vke/ListVirtualNodes#virtualnodekubernetesconfigresponse) |\- |The Kubernetes configuration information of the virtual node. |
|Status |Object of [VirtualNodeStatus](https://docs.byteplus.com/en/docs/vke/ListVirtualNodes#virtualnodestatus) |\- |The status of the virtual node. |
|CreateTime |String |2022\-05\-06T02:49:19Z |The time when the virtual node was created.<br><br>UTC + 0 time in standard [RFC3339](https://tools.ietf.org/html/rfc3339) format. |


<span id="virtualnodeconfig"></span>
### VirtualNodeConfig


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|VpcId |String |vpc\-2d73mgm\*\*\*\*\*\*\*\* |The ID of the VPC where the virtual node network is located. |
|SubnetIds |Array of String |["subnet\-2d73mhao7vj0g58ozf\*\*\*\*"] |The IDs of subnets where the virtual node network is located. |
|SecurityGroupIds |Array of String |["sg\-3re8ffwjclybk5zsk\*\*\*\*"] |The IDs of security groups where the virtual node network is located. |


<span id="virtualnodekubernetesconfigresponse"></span>
### VirtualNodeKubernetesConfigResponse


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Labels |Array of [Label](https://docs.byteplus.com/en/docs/vke/ListVirtualNodes#label) |\- |The Kubernetes label information of the virtual node. |
|Taints |Array of [Taint](https://docs.byteplus.com/en/docs/vke/ListVirtualNodes#taint) |\- |The Kubernetes taint information of the virtual node. |


<span id="label"></span>
### Label


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Key |String |label\-key |The label key. |
|Value |String |label\-value |The label value. |


<span id="taint"></span>
### Taint


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Effect |String |NoSchedule |The taint effect. Valid values:<br><br><br>* **NoSchedule**: No scheduling is performed.<br><br>* **NoExecute**: Pods that do not tolerate the taint are evicted.<br><br>* **PreferNoSchedule**: Avoid scheduling if possible. |
|Key |String |taint\-key |The taint key. |
|Value |String |taint\-value |The taint value. |


<span id="virtualnodestatus"></span>
### VirtualNodeStatus


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Phase |String |Creating |The status of the virtual node. Valid values:<br><br><br>* **Creating**<br><br>* **Running**<br><br>* **Deleting**<br><br>* **Failed**<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For valid combinations of <strong>Phase</strong> and <strong>Conditions.Type</strong>, see <a href="https://docs.byteplus.com/en/docs/vke/Resource-status-description">Resource status description</a>.</div><br> |
|Conditions |Array of [VirtualNodeStatusCondition](https://docs.byteplus.com/en/docs/vke/ListVirtualNodes#virtualnodestatuscondition) |\- |The condition under which the virtual node enters the primary status.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For valid combinations of <strong>Phase</strong> and <strong>Conditions.Type</strong>, see <a href="https://docs.byteplus.com/en/docs/vke/Resource-status-description">Resource status description</a>.</div><br> |


<span id="virtualnodestatuscondition"></span>
### VirtualNodeStatusCondition


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Type |String |Ok |The condition under which the virtual node enters the primary status. You can specify multiple conditions. Valid values:<br><br><br>* **Progressing**<br><br>* **Ok**<br><br>* **Unavailable**<br><br>* **CreateFailed** |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1 200 OK
Content-Type:application/json
{
    "ResponseMetadata": {
        "RequestId": "021635*******",
        "Action": "ListVirtualNodes",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    },
    "Result": {
        "TotalCount": 1,
        "PageNumber": 1,
        "PageSize": 10,
        "Items": [
            {
                "Id": "vck4gdidle********",
                "Name": "demo-6",
                "VirtualNodeConfig": {
                    "VpcId": "vpc-3reuafbrw1********",
                    "SubnetIds": [
                        "subnet-3rfcnoazj4cu85zsk2j******"
                    ],
                    "SecurityGroupIds": [
                        "sg-3reuafhozdwjk5zsk2i******"
                    ]
                },
                "KubernetesConfig": {
                    "Labels": [
                        {
                            "Key": "xx/aaaaa",
                            "Value": "v1"
                        }
                    ],
                    "Taints": [
                        {
                            "Key": "t1",
                            "Value": "tv1",
                            "Effect": "NoSchedule"
                        }
                    ]
                },
                "Status": {
                    "Phase": "Running",
                    "Conditions": [
                        {
                            "Type": "Ok"
                        }
                    ]
                },
                "CreateTime": "2023-09-19T02:26:17Z"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no error codes proprietary to this API. See [Public error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes) for details about public error codes.

&nbsp;

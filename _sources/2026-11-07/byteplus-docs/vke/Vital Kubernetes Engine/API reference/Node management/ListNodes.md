---
title: "ListNodes"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/ListNodes"
---

Query the list and details of nodes that meet the specified conditions.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point based on the region where your business is located.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=ListNodes&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListNodes&serviceCode=vke&version=2022-05-12&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameter

The following table describes the API request parameters. You also need to provide public parameters when calling this API. For details about public request parameters, see [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters).


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |ListNodes |The API name. The name of the current API is `ListNodes`. |
|Version |String |Yes |May 12, 2022 |The API version. The API version is `2022-05-12`. |
|Filter |Object of [ListNodesFilter](https://docs.byteplus.com/en/docs/90/21166#listnodesfilter) |No |\- |Node filter. |
|PageNumber |Integer |No |1 |The starting page number for paginated queries. The value starts at 1 and defaults to 1. |
|PageSize |Integer |No |10 |The number of results per page:<br><br><br>* Minimum value: 1<br><br>* Maximum value: 100<br><br>* Default value: 10 |


<span id="listnodesfilter"></span>
### ListNodesFilter


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|ClusterIds |Array of String |No |["cc5silumrsfeqxxxx"] |A list of cluster IDs.<br><br>You can call the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API to obtain cluster IDs. Up to 100 cluster IDs can be included in a single query.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If this parameter is an empty array, filtering is performed based on all clusters in the specified region within the account.</div><br> |
|Ids |Array of String |No |["nc5t5epmrsfxxxx"] |A list of node IDs.<br><br>At most 100 node IDs can be specified per call. |
|Name |String |No |test\-node |Node name.<br><br>Fuzzy matching is supported. |
|NodePoolIds |Array of String |No |["pc8oah9cbcvxxxx"] |A list of node pool IDs.<br><br>You can call the [ListNodePools](https://docs.byteplus.com/en/docs/vke/ListNodePools) API to obtain node pool IDs. At most 100 node pool IDs can be specified per call. |
|ZoneIds |Array of String |No |["cn\-beijing\-a"] |A list of availability zone IDs. For a complete list of VKE availability zones, see [Regions and availability zones](https://docs.byteplus.com/en/docs/vke/Regions-and-Availability-Zones). |
|Statuses |Array of [NodeStatusFilter](https://docs.byteplus.com/en/docs/90/21166#nodestatusfilter) |No |\- |Node status.<br><br>At most 15 array elements can be specified per call. The logic OR is applied to represent relations among multiple statuses. |
|CreateClientToken |String |No |BusinessRequest12345 |The ClientToken generated upon successful creation.<br><br>A string used to ensure the idempotency of the request. This string is passed in by the caller and must be unique across different requests. ClientToken is case\-sensitive and can consist of 64 ASCII characters at most. |
|InstanceIds |Array of String |No |["i\-yd329xxxx"] |The ID of the ECS instance corresponding to the node. Exact matching is required.<br><br>You can call the [DescribeInstances](https://docs.byteplus.com/en/docs/ecs/DescribeInstances) API to obtain the ECS instance ID of the node. Up to 100 ECS instance IDs can be specified per call. |
|MetadataName |String |No |192.168.\*\*\*.\*\*\* |Filter by node metadata name. Fuzzy matching is supported. |
|AffinityGroupIds |Array of String |No |["agp\-xxxx"] |[[Beta - apply for trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] Filter by affinity group ID for precise querying.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">To use affinity group\-related capabilities of node pools, you need to obtain beta access to both the VKE feature and ‌the ECS affinity group capabilities‌. Consult your BytePlus account manager for details.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">You can call the <a href="https://docs.byteplus.com/en/docs/ecs/DescribeCloudAssistantStatus">DescribeInstances</a> API to obtain the affinity group ID.</div><br> |


<span id="nodestatusfilter"></span>
### NodeStatusFilter


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Phase |String |No |Running |Node status. Valid values:<br><br><br>* **Creating**: It is being created.<br><br>* **Running**: It is running.<br><br>* **Deleting**: It is being deleted.<br><br>* **Failed**: An abnormality has occurred.<br><br>* **Updating**: It is being updated.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">At least one of <strong>Phase</strong> and <strong>Conditions.Type</strong> must be provided. Otherwise, it is an invalid array element. For valid combinations of <strong>Phase</strong> and <strong>Conditions.Type</strong>, see <a href="https://docs.byteplus.com/en/docs/vke/Resource-status-description">Resource status description</a>.</div><br> |
|Conditions.Type |String |No |Ok |The condition under which the node enters the primary status. You can specify multiple conditions. Valid values:<br><br><br>* **Progressing**: The processing is in progress.<br><br>* **Ok**: The status is normal.<br><br>* **Unschedulable**: It is unschedulable.<br><br>* **InitilizeFailed**: Initialization failed.<br><br>* **NotReady**: It is abnormal.<br><br>* **Balance**: The account is in arrears.<br><br>* **ResourceCleanupFailed**: Removal of linked resources failed.<br><br>* **Unknown**: An unknown error occurs.<br><br>* **ClusterVersionUpgrading**: The node version is being upgraded.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">At least one of <strong>Phase</strong> and <strong>Conditions.Type</strong> must be provided. Otherwise, it is an invalid array element. For valid combinations of <strong>Phase</strong> and <strong>Conditions.Type</strong>, see <a href="https://docs.byteplus.com/en/docs/vke/Resource-status-description">Resource status description</a>.</div><br> |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://vke.cn-beijing.byteplusapi.com.cn?Action=ListNodes&Version=2022-05-12 HTTP/1.1
Content-Type:application/json
{
    "PageNumber": 1,
    "PageSize": 10,
    "Filter": {
        "ClusterIds": [
            "cc5silumrsfeq****"
        ],
        "NodePoolIds": [
            "pc8oah9cbcv****"
        ],
        "Statuses": [
            {
                "Phase": "Running",
                "Conditions.Type": "Ok"
            }
        ]
    }
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

The following table contains the response parameters of this API. See [Response results](https://docs.byteplus.com/en/docs/vke/Response) for details about public response parameters.


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Items |Array of [Node](https://docs.byteplus.com/en/docs/90/21166#node) |\- |A list of nodes. |
|PageNumber |Integer |1 |The current page number. |
|PageSize |Integer |10 |Number of nodes displayed per page. |
|TotalCount |Integer |100 |Total number of nodes that meet the conditions. |


<span id="node"></span>
### Node


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Id |String |nc5t5ep\*\*\*\*\*\*\*\* |Node ID. |
|Name |String |test\-node |Node name. |
|ClusterId |String |cc5silum\*\*\*\*\*\*\*\* |Cluster ID. |
|InstanceId |String |i\-ybo922\*\*\*\*\*\*\*\* |ID of the ECS instance corresponding to the node. |
|NodePoolId |String |pc8oah9\*\*\*\*\*\*\*\* |The node pool ID. |
|ZoneId |String |cn\-bei\*\*\*\*\*\* |Availability zone ID. |
|Roles |Array of String |["Worker"] |Node role. Valid values:<br><br>**Worker**: Worker node |
|CreateClientToken |String |BusinessRequest12345 |The ClientToken generated upon successful creation.<br><br>The ClientToken is a string that ensures request idempotency. This string is provided by the caller. |
|CreateTime |String |2021\-10\-27T10:33:30Z |The creation time.<br><br>UTC+0 time in standard [RFC3339](https://tools.ietf.org/html/rfc3339) format. |
|UpdateTime |String |2021\-10\-29T10:33:30Z |Update time.<br><br>UTC+0 time in standard [RFC3339](https://tools.ietf.org/html/rfc3339) format. |
|Status |Object of [NodeStatus](https://docs.byteplus.com/en/docs/90/21166#nodestatus) |\- |Node status. |
|IsVirtual |Boolean |false |Whether it is a virtual node. Values:<br><br><br>* **false**: No<br><br>* **true**: Yes |
|AdditionalContainerStorageEnabled |Boolean |false |Whether a data volume on the node has been configured as the storage directory for container images and logs. Valid values:<br><br><br>* **false**: No<br><br>* **true**: Yes |
|ContainerStoragePath |String |/dev/vdb |Device name of the data volume used as the storage directory for container images and logs. |
|ImageId |String |image\-kd\*\*\*\*\*\*\*\* |ID of the image used by the ECS instance corresponding to the node. |
|InitializeScript |String |ZWNob\*\*\*\* |The script executed after creating the ECS node and deploying Kubernetes components. |
|KubernetesConfig |Object of [KubernetesConfigResponse](https://docs.byteplus.com/en/docs/90/21166#kubernetesconfigresponse) |\- |Kubernetes\-related configuration used during node initialization.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><strong>Labels</strong> and <strong>taints</strong> added after node creation will not be returned by this OpenAPI call. To obtain them, <a href="https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster">connect to the cluster</a> and use the Kubernetes API. For information about the Kubernetes API, see the <a href="https://kubernetes.io/docs/reference/kubernetes-api/cluster-resources/node-v1/">official documentation</a>.</div><br> |
|PreScript |String |ZWNob\*\*\*\* |[[Beta - apply for trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] Base64\-encoded content of the script executed before deploying the node.[Beta \- apply for trial] |
|MetadataName |String |192.168.\*\*\*.\*\*\* |Metadata name of the node object in Kubernetes. |
|AffinityGroupId |String |affinityGro\*\*\*\*\*\*\*\* |[[Beta - apply for trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] The ID of the affinity group to which the node belongs. |
|GpuDriverVersion |String |550.1.1 |GPU driver version. |
|ContainerStorageMountPoint |String |/mnt/vdb |The target mount directory after the data volume device is formatted. |


<span id="nodestatus"></span>
### NodeStatus


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Phase |String |Running |Node status. Valid values:<br><br><br>* **Creating**: It is being created.<br><br>* **Running**: It is running.<br><br>* **Deleting**: It is being deleted.<br><br>* **Failed**: An abnormality has occurred.<br><br>* **Updating**: It is being updated.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For valid combinations of <strong>Phase</strong> and <strong>Conditions.Type</strong>, see <a href="https://docs.byteplus.com/en/docs/vke/Resource-status-description">Resource status description</a>.</div><br> |
|Conditions |Array of [NodeStatusCondition](https://docs.byteplus.com/en/docs/90/21166#nodestatuscondition) |\- |The condition under which the node enters the primary status.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For valid combinations of <strong>Phase</strong> and <strong>Conditions.Type</strong>, see <a href="https://docs.byteplus.com/en/docs/vke/Resource-status-description">Resource status description</a>.</div><br> |


<span id="nodestatuscondition"></span>
### NodeStatusCondition


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Type |String |Ok |The condition under which the node enters the primary status. You can specify multiple conditions. Valid values:<br><br><br>* **Progressing**: The processing is in progress.<br><br>* **Ok**: The status is normal.<br><br>* **Unschedulable**: It is unschedulable.<br><br>* **InitilizeFailed**: Initialization failed.<br><br>* **NotReady**: It is abnormal.<br><br>* **Balance**: The account is in arrears.<br><br>* **ResourceCleanupFailed**: Removal of linked resources failed.<br><br>* **Unknown**: An unknown error occurs.<br><br>* **ClusterVersionUpgrading**: The node version is being upgraded. |


<span id="kubernetesconfigresponse"></span>
### KubernetesConfigResponse


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Labels |Array of [Label](https://docs.byteplus.com/en/docs/90/21166#label) |\- |Kubernetes labels of the node pool or node. |
|Taints |Array of [Taint](https://docs.byteplus.com/en/docs/90/21166#taint) |\- |The Kubernetes taints of the node pool or the node. |
|Cordon |Boolean |false |Node cordon configuration switch. Value description:<br><br><br>* **false**: Disable node cordoning.<br><br>* **true**: Enable node cordoning. |


<span id="label"></span>
### Label


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Key |String |label\-key |The tag key. |
|Value |String |label\-value |The label value. |


<span id="taint"></span>
### Taint


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Key |String |taint\-key |The taint key. |
|Value |String |taint\-value |The taint value. |
|Effect |String |NoSchedule |The taint effect. Valid values:<br><br><br>* **NoSchedule**: No scheduling is performed.<br><br>* **NoExecute**: Pods that do not tolerate the taint are evicted.<br><br>* **PreferNoSchedule**: Avoid scheduling if possible. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
{
    "ResponseMetadata": {
        "RequestId": "202306041104********",
        "Action": "ListNodes",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    },
    "Result": {
        "Items": [
            {
                "Id": "nc5t5ep********",
                "Name": "test-node",
                "Roles": [
                    "Worker"
                ],
                "Status": {
                    "Phase": "Running",
                    "Conditions": [
                        {
                            "Type": "Ok"
                        }
                    ]
                },
                "ZoneId": "cn-bei******",
                "ImageId": "image-kd********",
                "ClusterId": "cc5silum********",
                "IsVirtual": true,
                "PreScript": "ZWNob****",
                "CreateTime": "2021-10-27T10:33:30Z",
                "InstanceId": "i-ybo922********",
                "NodePoolId": "pc8oah9********",
                "UpdateTime": "2021-10-29T10:33:30Z",
                "MetadataName": "192.168.***.***",
                "AffinityGroupId": "affinityG********",
                "GpuDriverVersion": "550.1.1",
                "InitializeScript": "ZWNob****",
                "KubernetesConfig": {
                    "Cordon": true,
                    "Labels": [
                        {
                            "Key": "label-key",
                            "Value": "label-value"
                        }
                    ],
                    "Taints": [
                        {
                            "Key": "taint-key",
                            "Value": "taint-value",
                            "Effect": "NoSchedule"
                        }
                    ]
                },
                "CreateClientToken": "BusinessRequest12345",
                "ContainerStoragePath": "/dev/vdb",
                "ContainerStorageMountPoint": "/mnt/vdb",
                "AdditionalContainerStorageEnabled": true
            }
        ],
        "TotalCount": 100,
        "PageNumber": 1,
        "PageSize": 10
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

This API has no API\-specific error codes. For details about common error codes, see [Common error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes).

---
title: "CreateDiagnosticTask"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/CreateDiagnosticTask"
---

Creates a diagnostic, inspection, or check task.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point based on the region where your business is located.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=CreateDiagnosticTask&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateDiagnosticTask&serviceCode=vke&version=2022-05-12&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameter

The following table describes the API request parameters. You also need to provide public parameters when calling this API. For details about public request parameters, see [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters).


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |CreateDiagnosticTask |The API name. The API name is `CreateDiagnosticTask`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|TargetResources |Array of [DiagnoseResources](https://docs.byteplus.com/en/docs/90/120593#diagnoseresources) |Yes |\- |The list of target diagnostic resources. Length limit: 1. |
|Type |String |Yes |ClusterInspection |The diagnostic type. Specify this parameter by associating it with TargetResources. Valid values:<br><br><br>* **PrecheckControlPlane**: Control plane upgrade precheck<br><br>* **PrecheckDataPlane**: Data plane upgrade precheck<br><br>* **AddonPreCheck**: Add\-on pre\-check<br><br>* **AddonPostCheck**: Add\-on post\-check<br><br>* **AddonDiagnosis**: Add\-on inspection<br><br><br><div data-tips="true" data-tips-type="default">Description</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter can be set to <code>AddonDiagnosis</code> only if the add\-on is <code>alb-ingress-controller</code><strong>.</strong></div><br><br><br><br>* **ClusterInspection**: Cluster inspection<br><br>* **NodePoolDiagnosis**: Node pool diagnosis<br><br>* **NodeDiagnosis**: Node diagnosis<br><br>* **PodDiagnosis**: Pod diagnosis<br><br>* **NodePoolScalingDiagnosis**: Node pool scaling diagnosis<br><br>* **PathAnalysis**: Path analysis |
|Params |Array of [DiagnoseTaskParam](https://docs.byteplus.com/en/docs/90/120593#diagnosetaskparam) |No |\- |The parameters of the diagnostic task. |
|ClientToken |String |No |BC028527\-33B9\-4990\-A633\-84E9F9\*\*\*\* |A string used to ensure the idempotency of the request. This string is passed in by the caller and must be unique across different requests. ClientToken is case\-sensitive and can consist of 64 ASCII characters at most. |


<span id="diagnoseresources"></span>
### DiagnoseResources


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|ResourceIds |Array of String |Yes |["ccbm7\*\*\*\*"] |The diagnostic resource IDs.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">When <code>ResourceType</code> is <code>VkeAddon</code>, the <code>ResourceIds</code> input format is <code>clusterid_addonName</code>, such as <code>cdab****_alb-ingress-controller</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When <code>ResourceType</code> is <code>VkePod</code>, the <code>ResourceIds</code> input format is <code>clusterid_namespace_podName</code>, such as <code>cdab****_default_nginx-****</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When <code>ResourceType</code> is another resource type, enter the corresponding resource ID for <code>ResourceIds</code>.</div><br> |
|ResourceType |String |Yes |VkeCluster |The diagnostic resource type. Valid values:<br><br><br>* **VkeCluster**: cluster<br><br>* **VkeNodePool**: node pool<br><br>* **VkeNode**: node<br><br>* **VkeAddon**: add\-on<br><br>* **VkePod**: Pod |


<span id="diagnosetaskparam"></span>
### DiagnoseTaskParam


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Key |String |Yes |CurrentKubernetesVersion |The key of the diagnostic task parameter. |
|Value |String |Yes |v1.34.6‑vke.8 |The value of the diagnostic task parameter. |



&nbsp;

* When `Type` is set to `PrecheckControlPlane`, the diagnostic task parameters are as follows:

   
   |**DiagnoseTaskParam.key** |**DiagnoseTaskParam.value example** |**Required** |**Description** |
   |---|---|---|---|
   |ClusterId |ccbm7\*\*\*\* |Yes |Cluster ID.<br><br>You can call the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API to obtain cluster IDs. |
   |CurrentKubernetesVersion |v1.34.6‑vke.8 |Yes |The current Kubernetes version of the cluster. |
   |TargetKubernetesVersion |v1.36.4‑vke.2 |Yes |The target Kubernetes version to upgrade to. |
   |TargetContainerdVersion |1.6.38 |No |The target containerd container runtime version to upgrade to. |
   

* When `Type` is set to `PrecheckDataPlane`, the diagnostic task parameters are as follows:

   
   |**DiagnoseTaskParam.key** |**DiagnoseTaskParam.value example** |**Required** |**Description** |
   |---|---|---|---|
   |ClusterId |ccbm7\*\*\*\* |Yes |Cluster ID.<br><br>You can call the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API to obtain cluster IDs. |
   |TargetKubernetesVersion |v1.36.4‑vke.2 |No |The target Kubernetes version to upgrade to. |
   |TargetContainerdVersion |1.6.38 |No |The target containerd runtime version. |
   |ImageId |img\-1\*\*\*\* |No |The image ID. |
   |GpuDriverVersion |535.161.07 |No |The GPU driver version. |
   |TargetResourceScope |VkeNodePool:np\-001,np\-002 |No |The target resource scope, which specifies the granularity of resources on which the operation will be performed. |
   

* When `Type` is set to `AddonPreCheck`, the diagnostic task parameters are as follows:

   
   |**DiagnoseTaskParam.key** |**DiagnoseTaskParam.value example** |**Required** |**Description** |
   |---|---|---|---|
   |ClusterId |ccbm7\*\*\*\* |Yes |Cluster ID.<br><br>You can call the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API to obtain cluster IDs. |
   |Name |mgpu |Yes |The cluster add\-on name. |
   |Operation |UpdateAddonVersion |Yes |The operation on the add\-on. Valid values:<br><br><br>* **CreateAddon**: Create an add\-on.<br><br>* **UpdateAddonVersion**: Upgrade the version of an add\-on.<br><br>* **UpdateAddonConfig**: Update the configuration of an add\-on.<br><br>* **DeleteAddon**: Delete an add\-on. |
   |CurrentAddonVersion |v0.6.5 |Yes |The current version of the add\-on. |
   |TargetAddonVersion |v0.6.6 |No |The target runtime version of the add\-on.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When <code>Operation</code> is set to <code>CreateAddon</code> or <code>UpdateAddonVersion</code>, specify this parameter.</div><br> |
   |TargetAddonConfig |\- |No |Add\-on configuration. For configuration details, see [Add-on configuration information](https://docs.byteplus.com/en/docs/vke/CreateAddon#.57uE5Lu26YWN572u5L-h5oGv). |
   

* When `Type` is set to `AddonPostCheck`, the diagnostic task parameters are as follows:

   
   |**DiagnoseTaskParam.key** |**DiagnoseTaskParam.value example** |**Required** |**Description** |
   |---|---|---|---|
   |ClusterId |ccbm7\*\*\*\* |Yes |Cluster ID.<br><br>You can call the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API to obtain cluster IDs. |
   |Name |mgpu |Yes |The cluster add\-on name. |
   |Operation |UpdateAddonVersion |Yes |The operation on the add\-on. Valid values:<br><br><br>* **CreateAddon**: Create an add\-on.<br><br>* **UpdateAddonVersion**: Upgrade the version of an add\-on.<br><br>* **UpdateAddonConfig**: Update the configuration of an add\-on.<br><br>* **DeleteAddon**: Delete an add\-on. |
   |CurrentAddonVersion |v0.6.5 |Yes |The current version of the add\-on. |
   |TargetAddonVersion |v0.6.6 |No |The target runtime version of the add\-on.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When <code>Operation</code> is set to <code>CreateAddon</code> or <code>UpdateAddonVersion</code>, specify this parameter.</div><br> |
   |TargetAddonConfig |\- |No |Add\-on configuration. For configuration details, see [Add-on configuration information](https://docs.byteplus.com/en/docs/vke/CreateAddon#.57uE5Lu26YWN572u5L-h5oGv). |
   

* When `Type` is set to `ClusterInspection`, the diagnostic task parameters are as follows:

   
   |**DiagnoseTaskParam.key** |**DiagnoseTaskParam.value example** |**Required** |**Description** |
   |---|---|---|---|
   |ClusterId |ccbm7\*\*\*\* |Yes |Cluster ID.<br><br>You can call the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API to obtain cluster IDs. |
   

* When `Type` is set to `PerformanceRiskInspection`, the diagnostic task parameters are as follows:

   
   |**DiagnoseTaskParam.key** |**DiagnoseTaskParam.value example** |**Required** |**Description** |
   |---|---|---|---|
   |ClusterId |ccbm7\*\*\*\* |Yes |Cluster ID.<br><br>You can call the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API to obtain cluster IDs. |
   

* When `Type` is set to `NodePoolDiagnosis`, the diagnostic task parameters are as follows:

   
   |**DiagnoseTaskParam.key** |**DiagnoseTaskParam.value example** |**Required** |**Description** |
   |---|---|---|---|
   |ClusterId |ccbm7\*\*\*\* |Yes |Cluster ID.<br><br>You can call the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API to obtain cluster IDs. |
   

* When `Type` is set to `NodeDiagnosis`, the diagnostic task parameters are as follows:

   
   |**DiagnoseTaskParam.key** |**DiagnoseTaskParam.value example** |**Required** |**Description** |
   |---|---|---|---|
   |ClusterId |ccbm7\*\*\*\* |Yes |Cluster ID.<br><br>You can call the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API to obtain cluster IDs. |
   

* When `Type` is set to `PodDiagnosis`, the diagnostic task parameters are as follows:

   
   |**DiagnoseTaskParam.key** |**DiagnoseTaskParam.value example** |**Required** |**Description** |
   |---|---|---|---|
   |ClusterId |ccbm7\*\*\*\* |Yes |Cluster ID.<br><br>You can call the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API to obtain cluster IDs. |
   

* When `Type` is set to **`NodePoolScalingDiagnosis`**, the diagnostic task parameters are as follows:

   
   |**DiagnoseTaskParam.key** |**DiagnoseTaskParam.value example** |**Required** |**Description** |
   |---|---|---|---|
   |ClusterId |ccbm7\*\*\*\* |Yes |Cluster ID.<br><br>You can call the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API to obtain cluster IDs. |
   |NodePoolScaleRecordId |scale\-record\-001 |Yes |The scaling record ID of the node pool. You can view the scaling record ID in the console. For details, see [Manually scale node pools](https://docs.byteplus.com/en/docs/vke/Scaling-a-NodePool?lang=en#.57uT5p6c6aqM6K-B). |
   |NodePoolScaleType |ScaleUp |Yes |The node pool scaling type. Valid values:<br><br><br>* **ScaleUp**: scale\-out<br><br>* **ScaleDown**: scale\-in |
   

* When `Type` is set to `PathAnalysis`, the diagnostic task parameters are as follows:

   <div data-tips="true" data-tips-type="default">Description   </div>
   

* <div data-tips="true" data-tips-type="default"><code>TargetResources.ResourceType</code> can only be set to <code>VkePod</code> or <code>VkeNode</code>, and <code>TargetResources.ResourceIds</code> can only be set to a diagnostic resource ID.</div>


* <div data-tips="true" data-tips-type="default">For different targets, <code>TargetType</code> and <code>TargetId</code> are configured differently. For example:</div>


   * <div data-tips="true" data-tips-type="default">The target is a Pod: <code>TargetType=PrivateIP</code> and <code>TargetId=clusterid_namespace_podName</code></div>


   * <div data-tips="true" data-tips-type="default">The target is a node: <code>TargetType=ECS</code> and <code>TargetId=nodeid</code></div>


   * <div data-tips="true" data-tips-type="default">The target is a CLB instance: <code>TargetType=CLB</code> and <code>TargetId=clbid</code></div>


   * <div data-tips="true" data-tips-type="default">The target is an IP address: <code>TargetType=PrivateIP</code> and <code>TargetId=IP</code></div>


   
   |**DiagnoseTaskParam.key** |**DiagnoseTaskParam.value example** |**Description** |
   |---|---|---|
   |TargetType |ECS |The target resource type. |
   |TargetId |nd9lb\*\*\*\* |The target resource ID. |
   |TargetPort |80 |The target port. |
   |Protocol |TCP |The transmission protocol type. Valid values:<br><br><br>* TCP<br><br>* UDP<br><br>* ICMP |
   |TargetIP |\- |The IP address.<br><br><div data-tips="true" data-tips-type="default">Description</div><br><br><br><div data-tips="true" data-tips-type="default">Specify this parameter only if the target is an IP address.</div><br> |
   


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```JSON
POST https://vke.cn-beijing.byteplusapi.com.cn?Action=CreateDiagnosticTask&Version=2022-05-12
Content-Type: application/json
{
    "TargetResources": [
        {
            "ResourceIds": [
                "ccbm7****"
            ],
            "ResourceType": "VkeCluster"
        }
    ],
    "Type": "ClusterInspection",
    "Params": [
        {
            "Key": "CurrentKubernetesVersion",
            "Value": "v1.34.6‑vke.8"
        }
    ],
    "ClientToken": "BC028527-33B9-4990-A633-84E9F9****"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

The following table contains the response parameters of this API. See [Response results](https://docs.byteplus.com/en/docs/vke/Response) for details about public response parameters.


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |String |task\-202303\*\*\*\* |The ID of the diagnostic task. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420**********",
        "Action": "CreateDiagnosticTask",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    },
    "Result": {
        "Id": "task-20********"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no error codes proprietary to this API. See [Public error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes) for details about public error codes.

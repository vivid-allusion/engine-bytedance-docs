---
title: "UpdateClusterVersion"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/UpdateClusterVersion"
---

Upgrade the cluster control plane.

<span id="9fa3d1fa"></span>
## Considerations


* The upgrade of a Kubernetes minor version may involve changes to Kubernetes resource versions. Before upgrading, check if your application uses deprecated resources. If the chart of your application uses deprecated resources, update the resource versions in the chart to the latest ones and then update the chart in the cluster. For detailed descriptions of resource changes and deprecations, see [Kubernetes version release notes](https://docs.byteplus.com/en/docs/vke/Kubernetes-version-release-notes).

* Cross\-version upgrades of VKE\-adapted Kubernetes versions are not supported. For example, if the current cluster version is v1.32, it can only be upgraded to the latest patch version of v1.32 or the latest patch version of v1.34. Direct upgrade from v1.32 to v1.36 is not supported. For VKE\-adapted Kubernetes versions, see [Kubernetes version release notes](https://docs.byteplus.com/en/docs/vke/Kubernetes-version-release-notes).

* When continuously upgrading Kubernetes versions for the same cluster, we recommend an interval of more than 24 hours between upgrades for stable cluster operation. For example, after upgrading the cluster from v1.32 to v1.34 and running stably for 24 hours, you can then upgrade the cluster to v1.36.

* The control plane can be upgraded only if the Kubernetes version of the nodes and the control plane are consistent.

* During the upgrade of the Kubernetes cluster control plane, applications on the cluster will not be interrupted. If the applications have a strong dependency on the API server, the applications may be affected for a short period of time.

* The cluster control plane upgrade takes 5 to 10 minutes. During this period, you will not be able to operate your cluster via the API, console, or other methods.

* You cannot roll back the upgrade of the cluster control plane. Proceed with caution.

* If the cluster uses a custom operating system image, VKE cannot guarantee a successful cluster upgrade because such images have not been validated rigorously by VKE.

* After upgrading the Kubernetes control plane, there may be parameter incompatibilities. Therefore, the upgrade operation will not retain your cluster\-level custom Kubelet parameters. You need to reconfigure them after the upgrade to ensure that new nodes use the desired custom configurations. For related operations, see [Custom cluster kubelet parameters](https://docs.byteplus.com/en/docs/vke/Custom_cluster_kubelet_parameter).

* For more control plane upgrade precautions, see [Cluster upgrade operations](https://docs.byteplus.com/en/docs/vke/Upgrading-a-cluster).


<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point based on the region where your business is located.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=UpdateClusterVersion&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=UpdateClusterVersion&serviceCode=vke&version=2022-05-12&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameter

The following table describes the API request parameters. You also need to provide public parameters when calling this API. For details about public request parameters, see [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters).


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |UpdateClusterVersion |The API name. The current API name is `UpdateClusterVersion`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|Id |String |Yes |cc8o\*\*\*\*\*\* |The ID of the target cluster.<br><br>You can call the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API to obtain cluster IDs.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The cluster must be in <code>{Running,[Ok]}</code> status. You can call the <a href="https://docs.byteplus.com/en/docs/vke/ListClusters">ListClusters</a> API to view the current status of the cluster.</div><br> |
|KubernetesVersion |String |Yes |1.36 |The target Kubernetes version to upgrade to, in the format `x.xx`. The system will automatically upgrade to the latest VKE patch version corresponding to this Kubernetes version. For the release notes for Kubernetes versions supported by VKE, see [Kubernetes version release notes](https://docs.byteplus.com/en/docs/vke/Kubernetes-version-release-notes). |
|Operation |String |No |Precheck |The specific operation to be performed. Valid values:<br><br><br>* **Precheck**: (Default value) Only perform the upgrade precheck operation.<br><br>* **Upgrade**: Directly execute the upgrade task. The task performs an upgrade precheck and proceeds with the upgrade after the precheck passes. |
|IgnorePrecheckWarning |Boolean |No |true |Whether to stop the upgrade process when a **Warning** occurs during the upgrade precheck. Valid values:<br><br><br>* **true**: When the upgrade precheck result is **Warning**, ignore the check result and continue upgrading the cluster control plane.<br><br>* **false**: (Default value) When the upgrade precheck result is **Warning**, stop upgrading the cluster control plane. |
|ClientToken |String |No |BC028527\-33B9\-4990\-A633\-\*\*\*\*\*\* |A string used to ensure the idempotency of the request. This string is passed in by the caller and must be unique across different requests. ClientToken is case\-sensitive and can consist of 64 ASCII characters at most. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```JSON
POST https://vke.cn-beijing.byteplusapi.com.cn?Action=UpdateClusterVersion&Version=2022-05-12
Content-Type: application/json
{
    "Id": "cc8o******",
    "KubernetesVersion": "1.36",
    "Operation": "Precheck",
    "IgnorePrecheckWarning": true,
    "ClientToken": "BC028527-33B9-4990-A633-******"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

The following table contains the response parameters of this API. See [Response results](https://docs.byteplus.com/en/docs/vke/Response) for details about public response parameters.


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|TaskId |String |ud8ojr\*\*\*\* |Task ID. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420**********",
        "Action": "UpdateClusterVersion",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    },
    "Result": {
        "TaskId": "ud8oj*****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The error codes for this API are listed in the table below. For public error codes, see [Public error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes).


|**HTTP status code** |**Error code** |**Error message** |**Description** |
|---|---|---|---|
|400 |OperationDenied.ClusterStatus |The action is forbidden due to cluster status {{statusPhase}} and {{statusConditions}}. |The current status of the specified cluster does not support this operation. Confirm the required cluster status for this API and try again. |
|400 |OperationDenied.KubernetesVersion |The action has been denied due to the kubernetes version upgrade constraints. |The Kubernetes version upgrade constraints are violated. This operation cannot be performed. Please carefully read the control plane upgrade precautions, verify the parameter configuration, and try again. |

---
title: "CreateNodes"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/CreateNodes"
---

Add existing ECS instances to the specified cluster.

<span id=".5L2_55So6K-05piO"></span>
## Usage instructions


* Before you call this API, ensure that a node pool (default node pool or custom node pool) has been created and that the status of the node pool is `{Running, [*]}` or `{Scaling,[Progressing]}`. Otherwise, you cannot call this API to add existing ECS instances.

   * Default node pool: Call the [CreateDefaultNodePool](https://docs.byteplus.com/en/docs/vke/CreateDefaultNodePool) API to create a default node pool (vke\-default\-nodepool), or create a default node pool when you [add existing nodes](https://docs.byteplus.com/en/docs/vke/Adding-existing-nodes) in the console.

   * Custom node pool: Create a custom node pool by calling the [CreateNodePool](https://docs.byteplus.com/en/docs/vke/CreateNodePool) API or by clicking [Create node pool](https://docs.byteplus.com/en/docs/vke/Creating-a-NodePool) in the console.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">ECS instances can only be added to a custom node pool that meets the following conditions:      </div>
      

         * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2"><strong>Autoscaling</strong> is not enabled for the node pool.      </div>
      

         * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">The current node pool billing mode is <strong>Pay\-as\-you\-go</strong> or <strong>Subscription</strong>.      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Only ECS instances that meet the following conditions can be added to a custom node pool:      </div>
      

         * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Running in the same VPC as the current cluster.      </div>
      

         * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">The instance belongs to the same project as the target node pool.      </div>
      

         * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">The instance has not been added to any cluster or scaling group of the Auto Scaling service.      </div>
      

         * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">The instance only has one network interface card.      </div>
      

         * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">The <code>capacity</code> of the system volume is greater than or equal to the sum of the <code>image size configured for the target node pool</code> and <code>10 GiB</code>.      </div>
      

         * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">If you do not specify a custom data volume to be mounted by the node (the value of the <strong>AdditionalContainerStorageEnabled</strong> parameter is not <strong>true</strong>), the instance must have a data volume that has the same volume type and size specified for the target node pool. For example, if the target node pool is configured with five data volumes (including local disks), and the first data volume has "<strong>Format and mount to the container and image storage directory</strong>" enabled, while the third data volume has "<strong>Specify mount directory</strong>" enabled, then the ECS instance needs to have two data volumes (including local disks) that are the same as the first and the third ones of the target node pool in terms of type and size.      </div>
      

* Before you call this API, first call the [ListSupportedResourceTypes](https://docs.byteplus.com/en/docs/vke/ListSupportedResourceTypes) API to confirm whether the resources required for node creation are supported in the specified region and availability zone.

* This is an asynchronous API. When this API returns a success message, it will return the ID of the node, and the node will enter the `{Creating, [Progressing]} `state. After the node is created, it will enter the `{Running, [Ok]}` state. You can call the [ListNodes](https://docs.byteplus.com/en/docs/vke/ListNodes) API to obtain the current status of the node and check whether the node was created successfully.

* When taking added [Bare Metal](https://docs.byteplus.com/en/docs/ecs/General-purpose-EBM) nodes offline, ECS will attempt a normal shutdown based on the node status. If a normal shutdown is not possible, a forced shutdown will be performed. For more details, see [StopInstance](https://docs.byteplus.com/en/docs/ecs/StopInstance).


<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point based on the region where your business is located.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=CreateNodes&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateNodes&serviceCode=vke&version=2022-05-12&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameter

The following table describes the API request parameters. You also need to provide public parameters when calling this API. For details about public request parameters, see [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters).


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |CreateNodes |The API name. The name of the current API is `CreateNodes`. |
|Version |String |Yes |May 12, 2022 |The API version. The API version is `2022-05-12`. |
|ClientToken |String |No |ed6b1190\-dc17\-11ec\-9519\-eb58a7\*\*\*\*\*\* |A string used to ensure the idempotency of the request. This string is passed in by the caller and must be unique across different requests. ClientToken is case\-sensitive and can consist of 64 ASCII characters at most. |
|ClusterId |String |Yes |cc5sil\*\*\*\*\*\* |Cluster ID.<br><br>You can call the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API to obtain cluster IDs.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The cluster must be in <code>{Running,[*]}</code> or <code>{Updating,[Progressing]}</code> state. You can call the <a href="https://docs.byteplus.com/en/docs/vke/ListClusters">ListClusters</a> API to obtain the current status of the cluster.</div><br> |
|NodePoolId |String |No |pjklj\*\*\*\*\*\* |The node pool ID.<br><br><br>* If no parameter value is provided, specified existing ECS instances will be added to the default node pool.<br><br>* If a parameter value is provided, specified existing ECS instances will be added to the custom node pool. You can call the [ListNodePools](https://docs.byteplus.com/en/docs/vke/ListNodePools) API to obtain the ID of the target custom node pool.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If a <strong>custom node pool ID</strong> is provided here, the nodes to be added will use the Kubernetes and node configurations of the custom node pool. This includes ECS instance tags, labels, taints, node cordon configuration, project, node name prefix, and more. Therefore, the <strong>InitializeScript</strong>, <strong>KubernetesConfig</strong>, and <strong>ImageId</strong> parameters will be invalid. These parameters are only valid for adding existing nodes to the default node pool.</div><br> |
|InstanceIds |Array of String |Yes |["i\-ybo9229pdf\*\*\*\*","i\-ybo9229pdf\*\*\*\*"] |The ID of the ECS instance to be added to the cluster. Up to 100 ECS instance IDs can be specified per call.<br><br>You can call the [DescribeInstances](https://docs.byteplus.com/en/docs/ecs/DescribeInstances) API to obtain ECS instance IDs. The ECS instance must meet the following conditions:<br><br><br>* It is in the same VPC as the cluster.<br><br>* It is not used by another cluster.<br><br>* The instance status must be **Running** (`Running`).<br><br>* The number of nodes must not exceed the maximum number of nodes supported by the cluster.<br><br>* Do not repeatedly add the same ECS instance.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When adding ECS instances to a custom node pool, note the following:</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">If <strong>AffinityGroupConfig</strong> (beta) is enabled for the node pool, the number of ECS instance IDs must be an integer multiple‌ of the affinity group size. Otherwise, the addition will fail.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If <strong>AffinityGroupConfig</strong> (beta) is disabled for the node pool, providing IDs of ECS instances in an affinity group may cause unexpected behavior. We recommend not selecting ECS instances added to affinity groups for node pools for which Buy affinity group is not enabled.</div><br> |
|KeepInstanceName |Boolean |No |false |Whether to retain the original ECS instance name. Values:<br><br><br>* **false**: (Default) Do not retain the original ECS instance name. VKE will automatically assign a name.<br><br>* **true**: Retain the original ECS instance name. |
|AdditionalContainerStorageEnabled |Boolean |No |false |Specifies whether to format and mount the data volume of the node as the storage directory for container images and logs. Valid values:<br><br><br>* **false**: (Default) Disable.<br><br>   * Default node pool: Do not mount the data volume.<br><br>   * Custom node pool: Mount it according to the data volume configuration. ECS instances added to the node pool must include the specified data volumes (including local volumes), with an identical volume type and size.<br><br>* **true**: Yes. The **ContainerStoragePath** parameter must also be configured. Mounting will be performed based on the **ContainerStoragePath** setting. The data volume settings for the node pool will be ignored. No special requirements are imposed on the data volumes of ECS instances added to the node pool. |
|ContainerStoragePath |String |No |/dev/vdb |Use this data volume device to mount the container and image storage directory `/var/lib/containerd`.<br><br>It is valid only when `AdditionalContainerStorageEnabled` is true. It cannot be empty.<br><br>The following conditions must be met to achieve successful initialization.<br><br><br>* Only ECS instances with a mounted data volume are supported.<br><br>* When specifying a data volume device name, ensure that the data volume device exists. Otherwise, initialization will fail.<br><br>* When specifying a data volume partition or logical volume name, ensure that the partition or logical volume exists and uses the ext4 filesystem.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">If a data volume device is specified, it will be automatically formatted and mounted directly. Ensure that you back up your data in advance.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If a data volume partition or logical volume name is specified, formatting is not required.</div><br> |
|ImageId |String |No |image\-k\*\*\*\*\*\*\* |The ID of the image used by the ECS instance that corresponds to the node.<br><br>Image IDs vary based on different types of images. For details, see [Public images supported by VKE](https://docs.byteplus.com/en/docs/vke/Overview-of-operating-system-images#.5a655Zmo5pyN5Yqh5pSv5oyB55qE5YWs5YWx6ZWc5YOP).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If this parameter is not specified, an image ID from the veLinux 2.0 series is preferentially allocated.</div><br> |
|InitializeScript |String |No |ZWNo\*\*\*\*\*\* |The script executed after creating the ECS node and deploying Kubernetes components. Enter the Base64\-encoded shell script.<br><br><br>* If this parameter is left empty, the node inherits the initialization script `NodeConfig.InitializeScript` configured in the default node pool.<br><br>* If a custom script is provided, it will be used, and the initialization script configured in the default node pool will be ignored.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Base64\-encoded content can be up to 8 KB in length. If you specify both the <strong>InitializeScript</strong> and <strong>PreScript</strong> parameters, the total length of the two parameter values cannot exceed 8 KB.</div><br> |
|KubernetesConfig |Object of [KubernetesConfigRequest](https://docs.byteplus.com/en/docs/90/21164#kubernetesconfigrequest) |No |\- |Kubernetes configuration for the node.<br><br><br>* If it is left empty, the node inherits the Kubernetes configuration (`KubernetesConfig.Labels/Taints/Cordon`) from the default node pool.<br><br>* After a custom configuration is provided, the custom configuration applies and the Kubernetes configuration of the default node pool is ignored. |
|SkipReplaceSystem |Boolean |No |true |Whether to skip system resetting when adding an existing node:<br><br><br>* **true**: Skip system resetting. The operating system of the ECS instance corresponding to the existing node will not be reset.<br><br>* **false**: (Default) Do not skip system resetting. The operating system of the ECS instance corresponding to the existing node will be reset.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If you skip resetting the system (set the parameter to <code>true</code>), ensure:</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">The ECS instance status must be <strong>RUNNING</strong>. You can call <a href="https://docs.byteplus.com/en/docs/ecs/DescribeInstances">DescribeInstances</a> to query the instance status.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The ECS instance must have the Cloud Assistant agent installed, and the agent status must be <strong>Running</strong>. You can call the <a href="https://docs.byteplus.com/en/docs/ecs/DescribeCloudAssistantStatus">DescribeCloudAssistantStatus</a> API to query the Cloud Assistant agent status.</div><br> |
|PreScript |String |No |ZWNoby\*\*\*\*\*\* |[[Beta - apply for trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] The script to execute before node deployment. Enter the Base64\-encoded shell script.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If this parameter is left empty, the node to be added inherits the pre\-script (<strong>NodeConfigRequest.PreScript</strong>) from the default node pool configuration.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you enter custom script content, the pre\-script in the default node pool configuration will be ignored and the script specified here will be used.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Base64\-encoded content can be up to 8 KB in length. If you specify both the <strong>InitializeScript</strong> and <strong>PreScript</strong> parameters, the total length of the two parameter values cannot exceed 8 KB.</div><br> |
|GpuDriverVersion |String |No |550.127.05 | **[This parameter is deprecated. Use GpuDriverConfig instead.]**  Specifies the GPU driver version to be installed on the node.<br><br>You can call the [ListSupportedGpuDriverVersions](https://docs.byteplus.com/en/docs/vke/ListSupportedGpuDriverVersions) API to obtain the list of GPU driver versions that can be installed for an image. |
|GpuDriverConfig |Object of [GpuDriverConfig](https://docs.byteplus.com/en/docs/90/21164#gpudriverconfig) |No |\- |GPU driver configuration for the node. This configuration takes precedence over the `GpuDriverVersion` field.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter applies to default and custom node pools.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If a node is added to a custom node pool and this parameter is not configured, the node inherits the <code>GpuDriverConfig</code> configuration of the custom node pool.</div><br> |
|ContainerStorageMountPoint |String |No |/mnt/vdb |The target mount directory after the data volume device is formatted. This parameter is used together with `ContainerStoragePath`. If it is not specified, the default directory will be used. This parameter is valid only if `AdditionalContainerStorageEnabled is set to true`. |


<span id="kubernetesconfigrequest"></span>
### KubernetesConfigRequest


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Cordon |Boolean |No |false |Whether to cordon nodes. Valid values:<br><br><br>* **false**: Do not cordon nodes. This value is used by default.<br><br>* **true**: Cordon nodes.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When you update the configurations of a node pool, if you do not specify this parameter, the original parameter configurations are retained.</div><br> |
|Labels |Array of [Label](https://docs.byteplus.com/en/docs/90/21164#label) |No |\- |The Kubernetes labels of the node pool or the node. Up to 20 labels can be provided.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The node pool manages the label configurations of nodes in a centralized manner. Therefore, the label information will be synchronized to all nodes in the node pool. When labels are changed, the original label configurations will be overwritten.</div><br> |
|Taints |Array of [Taint](https://docs.byteplus.com/en/docs/90/21164#taint) |No |\- |The Kubernetes taints of the node pool or the node. Up to 20 taints can be specified.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The node pool manages the taint configurations of nodes in a centralized manner. Therefore, the taint information will be synchronized to all nodes in the node pool. When taints are changed, the original taint configurations will be overwritten.</div><br> |


<span id="label"></span>
### Label


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Key |String |Yes |label\-key |The label key. The requirements are as follows. For more rules, see [Kubernetes label rules](https://kubernetes.io/zh/docs/concepts/overview/working-with-objects/labels/#%E8%AF%AD%E6%B3%95%E5%92%8C%E5%AD%97%E7%AC%A6%E9%9B%86).<br><br>A valid label key consists of <prefix\> and <Name\>, which are separated by a slash (/).<br><br><br>* <Name\> is required, which can contain uppercase or lowercase letters, digits, hyphens (\-), underscores (_), and periods (.). It must start and end with a letter or digit and can be up to 63 characters in length.<br><br>* <prefix\> is optional. If <prefix\> is specified, it must be a DNS subdomain. It is a series of DNS labels separated by periods (.), with a length not exceeding 253 characters.<br><br>* The total length of <prefix\> and <Name\> must not exceed 82 characters. |
|Value |String |No |label\-value |The label value. The requirements are as follows. For more rules, see [Kubernetes label rules](https://kubernetes.io/zh/docs/concepts/overview/working-with-objects/labels/#%E8%AF%AD%E6%B3%95%E5%92%8C%E5%AD%97%E7%AC%A6%E9%9B%86).<br><br><br>* The value cannot exceed 63 characters in length and can be left empty.<br><br>* The value can start and end with an uppercase or lowercase letter, or a digit.<br><br>* The value can contain the following special characters: hyphens (\-), underscores (_), and periods (.). |


<span id="taint"></span>
### Taint


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Key |String |Yes |taint\-key |The taint key. The requirements are as follows. For more rules, see [Kubernetes label rules](https://kubernetes.io/zh/docs/concepts/overview/working-with-objects/labels/#%E8%AF%AD%E6%B3%95%E5%92%8C%E5%AD%97%E7%AC%A6%E9%9B%86).<br><br>A valid taint key consists of a `prefix` and a `name`, which are separated by a slash (/).<br><br><br>* The `name` is required. It can contain uppercase and lowercase letters, digits, and the following special characters: `- _ .`. It must start and end with a letter or digit, and can be up to 63 characters in length.<br><br>* The `prefix` is optional. If you specify the `prefix`, it must be a DNS subdomain: a series of DNS labels separated by periods (`.`). It can be up to 253 characters in length.<br><br>* The total length of the `prefix` and `name` cannot exceed 82 characters.The prefix and name can consist of 82 characters in total. |
|Value |String |No |taint\-value |The taint value. The requirements are as follows. For more rules, see [Kubernetes label rules](https://kubernetes.io/zh/docs/concepts/overview/working-with-objects/labels/#%E8%AF%AD%E6%B3%95%E5%92%8C%E5%AD%97%E7%AC%A6%E9%9B%86).<br><br><br>* The value cannot exceed 63 characters in length and can be left empty.<br><br>* The value can start and end with an uppercase or lowercase letter, or a digit.<br><br>* The following special characters are supported: `- _ .` |
|Effect |String |No |NoSchedule |The taint effect. Valid values:<br><br><br>* **NoSchedule**: (Default) No scheduling is performed.<br><br>* **NoExecute**: Pods that do not tolerate the taint are evicted.<br><br>* **PreferNoSchedule**: Avoid scheduling if possible. |


<span id="gpudriverconfig"></span>
### GpuDriverConfig


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|GpuDriverVersion |String |No |580.105.08 |Specifies the GPU driver version to be installed on the node.<br><br><br>* You can call the [ListSupportedGpuDriverVersions](https://docs.byteplus.com/en/docs/vke/ListSupportedGpuDriverVersions) API to obtain the list of GPU driver versions that can be installed for an image.<br><br>* When the configuration is empty, the system automatically populates the recommended GPU driver version based on the GPU model. |
|InstallGpuDriver |Boolean |No |true |Specifies whether to automatically install the GPU driver when the ECS instance is a GPU\-type model and uses a public base image (for example, veLinux 1.0 or Ubuntu 22.04). Valid values:<br><br><br>* **true**: Automatically installs the GPU driver. If you set the parameter to this value, you can use the `GpuDriverVersion` parameter to specify a GPU driver.<br><br>* **false**: Does not automatically install the GPU driver.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When the ECS instance is a GPU\-type model, this parameter defaults to <strong>true</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the ECS instance is a non\-GPU model, this configuration does not take effect.</div><br> |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://vke.cn-beijing.byteplusapi.com.cn?Action=CreateNodes&Version=2022-05-12
Content-Type: application/json
{
    "ClusterId": "cc5sil******",
    "InstanceIds": [
        "i-ybo9229pdf****",
        "i-ybo9229pdf****"
    ],
    "NodePoolId": "pjklj******",
    "KeepInstanceName": false,
    "AdditionalContainerStorageEnabled": false,
    "ContainerStoragePath": "/dev/vdb",
    "InitializeScript": "ZWNo******",
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
    "ImageId": "image-k*******",
    "SkipReplaceSystem": true,
    "PreScript": "ZWNoby******",
    "GpuDriverVersion": "550.127.05",
    "GpuDriverConfig": {
        "GpuDriverVersion": "580.105.08",
        "InstallGpuDriver": true
    },
    "ContainerStorageMountPoint": "/mnt/vdb",
    "ClientToken": "ed6b1190-dc17-11ec-9519-eb58a7******"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

The following table contains the response parameters of this API. See [Response results](https://docs.byteplus.com/en/docs/vke/Response) for details about public response parameters.


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Ids |Array of String |["nc5t5epmrsf\*\*\*\*"] |A list of node IDs. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
{
    "ResponseMetadata": {
        "RequestId": "202306041104********",
        "Action": "CreateNodes",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    },
    "Result": {
        "Ids": [
            "nc5t5epmrsf****"
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The error codes for this API are listed in the table below. For public error codes, see [Public error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes).


|HTTP status code |Error code |Error message |Description |
|---|---|---|---|
|400 |QuotaExceeded.Node |The number of nodes in the cluster has reached the limit. |The number of nodes in the current cluster has reached the limit. You can select another region or [submit a ticket](https://console.byteplus.com/ticket/createTicketV2/?step=2&Service=vke) to apply for a quota increase. |
|400 |OperationDenied.ClusterStatus |The action is forbidden due to cluster status {{statusPhase}} and {{statusConditions}}. |The current status of the specified cluster does not support this operation. Confirm the required cluster status for this API and try again. |
|400 |OperationDenied.NodePoolStatus |The action is forbidden on node pool {{nodePoolId}} due to node pool status {{statusPhase}} and {{statusConditions}}. |The current status of the specified node pool does not support this operation. Please confirm the required node pool status for this API and try again. |
|400 |ClusterVpcMismatch.{{parameter}} |The specified {{resourceType}} {{resourceId}} is not in the VPC of cluster. |The specified subnets, security groups, and HPC cluster belong to different VPCs from the cluster. Make sure that they are in the same VPC as the cluster. |
|400 |LimitExceeded.NodeInCluster |The number of nodes exceeds the cluster\-defined pods config limit. |The maximum nodes specified for the node pool exceeds the maximum nodes supported by the Flannel cluster. For limits on various resources of VKE, see [Resource limits](https://docs.byteplus.com/en/docs/vke/Limits).<br><br>The supported maximum nodes depend on **PodsConfig.FlannelConfig.PodCidrs** and **MaxPodsPerNode**. After a cluster is created, it cannot be modified. You need to plan cluster settings based on your business requirements. |
|400 |AlreadyInUse.{{parameter}} |The specified {{resourceType}} {{resourceId}} has already been used in another cluster. |The specified ECS instance has already been added to a cluster. Use another instance or remove this instance from the existing cluster, and try again later. |
|400 |OperationDenied.InstanceStatus |The operation has been denied due to the wrong status of the specified ECS instance {{instanceId}}. |The current ECS instance status does not support this operation. Confirm the required ECS instance status for calling this API and try again. |
|400 |ZoneMismatch.Instance |The specified ECS instance {{instanceId}} is not in the cluster defined zones. |The availability zone of the added instance is not among the availability zones corresponding to the pod subnets of the vpc\-cni cluster. |
|400 |NotSupported.{{parameter}} |The specified {{resourceType}} {{resourceContent}} is not supported. |The specified parameter (such as InstanceType or ImageId) is not supported. Check the parameter and try again. |
|400 |ClusterVersionMismatch.ImageId |The specified ImageId {{imageId}} and KubernetesVersion {{kubernetesVersion}} are mismatched. |The specified image ID (**ImageId**) does not match the cluster Kubernetes version. Specify appropriate parameter values based on the parameter descriptions and try again. |
|400 |ImageIdMismatch.InstanceId |The specified InstanceId {{instanceId}} and ImageId {{imageId}} are mismatched. |The specified ECS Instance IDs (**InstanceIds**) do not match the image ID (**ImageId**). Specify appropriate parameter values based on the parameter descriptions and try again. |
|400 |OperationDenied.NodePoolReplicas |The operation has been denied due to the node pool min/max replicas limit. |The maximum node count for this node pool has been reached. Please reduce the number of ECS instance IDs to be added and try again later.<br><br>If autoscaling is enabled for the target node pool, you can update the maximum number of nodes (MaxReplicas) in the target node pool. Then, call this API again to add existing nodes. Call the [UpdateNodePoolConfig](https://docs.byteplus.com/en/docs/vke/UpdateNodePoolConfig) API to update the node pool. |
|400 |AlreadyInScalingGroup.{{parameter}} |The specified InstanceId {{instanceId}} has already been used in another scaling group. |The specified instance is already used by another scaling group and cannot be added to the node pool. |
|400 |NodePoolConfigMismatch.InstanceId |The specified InstanceId {{instanceId}} and nodePool Config {{content}} are mismatched. |The specified ECS instances (**InstanceIds**) do not match the configuration of the target node pool  **(NodePoolId**). The node pool configuration includes the system volume, data volume, project, and more. Confirm the configuration alignment between the ECS instances and the target node pool before retrying. |
|400 |OperationDenied.NodePoolAutoScalingEnabled |The operation has been denied because nodePool AutoScaling is enabled. |The target node pool has the autoscaling feature enabled. Adding existing ECS instances to this node pool is not supported. Disable autoscaling for the node pool or change the node pool, and then retry. |
|400 |OperationDenied.InstanceEniNumber |The operation has been denied because the InstanceId {{instanceId}} has more than one eni. |The specified ECS instance has more than one NIC (including a secondary NIC), so the instance cannot be added to a node pool. Unbind the secondary NIC from the node pool or use a different ECS instance before retrying. |
|400 |ImageSizeMismatch.SystemVolumeSize |The specified system volume size and image size are mismatched. |The specified system volume size does not match the image size. The system volume must be at least 10 GiB larger than the image. Specify appropriate parameter values based on the parameter descriptions and try again. |
|404 |NotFound.DefaultNodePool |The default node pool is not found. |The default node pool does not exist. Create the default node pool in the console first.<br><br>For details on creating the default node pool, see [Adding existing nodes](https://docs.byteplus.com/en/docs/vke/Adding-existing-nodes). |
|409 |AlreadyExists.{{parameter}} |The specified {{resourceType}} {{resourceId}} already exists. |The specified ECS instance has been added to the default node pool. |
|400 |AffinityGroupMismatch.InstanceIds |The specified InstanceIds and AffinityGroup {{AffinityGroupId}} are mismatched. |The specified ECS instances do not match the affinity group configuration. The number of nodes in the affinity group\-based node pool must be an integer multiple of the affinity group size. Check the specified nodes and node pools, confirm the relevant parameters, and try again later. |
|400 |OperationDenied.CloudAssistantStatus |The operation has been denied due to the cloud assistant wrong status of the specified ECS instance {{instanceId}}. |The Cloud Assistant agent on the ECS instance is not in an expected state. The instance cannot be added to the cluster. Check the parameter and try again. |
|400 |LimitExceeded.ScriptLength |The InitializeScript and PreScript total length exceeds maximum allowed length. |The total length of the pre\-script and post\-script exceeds the limit. Specify appropriate parameter values based on the parameter descriptions and try again. |

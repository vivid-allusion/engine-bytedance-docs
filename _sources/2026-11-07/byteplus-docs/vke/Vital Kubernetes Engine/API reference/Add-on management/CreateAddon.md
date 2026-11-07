---
title: "CreateAddon"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/CreateAddon"
---

Install add\-ons for a specified cluster.

<span id=".5L2_55So6K-05piO"></span>
## Usage instructions


* Before calling this API, first call the [ListSupportedAddons](https://docs.byteplus.com/en/docs/vke/ListSupportedAddons) API to obtain the values of parameters (such as DeployMode and Version) for the add\-on to be installed. This helps reduce update failures.

* This API is asynchronous. When this API returns success, the add\-on is in the `{Creating, [Progressing]}` state until installation is successful and it enters the `{Running, [Ok]}` state. Call the [ListAddons](https://docs.byteplus.com/en/docs/vke/ListAddons) API to obtain the current status of the add\-on and check whether the add\-on was installed successfully.


<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. See [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) and select the most suitable endpoint for the region where your business operates.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=CreateAddon&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateAddon&serviceCode=vke&version=2022-05-12&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table describes the API request parameters. You also need to provide public parameters when calling this API. For details about public request parameters, see [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters).


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |CreateAddon |The API name. The current API name is `CreateAddon`. |
|Version |String |Yes |May 12, 2022 |The API version. The API version is `2022-05-12`. |
|ClusterId |String |Yes |cc5sil\*\*\*\*\*\*\* |The ID of the cluster in which the add\-on is to be installed.<br><br>You can call the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API to obtain cluster IDs.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The cluster in which the add\-on is to be installed must be in the <code>{Running,[*]}</code> state. You can call the <a href="https://docs.byteplus.com/en/docs/vke/ListClusters">ListClusters</a> API to obtain the current status of the cluster.</div><br> |
|Name |String |Yes |ingress\-nginx |The name of the add\-on to be installed.<br><br>Call [ListSupportedAddons](https://docs.byteplus.com/en/docs/vke/ListSupportedAddons) to obtain a list of add\-ons supported by VKE. |
|Version |String |No |v0.44.0 |The version of the add\-on to be installed.<br><br>You can call the [ListSupportedAddons](https://docs.byteplus.com/en/docs/vke/ListSupportedAddons) API to obtain the version of the add\-on to be installed. |
|DeployMode |String |No |Unmanaged |The deployment mode. Values:<br><br><br>* **Unmanaged**: Deploy in unmanaged mode.<br><br>* **Managed**: Deploy in managed mode.<br><br>   You can call the [ListSupportedAddons](https://docs.byteplus.com/en/docs/vke/ListSupportedAddons) API to obtain the supported deployment mode (managed or unmanaged) of the add\-on to be installed.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If no parameter value is provided, the parameter defaults to <strong>Managed</strong> if the add\-on supports the managed mode, and to <strong>Unmanaged</strong> if the add\-on does not support the managed mode.</div><br> |
|DeployNodeType |String |No |VirtualNode |Deployment node type. You need to specify this parameter only if `DeployModes is set to Unmanaged`. Valid values:<br><br><br>* **Node**: The deployment node type is nodes (ECS).<br><br>* **VirtualNode**: The deployment node type is virtual nodes (VCI).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If the target cluster has installed the vci\-virtual\-kubelet add\-on, the default value of this parameter is <strong>VirtualNode</strong>. Otherwise, the default value is <strong>Node</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Please call the <a href="https://docs.byteplus.com/en/docs/vke/ListAddons">ListAddons</a> API to obtain the add\-ons installed in the current cluster.</div><br> |
|Config |String |No | |Add\-on configuration. For configuration details, see [Add-on configuration information](https://docs.byteplus.com/en/docs/vke/CreateAddon#.57uE5Lu26YWN572u5L-h5oGv) below.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Only the add\-ons listed in <a href="https://docs.byteplus.com/en/docs/vke/CreateAddon#.57uE5Lu26YWN572u5L-h5oGv">Add\-on configuration information</a> require this parameter. Other add\-ons do not require this parameter.</div><br> |
|ClientToken |String |No |BC028527\-33B9\-4990\-A633\-84E9F9\*\*\*\*\*\* |A string used to ensure the idempotency of the request. This string is passed in by the caller and must be unique across different requests. ClientToken is case\-sensitive and can consist of 64 ASCII characters at most. |


<span id=".57uE5Lu26YWN572u5L-h5oGv"></span>
## Add\-on configuration

<span id="cr-credential-controller"></span>
### cr\-credential\-controller


* Configuration content

   
   |Parameter |Data type |Required |Example |Description |
   |---|---|---|---|---|
   |CrConfigmapData |Object |Yes |*  |The configuration data of the add\-on for controlling CR credentials. |
   |CrConfigmapData.Namespace |String |Yes |*  |The namespace in the current cluster that can pull private images without a Secret The default value is `*`. This indicates that all namespaces can pull private images without a Secret. You can also enter specific namespace names, and separate the names with commas (`,`). |
   |CrConfigmapData.ServiceAccount |String |Yes |*  |The service account in Kubernetes that can use the credential controller add\-on. The default value `*` indicates that all ServiceAccounts in the specified namespaces can pull private images without credentials. You can enter one or more specific ServiceAccounts. If you specify more than one, separate them with commas (`,`). |
   |CrConfigmapData.Registries |Array |Yes |*  |CR instance configuration. |
   |CrConfigmapData.Registries.0.Instance |String |Yes |cr\-basic |The target CR instance from which private images can be pulled without requiring a Secret.<br><br>You can call the [ListRegistries](https://docs.byteplus.com/en/docs/cr/listregistries) API to obtain the CR name.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can select one or more CR instances in the same region.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Private images that are pushed to the CR instance afterwards can also be pulled without requiring a Secret.</div><br> |
   |CrConfigmapData.Registries.0.Region |String |Yes |cn\-beijing |The region where the target CR instance is located. |
   

* Config example

   ```json
   {
     "CrConfigmapData": {
       "Namespace": "*",
       "ServiceAccount": "*",
       "Registries": [
         {
           "Instance": "cr-basic",
           "Region": "cn-beijing"
         }
       ]
     }
   }
   ```
   


<span id="b4f3f81f"></span>
### cr\-signature\-verifier

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">[<a href="https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features?lang=en">Beta \- apply for trial</a>] This add\-on is in beta. If necessary, apply to use it.</div>



* Configuration content

   
   |Parameter |Data type |Required |Example |Description |
   |---|---|---|---|---|
   |Replicas |Integer |No |2 |The number of replicas for the add\-on.<br><br><br>* Default value: 2<br><br>* Value range: Positive integers. |
   |WhitelistImages |Array |No |[] |The list of appended exempted images. Images matching this address will skip signature verification. Wildcards are supported. `*` matches one path level. `**` matches any depth of paths. Example: `docker.io/library/**`.<br><br>This list will not override Chart preset images. |
   |WhitelistNamespaces |Array |No |[] |The appended exempted namespaces. Pods in exempted namespaces will skip image signature verification.<br><br>This list does not override Chart preset namespaces. |
   |Rules |Array |Yes |*  |The list of image signature verification policies. You can enter up to 20 policies. Each policy is matched and takes effect in the declared order. |
   |Rules[].Name |String |Yes |production\-images |The name of the image signature verification policy. Any custom string. |
   |Rules[].Mode |String |Yes |Enforce |The processing method when image signature verification fails. The following two modes are supported:<br><br><br>* **Enforce**: Intercept deployment. Pod creation requests are rejected. This is suitable for production environments with high security requirements.<br><br>* **Audit**: Only alerts are recorded, and Pod deployment is not blocked. This is suitable for canary observation or test environments. This achieves troubleshooting without impacting business operations. |
   |Rules[].Namespaces |Array |Yes |["production"] |The namespace where the image signature verification policy takes effect. An empty array indicates all namespaces are matched. |
   |Rules[].ImagePatterns |Array |Yes |["cr\-cn\-beijing.volces.com/prod/\*\*"] |The address pattern of CR images that requires signature verification. Wildcards are supported. `*` matches one directory level. `**` matches any depth of directories.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Do not include public network image sources in the verification scope.</div><br> |
   |Rules[].Authorities |Array |Yes |*  |The list of trusted KMS signing keys. You can enter at least 1 key and up to 5 keys. |
   |Rules[].Authorities[].ProjectName |String |Yes |cr\-prod |The name of the project to which the KMS keyring belongs.  |
   |Rules[].Authorities[].KeyringName |String |Yes |cr\-signing\-keyring |The KMS keyring name. |
   |Rules[].Authorities[].KeyId |String |Yes |75c80f24\-d2ba\-\*\*\*\* |The KMS key ID. |
   

* Config example

   ```JSON
   {
     "Replicas": 2,
     "WhitelistImages": [],
     "WhitelistNamespaces": [],
     "Rules": [
       {
         "Name": "production-images",
         "Mode": "Enforce",
         "Namespaces": ["production"],
         "ImagePatterns": [
           "cr-cn-beijing.volces.com/prod/**"
         ],
         "Authorities": [
           {
             "ProjectName": "cr-prod",
             "KeyringName": "cr-signing-keyring",
             "KeyId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxx"
           }
         ]
       }
     ]
   }
   ```
   


<span id="prometheus-agent"></span>
### prometheus\-agent

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you modify the add\-on configuration by using the <a href="https://docs.byteplus.com/en/docs/vke/UpdateAddonConfig">UpdateAddonConfig</a> API, the <strong>VmAgent.InitShards</strong> and <strong>KubeStateMetrics.InitShards</strong> parameters cannot be updated. All other parameters can be updated as needed.</div>



* Configuration content

   
   |Parameter |Data type |Required |Example |Description |
   |---|---|---|---|---|
   |NodeExporterDisabled |Boolean |No |false |Whether to disable the node\-exporter add\-on. Valid values:<br><br><br>* **false**: (Default value) Do not disable it. The add\-on will be installed. The node\-exporter add\-on is used to collect various metrics of VMs on Linux.<br><br>* **true**: Disable the add\-on. The add\-on will not be installed. |
   |AutoScalingEnabled |Boolean |No |false |Whether to enable automatic scaling for the vm\-agent collector and kube\-state\-metrics add\-on. Valid values:<br><br><br>* **false**: (Default value) Disable automatic scale\-out. The number of shards for the add\-on is the configured initial shard count and will not automatically increase as resource utilization increases.<br><br>* **true**: Enable automatic scale\-out. |
   |VmAgent.InitShards |Integer |No |1 |Initial (minimum) shard count for vm\-agent.<br><br><br>* Default value: 1<br><br>* Value range: [1, 20]<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">This parameter cannot be modified after prometheus\-agent installation.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The recommended initial (minimum) shard count varies in clusters of different sizes. For details, see <a href="https://docs.byteplus.com/en/docs/vke/prometheus-agent-add-on?lang=en#MCvRXej7">Recommended specifications</a>.</div><br> |
   |VmAgent.MaxShards |Integer |No |5 |Maximum shard count for VM\-agent scale\-out.<br><br><br>* Default value: 5<br><br>* Value range: [Value of `VmAgent.InitShards`, 20]<br><br><br>It takes effect only when `AutoScalingEnabled` is true. |
   |VmAgent.Requests.Cpu |String |No |2 |VM\-agent resource CPU requests.<br><br><br>* Unit: core. When using millicores as the unit, specify the CPU request in the format `CPU request+m` , e.g., `100m` represents 100 millicores.<br><br>* Default value: 2 |
   |VmAgent.Requests.Memory |String |No |2Gi |The vm\-agent memory request.<br><br><br>* The unit is MiB or GiB, and the format is `memory request + unit`. For example, `90Mi` represents 90 MiB, and` 2Gi` represents 2 GiB.<br><br>* Default value: 2Gi |
   |VmAgent.Limits.Cpu |String |No |4 |VM\-agent CPU limit.<br><br><br>* Unit: core. When using millicores as the unit, specify the CPU request in the format `CPU request+m`. For example, `100m` represents 100 millicores.<br><br>* Default value: 4 |
   |VmAgent.Limits.Memory |String |No |4Gi |The maximum memory for the vm\-agent.<br><br><br>* The unit is MiB or GiB, and the format is `memory request + unit`. For example, `90Mi` indicates that the maximum memory is 90 MiB, and `2Gi` indicates that the maximum memory is 2 GiB.<br><br>* Default value: 4Gi |
   |KubeStateMetrics.InitShards |Integer |No |1 |Initial shard count of kube\-state\-metrics and minimum shard count for scale\-in.<br><br><br>* Default value: 1<br><br>* Value range: [1, 20]<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">This parameter cannot be modified after prometheus\-agent installation.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The recommended initial (minimum) shard count varies in clusters of different sizes. For details, see <a href="https://docs.byteplus.com/en/docs/vke/prometheus-agent-add-on?lang=en#MCvRXej7">Recommended specifications</a>.</div><br> |
   |KubeStateMetrics.MaxShards |Integer |No |5 |Maximum shard count for kube\-state\-metrics scale\-out.<br><br><br>* Default value: 5<br><br>* Value range: [value of `KubeStateMetrics.InitShards`, 20]<br><br><br>It takes effect only when `AutoScalingEnabled` is true. |
   |KubeStateMetrics.Requests.Cpu |String |No |200m |kube\-state\-metrics CPU resource request.<br><br><br>* Unit: core. When using millicores as the unit, specify the CPU request in the format `CPU request+m` , e.g., `100m` represents 100 millicores.<br><br>* Default value: 200m |
   |KubeStateMetrics.Requests.Memory |String |No |512Mi |kube\-state\-metrics resource memory request.<br><br><br>* The unit is MiB or GiB, and the format is `memory request + unit`. For example, `90Mi` represents 90 MiB, and` 2Gi` represents 2 GiB.<br><br>* Default value: 512Mi |
   |KubeStateMetrics.Limits.Cpu |String |No |800m |kube\-state\-metrics CPU limit.<br><br><br>* Unit: core. When using millicores as the unit, specify the CPU request in the format `CPU request+m`. For example, `100m` represents 100 millicores.<br><br>* Default value: 800m |
   |KubeStateMetrics.Limits.Memory |String |No |2Gi |Maximum kube\-state\-metrics memory request.<br><br><br>* The unit is MiB or GiB, and the format is `memory request + unit`. For example, `90Mi` indicates that the maximum memory request is 90 MiB, and `2Gi `indicates that the maximum memory is 2 GiB.<br><br>* Default value: 2Gi |
   

* Config example

   ```json
     {
         "NodeExporterDisabled": false,
         "VmAgent": {
             "InitShards": 2,
             "Requests": {
                 "Cpu": "500m",
                 "Memory": "512Mi"
             }
         }
     }
   ```
   


<span id="apmplus-opentelemetry-collector"></span>
### apmplus\-opentelemetry\-collector


* Configuration content

   
   |Parameter |Data type |Required |Example |Description |
   |---|---|---|---|---|
   |promReplicas |Integer |Yes |1 |Number of PrometheusScraper instances. A single instance supports 100,000 data entries per minute, with required resources of 1 CPU core and 2 GB of memory. In most cases, one instance can meet your business requirements. If the cluster generates 300,000 data entries per minute, set the number of instances to 3.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">PrometheusScraper is deployed by default as a Deployment.</div><br> |
   |otelReplicas |Integer |Yes |1 |Number of OpenTelemetryCollector instances. A single instance supports 10,000 traces per second, with required resources of 1 core CPU and 2 GB of memory. In most cases, one instance can meet your business requirements. If the cluster generates 30,000 traces per second, set the number of instances to 3.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">OpenTelemetryCollector is deployed as a StatefulSet by default.</div><br> |
   

* Config example

   ```json
   {
     "promReplicas": 1,
     "otelReplicas": 1
   }
   ```
   


<span id="cluster-autoscaler"></span>
### cluster\-autoscaler


* Configuration content

   
   |Parameter |Data type |Required |Sample value |Description |
   |---|---|---|---|---|
   |ScanInterval |String |No |10s |Autoscaling time interval in seconds. Values are `10s`, `15s`, `30s`, `60s`, `120s`, `180s`, and `300s`. |
   |MaxNodeProvisionTime |String |No |15 |Maximum timeout for waiting for node readiness. The value range is [1,60]. Default is 15. The unit is minutes. |
   |ScaleDown.Enabled |Boolean |Yes |false |Whether to enable automatic scale\-in. Values:<br><br><br>* **true**: Enable automatic scale\-in. After you enable this feature, automatic scale\-in is triggered if a certain number of idle nodes exist. This only takes effect for **pay\-as\-you\-go** node resources.<br><br>* **false**: (default value) Disable automatic scale\-in. |
   |ScaleDown.UtilizationThreshold |Float |No |0.5 |The scale\-in threshold for non\-GPU nodes. Value range: [0, 1].<br><br>This parameter is required when `ScaleDown.Enabled` is true. |
   |ScaleDown.GpuUtilizationThreshold |Float |No |0.5 |GPU node scale\-in threshold. Value range: [0,1].<br><br>This parameter is required when `ScaleDown.Enabled` is true. |
   |ScaleDown.UnneededTime |Integer |No |1 |Scale\-in trigger latency. The value range is [1,60]. The unit is minutes.<br><br>This parameter is required when `ScaleDown.Enabled` is true. |
   |ScaleDown.DelayAfterAdded |Integer |No |1 |Cooldown period for scale\-in after scale\-out. Value range: [1, 60], unit: Minutes.<br><br>This parameter is required when `ScaleDown.Enabled` is true. |
   |ScaleDown.DelayAfterFailure |Integer |No |1 |Cooldown period after scale\-in failure. Value range: [1,60]. Unit: minutes.<br><br>This parameter is required when `ScaleDown.Enabled` is true. |
   |ScaleDown.SkipNodesWithLocalStorageDisabled |Boolean |No |false |Whether to include nodes containing pods with local storage during scale\-in. Valid values:<br><br><br>* **true**: Yes, these are included.<br><br>* **false**: (Default value) No, these are not included.<br><br><br>This parameter is required when `ScaleDown.Enabled` is true. |
   |ScaleDown.SkipNodesWithSystemPodsDisabled |Boolean |No |false |Whether to include nodes running pods in the kube\-system namespace that are not managed by DaemonSet when scale\-in is triggered. Valid values:<br><br><br>* **true**: Yes, these are included.<br><br>* **false**: (Default value) No, these are not included.<br><br><br>This parameter is required when `ScaleDown.Enabled` is true. |
   |ScaleDown.MaxEmptyBulkDeleteNumber |Integer |No |5 |The maximum concurrent scale\-in capacity. Value range: [1, 15]. Unit: count.<br><br>This parameter is required when `ScaleDown.Enabled` is true. |
   |ScaleDown.MinReplicas |Integer |No |0 |Minimum number of pods allowed for workloads during draining |
   |ScaleDown.MaxGracefulTermination |Integer |No |600 |Maximum number of seconds to wait for pod termination when a node drains. |
   |ScaleDown.DaemonSetEvictionForNodesDisabled |Boolean |No |false |Specifies whether to exclude DaemonSet pods on the node from pod draining in node scale\-in.<br><br><br>* **true**: Yes, DaemonSet pods on the node are not drained.<br><br>* **false**: (Default value) No, DaemonSet pods on the node are drained. |
   |ScaleDown.IgnoreDaemonSetsUtilizationEnabled |Boolean |No |false |Whether to ignore DaemonSet pods when calculating resource utilization during scale\-in. Values:<br><br><br>* **true**: DaemonSet Pods are ignored during calculation.<br><br>* **false**: (Default) DaemonSet Pods are not ignored during calculation. |
   |ScaleDown.ScaleDownDelayTypeLocalEnabled |Boolean |No |false |Whether to calculate scale\-in delays based on the local status of node pools. Values: Valid values:<br><br><br>* **true**: Calculate scale\-in delays based on the local status of node pools. Maintain independent "scale\-in delay timers" for each node pool in the cluster, which can accelerate scale\-in and avoid resource waste.<br><br>* **false**: (Default) All node pools in the cluster share a single "scale\-in delay timer", and no scale\-in is performed during the scale\-in cooldown period. |
   |ScaleUp.Expander |String |Yes |random |Scale\-out policy used for automatically scaling out nodes. Valid values:<br><br><br>* **random**: (Default) Randomly select a node pool for scaling out.<br><br>* **most\-pods**: The node pool that can accommodate the most pods will be selected for scale\-out.<br><br>* **least\-waste**: The idle node pool with the least CPU resources will be selected for scale\-out.<br><br>* **priority**: The node pool with the highest configured priority will be selected for scale\-out. |
   

* Config example

   ```json
   {
       "ScanInterval": "15s",
       "ScaleDown": {
           "Enabled": false,
           "UtilizationThreshold": 0.5,
           "GpuUtilizationThreshold": 0.5,
           "UnneededTime": 10,
           "DelayAfterAdded": 10,
           "DelayAfterFailure": 3,
           "SkipNodesWithLocalStorageDisabled": true,
           "SkipNodesWithSystemPodsDisabled": true,
           "MaxEmptyBulkDeleteNumber": 5,
           "MinReplicas": 0,
           "MaxGracefulTermination": 600,
           "DaemonSetEvictionForNodesDisabled": false,
           "ScaleDownDelayTypeLocalEnabled": false,
           "IgnoreDaemonSetsUtilizationEnabled": false
       },
       "ScaleUp": {
           "Expander": "random"
       }
   }
   ```
   


<span id="event-collector"></span>
### event\-collector

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The add\-on configuration can be created only when you install the add\-on. You cannot call the <a href="https://docs.byteplus.com/en/docs/vke/UpdateAddonConfig">UpdateAddonConfig</a> API to modify the configuration later.</div>



* Configuration content

   
   |Parameter |Data type |Required |Example |Description |
   |---|---|---|---|---|
   |AccessKeyId |String |No |AK\*\*\*\*\*\*\*\*\*\*\*\* |This parameter is required when `DeployNodeType` is set to VirtualNode. Otherwise, it is optional.<br><br>Indicates that BytePlus AK/SK is used to authorize VCI to deploy this add\-on. |
   |AccessKeySecret |String |No |SK\*\*\*\*\*\*\*\*\*\* |This parameter is required when `DeployNodeType` is set to VirtualNode. Otherwise, it is optional.<br><br>Indicates that BytePlus AK/SK is used to authorize VCI to deploy this add\-on. |
   |ProjectId |String |Yes |4611ffdsa8\-\*\*\*\* |The ID of an existing log project associated with the current account in the region where the cluster is located.<br><br>You can call [DescribeProjects](https://docs.byteplus.com/en/docs/tls/api-describeprojects) to obtain the log project ID. If no log project is available, call [CreateProject](https://docs.byteplus.com/en/docs/tls/api-createproject) to create one. |
   |TopicId |String |Yes |f8fsdb36\-9fae\*\*\*\* |The ID of the log topic under the log project.<br><br>You can call [DescribeTopics](https://docs.byteplus.com/en/docs/tls/api-describetopics) to query the ID of the log topic. If no log topic is available, call [CreateTopic](https://docs.byteplus.com/en/docs/tls/api-createtopic) to create one. |
   

* Config example

   ```json
   {
     "ProjectId": "4611ffdsa8-****",
     "TopicId": "f8fsdb36-9fae-****",
     "AccessKeyId": "AK************",
     "AccessKeySecret": "SK**********"
   }
   ```
   


<span id="scheduler-plugin"></span>
### scheduler\-plugin


* Configuration content

   
   |Parameter |Data type |Required |Example |Description |
   |---|---|---|---|---|
   |NodePolicy |String |Yes |spread |The node scheduling policy. Values:<br><br><br>* **binpack**: Multiple pods are preferentially scheduled onto the same node. Resource scores, such as those for CPUs, memory, GPU computing power, and video memory, are comprehensively evaluated.<br><br>* **spread**: (Default) Multiple pods are scheduled across different nodes. Resource scores, such as those for CPUs, memory, GPU computing power, and video memory, are comprehensively evaluated. |
   |ResourceWeights |Array of **ResourceWeight** |No |[] |Resource weight for binpack/spread. For sub\-parameter description, see the **ResourceWeight** table in this topic. |
   |GPUShareCardPolicy |String |Yes |binpack |Scheduling policy for GPUs:<br><br><br>* **binpack**: (Default) Multiple pods preferentially use the same GPU.<br><br>* **spread**: Multiple pods use different GPUs.<br><br><br>If your workload has GPU Accelerated nodes and GPUs, see [Configuring scheduler custom parameters](https://docs.byteplus.com/en/docs/vke/Configuring-scheduler-parameters) for instructions on combining **NodePolicy** and **GPUShareCardPolicy**. |
   |PodTopologySpreadWeight |Integer |No |2 |Scoring weight of the native PodTopologySpread scheduling policy. The higher the score, the higher the priority of topology scattering scheduling, and the greater the probability that the pod will be dispatched to the decentralized topology region.<br><br><br>* Value range: [1,100]<br><br>* Default value: 2 |
   |PluginsCapacityScheduling |Boolean |No |false |[[Beta - apply for trial]](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features) Whether to enable capacity scheduling. Capacity scheduling enables resources to be shared among multi\-tenants through flexible quotas to improve the utilization of overall resources.<br><br><br>* **false**: (Default value) Disable.<br><br>* **true**: Enabled.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For more information about capacity scheduling, see <a href="https://docs.byteplus.com/en/docs/vke/Capacity-scheduling">Capacity scheduling</a>.</div><br> |
   |GangSchedulingEnabled |Boolean |No |false |[[Beta - apply for trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] Whether to enable Gang scheduling. Gang scheduling applies to the all\-or\-nothing scheduling scenario, in which either all pods are scheduled or no pods are scheduled if a group of pods are being scheduled at the same time.<br><br><br>* **false**: (Default value) Disable.<br><br>* **true**: Enabled.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For more information about Gang scheduling, see <a href="https://docs.byteplus.com/en/docs/vke/Gang-scheduling">Gang scheduling</a>.</div><br> |
   |ResourcePolicySchedulingEnabled |Boolean |No |false |Whether to enable ResourcePolicy scheduling. ResourcePolicy scheduling allows you to specify a custom ResourcePolicy to set the order in which pods of a workload are flexibly scheduled to different types of nodes, such as subscription ECS instances, pay\-as\-you\-go ECS instances, and virtual nodes.<br><br><br>* **false**: (Default value) Disable.<br><br>* **true**: Enabled.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">To enable ResourcePolicy scheduling, you need to configure <strong>ResourcePolicyWeight</strong>.</div><br><br><br><div data-tips="true" data-tips-type="warning">For instructions on using ResourcePolicy scheduling, see <a href="https://docs.byteplus.com/en/docs/vke/ResourcePolicy-scheduling">ResourcePolicy scheduling</a>.</div><br> |
   |ResourcePolicyWeight |Integer |No |100 |It takes effect only if ResourcePolicyScheduling is enabled. Set the scoring weight for ResourcePolicy scheduling. The higher the weight, the higher the score.<br><br><br>* Value range: [1,100].<br><br>* Default value: 100. |
   |LoadAwareSchedulingEnabled |Boolean |No |false |Whether to enable load\-aware scheduling. Load\-aware scheduling is performed based on the actual resource loads of nodes, which prevents application or node failures caused by excessive load on a single node.<br><br><br>* **false**: (Default value) Disable.<br><br>* **true**: Enabled.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For instructions on using load\-aware scheduling, see <a href="https://docs.byteplus.com/en/docs/vke/Load-aware-scheduling">Load\-aware scheduling</a>.</div><br> |
   |LoadAwareSchedulingConfig |Object |No |*  |This parameter takes effect after load\-aware scheduling is enabled (`LoadAwareSchedulingEnabled=true`).<br><br>Load\-aware scheduling configuration. For sub\-parameter description, see the **LoadAwareSchedulingConfig** table in this topic. |
   |NumaAwareSchedulingEnabled |Boolean |No |false |[[Beta - apply for trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] Whether to enable NUMA\-aware scheduling. NUMA\-aware scheduling provides the NUMA\-aware scheduling capability of central scheduler and stand\-alone cooperation to provide better performance for the load.<br><br><br>* **false**: (Default value) Disable.<br><br>* **true**: Enabled.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For more information about NUMA\-aware scheduling, see <a href="https://docs.byteplus.com/en/docs/vke/NUMA-aware-scheduling">NUMA\-aware scheduling</a>.</div><br> |
   

   **ResourceWeight**

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For more information about configuring <strong>Name</strong> and <strong>Weight</strong>, see <a href="https://docs.byteplus.com/en/docs/vke/Configuring-scheduler-parameters">Configuring custom scheduler parameters</a>.   </div>
   

   
   |Parameter |Data type |Required |Example |Description |
   |---|---|---|---|---|
   |Name |String |Yes |CPU |Enumeration values:<br><br><br>* CPU<br><br>* Memory<br><br>* nvidia.com/gpu<br><br>* vke.volcengine.com/mgpu\-core |
   |Weight |Integer |Yes |10 |The value range is [1,10]. Default value:<br><br><br>* CPU: 1<br><br>* Memory: 1<br><br>* nvidia.com/gpu: NULL<br><br>* vke.volcengine.com/mgpu\-core: 1 |
   

   **LoadAwareSchedulingConfig**

   
   |Parameter |Data type |Required |Example |Description |
   |---|---|---|---|---|
   |Scope |String |No |cluster |The application scope of the load\-aware scheduling policy. Values:<br><br><br>* **cluster**: The load\-aware scheduling policy takes effect at the cluster level, and all pod scheduling within the cluster uses the load\-aware scheduling add\-on.<br><br>* **pod**: (Default value) The load\-aware scheduling policy takes effect at the Pod level. You need to add an annotation to Pods to enable load\-aware scheduling. For information about how to configure it using annotations, see [Load-aware scheduling](https://docs.byteplus.com/en/docs/vke/Load-aware-scheduling). |
   |UsageThresholds |Array of **LoadAwareUsageThreshold** |No |*  |The resource utilization threshold of the load\-aware scheduling add\-on. For sub\-parameter description, see the **LoadAwareUsageThreshold** table in this topic. |
   |ResourceWeights |Array of **LoadAwareResourceWeight** |No |*  |Resource weight of the load\-aware scheduling add\-on. For sub\-parameter description, see the **LoadAwareResourceWeight** table in this topic. |
   

   **LoadAwareUsageThreshold**

   
   |Parameter |Data type |Required |Example |Description |
   |---|---|---|---|---|
   |Name |String |Yes |Memory |Node resource utilization threshold type for load\-aware scheduling. Values:<br><br><br>* **Cpu**: CPU resources<br><br>* **Memory**: Memory resources |
   |Threshold |Integer |Yes |100 |The node resource threshold in load\-aware scheduling.<br><br><br>* Value range: [1,100]<br><br>* Unit: %<br><br>* Default value:<br><br>   * Cpu: 70<br><br>   * Memory: 95 |
   

   **LoadAwareResourceWeight**

   
   |Parameter |Data type |Required |Example |Description |
   |---|---|---|---|---|
   |Name |String |Yes |Memory |Node resource weight type for load\-aware scheduling. Values:<br><br><br>* **Cpu**: CPU resources<br><br>* **Memory**: Memory resources |
   |Weight |Integer |Yes |10 |Node resource weight in load\-aware scheduling.<br><br><br>* The value range is [1,10]. The higher the weight, the higher the score.<br><br>* Default value:<br><br>   * Cpu: 1<br><br>   * Memory: 1 |
   

* Config example

   ```json
   {
    "NodePolicy": "spread",
    "GPUShareCardPolicy": "binpack",
    "PluginsCapacityScheduling": false
   }
   ```
   


<span id="ingress-nginx"></span>
### p2p\-accelerator


* Basic configuration

   
   |Parameter |Data type |Required |Example |Description |
   |---|---|---|---|---|
   |NydusEnabled |Boolean |Yes |false |Specify whether to enable P2P\-accelerated origin fetching for Nydus image lazy loading.<br><br><br>* **true**: Nydus fetches data from the origin through P2P Seed Peers. This applies to large\-scale scale\-out scenarios or situations where multiple nodes pull the same image at the same time. This solution reduces the back\-to\-origin request pressure on CR.<br><br>* **false**: (Default) Nydus fetches data directly from CR.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This configuration provides P2P\-accelerated origin fetching only for the image lazy loading feature. When you enable this feature, ensure the following conditions are met so that image lazy loading can function properly.</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The image\-accelerator add\-on is installed in the cluster. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Container-image-lazy-loading-solution?lang=en">Lazy loading of container images</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Lazy loading is enabled for the CR instance. For details, see <a href="https://docs.byteplus.com/en/docs/cr/create-image-lazy-loading-conversion-rules?lang=en">Creating rules for conversion to lazy\-loaded images</a>.</div><br> |
   |Registry |String |Yes |cr\-demo |Select a CR Standard Edition instance with P2P acceleration enabled. |
   |DeployNodeType |String |Yes |Node |The type of nodes used for add\-on deployment. Valid values:<br><br><br>* **Node**: Add\-ons are deployed on nodes (ECS instances).<br><br>* **VirtualNode**: Add\-ons are deployed on virtual nodes (VCI instances). |
   |NodeSelector |Array |No |[] |The global node selector for add\-ons. It can schedule resources such as Scheduler, Seed Peer, and Preheater Controller to specified nodes.<br><br><br>* If it is left empty, it indicates that nodes are not restricted.<br><br>* This configuration does not affect the scheduling of Peer, Watcher, and Preheater Agent resources. |
   |NodeSelector[].Key |String |No |cluster.vke.volcengine.com/pool\-name |The tag key used for node selection. |
   |NodeSelector[].Value |String |No |p2p |The tag value used for node selection. |
   |Tolerations |Array |No |[] |The global Kubernetes taint toleration rules for add\-ons. They are usually used together with node selectors (`NodeSelector`). This enables add\-ons to be scheduled onto tainted P2P dedicated node pools. |
   |Tolerations[].Key |String |No |cluster.vke.volcengine.com/pool\-name |The taint key in the toleration rule. Used to identify the taint on the P2P dedicated node pool. After configuration, the P2P add\-on workload can tolerate the taint with this key and can be scheduled to the corresponding dedicated node pool combined with `NodeSelector`. |
   |Tolerations[].Operator |String |No |Equal |The taint match method. Valid values:<br><br><br>* **Equal**: Indicates that both the taint key (Key) and the taint value (Value) must match the node taint.<br><br>* **Exists**: Indicates that only the taint key (Key) is matched. |
   |Tolerations[].Value |String |No |p2p |The taint value in the toleration rule. When `Operator` is `Equal`, this value must match the value configured for the node taint. |
   |Tolerations[].Effect |String |No |NoSchedule |The tolerated node taint effect must be consistent with the `Effect` configured for the taint on the node.<br><br>P2P dedicated node pools use `NoSchedule`. This indicates that, by default, workloads without corresponding toleration rules cannot be scheduled onto this node pool, thereby isolating P2P add\-ons from regular business workloads. |
   

* Scheduler configuration

   
   |Parameter |Data type |Required |Sample value |Description |
   |---|---|---|---|---|
   |Scheduler.Replicas |Integer |No |3 |The number of Scheduler replicas.<br><br><br>* The value is a positive integer. Default value: 3.<br><br>* We recommend configuring multiple replicas to prevent a single point of failure from affecting image pull scheduling across the cluster. |
   |Scheduler.Tolerations |Array |No |[] |Configure the taint toleration rules for the Scheduler. The priority of this rule is higher than the global rules in the basic configuration. |
   |Scheduler.Affinity |Object |No |{} |Configure the Kubernetes affinity rule of the Scheduler. |
   |Scheduler.Resources.Limits.Cpu |String |No |4 |The CPU upper limit of the Scheduler add\-on.<br><br><br>* The value is a string. The value must be greater than 0, and the precision must not be less than 1m.<br><br>* Unit: core or millicore.<br><br>   * When the unit is cores, no additional unit needs to be configured. For example, 2 indicates 2 CPUs.<br><br>   * When the unit is millicores, the format is `CPU request+m`. For example, `100m` indicates 100 millicores.<br><br>* Default value: 4. |
   |Scheduler.Resources.Limits.Memory |String |No |8Gi |The memory upper limit of the Scheduler add\-on.<br><br><br>* The value is a string, which is in the format of `number+unit`.<br><br>* Unit: Mi or Gi. For example, `90Mi` indicates that the memory is 90 MiB, and `2Gi` indicates that the memory is 2 GiB.<br><br>* Default value: 8 Gi. |
   |Scheduler.Resources.Requests.Cpu |String |No |2 |The CPU request for the Scheduler add\-on.<br><br><br>* The value is a string. The value must be greater than 0, and the precision must not be less than 1m.<br><br>* Unit: core or millicore.<br><br>   * When the unit is cores, no additional unit needs to be configured. For example, 2 indicates 2 CPUs.<br><br>   * When the unit is millicores, the format is `CPU request+m`. For example, `100m` indicates 100 millicores.<br><br>* The default value is 2. |
   |Scheduler.Resources.Requests.Memory |String |No |4Gi |The memory request for the Scheduler add\-on.<br><br><br>* The value is a string, which is in the format of `number+unit`.<br><br>* Unit: Mi or Gi. For example, `90Mi` indicates that the memory is 90 MiB, and `2Gi` indicates that the memory is 2 GiB.<br><br>* Default value: 4Gi. |
   

* Seed Peer configuration (DfdaemonProxy)

   
   |Parameter |Data type |Required |Example |Description |
   |---|---|---|---|---|
   |DfdaemonProxy.Replicas |Integer |No |3 |The number of Seed Peer replicas.<br><br><br>* The value is a positive integer. Default value: 3.<br><br>* We recommend configuring multiple replicas to prevent a single point of failure from affecting image pull scheduling across the cluster. |
   |DfdaemonProxy.Tolerations |Array |No |[] |Configure the taint toleration rules for the Seed Peer. The priority of this rule is higher than the global rules in the basic configuration. |
   |DfdaemonProxy.Affinity |Object |No |{} |Configure the Kubernetes affinity rule of the Seed Peer. |
   |DfdaemonProxy.Persistence.HostPath |Object |No |{} |Use the directory of the local disk for a node to save the image cache. |
   |DfdaemonProxy.Persistence.HostPath.Path |String |No |/mnt/p2pcache |When you use the local directory of a node to save the image cache, the save directory on the node is fixed to `/mnt/p2pcache`. Do not change it to another path. |
   |DfdaemonProxy.Persistence.HostPath.Type |String |No |DirectoryOrCreate |When using the local directory of a node to save the image cache, use the `HostPath` type. When the value is set to `DirectoryOrCreate`, it indicates that the system will automatically create the directory if it does not exist. |
   |DfdaemonProxy.Persistence.StorageClass |String |No |ebs\-ssd |Use cloud disks to save image caches and specify the StorageClass used by the PVC.<br><br>If the parameter is left empty, it indicates that the system will automatically select a PVC based on the cloud disk types supported by the account. |
   |DfdaemonProxy.Persistence.Size |String |No |100Gi |The cache disk capacity applied for each Seed Peer instance. Default value: 100 GiB. |
   |DfdaemonProxy.Resources.Limits.Cpu |String |No |12 |The CPU upper limit of the Seed Peer add\-on.<br><br><br>* The value is a string. The value must be greater than 0, and the precision must not be less than 1m.<br><br>* Unit: core or millicore.<br><br>   * When the unit is cores, no additional unit needs to be configured. For example, 2 indicates 2 CPUs.<br><br>   * When the unit is millicores, the format is `CPU request+m`. For example, `100m` indicates 100 millicores.<br><br>* Default value: 12. |
   |DfdaemonProxy.Resources.Limits.Memory |String |No |24Gi |The memory upper limit of the Seed Peer add\-on.<br><br><br>* The value is a string, which is in the format of `number+unit`.<br><br>* Unit: Mi or Gi. For example, `90Mi` indicates that the memory is 90 MiB, and `2Gi` indicates that the memory is 2 GiB.<br><br>* Default value: 24Gi. |
   |DfdaemonProxy.Resources.Requests.Cpu |String |No |4 |The CPU request for the Seed Peer add\-on.<br><br><br>* The value is a string. The value must be greater than 0, and the precision must not be less than 1m.<br><br>* Unit: core or millicore.<br><br>   * When the unit is cores, no additional unit needs to be configured. For example, 2 indicates 2 CPUs.<br><br>   * When the unit is millicores, the format is `CPU request+m`. For example, `100m` indicates 100 millicores.<br><br>* Default value: 4. |
   |DfdaemonProxy.Resources.Requests.Memory |String |No |8Gi |The memory request for the Seed Peer add\-on.<br><br><br>* The value is a string, which is in the format of `number+unit`.<br><br>* Unit: Mi or Gi. For example, `90Mi` indicates that the memory is 90 MiB, and `2Gi` indicates that the memory is 2 GiB.<br><br>* Default value: 8 Gi. |
   |DfdaemonProxy.Config.Storage.Keep |Boolean |No |true |Specify whether to retain existing cache data after the Seed Peer restarts.<br><br><br>* **true**: (Default) After the Seed Peer restarts, it continues to use the cached image data without affecting image pulls by other nodes.<br><br>* **false**: When the Seed Peer restarts, its cache is lost, but image data can still be obtained from the cache of other Peer nodes in the cluster. An origin pull from CR is triggered only when none of the nodes have cached data. We recommend using this option only when you must forcibly clear the Seed Peer cache. |
   |DfdaemonProxy.Config.Gc.Policy.TaskTtl |String |No |720h |The expiration time of the Seed Peer cache. Cache data that is not accessed within this period is marked as reclaimable.<br><br>The Kubernetes duration. The value is a string. It supports time units, such as 48h and 168h. |
   |DfdaemonProxy.Config.Gc.Policy.DiskThreshold |String |No |0 |The disk capacity involved in the cache reclaim threshold calculation, <br><br><br>* The value is a string, which is in the format of `number+unit`. such as 512GiB.<br><br>* This value must be less than the actual size of the cache disk.<br><br>* A value of 0 indicates that the actual capacity of the cache disk is used. |
   |DfdaemonProxy.Config.Gc.Policy.DiskHighThresholdPercent |Integer |No |90 |The high disk usage threshold, in percentage. When disk usage reaches this threshold, cache reclamation is triggered to clear data until usage drops below the low watermark.<br><br><br>* When disk capacity is small or the cache grows quickly, lower this value appropriately to trigger cache reclamation early and prevent disk space exhaustion.<br><br>* Increasing this value retains more cached data but risks exhausting disk space.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The value of this parameter must be greater than <code>DiskLowThresholdPercent</code>.</div><br> |
   |DfdaemonProxy.Config.Gc.Policy.DiskLowThresholdPercent |Integer |No |70 |The low disk usage threshold, in percentage. After reclamation is triggered, the system keeps clearing the cache until disk usage drops below this threshold. A lower value causes more data to be reclaimed in each cleanup cycle, which reduces reclamation frequency but deletes more potentially valid cache. Keep a reasonable gap from the high threshold to avoid frequent small\-scale reclamation.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The value of this parameter must be less than <code>DiskHighThresholdPercent</code>.</div><br> |
   

* Peer configuration (Dfdaemon)

   
   |Parameter |Data type |Required |Example |Description |
   |---|---|---|---|---|
   |Dfdaemon.Persistence.HostPath.Path |String |No |/mnt/p2pcache |The mount path of the Peer on the node. It is fixed to `/mnt/p2pcache`. Do not change it to another path.<br><br><br>* Only takes effect for nodes with the label `vke.volcengine.com/p2p-cache-disk=true`.<br><br>* Other nodes use emptyDir on the system volume. |
   |Dfdaemon.Persistence.HostPath.Type |String |No |DirectoryOrCreate |The HostPath type. When the value is set to `DirectoryOrCreate`, it indicates that the system will automatically create the directory if it does not exist. |
   |Dfdaemon.Resources.Limits.Cpu |String |No |2 |The CPU upper limit of the Peer add\-on.<br><br><br>* The value is a string. The value must be greater than 0, and the precision must not be less than 1m.<br><br>* Unit: core or millicore.<br><br>   * When the unit is cores, no additional unit needs to be configured. For example, 2 indicates 2 CPUs.<br><br>   * When the unit is millicores, the format is `CPU request+m`. For example, `100m` indicates 100 millicores.<br><br>* The default value is 2. |
   |Dfdaemon.Resources.Limits.Memory |String |No |4Gi |The memory upper limit of the Peer add\-on.<br><br><br>* The value is a string, which is in the format of `number+unit`.<br><br>* Unit: Mi or Gi. For example, `90Mi` indicates that the memory is 90 MiB, and `2Gi` indicates that the memory is 2 GiB.<br><br>* Default value: 4Gi. |
   |Dfdaemon.Resources.Requests.Cpu |String |No |200m |The CPU request for the Peer add\-on.<br><br><br>* The value is a string. The value must be greater than 0, and the precision must not be less than 1m.<br><br>* Unit: core or millicore.<br><br>   * When the unit is cores, no additional unit needs to be configured. For example, 2 indicates 2 CPUs.<br><br>   * When the unit is millicores, the format is `CPU request+m`. For example, `100m` indicates 100 millicores.<br><br>* Default value: 0.2. |
   |Dfdaemon.Resources.Requests.Memory |String |No |200Mi |The memory request for the Peer add\-on.<br><br><br>* The value is a string, which is in the format of `number+unit`.<br><br>* Unit: Mi or Gi. For example, `90Mi` indicates that the memory is 90 MiB, and `2Gi` indicates that the memory is 2 GiB.<br><br>* Default value: 200Mi. |
   |Dfdaemon.Config.Storage.Keep |Boolean |No |true |Specify whether to retain cache data on the node after the Peer restarts.<br><br><br>* **true**: After the Peer restarts, it continues to use the cached image data without affecting normal pulls on the node.<br><br>* **false**: When the Peer restarts, its cache is lost, but image data can still be obtained from the Seed Peer or the cache of other Peer nodes in the cluster. An origin pull from CR is triggered only when none of the nodes have cached data. We recommend using this option only when you must forcibly clear the cache on the node. |
   |Dfdaemon.Config.Gc.Policy.TaskTtl |String |No |168h |The expiration time of the Peer cache. Cache data that is not accessed within this period is marked as reclaimable.<br><br>The Kubernetes duration. The value is a string. It supports time units, such as 48h and 168h. |
   |Dfdaemon.Config.Gc.Policy.DiskThreshold |String |No |0 |The disk capacity involved in the cache reclaim threshold calculation, <br><br><br>* The value is a string, which is in the format of `number+unit`. such as 512GiB.<br><br>* This value must be less than the actual size of the cache disk.<br><br>* A value of 0 indicates that the actual capacity of the cache disk is used. |
   |Dfdaemon.Config.Gc.Policy.DiskHighThresholdPercent |Integer |No |90 |The high disk usage threshold, in percentage. When disk usage reaches this threshold, cache reclamation is triggered to clear data until usage drops below the low watermark.<br><br><br>* When disk capacity is small or the cache grows quickly, lower this value appropriately to trigger cache reclamation early and prevent disk space exhaustion.<br><br>* Increasing this value retains more cached data but risks exhausting disk space.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The value of this parameter must be greater than <code>DiskLowThresholdPercent</code>.</div><br> |
   |Dfdaemon.Config.Gc.Policy.DiskLowThresholdPercent |Integer |No |70 |The low disk usage threshold, in percentage. After reclamation is triggered, the system keeps clearing the cache until disk usage drops below this threshold. A lower value causes more data to be reclaimed in each cleanup cycle, which reduces reclamation frequency but deletes more potentially valid cache. Keep a reasonable gap from the high threshold to avoid frequent small\-scale reclamation.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The value of this parameter must be less than <code>DiskHighThresholdPercent</code>.</div><br> |
   

* Image warm\-up configuration

   
   |Parameter |Data type |Required |Example |Description |
   |---|---|---|---|---|
   |EnableImagePreheater |Boolean |No |true |Whether to deploy the image warm\-up add\-on. Valid values:<br><br><br>* **true**: Creates image warm\-up add\-ons, including Preheat Controller, Preheat Agent, and related resources.<br><br>* **false**: Do not create. |
   |PreheaterController.Replicas |Integer |No |2 |The number of Preheat Controller replicas.<br><br><br>* The value is an integer. Valid values: 1 to 5.<br><br>* The default value is 2. |
   |PreheaterController.Resources.Limits.Cpu |String |No |1 |The CPU upper limit of the Preheat Controller add\-on.<br><br><br>* The value is a string. The value must be greater than 0, and the precision must not be less than 1m.<br><br>* Unit: core or millicore.<br><br>   * When the unit is cores, no additional unit needs to be configured. For example, 2 indicates 2 CPUs.<br><br>   * When the unit is millicores, the format is `CPU request+m`. For example, `100m` indicates 100 millicores.<br><br>* Default value: 1. |
   |PreheaterController.Resources.Limits.Memory |String |No |1Gi |The memory upper limit of the Preheat Controller add\-on.<br><br><br>* The value is a string, which is in the format of `number+unit`.<br><br>* Unit: Mi or Gi. For example, `90Mi` indicates that the memory is 90 MiB, and `2Gi` indicates that the memory is 2 GiB.<br><br>* Default value: 1Gi. |
   |PreheaterController.Resources.Requests.Cpu |String |No |200m |The CPU request for the Preheat Controller add\-on.<br><br><br>* The value is a string. The value must be greater than 0, and the precision must not be less than 1m.<br><br>* Unit: core or millicore.<br><br>   * When the unit is cores, no additional unit needs to be configured. For example, 2 indicates 2 CPUs.<br><br>   * When the unit is millicores, the format is `CPU request+m`. For example, `100m` indicates 100 millicores.<br><br>* Default value: 0.2. |
   |PreheaterController.Resources.Requests.Memory |String |No |256Mi |The memory request for the Preheat Controller add\-on.<br><br><br>* The value is a string, which is in the format of `number+unit`.<br><br>* Unit: Mi or Gi. For example, `90Mi` indicates that the memory is 90 MiB, and `2Gi` indicates that the memory is 2 GiB.<br><br>* Default value: 256Mi. |
   |PreheaterAgent.Resources.Limits.Cpu |String |No |2 |The CPU upper limit of the Preheat Agent add\-on.<br><br><br>* The value is a string. The value must be greater than 0, and the precision must not be less than 1m.<br><br>* Unit: core or millicore.<br><br>   * When the unit is cores, no additional unit needs to be configured. For example, 2 indicates 2 CPUs.<br><br>   * When the unit is millicores, the format is `CPU request+m`. For example, `100m` indicates 100 millicores.<br><br>* The default value is 2. |
   |PreheaterAgent.Resources.Limits.Memory |String |No |512Mi |The memory upper limit of the Preheat Agent add\-on.<br><br><br>* The value is a string, which is in the format of `number+unit`.<br><br>* Unit: Mi or Gi. For example, `90Mi` indicates that the memory is 90 MiB, and `2Gi` indicates that the memory is 2 GiB.<br><br>* Default value: 512Mi. |
   |PreheaterAgent.Resources.Requests.Cpu |String |No |100m |The CPU request for the Preheat Agent add\-on.<br><br><br>* The value is a string. The value must be greater than 0, and the precision must not be less than 1m.<br><br>* Unit: core or millicore.<br><br>   * When the unit is cores, no additional unit needs to be configured. For example, 2 indicates 2 CPUs.<br><br>   * When the unit is millicores, the format is `CPU request+m`. For example, `100m` indicates 100 millicores.<br><br>* Default value: 0.1. |
   |PreheaterAgent.Resources.Requests.Memory |String |No |128Mi |The memory request for the Preheat Agent add\-on.<br><br><br>* The value is a string, which is in the format of `number+unit`.<br><br>* Unit: Mi or Gi. For example, `90Mi` indicates that the memory is 90 MiB, and `2Gi` indicates that the memory is 2 GiB.<br><br>* Default value: 128 Mi. |
   

* Config example

   ```json
   {
     "NydusEnabled": false,
     "Registry": "cr-demo",
     "DeployNodeType": "Node",
     "NodeSelector": [
       {
         "Key": "cluster.vke.volcengine.com/pool-name",
         "Value": "p2p"
       }
     ],
     "Tolerations": [
       {
         "Key": "cluster.vke.volcengine.com/pool-name",
         "Operator": "Equal",
         "Value": "p2p",
         "Effect": "NoSchedule"
       }
     ],
     "Scheduler": {
       "Replicas": 3,
       "Resources": {
         "Limits": { "Cpu": "4", "Memory": "8Gi" },
         "Requests": { "Cpu": "2", "Memory": "4Gi" }
       }
     },
     "DfdaemonProxy": {
       "Replicas": 3,
       "Persistence": {
         "StorageClass": "ebs-ssd",
         "Size": "100Gi"
       },
       "Resources": {
         "Limits": { "Cpu": "12", "Memory": "24Gi" },
         "Requests": { "Cpu": "4", "Memory": "8Gi" }
       },
       "Config": {
         "Storage": { "Keep": true },
         "Gc": {
           "Policy": {
             "TaskTtl": "720h",
             "DiskThreshold": "0",
             "DiskHighThresholdPercent": 90,
             "DiskLowThresholdPercent": 70
           }
         }
       }
     },
     "Dfdaemon": {
       "Persistence": {
         "HostPath": {
           "Path": "/mnt/p2pcache",
           "Type": "DirectoryOrCreate"
         }
       },
       "Resources": {
         "Limits": { "Cpu": "2", "Memory": "4Gi" },
         "Requests": { "Cpu": "200m", "Memory": "200Mi" }
       },
       "Config": {
         "Storage": { "Keep": true },
         "Gc": {
           "Policy": {
             "TaskTtl": "168h",
             "DiskThreshold": "0",
             "DiskHighThresholdPercent": 90,
             "DiskLowThresholdPercent": 70
           }
         }
       }
     },
     "EnableImagePreheater": true,
     "PreheaterController": {
       "Replicas": 2,
       "Resources": {
         "Limits": { "Cpu": "1", "Memory": "1Gi" },
         "Requests": { "Cpu": "200m", "Memory": "256Mi" }
       }
     },
     "PreheaterAgent": {
       "Resources": {
         "Limits": { "Cpu": "2", "Memory": "512Mi" },
         "Requests": { "Cpu": "100m", "Memory": "128Mi" }
       }
     }
   }
   ```
   


<span id="mgpu"></span>
### mgpu


* Configuration content

   
   |Parameter |Data type |Required |Example |Description |
   |---|---|---|---|---|
   |ExporterDisabled |Boolean |No |true |Whether to disable the mgpu\-exporter, which is an add\-on for monitoring resources of shared GPU resources:<br><br><br>* **false**: (Default value) Do not disable. This will install the add\-on and use Prometheus monitoring to monitor metrics related to mGPU.<br><br>* **true**: Disable. The add\-on will not be installed. You can install your own monitoring exporter to monitor mGPU\-related metrics. |
   

* Config example

   ```json
   {
     "ExporterDisabled": true
   }
   ```
   


<span id="nvidia-device-plugin"></span>
### nvidia\-device\-plugin


* Configuration content

   
   |Parameter |Data type |Required |Example |Description |
   |---|---|---|---|---|
   |ExporterDisabled |Boolean |Yes |true |Whether to disable the NVIDIA GPU resource monitoring add\-on dcgm\-exporter:<br><br><br>* **false**: (Default value) Do not disable. This will install the add\-on and use Prometheus monitoring to monitor metrics related to NVIDIA GPU resources.<br><br>* **true**: Disable the add\-on. You can install your own exporter to monitor NVIDIA GPU metrics. |
   

* Config example

   ```json
   {
     "ExporterDisabled": true
   }
   ```
   


<span id="prometheus-adapter"></span>
### Prometheus\-adapter

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The add\-on configuration can be created only when you install the add\-on. You cannot call the <a href="https://docs.byteplus.com/en/docs/vke/UpdateAddonConfig">UpdateAddonConfig</a> API to modify the configuration later.</div>



* Configuration content

   
   |Parameter |Data type |Required |Example |Description |
   |---|---|---|---|---|
   |AuthType |String |Yes |EcsRole |The authentication method for VMP workspaces. Values:<br><br>**EcsRole**: Use IAM roles of ECS for authentication. |
   

* Config example

   ```json
   {
     "AuthType": "EcsRole"
   }
   ```
   


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://vke.cn-beijing.byteplusapi.com.cn?Action=CreateAddon&Version=2022-05-12 HTTP/1.1
Content-Type:application/json
{
    "ClusterId": "cc5silum********",
    "Name": "ingress-nginx",
    "DeployMode": "Unmanaged",
    "DeployNodeType": [
        "VirtualNode"
    ],
    "Config": "{\"Replica\":1,\"Resource\":{\"Request\":{\"Cpu\":\"0.25\",\"Memory\":\"512Mi\"},\"Limit\":{\"Cpu\":\"0.5\",\"Memory\":\"1024Mi\"}},\"PrivateNetwork\":{\"SubnetId\":\"subnet-2d61qn69iji****\",\"IpVersion\":\"IPV4\"}}",
    "ClientToken": "BC028527-33B9-4990-A633-84E9F9******"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

This API has no API\-specific response parameters. For details about common response parameters, see [Response results](https://docs.byteplus.com/en/docs/vke/Response).

<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1 200 OK
Content-Type:application/json

{
    "ResponseMetadata": {
        "RequestId": "021635330********",
        "Action": "CreateAddon",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The error codes for this API are listed in the table below. For public error codes, see [Public error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes).


|HTTP status code |Error code |Error message |Description |
|---|---|---|---|
|409 |AlreadyExists.{{parameter}} |The specified {{resourceType}} {{resourceId}} already exists. |The specified resources already exist. |
|400 |OperationDenied.NetworkMode |The specified addon is not compatible with the current network mode. |The current network model is not supported. |
|400 |OperationDenied.DeployMode |The specified deploy mode is not supported. |The current deployment mode is not supported. |
|400 |OperationDenied.DeployNodeType |The specified deploy node type is not supported. |The current node type is not supported. |
|400 |OperationDenied.ClusterStatus |The action is forbidden due to cluster status {{statusPhase}} and {{statusConditions}}. |The current status of the specified cluster does not support this operation. Confirm the required cluster status for this API and try again. |
|400 |NotSupported.{{parameter}} |The specified {{resourceType}} {{resourceContent}} is not supported. |The specified resources cannot be installed. |

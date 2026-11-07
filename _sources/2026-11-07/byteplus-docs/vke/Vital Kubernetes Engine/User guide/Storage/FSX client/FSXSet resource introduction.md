---
title: "FSXSet resource introduction"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Introduction_to_FSXSet_resources"
---

FSXSet is a Kubernetes CRD for managing FSX clients. It can manage client deployment, versions, and upgrade policies by node group. This is suitable for scenarios requiring differentiated configurations, on‑demand creation, and client upgrades. This topic describes the basic concepts and configurations of FSXSet resources.

<span id="fce26GHt"></span>
## Resource overview

FSXSet is a cluster‑level Kubernetes CRD that performs centralized lifecycle management on FSX clients, such as creation, deletion, and hot upgrades. In addition, you can create one or more FSXSet objects to control the configurations of FSX clients on different nodes, such as resource specifications, image versions, and upgrade methods. FSXSet meets the requirements of the following scenarios:


* **Smooth node\-level canary upgrade**: You can create differentiated FSXSet configurations as needed and apply them only to a few designated test nodes. After validation, the new version can be rolled out to the entire cluster to achieve controllable canary hot upgrades.

* **Custom configurations for heterogeneous nodes**: You can specify different FSXSet configurations for different node pools. For example, for AI‑compute node pools, you can increase the CPU/memory quotas for the client. For idle nodes, you can enable automatic cleanup policies to reclaim resources.


<span id="PSPGmtLU"></span>
## Core feature

FSXSet provides the following core features for managing FSX clients.


|Core feature |Description |Related documentation |
|---|---|---|
|Node grouping and on‑demand management |* Use the node label `fsx.csi.volcengine.com/group` to divide nodes into logical groups so that different FSX client configurations can be applied to different groups.<br><br>* Different FSX client creation modes are supported, including Immediate (clients created immediately after nodes join groups) and WaitForFirstConsumer (clients created on‑demand). Select an appropriate mode flexibly based on your business requirements.<br><br>* On‑demand automatic reclamation is supported to release node resources. This applies to resource\-constrained scenarios. Persistent client deployment is supported to accelerate the first mount. |[Using FSXSet to implement on-demand client creation](https://docs.byteplus.com/en/docs/vke/Using_FSXSet_to_implement_on-demand_client_creation?lang=zh) |
|Differentiated configuration |* Create multiple FSXSet resources to configure differentiated Pod specifications (such as CPU, memory, and network resources) for different node groups. For example, assign different FSX client configurations to nodes with varying specifications in the cluster.<br><br>* Use `parameterTemplate` to flexibly define FSX client templates. |[Using FSXSet to implement differentiated configurations for clients](https://docs.byteplus.com/en/docs/vke/Using_FSXSet_to_implement_differentiated_configurations_for_clients?lang=zh) |
|Hot upgrade |* The rolling upgrade and canary upgrade policies are supported.<br><br>* You can trigger upgrades by modifying the image field in FSXSet. The controller automatically orchestrates the transition between old and new Pods.<br><br>* `maxSurge` and `maxUnavailable` are supported to control upgrade concurrency. |[Using FSXSet to implement smooth client upgrades](https://docs.byteplus.com/en/docs/vke/Using_FSXSet_to_implement_smooth_client_upgrades) |


<span id="X4TjxQ0w"></span>
## Description

When you install the fsxset\-controller add\-on in a cluster, the system will automatically install FSXSet custom resources. For details, see [fsxset-controller](https://docs.byteplus.com/en/docs/vke/fsxset-controller-add-on). You can view or configure the corresponding FSXSet resources by using the following methods.


<Tabs>
<Tab zoneid="A91jj7QWDa" title="Configure through the console">
<TabTitle>Configure through the console</TabTitle>

1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. Click the target cluster name to go to the management page of this cluster.

3. In the left navigation pane, select **Addons** and click the **Storage** tab.

4. In the lower\-right corner of the csi\-fsx add\-on card, click  **`...`**   **\> Client configuration**.

5. In the Client configuration panel, view the FSXSet resources in the cluster.

6. Find the target resource and click **Update** in the **Actions** column to view or update the FSXSet resource.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">To configure additional features, go to <strong>Workload \> Resource Explorer</strong> to view or modify the YAML file of the FSXSet resources.    </div>
   


</Tab>
<Tab zoneid="Yg5Nb9Oj1X" title="Configure through kubectl">
<TabTitle>Configure through kubectl</TabTitle>

1. [Connect to the cluster through kubectl](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

2. Run the following command to view FSXSet resources in the cluster.

   ```Bash
   kubectl get fsxset
   ```
   

   The expected result is as follows: The FSXSet resources that exist in the cluster are displayed.

   ```Bash
   NAME                GROUP               DESIREDREVISION    DESIRED   CURRENT   READY   AVAILABLE   UPDATED   MATCHED   AGE
   default             default             ed48241c49***                                                                  47h
   doc-demo            doc                 e12fd97867***      2         2         2       2           2         2         146m
   
   ```
   

3. Run the following command to view details of the specified FSXSet resource. `${fsxset-name}` is the FSXSet resource name.

   ```Bash
   kubectl get fsxset ${fsxset-name} -o yaml
   ```
   

   The following content displays the expected result and specific parameter descriptions.


</Tab>
</Tabs>


The following sample code shows how to view or configure FSXSet resources.

```YAML
apiVersion: csi.vke.volcengine.com/v1alpha1
kind: FSXSet
metadata:
  name: doc-demo # The FSXSet resource name.
spec:
  groupName: doc # The logical group name, which corresponds to the node label fsx.csi.volcengine.com/group. The system selects nodes on which to apply this FSXSet configuration based on this name. This achieves differentiated client configuration.
  isDefault: true # Whether it is the cluster default configuration. Valid values: true and false.
  createMode: WaitForFirstConsumer # The FSX client creation mode. Valid values: Immediate (The FSX client is created immediately after the target node is added to a group) and WaitForFirstConsumer (The FSX client is created only when a workload that depends on FSX is first deployed on the target node).
  scaleDownAfterNoDependency: true # Whether to automatically reclaim FSX client Pods when no workloads depend on FSX on the node. Valid values: true and false.
  scaleDownAfterIdleDuration: 3m # The idle wait duration before automatic reclamation of FSX client Pods.
  upgradeStrategy:
    type: RollingUpdate # The upgrade policy of the FSX client. Valid values: RollingUpdate and OnLabel.
    maxSurge: 1 # The number of additional Pods that can be created during a rolling upgrade. Default value: 1.
    maxUnavailable: 1 # The maximum number of nodes that can be unavailable simultaneously during a rolling upgrade.
  template:
    parameterTemplate: # The FSX client configuration template.
      image: vke-cn-beijing.cr.volces.com/vke/fsx-agent:v0.12.3 # The image address and version of the FSX client.
      resources: # The resource configuration of the FSX client.
        requests:
          cpu: 100m
          memory: 128Mi
        limits:
          cpu: 2000m
          memory: 2Gi
```


The following table describes the key parameters of FSXSet resources.


|**Type** |Parameter |Required |**Description** |
|---|---|---|---|
|Basic |metadata.name |Yes |The FSXSet resource name. It needs to be unique within the same cluster. |
||spec.groupName |No |The logical group name, which corresponds to the node label `fsx.csi.volcengine.com/group`. The system selects nodes on which to apply this FSXSet configuration based on this name. This achieves differentiated client configuration.<br><br><br>* This parameter cannot be left empty.<br><br>* If this parameter is not specified, the system uses the default FSXSet configuration named default.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For example, if this parameter is set to <code>doc</code>, the current FSXSet configuration will be applied to only nodes with the node label <code>fsx.csi.volcengine.com/group=doc</code>. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Using_FSXSet_to_implement_differentiated_configurations_for_clients">FSXSet to implement client\-differentiated configuration</a>.</div><br> |
||spec.isDefault |No |Whether it is the cluster default FSXSet, which is used to take over nodes that do not match any other grouping rules.  <br><br><br>* `true`: It is the cluster default FSXSet.<br><br>* `false`: (Default) It is not the cluster default FSXSet.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Only one resource object with <code>isDefault</code> set to <code>true</code> can exist in the cluster.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If this parameter is not configured, the default value is <code>false</code>. This indicates that it is not the system default FSXSet.</div><br> |
|Management policy |spec.createMode<br><br> |No |The FSX client creation mode.  <br><br><br>* `Immediate`: The FSX client is created immediately after the target node is assigned to a resource group.<br><br>* `WaitForFirstConsumer`: (Default) The FSX client is created only when a workload that depends on FSX is first deployed on the target node.<br><br><br><div data-tips="true" data-tips-type="warning">Note</div><br><br><br><div data-tips="true" data-tips-type="warning">If this parameter is set to <code>Immediate</code>, <code>scaleDownAfterNoDependency</code> cannot be set to <code>true</code>.</div><br> |
||spec.scaleDownAfterNoDependency<br><br> |No |Whether to automatically reclaim FSX client Pods when no workloads depend on FSX on the node.  <br><br><br>* `true`: Automatically reclaim FSX client Pods. This is suitable for scenarios where idle resource usage needs to be reduced.<br><br>* `false`: (Default value) Do not automatically reclaim FSX client Pods. In this mode, the first mount of the ECS instance is faster.<br><br><br><div data-tips="true" data-tips-type="warning">Note</div><br><br><br><div data-tips="true" data-tips-type="warning">If this parameter is set to <code>true</code>, <code>createMode</code> cannot be set to <code>Immediate</code>.</div><br> |
||spec.scaleDownAfterIdleDuration<br><br> |No |The idle wait duration before automatic reclamation of FSX client Pods. The value is a string that uses Go duration format. Supported units include s, m, and h. For example, `5m` means 5 minutes.<br><br>The default value is 3m if this parameter is not specified. |
||spec.upgradeStrategy.type |No |The upgrade policy of the FSX client.  <br><br><br>* `RollingUpdate`: Rolling upgrade.<br><br>* `OnLabel`: Canary or rotation upgrade.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">For the steps and considerations of the FSX client upgrade, see <a href="https://docs.byteplus.com/en/docs/vke/FSX_client_hot_upgrade">Upgrading FSX clients</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">In the system‑created default FSXSet resource (named default), the default value of this parameter is <code>OnLabel</code>. In user‑created FSXSet resources, the default value of this parameter is <code>RollingUpdate</code>.</div><br> |
||spec.upgradeStrategy.maxSurge |No |The number of additional Pods that can be temporarily created during a rolling upgrade. This parameter is required only if `spec.upgradeStrategy.type` is set to `RollingUpdate`.<br><br><br>* The value is an integer. Default value: 1.<br><br>* When the value is set to 0, the system does not create new Pods. Instead, it deletes the old Pods first. This does not consume extra resources, but each node may experience a brief interruption during the transition. |
||spec.upgradeStrategy.maxUnavailable |No |The maximum number of nodes that can be unavailable simultaneously during a rolling upgrade. For example, the value 1 indicates that only one node is upgraded each time. This parameter is required only if `spec.upgradeStrategy.type` is set to `RollingUpdate`.<br><br>The default value is 1 if this parameter is not specified. |
|Client configuration |template.parameterTemplate.image |Yes |The image address and version of the FSX client.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">In <code>RollingUpdate</code> mode, modifying the image version directly triggers an upgrade of the FSX client.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">You can obtain the supported image addresses and versions from the add\-on configuration page. For details, see <a href="https://docs.byteplus.com/en/docs/vke/csi-fsx-add-on">csi\-fsx</a>.</div><br> |
||template.parameterTemplate.resources |No |The resource quotas for the FSX client Pod. If this parameter is not specified, the global default configuration is used. |
||template.parameterTemplate.hostWorkDirectory |No |The working directory on the host for the FSX client. This is used for storing caches and temporary files and is mounted to `/tmp/fsx` in the container.<br><br><br>* In the system‑created default FSXSet resource (named default), the cacheDirectory configuration of the controller is inherited, which is `/tmp/fsx` by default.<br><br>* In user‑created FSXSet resources, if this parameter is not specified, this directory will not be mounted. |


&nbsp;

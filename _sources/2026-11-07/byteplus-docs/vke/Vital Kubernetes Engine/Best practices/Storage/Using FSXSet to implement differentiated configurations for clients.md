---
title: "Using FSXSet to implement differentiated configurations for clients"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using_FSXSet_to_implement_differentiated_configurations_for_clients"
---

As a Custom Resource Definition (CRD) provided by VKE, FSXSet is used to achieve fine\-grained scheduling and decoupled management of FSX clients. This topic describes how to use FSXSets to implement differentiated client configurations.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For more information about FSXSet resources, see <a href="https://docs.byteplus.com/en/docs/vke/Introduction_to_FSXSet_resources?lang=zh">FSXSet introduction</a>.</div>


<span id="ZsSLSyNY"></span>
## Scenario 1: Differentiated node management

<span id="3i9C81Yu"></span>
### Scenario introduction

In a VKE cluster, node pools typically consist of ECS instances of different specifications and purposes, for example, AI computing/GPU nodes with high\-concurrency read/write demands and general\-purpose computing nodes with lower read/write frequency. Because nodes of different specifications handle different workloads, their requirements for FSX client resource quotas, cleanup policies, and specific capabilities also vary. As a result, using a single unified FSX client configuration across all nodes in a cluster leads to the following issues:


* To meet resource requirements in high\-load scenarios, you may increase the FSX client's resources (CPU, memory, and more). However, this causes extra resource consumption on general nodes, crowding out scheduling capacity for workloads and resulting in wasted node resources.

* To conserve cluster\-wide resources, you may reduce FSX client resources (CPU, memory, and more). However, this causes performance bottlenecks on high\-concurrency nodes, introducing stability risks for workloads.


To address the above issues, VKE supports differentiated node management using a "node labels + FSXSet grouping" approach. This allows nodes to be divided into different groups based on node labels, with an independent FSXSet configured for each group, enabling differentiated configurations for different instance specifications. For example, you can assign dedicated labels to a specific node type (AI computing or GPU nodes) to add them to a corresponding group, then increase the FSX client resource quotas or key parameters in that group's FSXSet. Meanwhile, other nodes that are not configured with dedicated labels will automatically be assigned to the system default group and continue using their ‌resource\-efficient default configuration.

<span id="vVGkimFS"></span>
### Prerequisites


* The csi\-fsx add\-on has been installed and upgraded to v1.0.0 or later. For details, see [csi-fsx](https://docs.byteplus.com/en/docs/vke/csi-fsx-add-on).

* The fsxset\-controller add\-on has been installed. For details, see [fsxset-controller](https://docs.byteplus.com/en/docs/vke/fsxset-controller-add-on).

* (Optional) The target cluster has been connected through kubectl. For details, see [Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).


<span id="XB6dVs2y"></span>
### Procedure

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This document uses GPU nodes in a cluster as an example to demonstrate how FSXSet enables differentiated management of FSX clients across nodes.</div>


<span id="B1dQmcyT"></span>
#### Step 1: Create a dedicated configuration

After you install the fsxset\-controller add\-on in a cluster, the system will automatically create the FSXSet CRD and generate the default configuration. For details, see [FSXSet introduction](https://docs.byteplus.com/en/docs/vke/Introduction_to_FSXSet_resources). Therefore, you need to create a dedicated FSXSet configuration for GPU nodes with an elevated resource allocation.


<Tabs>
<Tab zoneid="ZSSMBV4TnR" title="Configure through the console">
<TabTitle>Configure through the console</TabTitle>

1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. Click the target cluster name to go to the management page of this cluster.

3. In the left navigation pane, select **Addons** and click the **Storage** tab.

4. In the lower\-right corner of the csi\-fsx add\-on card, click  **`...`**   **\> Client configuration**. Complete the dedicated client configuration for GPU nodes.  

   * **FSXSet label value**: Specify the value of the node label. In this example, the value is **gpu**, indicating a dedicated configuration for GPU nodes.

   * **Resource configuration**: Configure CPU and memory requests and limits for FSX client containers based on node performance requirements.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">For configuration details and parameter explanations, see <a href="https://docs.byteplus.com/en/docs/vke/csi-fsx-add-on">csi\-fsx</a>.      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The FSX client resource configuration in this example is for demonstration purposes only. In your actual scenarios, adjust settings based on node specifications and your business requirements.      </div>
      

5. Click **Confirm**.


</Tab>
<Tab zoneid="jZUO8zAIuo" title="Configure through kubectl">
<TabTitle>Configure through kubectl</TabTitle>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before you start, make sure that the following conditions are met:</div>



* <div data-tips="true" data-tips-type="tip">The kubectl tool has been installed on your on\-premises computer. For details, see <a href="https://kubernetes.io/docs/tasks/tools/">Installing and configuring kubectl</a>.</div>


* <div data-tips="true" data-tips-type="tip">The target cluster has been connected through kubectl. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster">Connecting to clusters</a>.</div>


1. Create a YAML file for the FSXSet. The following `fsxset-demo.yaml` file serves as an example:

   ```YAML
   apiVersion: csi.vke.volcengine.com/v1alpha1
   kind: FSXSet
   metadata:
     name: fsxset-gpu # The FSXSet resource name.
   spec:
     groupName: gpu # The logical group name, which corresponds to the node label fsx.csi.volcengine.com/group. The system selects nodes on which to apply this FSXSet configuration based on this name. This achieves differentiated client configuration.
     createMode: WaitForFirstConsumer
     template:
       parameterTemplate: # The FSX client configuration template.
         image: vke-cn-beijing.cr.volces.com/vke/fsx-agent:v1.3.4.268 # The image address and version of the FSX client.
         resources: # FSX client resource configuration. In this example, more resources are provided for the FSX clients on GPU nodes.
           requests:
             cpu: 2000m
             memory: 2Gi
           limits:
             cpu: 4000m
             memory: 4Gi
   ```
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Description   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For FSXSet parameter details, see <a href="https://docs.byteplus.com/en/docs/vke/Introduction_to_FSXSet_resources?lang=zh">FSXSet introduction</a>.   </div>
   

2. Run the following command to create the FSXSet.

   ```Bash
   kubectl apply -f fsxset-demo.yaml
   ```
   





</Tab>
</Tabs>


<span id="ngQJsjfD"></span>
#### Step 2: Add labels to nodes


<Tabs>
<Tab zoneid="BFrfOdL6jy" title="Add labels in batches via node pools">
<TabTitle>Add labels in batches via node pools</TabTitle>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Updates to node labels on a node pool apply only to new nodes added later. Labels on existing nodes remain unaffected. If necessary, manually add labels to the target existing nodes.</div>


* <div data-tips="true" data-tips-type="warning">Ensure that no FSX client pods exist on the target nodes where you want to add the label.</div>


1. In the left navigation bar of the cluster management page, click **Nodes \> Node pool**.

2. In the node pool list, find the target node pool and click **Edit** in the **Actions** column.

3. In the **Advanced settings** section, click **Add node labels**. In the pop\-up text box, add the following label key\-value pair:

   * **Key:**  The key is fixed as `fsx.csi.volcengine.com/group`.

   * **Value**: Enter the custom label value in the FSXSet configuration. In this example, the value is `gpu`.

4. Click **Confirm**.


</Tab>
<Tab zoneid="xzhg361Pq6" title="Manually add node labels">
<TabTitle>Manually add node labels</TabTitle>

1. In the left navigation bar of the cluster management page, click **Nodes \> Node**.

2. In the node list, find the target node and click **Actions** \> **Label management**.

3. Click **Add new**. In the pop\-up dialog box, add the following key\-value pairs:

   * **Key:**  The key is fixed as `fsx.csi.volcengine.com/group`.

   * **Value**: Enter the custom label value in the FSXSet configuration. In this example, the value is `gpu`.

4. Click **Confirm**.


</Tab>
</Tabs>


<span id="TMrsQjE5"></span>
### Validate results

After the configuration is complete, you can use FSX to mount PVs in the cluster and verify whether the FSX client configurations on different nodes meet your expectations.


1. Create a workload in the cluster and mount a PV by using FSX. For example, to mount a static TOS PV, see [Accessing static TOS PVs by using the FSX client](https://docs.byteplus.com/en/docs/vke/Using_static_TOS_Volumes_through_the_FSX_client).

2. Run the following command to view details about the FSXSet.

   ```Bash
   kubectl get fsxset fsxset-gpu
   ```
   

   The expected result is as follows: `DESIRED` and `READY` counts equal the number of target nodes, indicating that the FSX client has been created on the corresponding GPU nodes.

   ```Bash
   NAME         GROUP     DESIREDREVISION    DESIRED   CURRENT   READY   AVAILABLE   UPDATED   MATCHED   AGE
   default      default   3f2d716d885****    5         5         5       5           5         5         19m
   fsxset-gpu   gpu       8dec430c7ed****    2         2         2       2           2         2         17m
   ```
   

3. Run the following command to verify that the FSX client is running on the target nodes. Here, `fsxset-gpu` is the name of the FSXSet resource.

   ```Bash
   kubectl get pods -n kube-system -l addon.vke.volcengine.com/fsxset=fsxset-gpu -o wide
   ```
   

   The expected output is as follows:

   ```Bash
   NAME                         READY   STATUS    RESTARTS   AGE     IP              NODE            NOMINATED NODE   READINESS GATES
   fsx-agent-fsxset-gpu-2m***   1/1     Running   0          8m25s   192.168.1.39    192.168.1.39    <none>           <none>
   fsx-agent-fsxset-gpu-kg***   1/1     Running   0          8m25s   192.168.2.242   192.168.2.242   <none>           <none>
   ```
   


<span id="z2qpz7n3"></span>
## Scene 2: POC environment isolation

<span id="X8Byvccw"></span>
### Scenario introduction

After a cluster operates stably, the O&M team still needs to continuously validate and update new FSX client versions (for example, for new features or bug fixes) and observe mount/unmount operations and read/write performance under real business loads. In practice, this requires balancing version stability and feature evolution. On one hand, production environments prioritize storage mount stability to avoid compatibility, performance, or availability risks from client version changes. On the other hand, applications require prompt validation of functional enhancements, bug fixes, or performance optimizations in new versions to avoid stagnation in legacy versions and consequently hinder evolution.

To resolve this conflict between stable operation and new feature validation, VKE implements ‌physical environment isolation within the same cluster via the "node labels + FSXSet grouping" approach. In this approach, a small subset of nodes is designated as the POC environment, running only the new FSX client version. All other production nodes continue running the stable version. Both environments operate in parallel but remain isolated. After mount/unmount operations and read/write performance are validated under business loads in the POC environment, the POC scope can be gradually expanded, or a phased upgrade can be initiated. If the POC results do not meet expectations, simply reassigning the POC nodes back to their original group rolls back to the previous version, without affecting the production environment.

<span id="ZrjvcLfR"></span>
### Prerequisites


* The csi\-fsx add\-on has been installed and upgraded to v1.0.0 or later. For details, see [csi-fsx](https://docs.byteplus.com/en/docs/vke/csi-fsx-add-on).

* The fsxset\-controller add\-on has been installed. For details, see [fsxset-controller](https://docs.byteplus.com/en/docs/vke/fsxset-controller-add-on).

* (Optional) The target cluster has been connected through kubectl. For details, see [Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).


<span id="JdsEC4S9"></span>
### Procedure

<span id="1S5aoHb4"></span>
#### Step 1: Create a dedicated configuration

After you install the fsxset\-controller add\-on in a cluster, the system will automatically create the FSXSet CRD and generate the default configuration. For details, see [FSXSet introduction](https://docs.byteplus.com/en/docs/vke/Introduction_to_FSXSet_resources). Therefore, you need to create a dedicated FSXSet configuration for POC nodes, specifying the target version to validate.


<Tabs>
<Tab zoneid="K7ULYqxo" title="Configure through the console">
<TabTitle>Configure through the console</TabTitle>

1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. Click the target cluster name to go to the management page of this cluster.

3. In the left navigation pane, select **Addons** and click the **Storage** tab.

4. In the lower\-right corner of the csi\-fsx add\-on card, click  **`...`**   **\> Client configuration**. For the Client image setting, select the version that requires POC validation.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">For configuration details and parameter explanations, see <a href="https://docs.byteplus.com/en/docs/vke/csi-fsx-add-on">csi\-fsx</a>.      </div>
      

5. Click **Confirm**.


</Tab>
<Tab zoneid="FTWEuqDe" title="Configure through kubectl">
<TabTitle>Configure through kubectl</TabTitle>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before you start, make sure that the following conditions are met:</div>



* <div data-tips="true" data-tips-type="tip">The kubectl tool has been installed on your on\-premises computer. For details, see <a href="https://kubernetes.io/docs/tasks/tools/">Installing and configuring kubectl</a>.</div>


* <div data-tips="true" data-tips-type="tip">The target cluster has been connected through kubectl. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster">Connecting to clusters</a>.</div>


1. Create a YAML file for the FSXSet. The following `fsxset-demo.yaml` file serves as an example:

   ```YAML
   apiVersion: csi.vke.volcengine.com/v1alpha1
   kind: FSXSet
   metadata:
     name: fsxset-poc # The FSXSet resource name.
   spec:
     groupName: poc # The logical group name, which corresponds to the node label fsx.csi.volcengine.com/group. The system selects nodes on which to apply this FSXSet configuration based on this name. This achieves differentiated client configuration.
     createMode: WaitForFirstConsumer
     template:
       parameterTemplate: # The FSX client configuration template.
         image: vke-cn-beijing.cr.volces.com/vke/fsx-agent:v0.12.4 # The new image version for use in the POC environment.
   ```
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Description   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For FSXSet parameter details, see <a href="https://docs.byteplus.com/en/docs/vke/Introduction_to_FSXSet_resources?lang=zh">FSXSet introduction</a>.   </div>
   

2. Run the following command to create the FSXSet.

   ```Bash
   kubectl apply -f fsxset-demo.yaml
   ```
   





</Tab>
</Tabs>


<span id="QxNCeYmI"></span>
#### Step 2: Add labels to nodes


<Tabs>
<Tab zoneid="LeP7ZUEX" title="Add labels in batches via node pools">
<TabTitle>Add labels in batches via node pools</TabTitle>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Updates to ECS instance labels on a node pool apply only to new nodes added later. Labels on existing nodes remain unaffected. If necessary, manually add labels to the target existing nodes.</div>


* <div data-tips="true" data-tips-type="warning">Make sure that no FSX client Pods exist on the node to be labeled.</div>


1. In the left navigation bar of the cluster management page, click **Nodes \> Node pool**.

2. In the node pool list, find the target node pool and click **Edit** in the **Actions** column.

3. In the **Advanced settings** section, click **Add node labels**. In the pop\-up text box, add the following label key\-value pair:

   * **Key:**  The key is fixed as `fsx.csi.volcengine.com/group`.

   * **Value**: Enter the custom label value in the FSXSet configuration. In this example, the value is `gpu`.

4. Click **Confirm**.


</Tab>
<Tab zoneid="tCsPr2kR" title="Manually add node labels">
<TabTitle>Manually add node labels</TabTitle>

1. In the left navigation bar of the cluster management page, click **Nodes \> Node**.

2. In the node list, find the target node and click **Actions** \> **Label management**.

3. Click **Add new**. In the pop\-up dialog box, add the following key\-value pairs:

   * **Key:**  The key is fixed as `fsx.csi.volcengine.com/group`.

   * **Value**: Enter the custom label value in the FSXSet configuration. In this example, the value is `gpu`.

4. Click **Confirm**.


</Tab>
</Tabs>


<span id="yvPBYRXI"></span>
### Validate results

After the configuration is complete, you can use FSX to mount PVs in the cluster and verify whether the FSX client configurations on different nodes meet your expectations.


1. Create a workload in the cluster and mount a PV by using FSX. For example, to mount a static TOS PV, see [Accessing static TOS PVs by using the FSX client](https://docs.byteplus.com/en/docs/vke/Using_static_TOS_Volumes_through_the_FSX_client).

2. Run the following command to view details about the FSXSet.

   ```Bash
   kubectl get fsxset fsxset-poc
   ```
   

   The expected result is as follows: `DESIRED` and `READY` counts equal the number of target nodes, indicating that the FSX client has been created on the corresponding POC nodes.

   ```Bash
   NAME         GROUP     DESIREDREVISION    DESIRED   CURRENT   READY   AVAILABLE   UPDATED   MATCHED   AGE
   default      default   3f2d716d885****    5         5         5       5           5         5         19m
   fsxset-poc   poc       8dec430c7ed****    2         2         2       2           2         2         17m
   ```
   

3. Run the following command to verify that the FSX client is running on the target nodes. Here, `fsxset-gpu` is the name of the FSXSet resource.

   ```Bash
   kubectl get pods -n kube-system -l addon.vke.volcengine.com/fsxset=fsxset-poc -o wide
   ```
   

   The expected output is as follows:

   ```Bash
   NAME                         READY   STATUS    RESTARTS   AGE     IP              NODE            NOMINATED NODE   READINESS GATES
   fsx-agent-fsxset-poc-2m***   1/1     Running   0          8m25s   192.168.1.39    192.168.1.39    <none>           <none>
   fsx-agent-fsxset-poc-kg***   1/1     Running   0          8m25s   192.168.2.242   192.168.2.242   <none>           <none>
   ```
   


<span id="RLefygcg"></span>
### Subsequent configurations

<span id="LUK7YJLp"></span>
#### POC application validation

After you complete the configuration, we recommend running real business workloads on POC nodes to observe the performance of the new FSX client under actual conditions. During validation, pay special attention to the following:


* Whether mounting/unmounting operates normally with the expected duration.

* Whether business read/write paths are stable or show significant latency spikes, throughput drops, or error rate increases.

* Whether client logs, monitoring metrics, and business\-side alerts show any anomalies.

* Whether there are behavioral differences or compatibility issues compared to the stable version running in the production environment.


If conditions allow, we recommend covering key scenarios such as typical peak traffic, batch mounts, and failure recovery in the POC environment to improve the reliability of the validation conclusions.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can enable cloud\-native observability and CSI storage observability in the cluster to confirm whether the relevant metrics are normal. For details, see <a href="https://docs.byteplus.com/en/docs/vke/CSI-storage-observability">CSI storage observability</a>.</div>


<span id="ThNokE7w"></span>
####  **‌Post\-POC upgrade**

If the POC validation results meet expectations, we recommend mapping the production POC environments to two FSXSet groups with relatively fixed scopes, respectively, and maintaining the version configurations of both groups.

In this model, the production environment group serves stable online applications and uses the validated stable client version by default. The POC group is used for version validation and uses the to\-be\-validated version by default. After validation is complete, you can update the FSXSet version for the production environment group to the validated version, thereby completing the online upgrade. During the upgrade, we recommend continuously monitoring the FSXSet status, client Pod status, and application\-side mount, read/write, and monitoring metrics to verify that the production environment is running stably.

<span id="pyssVePR"></span>
#### POC failure rollback

If the POC validation fails, we recommend reverting the FSXSet version for the POC group to the original stable version, rather than continuing to expand POC node scope to force an upgrade. This approach keeps a stable boundary between the production and POC environments, simplifies rollback when version validation fails, and minimizes business impact.

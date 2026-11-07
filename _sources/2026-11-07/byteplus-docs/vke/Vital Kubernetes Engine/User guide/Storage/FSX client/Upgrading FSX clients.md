---
title: "Upgrading FSX clients"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/FSX_client_hot_upgrade"
---

The FSX client (fsx\-agent) supports image version upgrades through FSXSet. Multiple upgrade solutions, including rolling upgrade, canary upgrade, and rotation upgrade, are supported. This topic describes the trigger methods, applicable scenarios, and selection recommendations for each upgrade solution. This helps users select an appropriate upgrade strategy based on business continuity requirements.

<span id="NvvuQalJ"></span>
## Upgrade solutions

As FSX features continue to evolve, you need to upgrade the FSX client to obtain new capabilities, fix known issues, and improve operational stability. By upgrading the FSX client, you can enable the node‑side client to acquire new mounting capabilities, compatibility optimizations, and bug fixes without affecting business applications.

VKE clusters manage FSX clients across the entire lifecycle, such as creation, deletion, and upgrade, through FSXSet custom resources. We recommend selecting an appropriate client upgrade strategy based on your business requirements, release notes, and cluster status. The following table describes currently supported upgrade strategies.


|**Upgrade solution** |**Upgrade behavior** |**Application scenario** |**Features** |
|---|---|---|---|
|Rolling upgrade |After you modify the `image` field of FSXSet, FSXSet performs a rolling upgrade on all nodes in the target cluster. |The FSX client versions in the cluster need to be unified within a short period. |* High upgrade efficiency.<br><br>* Supports controlling concurrency via `maxUnavailable` and `maxSurge`. |
|Canary upgrade |* New nodes use the new image version.<br><br>* Proactive replacement will not be performed on existing nodes. You can add the `fsx.vke.volcengine.com/upgrade=true` label to nodes to trigger an upgrade. |The new version needs to be verified on a small number of nodes first. After confirming the version stability, you can expand the upgrade scope. |* Upgrade scope is controllable. It supports phased releases.<br><br>* Applicable to business scenarios that are sensitive to version changes. |
|Rotation upgrade (OnLabel) |* New nodes use the new image version.<br><br>* Proactive replacement will not be performed on existing nodes. When `scaleDownAfterNoDependency` is set to `true`, the system will automatically reclaim and rotate FSX clients:<br><br>   * When no workloads on a node depend on FSX, the system will automatically remove the old\-version client from that node.<br><br>   * When the node has scheduled workloads that require FSX again, the system will recreate the client using the latest image, thereby progressively completing the version transition. |The original version is stable, the cluster is large in scale, or you want to minimize impacts on workloads when FSX clients are proactively replaced. |* Smooth upgrade.<br><br>* The overall completion time depends on the rotation cycle. |


<span id="erQGXwof"></span>
## Considerations


* A hot upgrade of the FSX client may cause brief service disruption. We recommend performing the upgrade during off\-peak business hours to minimize the impact.

* During a rolling upgrade, the system will create a new FSX client pod on the node. This results in the coexistence of both new and old Pods for a short period, doubling the cluster resource consumption. To prevent upgrade failure due to insufficient resources, make sure that each node in the cluster has sufficient resources for the upgrade.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">During the upgrade, a headroom Pod is created to pre‑occupy resources. If resources are insufficient, the upgrade will not be triggered and will not affect existing workloads.   </div>
   

<span id="27qovjIA"></span>
## Preparations


1. In the left navigation bar of the cluster management page, go to **Cluster management \> Addons**.

2. Click the **Storage** tab and find the csi\-fsx add\-on. Move the pointer over the add\-on card. In the lower\-right corner of the card, click  **`...`**   **\> Client configuration** to view the resource configurations of the add\-on.

   The amount of idle resources on the node must be greater than the configured value. For example, in this case, the CPU request of fsx\-agent\-pod is 2 cores and the memory request is 2 GiB, so the idle resources on the node must be greater than 2 CPU cores and 2 GiB of memory.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d069946c0ecbc94ce995f35e101b3446.png) </span>

3. In the left navigation bar of the cluster management page, click **Workload** \> **Pod**.

   * Select **kube\-system** from the **Namespace** drop\-down list.

   * In the search box, enter the pod name keyword `fsx-agent` to perform a fuzzy search and find the FSX client pod.

   * Click the IP address in the **Node** column of the target Pod to display the node overview. Then, click **Click to view node details** to go to the node details page.

4. Check the current resource usage of the node and ensure the following requirements are met:

   * Check the currently available CPU and memory, which must be greater than the **CPU request** and **Memory request** configured for csi\-fsx.

   * Check the number of allocatable pods, which must be greater than 1.

5. If all of the above resources meet the corresponding requirements, you can perform the upgrade steps below. If the requirements are not met, [submit a ticket](https://console.byteplus.com/ticket/createTicketV2/?step=2&Service=vke) or contact your account manager to obtain further technical support.


<span id="ueuarc8v"></span>
## Procedure

<span id="c5wf6DHF"></span>
### Rolling upgrade


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. On the right page, click the target cluster name to open the management page of this cluster.

3. In the left navigation bar, click **Workload \> Resource Explorer**. In the resource list, click the name of the **fsxset** resource to go to the resource details page.

4. In the resource list, find the resource to upgrade and click **Edit Yaml** in the **Actions** column.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_93af3c0dfdc09ca1726741192291a897.png) </span>

5. In the YAML configuration, modify the `parameterTemplate.image` field under `spec.template` to the target image version to trigger the rolling upgrade of the FSX client.

   ```YAML
   apiVersion: csi.vke.volcengine.com/v1alpha1
   kind: FSXSet
   metadata:
     name: default
   spec:
     groupName: default
     createMode: WaitForFirstConsumer
     scaleDownAfterNoDependency: true
     mountPrefix: /mnt/fsx
     podHostName: fsx-agent
     upgradeStrategy:
       type: RollingUpdate # Upgrade strategy. In this example, the value is RollingUpdate, indicating a rolling upgrade.
       maxSurge: 0 # The number of additional Pods that can be created during an upgrade. The value 0 indicates that no additional Pods are created.
       maxUnavailable: 1 # The maximum number of nodes that can be unavailable simultaneously during a rolling upgrade. For example, the value 1 indicates that only one node is upgraded each time.
     template:
       parameterTemplate:
         image: vke-***.cr.volces.com/vke/fsx-agent:v0.12.3 # Change the value to the target image version to trigger a rolling upgrade.
         resources:
           requests:
             cpu: 100m
             memory: 128Mi
           limits:
             cpu: 2000m
             memory: 2Gi
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For more information about FSXSet parameters, see <a href="https://docs.byteplus.com/en/docs/vke/Introduction_to_FSXSet_resources">Introduction to FSXSet resources</a>.   </div>
   

6. Click **Confirm** to save the configurations. The system will start the rolling upgrade of all FSX clients in the cluster.


<span id="rNp6K2rf"></span>
### Canary/Rotation upgrade (OnLabel)


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. On the right page, click the target cluster name to open the management page of this cluster.

3. In the left navigation bar, click **Workload \> Resource Explorer**. In the resource list, click the name of the **fsxset** resource to go to the resource details page.

4. In the resource list, find the resource to upgrade and click **Edit Yaml** in the **Actions** column.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_93af3c0dfdc09ca1726741192291a897.png) </span>

5. In the YAML configuration, modify the `type` field under `spec.upgradeStrategy` to `OnLabel`, and modify the `parameterTemplate.image` field under `spec.template` to the target image version.

   ```YAML
   apiVersion: csi.vke.volcengine.com/v1alpha1
   kind: FSXSet
   metadata:
     name: default
   spec:
     groupName: default
     createMode: WaitForFirstConsumer
     scaleDownAfterNoDependency: true # For a rotation upgrade, set this parameter to true.
     mountPrefix: /mnt/fsx
     podHostName: fsx-agent
     upgradeStrategy:
       type: OnLabel # Upgrade strategy. In this example, the value is OnLabel, indicating a canary or rotation upgrade.
       maxSurge: 0
       maxUnavailable: 1
     template:
       parameterTemplate:
         image: vke-***.cr.volces.com/vke/fsx-agent:v0.12.3 # Change the value to the target image version.
         resources:
           requests:
             cpu: 100m
             memory: 128Mi
           limits:
             cpu: 2000m
             memory: 2Gi
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For more information about FSXSet parameters, see <a href="https://docs.byteplus.com/en/docs/vke/Introduction_to_FSXSet_resources">Introduction to FSXSet resources</a>.   </div>
   

6. Click **Confirm** to save the configurations.

7. After the configuration is complete, the FSX client upgrade strategy in the cluster is as follows:

   * Rotation upgrade: For newly created or rotated nodes in the cluster, the system will create new\-version FSX clients based on the `image` field in the FSXSet configuration.

   * Canary upgrade: For existing nodes, allow execution of the following command, which adds the upgrade label to target FSX clients to trigger a canary upgrade. `${agent-pod-name}` is the name of the FSX client Pod to be upgraded.

      ```Bash
      kubectl label pod -n kube-system ${agent-pod-name} fsx.vke.volcengine.com/upgrade=true
      ```
      


<span id="AKbAglHn"></span>
## Validate results

The FSX client is named `fsx-agent-***` and located in the kube\-system namespace. You can use the following command to continuously monitor the upgrade progress of the pod. During an upgrade of the FSX client, the system creates another FSX client pod and destroys the original pod.

```Bash
kubectl get pod -A --show-labels | grep fsx-agent
```


The expected result is as follows: When the FSX client is upgraded, the cluster contains both a new FSX client and a terminated old FSX client.

```Bash
kube-system        fsx-agent-default-5z***                               0/1     Running       0                25s     addon.vke.volcengine.com/fsxset-revision=ed48241c4***,addon.vke.volcengine.com/fsxset=default,app.kubernetes.io/instance=fsx-agent,app.kubernetes.io/managed-by=fsxset,app.kubernetes.io/name=agent,app.kubernetes.io/node=192.168.245.142,app.kubernetes.io/version=v0.12.2,app=agent,container-image.agent.fsx/tag=v0.12.2
kube-system        fsx-agent-default-js***                               1/1     Terminating   0                2m40s   addon.vke.volcengine.com/fsxset-revision=2b856293a***,addon.vke.volcengine.com/fsxset=default,app.kubernetes.io/instance=fsx-agent,app.kubernetes.io/managed-by=fsxset,app.kubernetes.io/name=agent,app.kubernetes.io/node=192.168.245.142,app.kubernetes.io/version=v0.12.1,app=agent,container-image.agent.fsx/tag=v0.12.1
```


After the upgrade is complete, run the following command to view FSXSet details.

```Bash
kubectl get fsxset -o wide
```


The expected result is as follows: When the value of `UPDATED` equals the value of `DESIRED`, it indicates that all FSX clients are upgraded.

```Bash
NAME      GROUP     DESIRED   CURRENT   READY   AVAILABLE   UPDATED   MATCHED   MISSCHEDULED   AGE
default   default   1         1         1       1           1         2                        23h
```

---
title: "Using FSXSet to implement smooth client upgrades"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using_FSXSet_to_implement_smooth_client_upgrades"
---

As a Custom Resource Definition (CRD) provided by VKE, FSXSet is used to achieve fine\-grained scheduling and decoupled management of FSX clients. This topic describes how to use FSXSets to implement smooth client upgrades.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For more information about FSXSet resources, see <a href="https://docs.byteplus.com/en/docs/vke/Introduction_to_FSXSet_resources?lang=zh">FSXSet introduction</a>.</div>


<span id="oJgursej"></span>
## Scenario introduction

In VKE clusters, FSX clients handle mounting and unmounting requests for FSX volumes. Production environments typically run business applications on stable old FSX client versions. Meanwhile, as FSX capabilities evolve, client upgrades become necessary to access new features, fix known issues, and enhance operational stability. FSX clients support multiple upgrade strategies, including ‌rolling upgrades (RollingUpdate), ‌canary upgrades (OnLabel), and rotation upgrades. For details, see [FSX client upgrades](https://docs.byteplus.com/en/docs/vke/FSX_client_hot_upgrade?lang=zh).

When the RollingUpdate strategy is used, the controller actively replaces the FSX client on each existing node one by one. During replacement, both old and new clients temporarily coexist on the same node, requiring double resources to be reserved. For large\-scale clusters that require high stability and gradual adoption of new features, we recommend against replacing FSX clients on all existing nodes simultaneously.

In this case, we recommend using the canary upgrade (OnLabel) or rotation upgrade strategy in combination with the node pool scaling cadence and the `scaleDownAfterNoDependency` configuration. This approach allows the old version to be phased out gradually over time: existing workloads continue using the old client version for stability, while new workloads gradually transition to the new version. Eventually, the upgrade completes smoothly as the old and new versions naturally converge.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This approach suits production clusters that are ‌version\-sensitive‌, ‌cannot tolerate large\-scale active replacements‌, but have ‌relatively flexible upgrade windows‌. If the upgrade aims to fix urgent CVEs or critical defects that require rapid cluster\-wide convergence, use the ‌RollingUpdate‌ strategy instead. For details, see <a href="https://docs.byteplus.com/en/docs/vke/FSX_client_hot_upgrade?lang=zh">Upgrading FSX clients</a>.</div>


<span id="ZVFt9nPZ"></span>
## Prerequisites


* The csi\-fsx add\-on has been installed and upgraded to v1.0.0 or later. For details, see [csi-fsx](https://docs.byteplus.com/en/docs/vke/csi-fsx-add-on).

* The fsxset\-controller add\-on has been installed. For details, see [fsxset-controller](https://docs.byteplus.com/en/docs/vke/fsxset-controller-add-on).

* You have created an FSXSet resource and node pool and completed grouping based on `fsx.csi.volcengine.com/group` to ensure the FSXSet can correctly match the target nodes. For details, see [Using FSXSets to implement differentiated client configurations](https://docs.byteplus.com/en/docs/vke/Using_FSXSet_to_implement_differentiated_configurations_for_clients).

* You have deployed your business application and have created the FSX client. For example, [use dynamic EFS volumes via an FSX client](https://docs.byteplus.com/en/docs/6460/2535749).

* You have enabled cloud\-native observability and CSI storage observability. For details, see [Enabling observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability) and [CSI storage observability](https://docs.byteplus.com/en/docs/vke/CSI-storage-observability).

* (Optional) The target cluster has been connected through kubectl. For details, see [Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).


<span id="nV0kzVVz"></span>
## Procedure

<span id="LPCgqKV8"></span>
### Step 1: Update the configuration


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. On the right page, click the target cluster name to open the management page of this cluster.

3. In the left navigation bar, click **Workload \> Resource Explorer**. In the resource list, click the name of the **fsxset** resource to go to the resource details page.

4. In the resource list, select the resource to upgrade and click **Edit Yaml** in the **Actions** column to update the FSXSet configuration. Key parameters and examples are as follows:

   * Set `spec.template.parameterTemplate.image` to a new version. You can obtain the version number from the add\-on console. For details, see [csi-fsx](https://docs.byteplus.com/en/docs/vke/csi-fsx-add-on?lang=zh).

   * Set `spec.upgradeStrategy.type` to `OnLabel` (canary upgrade) to avoid actively replacing FSX clients on the existing nodes.

   * Set `scaleDownAfterNoDependency` to `true`. When no applications on a node depend on FSX, the system will automatically reclaim FSX client pods to improve rotation efficiency.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">This topic uses modifications to a custom FSXSet configuration as an example.   </div>
   

   ```YAML
   apiVersion: csi.vke.volcengine.com/v1alpha1
   kind: FSXSet
   metadata:
     name: doc-demo
   spec:
     groupName: doc # The logical group name, which corresponds to the node label fsx.csi.volcengine.com/group. The system selects nodes on which to apply this FSXSet configuration based on this name. This achieves differentiated client configuration.
     createMode: WaitForFirstConsumer # FSX client creation mode. In this example, it is WaitForFirstConsumer, meaning the FSX client is created on a node only when the first dependent workload is deployed to the node.
     scaleDownAfterNoDependency: true # Whether to automatically reclaim the FSX client Pod when the node has no FSX-dependent workloads. Recommended: true (enables automatic reclaim for improved rotation efficiency).
     upgradeStrategy:
       type: OnLabel # FSX client upgrade strategy. In this example, set it to OnLabel (indicates a canary upgrade).
       maxSurge: 0
       maxUnavailable: 1
     template:
       parameterTemplate:
         image: vke-cn-beijing.cr.volces.com/vke/fsx-agent:v1.3.4.286 # Change the value to the target image version.
         resources:
           requests:
             cpu: 100m
             memory: 128Mi
           limits:
             cpu: 2000m
             memory: 2Gi
   ```
   

5. Click **Confirm** to save the configurations.


<span id="y7tcnG9W"></span>
### Step 2: Upgrade clients


1. Run the following command to view the status of existing FSX clients in the cluster. Here, `doc-demo` is the name of the FSXSet resource.

   ```Bash
   kubectl get pod -n kube-system -l addon.vke.volcengine.com/fsxset=doc-demo --show-labels
   # Check the proportions of pods with the label app.kubernetes.io/version=<old-version> and pods with the label value set to <new-version>.
   # During a smooth upgrade, the old-version count should decrease monotonically, while the new-version count should increase as the count of nodes using the new version increases.
   ```
   

   The expected output is as follows: In OnLabel mode, the system will not automatically upgrade existing clients. The existing clients remain in the `Running` status and are not rebuilt.

   ```Bash
   NAME                       READY   STATUS    RESTARTS   AGE     LABELS
   fsx-agent-doc-demo-d5***   1/1     Running   0          2m33s   addon.vke.volcengine.com/fsxset-revision=b5e31ff826***,addon.vke.volcengine.com/fsxset=doc-demo,app.kubernetes.io/instance=fsx-agent,app.kubernetes.io/managed-by=fsxset,app.kubernetes.io/name=agent,app.kubernetes.io/node=192.168.2.246,app.kubernetes.io/version=v0.10.2,container-image.agent.fsx/tag=v0.10.2
   fsx-agent-doc-demo-pz***   1/1     Running   0          6m18s   addon.vke.volcengine.com/fsxset-revision=b5e31ff826***,addon.vke.volcengine.com/fsxset=doc-demo,app.kubernetes.io/instance=fsx-agent,app.kubernetes.io/managed-by=fsxset,app.kubernetes.io/name=agent,app.kubernetes.io/node=192.168.1.45,app.kubernetes.io/version=v0.10.2,container-image.agent.fsx/tag=v0.10.2
   fsx-agent-doc-demo-zn***   1/1     Running   0          4m15s   addon.vke.volcengine.com/fsxset-revision=b5e31ff826***,addon.vke.volcengine.com/fsxset=doc-demo,app.kubernetes.io/instance=fsx-agent,app.kubernetes.io/managed-by=fsxset,app.kubernetes.io/name=agent,app.kubernetes.io/node=192.168.2.253,app.kubernetes.io/version=v0.10.2,container-image.agent.fsx/tag=v0.10.2
   ```
   

2. Update existing FSX clients. In OnLabel mode, you can use the following methods to update existing clients.

   
   <Tabs>
   <Tab zoneid="raTwGiwtJu" title="Rotation update">
   <TabTitle>Rotation update</TabTitle>
   
   When new nodes are added to the target node pool or existing node pools undergo rotation, and new business Pods are scheduled to those nodes, the system creates new\-version FSX clients based on the `image` field in the FSXSet configuration. For example, if one new node is added to the node pool and your application is deployed to that node:
   
   
      * The newly created FSX client `fsx-agent-doc-demo-cj***` uses the latest version `v1.3.4.286`, verified via the `container-image.agent.fsx/tag` label.
   
      * Existing FSX clients retain the old version `v0.10.2`, verified via their `container-image.agent.fsx/tag` labels.
   
      ```Bash
      NAME                       READY   STATUS    RESTARTS   AGE     LABELS
      fsx-agent-doc-demo-cj***   1/1     Running   0          76s     addon.vke.volcengine.com/fsxset-revision=6c356***,addon.vke.volcengine.com/fsxset=doc-demo,app.kubernetes.io/instance=fsx-agent,app.kubernetes.io/managed-by=fsxset,app.kubernetes.io/name=agent,app.kubernetes.io/node=192.168.1.58,app.kubernetes.io/version=v1.3.4.286,container-image.agent.fsx/tag=v1.3.4.286
      fsx-agent-doc-demo-d5***   1/1     Running   0          3m43s   addon.vke.volcengine.com/fsxset-revision=b5e31***,addon.vke.volcengine.com/fsxset=doc-demo,app.kubernetes.io/instance=fsx-agent,app.kubernetes.io/managed-by=fsxset,app.kubernetes.io/name=agent,app.kubernetes.io/node=192.168.2.246,app.kubernetes.io/version=v0.10.2,container-image.agent.fsx/tag=v0.10.2
      fsx-agent-doc-demo-pz***   1/1     Running   0          7m28s   addon.vke.volcengine.com/fsxset-revision=b5e31***,addon.vke.volcengine.com/fsxset=doc-demo,app.kubernetes.io/instance=fsx-agent,app.kubernetes.io/managed-by=fsxset,app.kubernetes.io/name=agent,app.kubernetes.io/node=192.168.1.45,app.kubernetes.io/version=v0.10.2,container-image.agent.fsx/tag=v0.10.2
      fsx-agent-doc-demo-zg***   1/1     Running   0          5m25s   addon.vke.volcengine.com/fsxset-revision=b5e31***,addon.vke.volcengine.com/fsxset=doc-demo,app.kubernetes.io/instance=fsx-agent,app.kubernetes.io/managed-by=fsxset,app.kubernetes.io/name=agent,app.kubernetes.io/node=192.168.2.253,app.kubernetes.io/version=v0.10.2,container-image.agent.fsx/tag=v0.10.2
      ```
      
   
   
   
   
   
   </Tab>
   <Tab zoneid="A92QObjRDo" title="Manual update">
   <TabTitle>Manual update</TabTitle>
   
   1. Run the following command to add the upgrade label to the FSX clients to be upgraded, triggering the upgrade. `${agent-pod-name}` is the name of the FSX client Pod to be upgraded.
   
      ```Bash
      kubectl label pod -n kube-system ${agent-pod-name} fsx.vke.volcengine.com/upgrade=true
      ```
      
   
   2. Run the following command to view the status of existing FSX clients in the cluster. Here, `doc-demo` is the name of the FSXSet resource.
   
      ```Bash
      kubectl get pod -n kube-system -l addon.vke.volcengine.com/fsxset=doc-demo --show-labels
      ```
      
   
      The expected result is as follows: The clients on the specified nodes have been rebuilt and have completed the update.
   
      ```Bash
      NAME                       READY   STATUS    RESTARTS   AGE     LABELS
      fsx-agent-doc-demo-mg***   1/1     Running   0          2m33s   addon.vke.volcengine.com/fsxset-revision=b5e31ff826***,addon.vke.volcengine.com/fsxset=doc-demo,app.kubernetes.io/instance=fsx-agent,app.kubernetes.io/managed-by=fsxset,app.kubernetes.io/name=agent,app.kubernetes.io/node=192.168.2.246,app.kubernetes.io/version=v1.3.4.286,container-image.agent.fsx/tag=v1.3.4.286
      fsx-agent-doc-demo-pz***   1/1     Running   0          6m18s   addon.vke.volcengine.com/fsxset-revision=b5e31ff826***,addon.vke.volcengine.com/fsxset=doc-demo,app.kubernetes.io/instance=fsx-agent,app.kubernetes.io/managed-by=fsxset,app.kubernetes.io/name=agent,app.kubernetes.io/node=192.168.1.45,app.kubernetes.io/version=v0.10.2,container-image.agent.fsx/tag=v0.10.2
      fsx-agent-doc-demo-zn***   1/1     Running   0          4m15s   addon.vke.volcengine.com/fsxset-revision=b5e31ff826***,addon.vke.volcengine.com/fsxset=doc-demo,app.kubernetes.io/instance=fsx-agent,app.kubernetes.io/managed-by=fsxset,app.kubernetes.io/name=agent,app.kubernetes.io/node=192.168.2.253,app.kubernetes.io/version=v0.10.2,container-image.agent.fsx/tag=v0.10.2
      ```
      
   
   
   
   
   
   </Tab>
   </Tabs>
   


<span id="DLwTHXcS"></span>
## Verifying the upgrade result


1. Run the following command to check whether all FSX clients in the cluster have been switched to the new version.

   ```Bash
   kubectl get fsxset -o wide
   ```
   

   The expected result is as follows: If `MATCHED` and `UPDATED` counts are equal and only the new client version remains, all FSX clients in the cluster have been upgraded to the new version.

   ```Bash
   NAME         GROUP     DESIREDREVISION    DESIRED   CURRENT   READY   AVAILABLE   UPDATED   MATCHED   AGE
   default      default   3f2d716d885****                                                                78m
   doc-demo     doc       8dec430c7ed****    4         4         4       4           4         4         39m
   ```
   

2. Run the following command to view FSX clients that have been upgraded to the specified version, where `v1.3.4.286` is the version number to query.

   ```Bash
   kubectl get pod -n kube-system -l app.kubernetes.io/instance=fsx-agent,container-image.agent.fsx/tag=v1.3.4.286 -o wide
   ```
   

   The expected output is as follows:

   ```Bash
   NAME                       READY   STATUS    RESTARTS   AGE   IP              NODE           NOMINATED NODE   READINESS GATES
   fsx-agent-doc-demo-cj***   1/1     Running   0          39s   192.168.1.58    192.168.1.58   <none>           <none>
   fsx-agent-doc-demo-d5***   1/1     Running   0          39s   192.168.2.246   192.168.2.246  <none>           <none>
   fsx-agent-doc-demo-pz***   1/1     Running   0          39s   192.168.1.45    192.168.1.45   <none>           <none>
   fsx-agent-doc-demo-zg***   1/1     Running   0          39s   192.168.2.253   192.168.2.253  <none>           <none>
   ```
   

3. Run the following command to check Pod mount events for anomalies. Here, `${pod-name}` is the Pod name.

   ```Bash
   kubectl describe pod ${pod-name}
   ```
   

   The expected output is as follows:

   ```Bash
   Name:             efs-deployment-demo-5459***
   Namespace:        default
   Priority:         0
   Service Account:  default
   Node:             192.168.1.58/192.168.1.58
   Start Time:       Fri, 17 Jul 2026 15:52:50 +0800
   Labels:           app=efs-deployment-demo
                     pod-template-hash=5459***
   Annotations:      <none>
   Status:           Running
   IP:               192.168.1.64
   IPs:
     IP:           192.168.1.64
   Controlled By:  ReplicaSet/efs-deployment-demo-4-5459***
   Containers:
     nginx:
       Container ID:   containerd://70129417e6251d06232fd6058c45***
       Image:          doc-cn-beijing.cr.volces.com/vke/nginx-demo:v1.0
       Image ID:       doc-cn-beijing.cr.volces.com/vke/nginx-demo@sha256:4424e31f2c366108***
       Port:           <none>
       Host Port:      <none>
       State:          Running
         Started:      Fri, 17 Jul 2026 15:53:36 +0800
       Ready:          True
       Restart Count:  0
       Environment:    <none>
       Mounts:
         /tmp from efs-pv (rw)
         /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-kw7v5 (ro)
   Conditions:
     Type                        Status
     PodReadyToStartContainers   True 
     Initialized                 True 
     Ready                       True 
     ContainersReady             True 
     PodScheduled                True 
   Volumes:
     efs-pv:
       Type:       PersistentVolumeClaim (a reference to a PersistentVolumeClaim in the same namespace)
       ClaimName:  efs-pvc-demo
       ReadOnly:   false
     kube-api-access-kw7v5:
       Type:                    Projected (a volume that contains injected data from multiple sources)
       TokenExpirationSeconds:  3607
       ConfigMapName:           kube-root-ca.crt
       Optional:                false
       DownwardAPI:             true
   QoS Class:                   BestEffort
   Node-Selectors:              <none>
   Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                                node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
   Events:
     Type    Reason   Age    From     Message
     ----    ------   ----   ----     -------
     Normal  Pulling  4m24s  kubelet  spec.containers{nginx}: Pulling image "doc-cn-beijing.cr.volces.com/vke/nginx-demo:v1.0"
     Normal  Pulled   4m15s  kubelet  spec.containers{nginx}: Successfully pulled image "doc-cn-beijing.cr.volces.com/vke/nginx-demo:v1.0" in 8.778s (8.779s including waiting). Image size: 56730696 bytes.
     Normal  Created  4m15s  kubelet  spec.containers{nginx}: Created container nginx
     Normal  Started  4m15s  kubelet  spec.containers{nginx}: Started container nginx
   ```
   

4. (Optional) After all FSX clients in the cluster have completed the upgrade, you can revert the `upgradeStrategy.type` parameter in the FSXSet configuration to the original strategy as needed.


<span id="KzFM7L47"></span>
## Upgrade observability

During the upgrade window, we recommend monitoring metrics simultaneously, such as ‌mount duration‌, ‌csi\-fsx error rate, and ‌FSX client version distribution, to proactively detect anomalies. For details, see [CSI Storage observability](https://docs.byteplus.com/en/docs/vke/CSI-storage-observability).

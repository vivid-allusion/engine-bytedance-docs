---
title: "Container image-aware scheduling"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Container_image-aware_scheduling"
---

This topic describes how to use the container image\-aware scheduling capability provided by VKE to prioritize scheduling Pods to nodes with image caches, thereby reducing container cold\-startup latency, accelerating autoscaling, and reducing pressure on image registries and network bandwidth.

<span id="836iNKFf"></span>
## Feature overview

Container image\-aware scheduling is a VKE policy that schedules Pods based on nodes' image cache status. During scheduling, the scheduler references cached image information on each node, prioritizing scheduling Pods to nodes with existing image caches. This avoids prolonged cold startups caused by repeatedly pulling large images across nodes.

Compared with the Kubernetes\-native ImageLocality plugin, container image\-aware scheduling provides the following enhancements.


|**Comparison dimension** |**Kubernetes\-native solution** |**Container image\-aware scheduling** |
|---|---|---|
|Reported image scale |A default maximum of about 50 per node. An oversized image list can easily cause nodes to exceed the recommended 20 KiB write limit. |Employs prefix\-tree compression storage and an independent Custom Resource Definition (CRD), supporting 4 to 5 times larger per\-node image capacity than the native solution. It enables second\-granular awareness of image changes, sizes, and last pull times. |
|Reporting policy |Only sorts images in reverse order by image size, without considering warm\-up and usage. |Supports filtering by dimensions such as last pull time, image size, and prefix matching, enabling flexible control through configuration. |
|Scenarios |Tends to distribute identical images across multiple nodes (suited for online services). It assigns low priority to scenarios such as reinforcement learning (RL) where one image corresponds to one Pod. |Uses matched image size as base score. It naturally adapts to high\-frequency, large\-image scenarios such as reinforcement learning, rapid function compute scaling, and quick agent sandbox startup. |
|Control plane coupling |Image information is mounted on nodes and watched by multiple components, such as DaemonSet, Autoscaler, and kubelet, likely leading to a traffic storm. |Image information is stored independently in a dedicated CRD watched only by the scheduler, achieving loose control plane coupling. |


<span id="bAnx16Qs"></span>
## Usage limits

Take note of the following limitations and considerations when using this feature:


* Container image\-aware scheduling is currently supported only in clusters that run the following Kubernetes versions. If the cluster version does not meet the requirements, upgrade the cluster. For details, see [Upgrading clusters](https://docs.byteplus.com/en/docs/vke/Upgrading-a-cluster):

   * [Kubernetes v1.30](https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v1_30): v1.30.4\-vke.18 and later

   * [Kubernetes v1.32](https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v1_32): v1.32.3\-vke.15 and later

   * [Kubernetes v1.34](https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v1_34): v1.34.6\-vke.11 and later

   * [Kubernetes v1.36](https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v1_36): v1.36.1\-vke.3 and later

   * Other later [Kubernetes versions](https://docs.byteplus.com/en/docs/vke/Kubernetes-version-release-notes) released by VKE

* This feature depends on the katalyst add\-on v0.5.13\-vke.16 or later. You must configure the image\-aware scheduling toggle in the ConfigMap for the add\-on. For details about the add\-on, see [katalyst](https://docs.byteplus.com/en/docs/vke/katalyst-add-on).

* We recommend that clusters with this feature enabled have no more than 2,000 nodes with no more than 100 images on each node.


<span id="7vr8METe"></span>
## Prerequisites


* The cluster is in the **Running** state and has multiple available nodes. This topic uses a cluster with four nodes as an example. To add nodes to a cluster, see [Adding nodes](https://docs.byteplus.com/en/docs/vke/Adding-nodes).

* The [katalyst](https://docs.byteplus.com/en/docs/vke/katalyst-add-on) add\-on v0.5.13\-vke.16 or later is installed. If the add\-on version does not meet the requirements, upgrade the add\-on. For detailed operations, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

* (Optional) To improve the hit rate during scheduling, you can warm up the target image and distribute the image to the corresponding nodes in advance.


<span id="EnChPEiy"></span>
## Procedure

<span id="6HLg6ZuO"></span>
### Step 1: Add a label to a node

Add a label that enables katalyst\-based resource management to nodes.


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. On the page that appears, click the name of the target cluster.

3. On the cluster management page, add a label to the node where the pod is located by following the steps below.

   
   <Tabs>
   <Tab zoneid="RaxMO0B3" title="Add a label at the node pool level">
   <TabTitle>Add a label at the node pool level</TabTitle>
   
   <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
   
   
   <div data-tips="true" data-tips-type="default">We recommend using this labeling method, as it allows labels to be added to nodes within the node pool.</div>
   
   
   
   1. In the left navigation pane, click **Nodes** \> **Node pool**.
   
   2. On the **Node pool** page, find the target node pool and click **Edit** in the **Actions** column.
   
   3. On the **Edit node pool** page, specify the **Node labels** parameter and select **Enable auto renew for node labels and taints** in the **Advanced configurations** section in the **Node pool configuration** step.
   
      * **Label key**: `vke.node.katalyst.deploy`
   
      * **Label value**: `true`
   
      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ec8a2ae2c96668ee278b964df334b9a8.png) </span>
   
   4. Update the configurations of the node pool based on the console wizard.
   
   
   </Tab>
   <Tab zoneid="Kg73vqs5" title="Add a label at the node level">
   <TabTitle>Add a label at the node level</TabTitle>
   
   1. In the left navigation pane, click **Nodes** \> **Node**.
   
   2. On the **Node** page, find the target node and click `...` \> **Label management** in the **Actions** column.
   
   3. On the **Node details page**, click **Add new** on the **Label** tab, add the following label to the node, and then click **Confirm**.
   
      * **Label key**: `vke.node.katalyst.deploy`
   
      * **Label value**: `true`
   
   
   </Tab>
   </Tabs>
   


<span id="W6a6ZMqs"></span>
### Step 2: Enable image\-aware scheduling

After the katalyst add\-on is installed, the system automatically generates a ConfigMap. The image\-aware scheduling toggle is off by default in this ConfigMap. You need to edit the ConfigMap to enable this feature.


1. In the left navigation pane of the cluster management page, click **Configurations** \> **ConfigMap**.

2. On the **ConfigMap** page, select the **katalyst\-system** namespace, find the **katalyst\-config** ConfigMap, and in the **Actions** column, click `...` \> **Edit Yaml**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bfe641b377cbfab5427e64465f73b336.png) </span>

3. Set the `imageAffinity.enable` field in the ConfigMap YAML to `true`. After you save the changes to the YAML file, image\-aware scheduling takes effect automatically, without requiring a katalyst restart.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_65c23f6308f68a550dfd22ec9c548220.png) </span>


<span id="OmvsePBq"></span>
### Step 3: Query node image information

After completing the above steps, node image information is recorded in the Kubernetes NodeImageCache CRD.


1. Use kubectl to connect to the cluster. For details, see [Connecting to a cluster](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

2. Run the following command to query the NodeImageCache for nodes in the cluster.

   Replace `<node-name>` with your node name.

   ```Bash
   kubectl get nodeimagecache <node-name> -oyaml
   ```
   

   The expected query result is as follows. You can view the comments in the NodeImageCache object to get node image information.

   ```YAML
   apiVersion: node.katalyst.kubewharf.io/v1alpha1
   kind: NodeImageCache
   metadata:
     name: 192.168.1.92
   status:
     updateTime: "2026-07-23T12:49:16Z"
     # Organize image information in a tree structure to improve retrieval speed and save storage space.
     images:
       "docker.io":
         chd:
           "library":
             chd:
               "nginx":
                 lef:
                 # Different versions of the image, with three parts separated by commas: tag, SHA256 digest prefix, and image size in bytes.
                   - "1.25,abc123def456,150000000"
                   - "1.24,def456abc789,145000000"
               "redis":
                 lef:
                   - "7-alpine,ghi789jkl012,35000000"
               "busybox":
                 lef:
                   - "latest,jkl345mno678,2000000"
       "cc-test-standard-cn-beijing.cr.volces.com":
         chd:
           "jianshan":
             chd:
               "nginx":
                 lef:
                   - "0.0.1-watch-sbx,fafd5f55,75916902"
       "registry.k8s.io":
         chd:
           "pause":
             lef:
               - "3.9,pqr567stu890,700000"
           "kube-proxy":
             lef:
               - "v1.30.0,stu234vwx5678,120000000"
       "aibrix-cn-beijing.cr.volces.com":
         chd:
           "dcp":
             chd:
               "busybox":
                 lef:
                   - "latest,ec06ff94,2202009"
   ```
   


<span id="NjwgtL3K"></span>
## Examples

This topic demonstrates the effect of image\-aware scheduling by pulling the required images on a managed cluster with four nodes.

<span id="XjK1e6Jv"></span>
### Step 1: Prepare a container image and warm it up


1. Prepare the required container image. VKE supports images in BytePlus Container Registry (CR) and third\-party image registries. To upload an image to CR, see [Pushing and pulling images](https://docs.byteplus.com/en/docs/cr/push-and-pull-images).

   You can prepare an image yourself or use the test image provided in this topic: `vke-cn-beijing.cr.volces.com/vke/nginx:latest`.

2. Log in to the node using [ECS Terminal](https://docs.byteplus.com/en/docs/vke/Managing-nodes#ecs-terminal) and run the `crictl` command to download the prepared image to one node in advance for image warm\-up. The other three nodes do not pull this image.

   ```Bash
   crictl pull vke-cn-beijing.cr.volces.com/vke/nginx:latest
   ```
   

   The image pulling status for the four nodes used in this example is as follows:

   
   |Node IP |192.168.174.132 |192.168.174.133 |192.168.174.134 |192.168.174.135 |
   |---|---|---|---|---|
   |**Whether the target image was pulled** |No |Yes |No |No |
   


<span id="QpbysKJz"></span>
### Step 2: Create a workload

The following content uses Deployment creation as an example. For more workload operations, see [Workloads](https://docs.byteplus.com/en/docs/vke/Workloads).


1. Connect to the cluster via kubectl. For details, see [Connecting to a cluster](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

2. Create a YAML file for the Deployment. The following `nginx-deployment-scn-test.yaml` file serves as an example:

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For a more intuitive demonstration, the number of replicas in the example Deployment is set to 10, and no instance dispersal policy is configured. In production environments, configure a strict instance dispersal policy and prepare image caches across multiple nodes to prevent all instances from being scheduled to the same node. For online services requiring high availability, we recommend disabling the container image\-aware scheduling feature.   </div>
   

   ```YAML
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: nginx-deployment-scn-test  # Deployment name.
     namespace: default  # The namespace of the Deployment.
   spec:
     progressDeadlineSeconds: 600
     replicas: 10  # The number of replicas for the Deployment.
     revisionHistoryLimit: 10
     selector:
       matchLabels:
         app: nginx
     strategy:
       rollingUpdate:
         maxSurge: 25%
         maxUnavailable: 25%
       type: RollingUpdate
     template:
       metadata:
         labels:
           app: nginx
       spec:
         containers:
         - image: vke-cn-beijing.cr.volces.com/vke/nginx:latest  # Container image address and tag. This must be the same as the address of the warmed-up image.
           imagePullPolicy: Always
           name: nginx
           ports:
           - containerPort: 80
             protocol: TCP
           resources: {}
           terminationMessagePath: /dev/termination-log
           terminationMessagePolicy: File
         dnsPolicy: ClusterFirst
         restartPolicy: Always
         schedulerName: default-scheduler
         securityContext: {}
         terminationGracePeriodSeconds: 30
   ```
   

3. Run the following command to create the Deployment.

   ```Bash
   kubectl apply -f nginx-deployment-scn-test.yaml
   ```
   


<span id="O6a8Ad6u"></span>
### Step 3: Validate results


<Tabs>
<Tab zoneid="OqhuPgTbG9" title="Image-aware scheduling not enabled">
<TabTitle>Image-aware scheduling not enabled</TabTitle>

The following example assumes that image\-aware scheduling is not enabled, that is, the `imageAffinity.enable` field in the katalyst\-config ConfigMap is set to `false`.


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. Find the target cluster and click its name.

3. In the left navigation bar of the cluster management page, click **Workload** \> **Deployment**.

4. On the **Deployment** page, find the Deployment created in **Step 2** and click its name.

5. On the **Deployment details page**, click the **List of instances** tab to view pod scheduling to nodes.

   The expected result is as shown in the figure below: Only one pod is scheduled to the node with a warmed\-up image (`192.168.174.133`), and the image cache hit rate is 10%.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e6ca37440e51fa57c0ee5dd6ab9a6a25.png) </span>


</Tab>
<Tab zoneid="Uj5nbu0kb5" title="Image-aware scheduling enabled">
<TabTitle>Image-aware scheduling enabled</TabTitle>

1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. Find the target cluster and click its name.

3. In the left navigation bar of the cluster management page, click **Workload** \> **Deployment**.

4. On the **Deployment** page, find the Deployment created in **Step 2**, and in the corresponding Actions column, click `...` \> **Edit Yaml** to reduce the replica count in the Deployment to 0.

5. Log in to the three nodes, respectively, using [ECS Terminal](https://docs.byteplus.com/en/docs/vke/Managing-nodes#ecs-terminal). Run the following command to delete the image cache on the nodes and retain the image cache on only one node (in this example, the image cache on the `192.168.174.133` node is retained).

   ```Bash
   crictl rmi vke-cn-beijing.cr.volces.com/vke/nginx:latest
   ```
   

6. On the **Configurations** \> **ConfigMap** page, find the **katalyst\-config** ConfigMap, set the `imageAffinity.enable` field value in its YAML to `true` to enable image\-aware scheduling. For detailed instructions, see [Procedure - Step 2](https://docs.byteplus.com/en/docs/vke/Container_image-aware_scheduling#W6a6ZMqs) above.

7. Query the node image information to ensure that all four nodes have NodeImageCache objects, and that the NodeImageCache object on the `192.168.174.133` node contains the target image. For detailed instructions, see [Procedure - Step 3](https://docs.byteplus.com/en/docs/vke/Container_image-aware_scheduling#OmvsePBq).

8. On the **Workload** \> **Deployment** page, find the target Deployment, and in the corresponding Actions column, click `...` \> **Edit Yaml** to adjust the replica count in the Deployment back to 10.

9. After adjusting the replica count in the Deployment, click the Deployment name to go to the **Deployment details page**. Then, click the **List of instances** tab to view information about scheduling Pods to nodes.

   The expected result is as shown below: All 10 pods are scheduled to the node with a warmed\-up image (`192.168.174.133`), and the image cache hit rate is 100%.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_588b4f623263485bf8d4f2599c9485ee.png) </span>


</Tab>
</Tabs>

---
title: "Using FSXSet to implement on-demand client creation"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using_FSXSet_to_implement_on-demand_client_creation"
---

As a Custom Resource Definition (CRD) provided by VKE, FSXSet is used to achieve fine\-grained scheduling and decoupled management of FSX clients. This topic describes how to use FSXSets to implement on\-demand client creation.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For more information about FSXSet resources, see <a href="https://docs.byteplus.com/en/docs/vke/Introduction_to_FSXSet_resources?lang=zh">FSXSet introduction</a>.</div>


<span id="nFArLZeH"></span>
## Scenario introduction

In VKE clusters, FSX clients run on cluster nodes and continuously consume node\-level resources, such as CPU and memory. In certain scenarios, they may further request scarce resources, such as vRDMA or ENIs. Consequently, the timing of FSX client creation involves balancing ‌application startup efficiency and node resource consumption. This is especially critical in large\-scale clusters, uneven workload distributions, or frequently autoscaled node pools.

VKE provides the following client creation strategies that you can select based on preferences for resource efficiency or startup latency:


|Creation strategy |Strategy description |Main issue |Application scenario |
|---|---|---|---|
|On\-demand creation (WaitForFirstConsumer) |The FSX client is created on a node only when a workload dependent on FSX is first scheduled to the node. |When a workload dependent on FSX is first scheduled to a node, it must wait for the FSX client to be created and initialized before mounting FSX volumes. This extends application startup time, particularly noticeable in frequently autoscaled node pools with startup\-sensitive workloads. |This applies to clusters where few nodes use FSX volumes, or large clusters that prioritize minimal resource overhead. Generally, this is the default option for common scenarios.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This strategy is mandatory in cross\-tenant mounting scenarios.</div><br> |
|Immediate creation (Immediate) |FSX clients are created immediately on all nodes selected by the FSXSet. |Even when no workloads on a node depend on FSX, the FSX client remains resident, continuously consuming the node's scheduling capacity. In resource\-constrained or cost\-sensitive clusters, this can crowd out the available resources for business Pods. |This applies to node pools where autoscaling is frequent, and business applications are extremely sensitive to startup latency (for example, online inference and real\-time tasks). |


<span id="c5ldYsuj"></span>
## Prerequisites


* The csi\-fsx add\-on has been installed and upgraded to v1.0.0 or later. For details, see [csi-fsx](https://docs.byteplus.com/en/docs/vke/csi-fsx-add-on).

* The fsxset\-controller add\-on has been installed. For details, see [fsxset-controller](https://docs.byteplus.com/en/docs/vke/fsxset-controller-add-on).

* (Optional) The target cluster has been connected through kubectl. For details, see [Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).


<span id="jWFEwpR2"></span>
## Scenario 1: On\-demand creation

<span id="MG8TbFQi"></span>
### Procedure

When creating or updating an FSXSet configuration, specify the FSX client creation strategy using the `createMode` parameter. The following is a code sample:

```YAML
apiVersion: csi.vke.volcengine.com/v1alpha1
kind: FSXSet
metadata:
  name: doc-demo # The FSXSet resource name.
spec:
  groupName: doc
  createMode: WaitForFirstConsumer # FSX client creation strategy. In this example, the value is WaitForFirstConsumer, which means on-demand creation.
  template:
    parameterTemplate:
      image: vke-cn-beijing.cr.volces.com/vke/fsx-agent:v1.3.4.286
      resources:
        requests:
          cpu: 100m
          memory: 128Mi
        limits:
          cpu: 2000m
          memory: 2Gi
```


<span id="6ZJr30dg"></span>
### Validate results


1. Create a node pool and assign nodes in the node pool to the current group by using `fsx.csi.volcengine.com/group=doc`. Run the following command to view an overview of FSX clients in the cluster.

   ```Bash
   kubectl get fsxset -o wide
   ```
   

   The expected result is as follows: Since the on\-demand creation (WaitForFirstConsumer) strategy is adopted, no FSX clients are created in the cluster.

   ```Bash
   NAME         GROUP     DESIREDREVISION    DESIRED   CURRENT   READY   AVAILABLE   UPDATED   MATCHED   AGE
   default      default   3f2d716d885****                                                                78m
   doc-demo     doc       8dec430c7ed****                                                                39m
   ```
   

2. Create a business Pod and mount an FSX volume. For example, to mount a static TOS PV, see [Accessing static TOS PVs by using the FSX client](https://docs.byteplus.com/en/docs/vke/Using_static_TOS_Volumes_through_the_FSX_client).

3. Run the following command again to view information about FSX clients in the cluster.

   ```Bash
   kubectl get fsxset -o wide
   ```
   

   The expected result is that the FSX client on the corresponding node has been created.

   ```Bash
   NAME         GROUP     DESIREDREVISION    DESIRED   CURRENT   READY   AVAILABLE   UPDATED   MATCHED   AGE
   default      default   3f2d716d885****                                                                78m
   doc-demo     doc       8dec430c7ed****    1         1         1       1           1         1         39m
   ```
   

4. Run the following command to view details about FSX clients in the cluster. Here, `doc-demo` is the name of the FSXSet resource.

   ```Bash
   kubectl get pod -n kube-system -l addon.vke.volcengine.com/fsxset=doc-demo --show-labels
   ```
   

   The expected result is as follows. You can view the FSX client.

   ```Bash
   NAME                       READY   STATUS    RESTARTS   AGE     LABELS
   fsx-agent-doc-demo-d5***   1/1     Running   0          2m33s   addon.vke.volcengine.com/fsxset-revision=b5e31ff826***,addon.vke.volcengine.com/fsxset=doc-demo,app.kubernetes.io/instance=fsx-agent,app.kubernetes.io/managed-by=fsxset,app.kubernetes.io/name=agent,app.kubernetes.io/node=192.168.2.246,app.kubernetes.io/version=v1.3.4.286,container-image.agent.fsx/tag=v1.3.4.286
   ```
   


<span id="Isl8f39a"></span>
## Scenario 2: Immediate creation

<span id="LHvJGSm4"></span>
### Procedure

When creating or updating an FSXSet configuration, specify the FSX client creation strategy using the `createMode` parameter. The following is a code sample:

```YAML
apiVersion: csi.vke.volcengine.com/v1alpha1
kind: FSXSet
metadata:
  name: doc-demo # The FSXSet resource name.
spec:
  groupName: doc
  createMode: WaitForFirstConsumer # FSX client creation strategy. In this example, the value is Immediate, meaning that the FSX client is created immediately after the node is assigned.
  template:
    parameterTemplate:
      image: vke-cn-beijing.cr.volces.com/vke/fsx-agent:v1.3.4.286
      resources:
        requests:
          cpu: 100m
          memory: 128Mi
        limits:
          cpu: 2000m
          memory: 2Gi
```


<span id="hjxgiRUK"></span>
### Validate results


1. Create a node pool and assign nodes in the node pool to the current group by using `fsx.csi.volcengine.com/group=doc`. Run the following command to view an overview of FSX clients in the cluster.

   ```Bash
   kubectl get fsxset -o wide
   ```
   

   The expected result is as follows: Since the Immediate strategy is adopted, all nodes in the node pool (4 nodes in this example) have FSX clients created on them.

   ```Bash
   NAME         GROUP     DESIREDREVISION    DESIRED   CURRENT   READY   AVAILABLE   UPDATED   MATCHED   AGE
   default      default   3f2d716d885****                                                                78m
   doc-demo     doc       8dec430c7ed****    4         4         4       4           4         4         39m
   ```
   

2. Run the following command to view details about FSX clients in the cluster. Here, `doc-demo` is the name of the FSXSet resource.

   ```Bash
   kubectl get pod -n kube-system -l addon.vke.volcengine.com/fsxset=doc-demo --show-labels
   ```
   

   The expected result is as follows. You can view all FSX clients created.

   ```Bash
   NAME                       READY   STATUS    RESTARTS   AGE     LABELS
   fsx-agent-doc-demo-cj***   1/1     Running   0          76s     addon.vke.volcengine.com/fsxset-revision=6c356a68629c9591,addon.vke.volcengine.com/fsxset=doc-demo,app.kubernetes.io/instance=fsx-agent,app.kubernetes.io/managed-by=fsxset,app.kubernetes.io/name=agent,app.kubernetes.io/node=192.168.1.58,app.kubernetes.io/version=v1.3.4.286,container-image.agent.fsx/tag=v1.3.4.286
   fsx-agent-doc-demo-d5***   1/1     Running   0          3m43s   addon.vke.volcengine.com/fsxset-revision=b5e31ff826ab03c2,addon.vke.volcengine.com/fsxset=doc-demo,app.kubernetes.io/instance=fsx-agent,app.kubernetes.io/managed-by=fsxset,app.kubernetes.io/name=agent,app.kubernetes.io/node=192.168.2.246,app.kubernetes.io/version=v1.3.4.286,container-image.agent.fsx/tag=v1.3.4.286
   fsx-agent-doc-demo-pz***   1/1     Running   0          7m28s   addon.vke.volcengine.com/fsxset-revision=b5e31ff826ab03c2,addon.vke.volcengine.com/fsxset=doc-demo,app.kubernetes.io/instance=fsx-agent,app.kubernetes.io/managed-by=fsxset,app.kubernetes.io/name=agent,app.kubernetes.io/node=192.168.1.45,app.kubernetes.io/version=v1.3.4.286,container-image.agent.fsx/tag=v1.3.4.286
   fsx-agent-doc-demo-zg***   1/1     Running   0          5m25s   addon.vke.volcengine.com/fsxset-revision=b5e31ff826ab03c2,addon.vke.volcengine.com/fsxset=doc-demo,app.kubernetes.io/instance=fsx-agent,app.kubernetes.io/managed-by=fsxset,app.kubernetes.io/name=agent,app.kubernetes.io/node=192.168.2.253,app.kubernetes.io/version=v1.3.4.286,container-image.agent.fsx/tag=v1.3.4.286
   ```

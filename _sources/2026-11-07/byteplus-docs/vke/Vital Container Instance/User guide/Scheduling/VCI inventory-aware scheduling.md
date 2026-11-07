---
title: "VCI inventory-aware scheduling"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/VCI-inventory-aware-scheduling"
---

This topic describes how to enable and use inventory\-aware scheduling in VCI scenarios. This capability incorporates real\-time VCI inventory information into scheduling decision\-making. It improves the success rate of creating Pods in specified availability zones and reduces creation failures and repeated retries caused by insufficient inventory.

<span id="5PcnQ7s5"></span>
## Background

In the traditional VCI creation process, the scheduler cannot detect the actual inventory of the underlying VCI resources when selecting an availability zone for a Pod. As a result, the scheduler may schedule the Pod to an availability zone with insufficient inventory, causing instance creation to fail. After the failure, the system must repeat the complete scheduling and creation process. This increases the creation time and reduces the Pod creation success rate.

Inventory\-aware scheduling incorporates real\-time inventory information managed by VCI into scheduling decision\-making. Before instance creation begins, VCI leverages real\-time inventory information to return suitable availability zones and reserved pre\-scheduled instances, and then creates the instance based on the returned result. This mechanism checks inventory first, determines the availability zone, and then creates the instance. It reduces the probability that a Pod is scheduled to an availability zone with insufficient inventory, thereby decreasing retries after creation failures.

<span id="J5PurDaK"></span>
## Feature description

You can enable inventory\-aware scheduling by adding an annotation to a Pod. The following table describes the core annotation.


|Annotation key |Annotation sample value |Description |
|---|---|---|
|vci.volcengine.com/inventory\-aware |true |Whether to enable inventory\-aware scheduling for VCI instances:<br><br><br>* **false**: (Default value) Disable.<br><br>* **true**: Enabled Inventory\-aware scheduling must be enabled in this scenario. |


After you enable VCI inventory\-aware scheduling, you can also use the following annotations to declare scheduling preferences. This helps match more suitable availability zones and VCI instance specifications during inventory filtering. For more information about annotations, see [Pod annotations](https://docs.byteplus.com/en/docs/vke/VCI-Pod-annotations).


|Annotation key |Description |
|---|---|
|vke.volcengine.com/burst\-to\-vci |Pod scheduling mode. The valid value is **enforce**, which enforces scheduling of Pods to VCI. |
|vke.volcengine.com/preferred\-subnet\-ids |Specify the subnets used by the VCI instance. Separate multiple subnets with commas (`,`). The system selects the subnet with the most remaining IP addresses to create the VCI instance. |
|vci.vke.volcengine.com/preferred\-instance\-types |Specify VCI instance types. Separate multiple instance types with commas (`,`) and prioritize them in the order they are listed.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Use either this annotation or <code>preferred-instance-family</code>. Do not configure both instance types and instance families simultaneously. Otherwise, resource selection conflicts may occur.</div><br> |
|vci.vke.volcengine.com/preferred\-instance\-family |Specify the instance families used by the VCI instance. Separate multiple instance families with commas (`,`) and prioritize them in the order they are listed.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Use either this annotation or <code>preferred-instance-types</code>. Do not configure both instance types and instance families simultaneously. Otherwise, resource selection conflicts may occur.</div><br> |


<span id="Sbz8X2OT"></span>
## Limits

When you use inventory\-aware scheduling, take note of the following limitations.


|Limitation item |Description |
|---|---|
|Effective scope |Inventory\-aware scheduling takes effect only when a Pod is forcibly scheduled to VCI, that is, when the Pod meets one of the following conditions:<br><br><br>* The Pod is forcibly scheduled to VCI by using the `vke.volcengine.com/burst-to-vci: enforce` annotation. For more information about the annotation, see [Pod annotations](https://docs.byteplus.com/en/docs/vke/VCI-Pod-annotations).<br><br>* The Pod matched by the `selector` is forcibly scheduled to VCI using a vci\-profile that contains `enforceSelectorToVci: "true"`. For more information about a vci\-profile, see [Using VCI by configuring a vci-profile](https://docs.byteplus.com/en/docs/vke/Using-VCI-by-configuring-vci-profile).<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Inventory\-aware scheduling does not take effect if you use a <code>node name</code> to specify a virtual node for a Pod.</div><br> |
|No support for VKE and VCI hybrid deployments |Inventory\-aware scheduling is not supported in VKE and VCI hybrid deployments based on ResourcePolicy. For more information about ResourcePolicy, see [ResourcePolicy scheduling](https://docs.byteplus.com/en/docs/vke/ResourcePolicy-scheduling). |
|Incompatibility with delayed PVC binding  |PVCs that use WaitForFirstConsumer (delayed binding) are incompatible with inventory\-aware scheduling. These Pods are rejected by a webhook. |
|Incompatibility with specifying a network interface |Pods that use pod\-networks\-definition to specify network interfaces are incompatible with inventory\-aware scheduling and are rejected by a webhook. |
|Pods are pending in case of insufficient inventory |After inventory\-aware scheduling is enabled, if inventory in the target availability zone is insufficient, the Pod remains in the Pending state and keeps retrying based on exponential backoff with no retry timeout by default until inventory becomes available and the instance is created. |


<span id="oxJTBPlD"></span>
## Prerequisites


* A cluster required by the VCI service has been created. For details, see [Using VCI in VPC-CNI clusters](https://docs.byteplus.com/en/docs/vke/Using-VCI-in-Vital-Kubernetes-Engine) and [Using VCI in Flannel clusters](https://docs.byteplus.com/en/docs/vke/Using-VCI-in-Flannel-cluster).

* The vci\-virtual\-kubelet add\-on has been installed in the cluster. For detailed instructions, see [vci-virtual-kubelet](https://docs.byteplus.com/en/docs/vke/vci-virtual-kubelet-add-on).


<span id="RfLDJPBF"></span>
## Procedure

<span id="X8RE4vea"></span>
### Step 1: Force scheduling to VCI

Force all Pods in the workload to be scheduled to VCI. This topic uses the creation of a Deployment as an example. For information about creating other workloads, see [Creating workloads](https://docs.byteplus.com/en/docs/vke/Deployments).


1. Use kubectl to connect to the cluster. For details, see [Connecting to a cluster](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

2. Create a YAML file for the Deployment. The following `inventory-aware-demo.yaml` file provides a code sample.

   ```YAML
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: inventory-aware-demo  # Deployment name.
     namespace: default  # The namespace of the Deployment.
   spec:
     replicas: 1  # The number of replicas defined in the Deployment, that is, the number of Pods.
     selector:
       matchLabels:
         app: inventory-aware-demo
     template:
       metadata:
         labels:
           app: inventory-aware-demo
         annotations:
           vke.volcengine.com/burst-to-vci: "enforce"  # Enforce Pod scheduling to VCI.
           vci.volcengine.com/inventory-aware: "true"  # Whether to enable inventory-aware scheduling for VCI instances. Valid values: true (enabled) and false (disabled).
           vke.volcengine.com/preferred-subnet-ids: "subnet-xxxxxxxx"  # Specify the subnet ID used by the Pod.
           vci.vke.volcengine.com/preferred-instance-family: "vci-g3i"  # Specify the VCI instance family used by the Pod.
   
       spec:
         containers:
         - name: app
           image: your-image
           command: ["/bin/sh", "-c", "sleep 36000"]
           resources:
             requests:
               cpu: "1"
               memory: 2Gi
             limits:
               cpu: "1"
               memory: 2Gi
   ```
   

3. Run the following command to create the Deployment.

   ```Bash
   kubectl apply -f inventory-aware-demo.yaml
   ```
   


<span id="ZLwBKIbw"></span>
### Step 2: Verify the effect of inventory\-aware scheduling

After you create the workload, the scheduler first initiates pre\-scheduling to VCI. If inventory is sufficient, the Pod is scheduled to an availability zone with inventory, and the instance is created. If inventory is insufficient, the Pod remains in the Pending state and keeps retrying based on the backoff policy until inventory becomes available and the instance is created. You can perform the following steps to view the Pod scheduling and creation status.


1. Run the following command to view the Pod status.

   ```Bash
   kubectl get pod -l app=inventory-aware-demo -o wide
   ```
   

   The expected output is as follows:

   
   <Tabs>
   <Tab zoneid="o0SH59IZ21" title="Sufficient inventory">
   <TabTitle>Sufficient inventory</TabTitle>
   
   ```Bash
   NAME                                    READY   STATUS    RESTARTS   AGE   IP             NODE        NOMINATED NODE   READINESS GATES
   inventory-aware-demo-xxxxxxxxx-xxxxx    1/1     Running   0          2m    192.168.x.x    x.x.x.x     <none>           <none>
   ```
   
   
   
   </Tab>
   <Tab zoneid="q7X57SRirC" title="Insufficient inventory">
   <TabTitle>Insufficient inventory</TabTitle>
   
   ```Bash
   NAME                                    READY   STATUS    RESTARTS   AGE   IP             NODE        NOMINATED NODE   READINESS GATES
   inventory-aware-demo-xxxxxxxxx-xxxxx    0/1     Pending   0          30s   <none>         <none>      <none>           <none>
   ```
   
   
   
   </Tab>
   </Tabs>
   

2. Run the following command to view scheduling and creation events.

   ```Bash
   kubectl describe pod <pod-name>
   # Replace <pod-name> in the command with the actual Pod name obtained from the previous query result.
   ```
   

   The expected response is as follows:

   
   <Tabs>
   <Tab zoneid="gSAtfr6M" title="Sufficient inventory">
   <TabTitle>Sufficient inventory</TabTitle>
   
   ```Bash
   Events:
     Type    Reason     Age   From               Message
     ----    ------     ----  ----               -------
     Normal  Scheduled  2m    default-scheduler  Successfully assigned default/inventory-aware-demo-xxx to cn-hangzhou.x.x
     Normal  Pulled     2m    kubelet            Container image already present on machine
     Normal  Created    2m    kubelet            Created container inventory-aware-demo
     Normal  Started    2m    kubelet            Started container inventory-aware-demo
   ```
   
   
   
   </Tab>
   <Tab zoneid="sgK8oY4m" title="Insufficient inventory">
   <TabTitle>Insufficient inventory</TabTitle>
   
   ```Bash
   Events:
     Type     Reason             Age                From                     Message
     ----     ------             ----               ----                     -------
     Warning  FailedScheduling   2s                 vci-scheduler            Failed to Pre-schedule, ResourceSoldOut the specified resource vci.n2i of cn-beijing-a has been soldout, try other instance families of resources or other zones map[xxxx]
   ```
   
   
   
   </Tab>
   </Tabs>

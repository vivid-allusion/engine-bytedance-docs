---
title: "VCI Pod fail-fast"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/VCI_Pod_fail-fast"
---

This topic describes how to enable the Pod fail‑fast capability in VCI scenarios through a failure handling policy. When a VCI instance fails to be created due to insufficient inventory, unavailable instance types, or other reasons, the system promptly returns a failure result with a clear identifier. This helps you detect the issue in time and switch to a fallback plan (such as switching from instance family A to instance family B), preventing prolonged, ineffective waiting.

<span id="gl265pNK"></span>
## Background

By default, when a VCI Pod fails to be created, the system automatically retries using a backoff algorithm and keeps attempting until the instance is created. This is applicable to scenarios that are sensitive to success rates and can tolerate temporary resource shortages. However, in scenarios with scarce resources such as GPUs, this mechanism causes Pods to remain in the Pending state for an extended period with repeated retries. This requires you to wait 2 to 5 minutes before confirming the failure, which does not meet the requirements of actual business scenarios.

To address this issue, VCI provides a failure handling policy (Fail‑strategy) that allows you to declare fail‑fast behavior on Pods. When resource creation tasks fail, the system no longer retries for a long time. Instead, it quickly determines the failure and exposes a clear failure reason, reducing the failure confirmation time from minutes to seconds.

<span id="o9CPT8ac"></span>
## Feature description

You can enable the Pod fail‑fast capability by adding an annotation to the target Pod. The following table describes the core annotation.


|Annotation key |Annotation sample value |Description |
|---|---|---|
|vci.volcengine.com/fail\-strategy |fail\-fast |Specifies how to handle the case where a VCI Pod fails to be created. Valid values: Valid values:<br><br><br>* **fail\-back**: (Default) Automatic failure recovery. After a Pod fails to be created, the system automatically retries using a backoff algorithm until the Pod is created.<br><br>* **fail\-fast**: Fail‑fast. After a Pod fails to be created, the system immediately reports an error without retrying for a long time and exposes a clear failure identifier (`status.reason`): CreatePodError.<br><br>   After **fail** **\-** **fast** is enabled, the Pod behaves as follows:<br><br>   * When a resource creation task fails, the system immediately rolls back the creation process without prolonged retries.<br><br>   * The `status.phase` of the Pod remains Pending, and the failure reason exposes the fail‑fast identifier (such as CreatePodError).<br><br>   * Upper‑layer workloads (such as Deployments and StatefulSets) can identify a fast failure based on the reason and trigger Pod recreation. You can then quickly switch to a fallback instance type. Native Kubernetes does not automatically recreate Pods by default. This needs to be handled by user‑defined workload controllers. |


<span id="WX0OU4l9"></span>
## Limits

Take note of the following limits when you use the VCI Pod fail\-fast capability.


|Limitation item |Description |
|---|---|
|Only Pod creation tasks support fail‑fast |Fail‑fast only applies to Pod creation. Creation failures for other types of tasks still follow the default retry logic. |
|Recreation depends on the upper‑layer workload |By default, native Kubernetes does not automatically recreate a Pod that has failed fast. Custom workload controllers (such as Deployments and StatefulSets) are required to trigger the recreation based on the failure reason. |


<span id="wclN5JXF"></span>
## Prerequisites


* A cluster required by the VCI service has been created. For details, see [Using VCI in VPC-CNI clusters](https://docs.byteplus.com/en/docs/vke/Using-VCI-in-Vital-Kubernetes-Engine) and [Using VCI in Flannel clusters](https://docs.byteplus.com/en/docs/vke/Using-VCI-in-Flannel-cluster).

* A fallback solution has been prepared to enable timely switching after a fast failure. For an example of how to switch to a fallback solution, see the [Switch to a fallback solution](https://docs.byteplus.com/en/docs/vke/VCI_Pod_fail-fast#pji203my) section of this topic.


<span id="ZjaCftAQ"></span>
## Procedure

The following example uses a Deployment with the general\-purpose instance type `vci.n3a.4c-8gi`. By pinning the Pod subnet to the cn\-beijing\-a availability zone, it simulates a scenario where the `vci.n3a` instance type is out of stock in the zone, thereby validating the result when fail\-fast is enabled. For VCI instance types supported in each region and availability zone, see [Regions and availability zones](https://docs.byteplus.com/en/docs/vke/VCI-Regions-and-Availability-Zones). For instructions on configuring VCI Pod subnets, see [Managing virtual nodes](https://docs.byteplus.com/en/docs/vke/Managing_virtual_nodes).

<span id="lzajh2sg"></span>
### Step 1: Declare a fail\-fast policy in a workload

Enable fail\-fast in the workload via a Pod annotation.


1. Use kubectl to connect to the cluster. For details, see [Connecting to a cluster](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

2. Create a YAML file for the Deployment. The following `vci-failfast-demo.yaml` file provides a code sample.

   ```YAML
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: vci-failfast-demo  # The Deployment name.
     namespace: default  # The namespace of the Deployment.
   spec:
     replicas: 1  # The number of Pods.
     selector:
       matchLabels:
         app: vci-failfast-demo
     template:
       metadata:
         labels:
           app: vci-failfast-demo
         annotations:
           vke.volcengine.com/burst-to-vci: "enforce"  # Enforce Pod scheduling to VCI.
           vci.volcengine.com/fail-strategy: "fail-fast"  # Enable fail-fast. After a Pod fails to be created, the system immediately exposes a failure identifier without retrying for a long time. Valid values: fail-fast and fail-back.
           vci.vke.volcengine.com/preferred-instance-types: "vci.n3a.4c-8gi"   # Specify a VCI general-purpose instance type (4 vCPUs and 8 GiB of memory).
       spec:
         containers:
           - name: nginx
             image: doc-cn-beijing.cr.volces.com/vke/nginx-demo:v1.0   # The address and version of the container image. Replace the value with your actual information. If you need to use a public image, make sure that the cluster can access the public network.
             resources:
               requests:
                 cpu: "4"
                 memory: 8192Mi
               limits:
                 cpu: "4"
                 memory: 8192Mi
   ```
   

3. Run the following command to create a Deployment.

   ```Bash
   kubectl apply -f vci-failfast-demo.yaml
   ```
   


<span id="ieihrNqu"></span>
### Step 2: Verify whether fail\-fast takes effect

After fail‑fast is enabled, the Pod does not immediately become Failed. Instead, its `status.phase` remains `Pending`, `status.reason` is set to `CreatePodError`, the `status.message` provides the specific failure reason, and the container remains in the `ContainerCreating` state.


1. Run the following command to obtain the name of the Pod in the Deployment.

   ```Bash
   kubectl get pod -l app=vci-failfast-demo -n default
   ```
   

   The expected output is as follows:

   ```Bash
   NAME                                READY   STATUS              RESTARTS   AGE
   vci-failfast-demo-7c9f8d6b5-*****   0/1     ContainerCreating   0          10s
   ```
   

2. Run the following command to view the `status` field of the Pod.

   ```Bash
   kubectl get pod vci-failfast-demo-7c9f8d6b5-***** -n default -o yaml
   ```
   

   The expected result is as follows (excerpt of the `status` section):

   ```YAML
   status:
     phase: Pending
     reason: CreatePodError
     message: The specified resource vci.n3a of cn-beijing-a is sold out, try other instance types of resources or other zones.
     hostIP: 192.168.XX.XX
     qosClass: Guaranteed
     startTime: "2026-08-21T03:54:48Z"
     containerStatuses:
     - name: nginx
       image: doc-cn-beijing.cr.volces.com/vke/nginx-demo:v1.0
       ready: false
       started: false
       restartCount: 0
       state:
         waiting:
           reason: ContainerCreating
   ```
   


<span id="pji203my"></span>
### Step 3: (Optional) Switch to a fallback solution

Upper‑layer workloads or O&M processes can trigger switching logic based on the fail‑fast identifier. For example, when GPUs are out of stock, you can submit a workload with large\-core CPU specifications to continue the computation. The following content provides two solutions. You can adopt other solutions based on your business requirements.


<Tabs>
<Tab zoneid="wFQyYUNXJC" title="Solution 1 (recommended)">
<TabTitle>Solution 1 (recommended)</TabTitle>

Make sure that the business workload is created and runs as expected by appending fallback instance types within the same workload.

The VCI annotations for specifying instance types or families (such as `preferred-instance-types`) support multiple values separated by commas, ordered by priority. When a higher‑priority instance type is unavailable, the system uses a lower‑priority type or family to create the instance.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This solution shifts the switching operation forward to the creation stage. The majority of inventory fluctuations are automatically covered by a fallback mechanism without requiring manual intervention, and the fail\-fast mode is triggered only when all candidate instance types are unavailable.</div>


A sample annotation is shown as follows. For more instructions, see [Creating VCI instances](https://docs.byteplus.com/en/docs/vke/Creating-an-instance?lang=en).

```YAML
      annotations:
        vke.volcengine.com/burst-to-vci: "enforce"
        vci.volcengine.com/fail-strategy: "fail-fast"
        vci.vke.volcengine.com/preferred-instance-types: "vci.n3a.4c-8gi,vci.u1.4c-8gi"   # Try vci.n3a.4c-8gi first. If it is out of stock, the system automatically switches to vci.u1.4c-8gi.
```



</Tab>
<Tab zoneid="BaR2hXpXue" title="Solution 2">
<TabTitle>Solution 2</TabTitle>

After a fail‑fast event, switch to another instance type and recreate the Pod to ensure that the business workload is created and runs as expected.

When all candidate instance types are out of stock and the Pod has exposed `CreatePodError`, modify the instance type annotation in the workload to switch to a new fallback instance type and trigger a rolling update to recreate the Pod.


1. Switch to the fallback instance type. The following command switches the instance type from `vci.n3a.4c-8gi` to the fallback instance type `vci.u1.4c-8gi`.

   ```Bash
   kubectl patch deployment vci-failfast-demo -n default --type merge \
     -p '{"spec":{"template":{"metadata":{"annotations":{"vci.vke.volcengine.com/preferred-instance-types":"vci.u1.4c-8gi"}}}}}'
   ```
   

   The expected output is as follows:

   ```Bash
   deployment.apps/vci-failfast-demo patched
   ```
   

2. Run the following command to observe the progress of the rolling update.

   ```Bash
   kubectl rollout status deployment/vci-failfast-demo -n default
   ```
   

   The expected output is as follows:

   ```Bash
   Waiting for deployment "vci-failfast-demo" rollout to finish: 0 of 1 updated replicas are available...
   deployment "vci-failfast-demo" successfully rolled out
   ```
   

3. Run the following command to confirm the new Pod is running as expected.

   ```Bash
   kubectl get pod -l app=vci-failfast-demo -n default -o wide
   ```
   

   The expected output is as follows:

   ```Bash
   NAME                                READY   STATUS    RESTARTS   AGE   IP            NODE               NOMINATED NODE   READINESS GATES
   vci-failfast-demo-6d5c7b9f4-*****   1/1     Running   0          30s   10.XX.XX.XX   vci-virtual-node   <none>           <none>
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For Solution 2, you can implement an automated process where a custom controller or O&M script continuously watches the <code>status.reason</code> of the Pod. If <code>CreatePodError</code> is detected, it automatically performs the preceding patch and recreation operations based on a predefined list of fallback instance types. This achieves quick switching without manual intervention.   </div>
   


</Tab>
</Tabs>

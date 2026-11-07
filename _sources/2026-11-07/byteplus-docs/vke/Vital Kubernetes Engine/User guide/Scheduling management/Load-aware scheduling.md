---
title: "Load-aware scheduling"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Load-aware-scheduling"
---

This topic mainly describes how to use the load\-aware scheduling capability provided by Vital Kubernetes Engine (VKE) to achieve node load balancing.

<span id=".5Yqf6IO95qaC6L-w"></span>
## Feature overview

Load\-aware scheduling is a policy provided by VKE that performs appropriate scheduling based on the load of nodes. During scheduling, pods are preferentially scheduled to nodes with lower load according to node load statistics to balance loads among nodes. This prevents application or node failures caused by a high load on a single node.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c70df37d5d3939b484ae146bf04bc4ae.png) </span>

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A cluster is in the **Running** state and has two or more nodes. Load balancing among these nodes is required. For detailed operations, see [Adding nodes](https://docs.byteplus.com/en/docs/vke/Adding-nodes).

* The Kubernetes version of the cluster must meet the following requirements to achieve load\-aware scheduling. For detailed operations, see [Upgrading clusters](https://docs.byteplus.com/en/docs/vke/Upgrading-a-cluster).

   * [Kubernetes v1.24](https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v-1_24): v1.24.15\-vke.18 and later

   * [Kubernetes v1.26](https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v-1_26): v1.26.6\-vke.7 and later

   * Other later [Kubernetes versions](https://docs.byteplus.com/en/docs/vke/Kubernetes-version-release-notes) released by VKE

* The scheduler\-plugin add\-on has been installed in the cluster. For detailed operations, see [scheduler-plugin](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on#.c2NoZWR1bGVyLXBsdWdpbi3nu4Tku7Y=).


<span id=".5L2_55So5pa55rOV"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5byA5ZCv6LCD5bqm5Zmo55qE6LSf6L295oSf55-l6LCD5bqm5Yqf6IO9"></span>
### Step 1: Enable the load\-aware scheduling feature of the scheduler

Enable the load\-aware scheduling feature of the scheduler in the cluster. You can enable this feature by using the [VKE console](https://console.byteplus.com/vke) or by calling the [CreateAddon](https://docs.byteplus.com/en/docs/vke/CreateAddon) or [UpdateAddonConfig](https://docs.byteplus.com/en/docs/vke/UpdateAddonConfig) API.


* Enabling the feature in the console

   In the cluster that meets the requirements, configure the **scheduler\-plugin** add\-on to enable the **load\-aware scheduling** feature. For detailed operations, see [scheduler-plugin](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on#.c2NoZWR1bGVyLXBsdWdpbi3nu4Tku7Y=).

   
   |Parameters |Description |
   |---|---|
   |Effective scope |Specify the effective scope of load\-aware scheduling.<br><br><br>* If you select **Specific pod**, configure the load\-aware scheduling annotation for the specified pods based on the instructions in this topic.<br><br>* If you select **Global**, all pods in the cluster use load\-aware scheduling by default, and no additional configuration is required.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The <strong>Effective scope</strong> parameter is displayed only for clusters of the following Kubernetes versions:</div><br><br><br>   * <div data-tips="true" data-tips-type="default"><a href="https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v-1_26">Kubernetes v1.26</a>: v1.26.15\-vke.33 and later</div><br><br><br>   * <div data-tips="true" data-tips-type="default"><a href="https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v-1_28">Kubernetes v1.28</a>: v1.28.15\-vke.26 and later</div><br><br><br>   * <div data-tips="true" data-tips-type="default"><a href="https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v1_30">Kubernetes v1.30</a>: v1.30.4\-vke.11 and later</div><br><br><br>   * <div data-tips="true" data-tips-type="default">Other later <a href="https://docs.byteplus.com/en/docs/vke/Kubernetes-version-release-notes">Kubernetes versions</a> released by VKE</div><br><br><br>* <div data-tips="true" data-tips-type="default">If load\-aware scheduling is enabled for the cluster for the first time, the feature globally takes effect by default.</div><br> |
   |Advanced configuration |Specify the parameters of node resources for load\-aware scheduling based on your business requirements.<br><br><br>* **Node resource utilization threshold**: Specify the node CPU and memory utilization. Load\-aware scheduling filters nodes based on these values.<br><br>* **Node scoring resource weight**: Specify the weight for different resources when the load\-aware scheduling add\-on scores nodes based on resource utilization. Valid values: 1 to 10. The higher the weight, the higher the score. |
   

* Enabling the feature by calling the API

   Call the [CreateAddon](https://docs.byteplus.com/en/docs/vke/CreateAddon) API to install the **scheduler\-plugin** add\-on in the cluster that meets the requirements, or specify the following parameters to enable load\-aware scheduling when you update the add\-on configurations by calling the [UpdateAddonConfig](https://docs.byteplus.com/en/docs/vke/UpdateAddonConfig) API:

   * Set the **LoadAwareSchedulingEnabled** parameter to **true**.

   * Set the **Scope** sub\-parameter of the **LoadAwareSchedulingConfig** parameter to **pod**.


<span id=".5q2l6aqk5LqM77ya5Li6LXBvZC3mt7vliqDlkK_nlKjotJ_ovb3mhJ_nn6XosIPluqbnmoQtYW5ub3RhdGlvbg=="></span>
### Step 2: Add an annotation that enables load\-aware scheduling for a pod

Add annotations to a pod to indicate whether to enable load\-aware scheduling for the pod based on the actual load of nodes.


|Annotation key |Annotation sample value |Description |
|---|---|---|
|vke.volcengine.com/load\-aware\-enabled |true |Whether to enable load\-aware scheduling. Valid values:<br><br><br>* **true**<br><br>* **false** |


The following YAML file serves as an example.

```yaml
apiVersion: v1
kind: Pod
metadata:
  annotations:
    vke.volcengine.com/load-aware-enabled: "true"  # Whether to enable load-aware scheduling.
  labels:
    app: load-aware-pod
  name: load-aware-pod  # The pod name.
  namespace: default  # The namespace to which the pod belongs.
spec:
  containers:
    - name: hello-pod # The container name.
      image: nginx:latest # The address of the container image.
      ports:
        - containerPort: 8080 # The container port.
```


<span id=".5L2_55So56S65L6L"></span>
## Examples

This topic uses a cluster with three nodes (each with 4 cores and 16 GiB of memory) as an example. It compares node load differences before and after load\-aware scheduling is used. It also introduces methods of scheduling pods to lower\-load nodes for load balancing.

<span id=".5pyq5L2_55So6LSf6L295oSf55-l6LCD5bqm"></span>
### When load\-aware scheduling is not used


1. Connect to the target cluster. For details, see [Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

2. Create the YAML file of the workload. The following code of the sample file `stress-test.yaml` shows how to create a Deployment.

   ```yaml
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: stress-test # The name of the Deployment.
     namespace: default # The namespace of the Deployment.
     labels:
       app: stress-test
   spec:
     replicas: 2 # The number of pods.
     selector:
       matchLabels:
         app: stress-test
     template:
       metadata:
         name: stress-test
         labels:
           app: stress-test
       spec:
         containers:
           - args:
               - '--vm'
               - '3'
               - '--vm-bytes'
               - '1800M'
               - '-c'
               - '3'
               - '--vm-hang'
               - '10'
             command:
               - stress
             image: polinux/stress
             imagePullPolicy: Always
             name: stress
             resources:
               limits:
                 cpu: '3'
                 memory: 6Gi
               requests:
                 cpu: '3'
                 memory: 6Gi
         restartPolicy: Always
   ```
   

3. Execute the following command to create the workload.

   ```bash
   kubectl apply -f stress-test.yaml
   ```
   

4. View the nodes to which the pods of the workload created in the previous step are scheduled.

   ```bash
   kubectl get pods -o wide
   ```
   

   The expected response is as follows, which indicates that the pods have been scheduled to the `192.168.1.5` and `192.168.1.3` nodes.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_69a067db909108e36c1ac01e250b1d9e.png) </span>

5. View the resource usage of nodes.

   ```bash
   kubectl top nodes
   ```
   

   The expected response is as follows, which indicates that the nodes `192.168.1.5` and `192.168.1.3` are high\-load nodes.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c5f5e605bd3faf011d6e64c5c07a0492.png) </span>


<span id=".5L2_55So6LSf6L295oSf55-l6LCD5bqm"></span>
### When load\-aware scheduling is used

The preceding result indicates that load balancing among nodes is not achieved. To schedule as many pods as possible to the `192.168.1.4` node in subsequent operations, add annotations to the pods to enable load\-aware scheduling based on the following descriptions.


1. Create a workload with six pods with load\-aware scheduling enabled and request 500 mCore of CPU for each pod.

   ```yaml
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: nginx # The name of the Deployment.
       namespace: default # The namespace of the Deployment.
     labels:
       app: nginx
   spec:
     replicas: 6
     selector:
       matchLabels:
         app: nginx
     template:
       metadata:
         annotations:
           vke.volcengine.com/load-aware-enabled: "true" # Enable load-aware scheduling.
         name: nginx
         labels:
           app: nginx
       spec:
         containers:
         - name: nginx-cantainer
           image: nginx:latest # The container image address and tag of the pod.
           resources:
             limits:
               cpu: 500m # The upper limit of the container CPU.
             requests:
               cpu: 500m # The container CPU request.
   ```
   

2. View the nodes on which the pods of the workload created in the previous step are scheduled.

   ```bash
   kubectl get pods -owide
   ```
   

   The expected response is as follows, which indicates that all six pods have been scheduled to the `192.168.1.4` node.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b0a196d2d862bcdb84d293b373121934.png) </span>

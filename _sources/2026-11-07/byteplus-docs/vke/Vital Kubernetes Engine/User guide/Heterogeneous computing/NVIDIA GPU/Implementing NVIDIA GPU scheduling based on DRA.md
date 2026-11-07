---
title: "Implementing NVIDIA GPU scheduling based on DRA"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Implementing_NVIDIA_GPU_scheduling_based_on_DRA"
---

Dynamic resource allocation (DRA) is a declarative resource management mechanism provided by Kubernetes. DRA is designed to address complex resource control challenges in scenarios such as fine\-grained allocation, topology\-aware scheduling, and cross\-node sharing for GPUs and other high\-performance hardware. This article details the technical working principles of DRA, its differences from traditional scheduling mechanisms, and relevant configuration methods.

<span id="A8LLvNlz"></span>
## Background

<span id="zQUUwArA"></span>
### DRA overview

DRA is a Kubernetes resource management framework. In VKE, it allows workloads to request and share hardware resources (such as GPUs and RDMA network interfaces) declaratively. By abstracting hardware resources into programmable API objects, DRA decouples resource management logic from the built\-in kubelet logic and migrates it to third\-party drivers. DRA significantly enhances resource allocation precision and utilization, particularly in advanced scenarios that require cross\-node unified GPU memory addressing, GPU sharing, and high\-performance network alignment, delivering greater scheduling flexibility.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For more details on DRA, see the <a href="https://kubernetes.io/docs/concepts/scheduling-eviction/dynamic-resource-allocation/">official documentation</a>.</div>


<span id="Gz63PZtn"></span>
### Scheduling mechanism

Compared with traditional Device Plugin scheduling, DRA differs significantly in resource description and scheduling logic. The following table provides details.


|Scheduling mechanism |Resource description |Scheduling decision |
|---|---|---|
|Device Plugin |Uses an "integer counting" model (for example, `nvidia.com/gpu: 1`), which can only describe the quantity of resources and cannot express hardware memory capacity, architecture version, or topology connections. |The scheduler performs node pre\-selection only based on the quantity, while the specific device binding is completed on the kubelet side. This can easily lead to inconsistencies between scheduling decisions and the actual hardware topology. |
|DRA |Adopts an "attribute\-based declaration" model. In this scheduling mechanism, structured device properties are published through a ResourceSlice. You can use Common Expression Language (CEL) expressions to precisely filter devices and describe complex hardware characteristics. |The scheduler can access the complete list of hardware attributes (ResourceSlice) during the pre\-selection phase and directly participate in the specific device allocation decisions. This ensures that Pods can be precisely allocated to hardware combinations that meet topology constraints. |


<span id="MtjTr4EM"></span>
### Resource objects

DRA uses resource objects such as ResourceClaims to detect, request, and allocate underlying shared hardware resources. The resource objects involved in this topic are described in the table below.


|Resource Object |Resource description |
|---|---|
|ResourceSlice |A cluster\-level resource object, published by the DRA driver on each node based on the results of the underlying hardware detection. It acts as an "attribute manifest" for hardware capabilities, recording metadata of each specific device on the node (such as device ID, NUMA affinity, and PCIe topology location). During the scheduling phase, a ResourceSlice provides the kube\-scheduler with a full view of hardware status and thereby enables the kube\-scheduler to globally evaluate which devices meet the requirements of the workload. |
|ResourceClaimTemplate |An API object that describes resource needs. It defines the expected specifications of the resource requests, including the referenced device category (DeviceClass) and the allocation mode (for example, full allocation or on\-demand creation). It does not represent actual resource consumption, but serves as an instruction template for generating specific ResourceClaims. You can use templates to define generic hardware configuration standards for multiple workloads to reference, ensuring consistency in storage and computing resource requests. |
|ResourceClaim |A key object that records the resource allocation status and serves as the logical link between the Pod and physical resources. It carries the transition state from "requirement declaration" to "physical binding". When a Pod is created, the system generates a ResourceClaim based on the template. Once scheduling is complete, information about the specific allocated device (such as device ID) is written into the status of the ResourceClaim, which locks the resource. The ResourceClaim manages the entire lifecycle of the resource and ensures that the resources are held as expected during Pod runtime. It triggers the resource release or reclamation process according to the policy after the Pod is destroyed. |


<span id="KKxK47rz"></span>
## Usage limits


* Clusters do not support automatic DRA configuration. To use DRA, manually configure it by following the configuration methods described in this topic.

* When nodes in the cluster use DRA, the following GPU features cannot be used:

   * NVIDIA GPU scheduling. For details, see [Configuring NVIDIA GPU scheduling](https://docs.byteplus.com/en/docs/vke/NVIDIA-GPU-scheduling).

   * mGPU scheduling. For details, see [Configuring mGPU scheduling](https://docs.byteplus.com/en/docs/vke/Using-mGPU).


<span id="092f8hCf"></span>
## Prerequisites


* You have created a VKE cluster with the Kubernetes version being v1.34 or later.

* The kubectl tool has been installed in the local environment. For details, see [Installing and setting up kubectl](https://kubernetes.io/docs/tasks/tools/).


<span id="UjG2uzuU"></span>
## Procedure

<span id="EDDMgtSE"></span>
### Step 1: Create a GPU node pool


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. In the cluster list, click the name of the target cluster to open the cluster management page.

3. In the left navigation bar, click **Node pool**.

4. On the Node pool page, click **Create node pool** to create a node pool that meets your requirements. For parameter details, see [Creating node pools](https://docs.byteplus.com/en/docs/vke/Creating-a-NodePool).   

   * For **Instance type**, select **GPU Accelerated** to add nodes with GPUs to the cluster. 

   * For the **Container runtime** configuration item, set the containerd version to 2.1 or later.

   * In the **Advanced settings** section, click **Add node labels** to add the following labels to the node pool.

      * Set the label key as `vke.node.gpu.schedule` and the label value to `nvidia-dra`. This enables DRA\-based GPU scheduling on nodes in this node pool.

      * Set the label key to `nvidia.com/gpu.present` and the label value to `true`. This indicates that the DRA driver runs on nodes in this node pool.

5. Configure other parameters. Then, click **Confirm** to create the node pool.


<span id="EGIpINmL"></span>
### Step 2: Install the NVIDIA DRA driver


1. Connect to the target cluster using kubectl. For details, see [Connecting to a cluster](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

2. Run the following commands to add the NVIDIA Helm repository.

   ```Bash
   helm repo add nvidia https://helm.ngc.nvidia.com/nvidia
   helm repo update
   ```
   

3. Run the following command to install the NVIDIA DRA driver. This example shows how to install version 25.8.1 of the driver.

   ```Bash
   helm install nvidia-dra-driver-gpu nvidia/nvidia-dra-driver-gpu \
       --version="25.8.1" \
       --create-namespace \
       --namespace nvidia-dra-driver-gpu \
       --set controller.affinity=null \
       --set gpuResourcesEnabledOverride=true \
       --set resources.computeDomains.enabled=false \
       --set "kubeletPlugin.affinity.nodeAffinity.requiredDuringSchedulingIgnoredDuringExecution.nodeSelectorTerms[0].matchExpressions[0].key=vke.node.gpu.schedule" \
       --set "kubeletPlugin.affinity.nodeAffinity.requiredDuringSchedulingIgnoredDuringExecution.nodeSelectorTerms[0].matchExpressions[0].operator=In" \
       --set "kubeletPlugin.affinity.nodeAffinity.requiredDuringSchedulingIgnoredDuringExecution.nodeSelectorTerms[0].matchExpressions[0].values[0]=nvidia-dra"
   ```
   


<span id="wgDofhrB"></span>
### Step 3: Confirm the NVIDIA DRA environment

After you install the NVIDIA DRA driver, check whether it is running normally in the cluster and whether GPU resources have been reported to the cluster.


1. Run the following command to check DRA\-related API resources in the cluster.

   ```Bash
   kubectl api-resources | grep resource.k8s.io
   ```
   

   The expected response is similar to the following one.

   ```Bash
   deviceclasses                                              resource.k8s.io/v1                           false        DeviceClass
   resourceclaims                                             resource.k8s.io/v1                           true         ResourceClaim
   resourceclaimtemplates                                     resource.k8s.io/v1                           true         ResourceClaimTemplate
   resourceslices                                             resource.k8s.io/v1                           false        ResourceSlice
   ```
   

2. Run the following command to check the information about the NVIDIA DRA Pod.

   ```Bash
   kubectl get pods -n nvidia-dra-driver-gpu -o wide
   ```
   

   The expected response is similar to the following one, which indicates that the Pod has been deployed and is `running`.

   ```Bash
   NAME                                         READY   STATUS    RESTARTS   AGE   IP              NODE          NOMINATED NODE   READINESS GATES
   nvidia-dra-driver-gpu-kubelet-plugin-mq***   1/1     Running   0          71s   192.168.2.253   192.168.2.8   <none>           <none>
   ```
   

3. Run the following command to check the available NVIDIA DRA resources in the cluster.

   ```Bash
   kubectl get deviceclass,resourceslice
   ```
   

   The expected response is similar to the following one.

   ```Bash
   NAME                                         AGE
   deviceclass.resource.k8s.io/gpu.nvidia.com   2m51s
   deviceclass.resource.k8s.io/mig.nvidia.com   2m51s
   
   NAME                                                             NODE          DRIVER           POOL          AGE
   resourceslice.resource.k8s.io/192.168.2.8-gpu.nvidia.com-tn***   192.168.2.8   gpu.nvidia.com   192.168.2.8   2m31s
   ```
   

4. Run the following command to query the resources reported by NVIDIA DRA nodes.

   ```Bash
   kubectl get resourceslice -o yaml 
   ```
   

   The expected response is similar to the following one.

   ```YAML
   apiVersion: v1
   items:
   - apiVersion: resource.k8s.io/v1
     kind: ResourceSlice
     metadata:
       creationTimestamp: "2026-04-17T06:33:10Z"
       generateName: 192.168.2.8-gpu.nvidia.com-
       generation: 1
       name: 192.168.2.8-gpu.nvidia.com-t***
       ownerReferences:
       - apiVersion: v1
         controller: true
         kind: Node
         name: 192.168.2.8
         uid: e62793a4-d8fe-4a11-bd56-60e***
       resourceVersion: "3880"
       uid: db0ea1ae-9f6d-43d5-8ee7-7f23f***
     spec:
       devices:
       - attributes:
           architecture:
             string: Ampere
           brand:
             string: Nvidia
           cudaComputeCapability:
             version: 8.0.0
           cudaDriverVersion:
             version: 12.2.0
           driverVersion:
             version: 535.129.3
           pcieBusID:
             string: 0000:65:01.0
           productName:
             string: NVIDIA A30
           resource.kubernetes.io/pcieRoot:
             string: pci0000:64
           type:
             string: gpu
           uuid:
             string: GPU-c8133a35-9d03-a6b2-31dd-26***
         capacity:
           memory:
             value: 24Gi
         name: gpu-0
       driver: gpu.nvidia.com
       nodeName: 192.168.2.8
       pool:
         generation: 1
         name: 192.168.2.8
         resourceSliceCount: 1
   kind: List
   metadata:
     resourceVersion: ""
   ```
   

5. Run the following command to verify that node resources are correct and that `nvidia.com/gpu` resources are no longer displayed. In the command, `${dra-node-name}` is the node name, for example, `192.168.2.8`.

   ```Bash
   kubectl describe node ${dra-node-name} | grep -E 'nvidia\.com/gpu|Capacity|Allocatable'
   ```
   

   The expected response is similar to the following one, where `Capacity` and `Allocatable` should be empty.

   ```Bash
                       nvidia.com/gpu.present=true
   Capacity: # Capacity and Allocatable are expected to be empty.
   Allocatable:
     Warning  InvalidDiskCapacity      8m43s                  kubelet                invalid capacity 0 on image filesystem
     Normal   NodeAllocatableEnforced  8m43s                  kubelet                Updated Node Allocatable limit across pods
   ```
   


<span id="6IhbqJ2M"></span>
## Validating results

After you have installed the NVIDIA DRA driver in the cluster, you can create a resource claim (ResourceClaim) through the ResourceClaimTemplate resource to enable workloads to request and use GPU resources based on DRA.

<span id="tFWKviGl"></span>
### Create a ResourceClaimTemplate


1. Create a YAML file for the ResourceClaimTemplate. The following `resource-claim-template-single-gpu.yaml` file serves as an example:

   ```YAML
   apiVersion: resource.k8s.io/v1
   kind: ResourceClaimTemplate
   metadata:
     name: single-gpu # Resource name, serving as the globally unique identifier of the resource.
   spec:
     spec:
       devices:
         requests:
         - name: gpu # Local identifier of the resource. The Pod references this name to mount the physical GPU allocated by the system into its own runtime environment.
           exactly:
             allocationMode: ExactCount # Resource allocation mode. In this example, the scheduler locks the corresponding hardware resources in the resource pool of the physical node according to a fixed quantity.
             deviceClassName: gpu.nvidia.com # Specify the underlying driver to process this request.
             count: 1 # The metric for locking physical resources. In this example, the system needs to allocate one complete GPU exclusively on the node for the bound workload.
   ```
   

2. Run the following command to create the ResourceClaimTemplate.

   ```Bash
   kubectl apply -f resource-claim-template-single-gpu.yaml
   ```
   

3. Run the following command to check the status of the created ResourceClaimTemplate resource.

   ```Bash
   kubectl get resourceclaimtemplates
   ```
   

   The expected response is similar to the following one.

   ```Bash
   NAME         AGE
   single-gpu   12s
   ```
   


<span id="W2b3MDIn"></span>
### Deploy workloads that use DRA


1. Create a workload that uses the ResourceClaimTemplate to request resources. This example demonstrates how to create a Deployment using the following `resource-claim-template-pod.yaml` manifest:

   ```YAML
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: gpu-test
   spec:
     replicas: 1
     selector:
       matchLabels:
         app: gpu-test
     template:
       metadata:
         labels:
           app: gpu-test
       spec:
         containers:
         - image: doc-cn-beijing.cr.volces.com/vke/gpu-burn:1.0
           name: test
           args:
           - -c
           - nvidia-smi -L; sleep 600
           command:
           - sh
           resources:
             claims:
             - name: gpu
         terminationGracePeriodSeconds: 3
         resourceClaims:
         - name: gpu # The local resource identifier specified in the ResourceClaimTemplate.
           resourceClaimTemplateName: single-gpu # The ResourceClaimTemplate name.
   ```
   

2. Run the following command to create the workload.

   ```Bash
   kubectl apply -f resource-claim-template-pod.yaml
   ```
   

3. Run the following command to view the Pod status of the workload.

   ```Bash
   kubectl get pods -o wide
   ```
   

   If the response is similar to the following one, the workload has been deployed, and its Pod status is `Running`.

   ```Bash
   NAME                  READY   STATUS    RESTARTS   AGE   IP              NODE          NOMINATED NODE   READINESS GATES
   gpu-test-5c47d94***   1/1     Running   0          96s   192.168.2.254   192.168.2.8   <none>           <none>
   ```
   

4. Run the following command to view the ResourceClaims associated with the workload.

   ```Bash
   kubectl get resourceclaims
   ```
   

   The expected response is similar to the following one.

   ```Bash
   NAME                        STATE                AGE
   gpu-test-5c47d94bf9-fb***   allocated,reserved   3m18s
   ```
   

&nbsp;

5. Run the following command to view the details of the ResourceClaim resource.

   ```Bash
   kubectl describe resourceclaims
   ```
   

   The expected response is similar to the following one, including details of devices allocated to the Pod.

   ```YAML
   Name:         gpu-test-5c47d94***
   Namespace:    default
   Labels:       <none>
   Annotations:  resource.kubernetes.io/pod-claim-name: gpu
   API Version:  resource.k8s.io/v1
   Kind:         ResourceClaim
   Metadata:
     Creation Timestamp:  2026-04-17T06:41:51Z
     Finalizers:
       resource.kubernetes.io/delete-protection
     Generate Name:  gpu-test-5c47d94***
     Owner References:
       API Version:           v1
       Block Owner Deletion:  true
       Controller:            true
       Kind:                  Pod
       Name:                  gpu-test-5c47d94***
       UID:                   691d19b1-5ca8-40c***
     Resource Version:        6101
     UID:                     85fbff51-0247-43***
   Spec:
     Devices:
       Requests:
         Exactly:
           Allocation Mode:    ExactCount
           Count:              1
           Device Class Name:  gpu.nvidia.com
         Name:                 gpu
   Status:
     Allocation:
       Devices:
         Results:
           Device:   gpu-0
           Driver:   gpu.nvidia.com
           Pool:     192.168.2.8
           Request:  gpu
       Node Selector:
         Node Selector Terms:
           Match Fields:
             Key:       metadata.name
             Operator:  In
             Values:
               192.168.2.8
     Reserved For:
       Name:      gpu-test-5c47d94***
       Resource:  pods
       UID:       691d19b1-5ca8-40c***
   Events:        <none>
   ```
   

6. Run the following command to view the Pod logs of the workload.

   ```Bash
   kubectl logs deployment/gpu-test --all-pods=true
   ```
   

   The expected response is similar to the following one.

   ```Bash
   [pod/gpu-test-5c47d94***/test] GPU 0: NVIDIA A30 (UUID: GPU-c8133a35-9d0***)
   ```

---
title: "Elastic network interface dedicated to a pod with Trunk ENI"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using-Trunk-ENI-to-enable-the-exclusive-ENI-mode-for-pods"
---

In large\-scale scenarios, dedicated ENIs (elastic network interfaces) improve the network performance between pods and let you bind a separate security group to to the ENI of each pod to meet pod\-level network isolation requirements. This topic describes how to configure a dedicated ENI for a pod.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">[<a href="https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features"><strong>Beta·Apply for Trial</strong></a>]: This feature is currently in beta. Submit an application to use it.</div>


<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

The VKE supports enabling Trunk ENI mode in clusters using the VPC\-CNI network model. On Trunk ENI nodes, exclusive ENI resources are provided for pods. In addition, subnets and security groups can be specified for pods.

In the scenarios of large\-scale applications, the dedicated ENI (elastic network interface) can provide better communication performance between pods. Meanwhile, it allows each pod to be bound to a security group, satisfying the need for network isolation between pods. Trunk ENI has the following features:


* It can be exclusively assigned to a pod, providing security\-group\-based traffic isolation at the network\-interface level.

* It allows IPs from custom subnets assigned to pods, meeting the requirement for fine\-grained traffic isolation.


The following CRD objects are involved when configuring dedicated ENI for pods:


* **VPCENIDefinition object**: Used to define the VPC IPAM configuration of the ENI. including VPC ID, IP allocation mode, security groups, and subnet ID.

* **PodNetworkDefinition object**: Used to define the network configuration of the pod, including the information of IPAM  and pod selection.


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage limits


* Only supported in clusters using the VPC\-CNI network model.

* Once Trunk ENI is enabled, each node reserves one ENI as the Trunk interface. As a result, the number of shared IPs available to pods is reduced accordingly.

* With Trunk ENI, network interfaces cannot be pre\-allocated. As a result, creating and deleting network resources takes longer than when using shared IPs.

* The pod name can be up to 63 characters in length.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5Yib5bu66ZuG576k5bm26YWN572uLXRydW5rLWVuaQ=="></span>
### Step 1: Enable Trunk ENI


<Tabs>
<Tab zoneid="C02V6APA0O" title="Enable when creating clusters">
<TabTitle>Enable when creating clusters</TabTitle>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This topic only covers the key configurations for enabling Trunk ENI when creating a cluster, including installing the vpc\-cni\-controlplane add\-on. For more details about creating a cluster, see <a href="https://docs.byteplus.com/en/docs/vke/Creating-a-cluster">Creating clusters</a>.</div>



1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. On the cluster management page, select **Cluster** in the left navigation bar.

3. Click **Create cluster** in the upper left corner to go to the **Cluster configuration** page. Finish the configurations on the page and click **Next: Node pool configuration** in the lower\-right corner.

   The key parameters are as follows. Configure other parameters as needed.

   
   |**Parameter** |**Description** |
   |---|---|
   |Network model |Select a Container Network Interface (CNI) for the cluster. In this case, **VPC\-CNI** is required. |
   |Trunk ENI |Disabled by default. After enabling this option, Trunk ENI can be used to support exclusive ENIs for pods, providing advanced capabilities such as binding security groups to pods and scheduling pods to specified subnets. You need to **enable** this configuration in this scenario. |
   

4. Finish the necessary configurations on the **Node pool configuration** page, and click **Next: Addon configuration** in the lower right corner.

5. The vpc\-cni\-controlplane add\-on is selected by default on the page. You can select more add\-ons if necessary and then click **Next: Configuration confirmation** to finish.

6. Ensure that all cluster information and billing details are correct. Read the "VKE Dedicated Service Terms" and click the checkbox. Then click **Confirm** on the page to start creating the cluster.


</Tab>
<Tab zoneid="rXs9GiaXDf" title="Enable for the existing clusters">
<TabTitle>Enable for the existing clusters</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">To enable Trunk ENI in an existing cluster, ensure the cluster meets the following conditions:</div>



* <div data-tips="true" data-tips-type="default">When creating a cluster, set the network mode to <strong>Shared ENI</strong>.</div>


* <div data-tips="true" data-tips-type="default">The vpc\-cni add\-on has been upgraded to 1.8.10 or later. For details, see <a href="https://docs.byteplus.com/en/docs/vke/vpc-cni-add-on">Upgrading vpc\-cni add\-on</a>.</div>


* <div data-tips="true" data-tips-type="default">The vpc\-cni\-controlplane addon has been installed and upgraded to v1.4.5 or later. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Installing-an-add-on">Installing add\-ons</a>.</div>


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. On the right page, click the target cluster name to open the management page of this cluster.

3. Click **Overview** in the left navigation bar, and then select the **Overview** tab on the right page.

4. In **Cluster network configuration** section, check **Enable Trunk ENI**. In the pop\-up window, click **Confirm**.

5. In the left navigation bar of the cluster management page, click **Addons**. On the page that appears, click the **Network** tab.

6. Locate the vpc\-cni add\-on, hover the mouse over it, and click **Configuration**.

7. There is no need to make any changes to the add\-on configuration. Click **Confirm**.

   * If the vpc\-cni add\-on is v1.9.6 or later, the system will automatically restart the add\-on after you click Confirm to apply the configuration.

   * If the vpc\-cni add\-on version is earlier than v1.9.6, you need to [connect to the cluster using kubectl](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster) and execute the following command to perform a rolling restart of the Cello pods to apply the configuration.

      ```Bash
      kubectl rollout restart daemonset cello -n kube-system
      ```
      

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">To ensure business stability, we recommend performing the above add\-on restart operation during low\-peak hours.      </div>
      


</Tab>
</Tabs>


<span id=".5q2l6aqk5LqM77ya5Yib5bu6LXZwY2VuaWRlZmluaXRpb24t5a-56LGh"></span>
### Step 2: Create a VPCENIDefinition object

Create a VPCENIDefinition object. The configuration example and key parameter description are as follows:

```YAML
apiVersion: network.volcengine.com/v1beta1
kind: VPCENIDefinition
metadata:
  name: vpceni-default # custom VPCENIDefinition object name
  namespace: default
spec:
  vpcID: vpc-rr1s2d*** # Required. The ID of the VPC (Virtual Private Cloud) to which the cluster belongs.
  allocateType:
    type: Elastic # Required, IP allocation mode, Elastic means elastic IP
  securityGroupIDs: 
  - sg-rrhowl*** # Required, the default security group for pods
  subnetIDs:
  - subnet-13f64*** # (Required) Specify the ID of a subnet in the VPC. They can be some or all of the subnets assigned to cluster pods, or subnets in the specified VPC that are not assigned to any pods.
  - subnet-13fy9***
```


The parameters under `spec` are listed below.


|Parameter ||Required |Description |
|---|---|---|---|
|vpcID |\- |Yes |The ID of the VPC (Virtual Private Cloud) to which the cluster belongs. |
|allocateType |type |Yes |IP allocation mode. In this example, it is set to **Elastic**, which represents the elastic IP policy. The IP resources are released as soon as pods are deleted. |
|securityGroupIDs |\- |Yes |Pod security group ID. Multiple security groups can be configured and will be effective simultaneously. |
|subnetIDs |\- |Yes |Specify one or more subnet IDs within the VPC. They can be some or all of the subnets assigned to cluster pods, or subnets in the specified VPC that are not assigned to any pods. |


<span id=".5q2l6aqk5LiJ77ya5Yib5bu6LXBvZG5ldHdvcmtkZWZpbml0aW9uLeWvueixoQ=="></span>
### Step 3: Create a PodNetworkDefinition object

Create a PodNetworkDefinition object. Configuration examples and key parameter descriptions are as follows:

```YAML
apiVersion: network.volcengine.com/v1beta1
kind: PodNetworkDefinition
metadata:
  name: vpceni1 # Custom PodNetworkDefinition object name
  namespace: default # the namespace to which the PodNetworkDefinition object belongs
spec:
  ipResource:
    name: vpceni-default # Required, custom VPCENIDefinition object name, consistent with the name in the previous step
    type: VPCENIDefinition # Required, specify the resource type, fixed value
  selectors:
  - podSelector:
      matchLabels:
        foo: bar # Custom labels to match specified pods, enabling exclusive ENIs for pods.
    namespaceSelector:
      matchLabels:
        foo: bar # Custom labels to match specified namespaces, providing exclusive ENI capability for all pods within the namespace.
```


The parameters under `spec` are listed below.


|Parameter ||Required |Description |
|---|---|---|---|
|ipResource |name |Yes |Specify a name for the network resource, which needs to be consistent with the name of the VPCENIDefinition object. |
||type |Yes |Specify the type of network resource. It needs to be `VPCENIDefinition` in this case. |
|selectors |podSelector |No |Specify labels for matching Pods. Matching Pods will use the network resources specified by `ipResource` during Pod creation. |
||namespaceSelector |No |Specify labels for selecting namespaces. All Pods in the matching namespaces will use the network resources specified by `ipResource` during Pod creation. |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning"><code>podSelector</code> and <code>namespaceSelector</code> are optional parameters that can be configured as needed. At least one of them must be configured so that the feature can take effect.</div>


* <div data-tips="true" data-tips-type="warning">The <code>selectors</code> is a list that may contain multiple namespaces and pod labels. Each individual member in the list can have labels for both namespaces and pods simultaneously.</div>


* <div data-tips="true" data-tips-type="warning">Within each list member, the selectors are combined using AND logic. If both a namespace selector and a pod selector are configured, an ENI is assigned to a pod only when both the pod labels and the labels of its namespace match the corresponding selectors.</div>


* <div data-tips="true" data-tips-type="warning">If the list contains multiple members, the members are combined using OR logic. A pod that matches the selectors of any member in the list is assigned an ENI.</div>



<span id=".5q2l6aqk5Zub77ya6YWN572uLXBvZC3ni6zljaDlvLnmgKfnvZHljaE="></span>
### Step 4: Configure a dedicated ENI for a pod

There are several methods to do it:


* **Namespace label**: Use namespace labels to assign ENIs to all the pods under the namespaces.

* **Pod label**: Use pod labels to assign ENIs to specific pods.



<Tabs>
<Tab zoneid="WR9WHqHcpK" title="Configuring namespace labels">
<TabTitle>Configuring namespace labels</TabTitle>

You can add the label defined in the PodNetworkDefinition object (e.g., `foo: bar`) when creating a namespace, so that all the pods in that namespace can have dedicated ENIs The example is as follows:

```YAML
apiVersion: v1
kind: Namespace
metadata:
  name: namespace-demo # The name of the namespace
  labels:
    foo: bar  # Specify the label defined in the PodNetworkDefinition object
```



</Tab>
<Tab zoneid="dJOvaDGJTf" title="Creating pods and adding labels">
<TabTitle>Creating pods and adding labels</TabTitle>

You can add the label defined in the PodNetworkDefinition object (e.g., `foo: bar`) when creating a pod, so that the pod has a dedicated ENI. The example is as follows:

```YAML
apiVersion: v1
kind: Pod
metadata:
  name: pod-demo # Pod name
  namespace: default # the namespace to which the pod belongs
  labels:
    foo: bar  # Specify the label defined in the PodNetworkDefinition object
spec:
  containers:
    - name: hello-pod 
      image: doc-cn-beijing.cr.volces.com/vke/nginx-demo:v1.0
      ports:
        - containerPort: 80
```



</Tab>
<Tab zoneid="gW4q693Y8a" title="Creating workloads and adding labels">
<TabTitle>Creating workloads and adding labels</TabTitle>

You can add the label defined in the PodNetworkDefinition object (e.g., `foo: bar`) when creating a pod, so that the pod has a dedicated ENI. Here is an example of stateless workload:

```YAML
apiVersion: apps/v1
kind: Deployment
metadata:
  name: deployment-demo # Workload name
  namespace: default # Namespace to which the workload belongs
spec:
  replicas: 1 
  selector:
    matchLabels:
      foo: bar
  template:
    metadata:
      labels:
        foo: bar
    spec:
      containers:
      - name: nginx 
        image: doc-cn-beijing.cr.volces.com/vke/nginx-demo:v1.0
        ports:
        - containerPort: 80 
```



</Tab>
</Tabs>


<span id=".57uT5p6c6aqM6K-B"></span>
## Validating results

When the configurations are saved, the system adds necessary annotations (including ENI request/limit) to pods matching the labels in the PodNetworkDefinition object. It then relocates these pods to Trunk\-enabled nodes and provides them with dedicated ENIs.

As shown in the figure below, the annotation `k8s.volcengine.com/network-status` added automatically by the system indicates that the pod already has a dedicated ENI.

The information about ENI can be found in the **Network interface** tab on the pod details page.

&nbsp;

&nbsp;

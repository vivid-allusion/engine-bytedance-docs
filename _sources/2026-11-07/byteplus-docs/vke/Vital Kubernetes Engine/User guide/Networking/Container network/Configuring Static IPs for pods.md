---
title: "Configuring Static IPs for pods"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Configuring-a-fixed-IP-address-for-a-pod"
---

Vital Kubernetes Engine allows static IPs for pods to address requirements such as IP\-based access control, service registration, service discovery, and audit logging. This topic describes how to configure static IPs for pods.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">[<a href="https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features">Beta \- apply for trial</a>]: This feature is currently in beta. Submit an application to use it.</div>


<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

Vital Kubernetes Engine allows the Trunk ENI mode enabled when creating clusters with the VPC\-CNI network model. The pods running on a Trunk ENI node can have ENI (elastic network interface) of their own with the specified subnets and security groups.

A pod can be assigned a static IP if it has a dedicated network interface. It facilitates configurations such as access control, service registration, service discovery, and audit logging based on the IP of a pod. Here are the CRD objects to be used when configuring static IPs:


* **VPCENIDefinition object**: This object defines the VPC IPAM configuration of the ENI, including VPC ID, IP allocation mode, security groups, and subnet ID.

* **PodNetworkDefinition object**: This object is used to define the network configuration of a pod, including IPAM and Pod selector.


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage limits


* Trunk ENI is applicable only to clusters using the VPC\-CNI network model.

* The pod name must not exceed 63 characters.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The vpc\-cni add\-on has been installed and upgraded to v1.6.0 or later.

* The vpc\-cni\-controlplane add\-on has been installed and upgraded to v1.6.0 or later.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For details about the versions and upgrading add\-ons, see <a href="https://docs.byteplus.com/en/docs/vke/Network-add-ons">Add\-on release notes</a> and <a href="https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on">Upgrading add\-ons</a>.</div>


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id="1tSZb6mF"></span>
### Step 1: Enable Trunk ENI


<Tabs>
<Tab zoneid="0eKlFo3e" title="Enable when creating clusters">
<TabTitle>Enable when creating clusters</TabTitle>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This topic only covers the key configurations for enabling Trunk ENI when creating a cluster, including installing the vpc\-cni\-controlplane add\-on. For more details about creating a cluster, see <a href="https://docs.byteplus.com/en/docs/vke/Creating-a-cluster">Creating clusters</a>.</div>



1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. On the cluster management page, select **Cluster** in the left navigation bar.

3. Click **Create cluster** in the upper left corner to go to the **Cluster configuration** page. Finish the configurations on the page and click **Next: Node pool configuration** in the lower\-right corner.

   The key parameters are as follows. Other parameters can be configured as needed.

   
   |**Parameter** |**Description** |
   |---|---|
   |Network model |Select a Container Network Interface (CNI) for the cluster. In this case, **VPC\-CNI** is required. |
   |Trunk ENI |Disabled by default. After enabling this option, Trunk ENI can be used to support exclusive ENIs for pods, providing advanced capabilities such as binding security groups to pods and scheduling pods to specified subnets. You need to **enable** this configuration in this scenario. |
   

4. Finish the necessary configurations on the **Node pool configuration** page, and click **Next: Addon configuration** in the lower right corner.

5. The vpc\-cni\-controlplane add\-on is selected by default on the page. You can select more add\-ons if necessary and then click **Next: Configuration confirmation** to finish.

6. After confirming that the cluster information and billing details are correct, read the Vital Kubernetes Engine Specific Terms of Service, select the checkbox to accept them, and then click Confirm to start creating the cluster.


</Tab>
<Tab zoneid="qnYqbzXI" title="Enable for existing clusters">
<TabTitle>Enable for existing clusters</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">To enable Trunk ENI in an existing cluster, ensure that the cluster meets the following conditions:</div>



* <div data-tips="true" data-tips-type="default">When creating a cluster, set the network mode to <strong>Shared ENI</strong>.</div>


* <div data-tips="true" data-tips-type="default">The vpc\-cni add\-on has been upgraded to 1.8.10 or later. For details, see <a href="https://docs.byteplus.com/en/docs/vke/vpc-cni-add-on">Upgrading vpc\-cni add\-on</a>.</div>


* <div data-tips="true" data-tips-type="default">The vpc\-cni\-controlplane add\-on has been installed and upgraded to v1.4.5 or later. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Installing-an-add-on">Installing add\-ons</a>.</div>


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. In the right part of the page, click the target cluster name to open the management page of this cluster.

3. In the left navigation bar, click **Overview**, and then select the **Overview** tab on the right page.

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


<span id=".5q2l6aqk5LqM77ya5byA5ZCvLXBvZC3lm7rlrpotaXAt5Yqf6IO9"></span>
### Step 2: Enable static IP for pods


1. Click the cluster name you just created to enter the cluster management page.

2. Select **Addons** in the left navigation bar.

3. On the **Network** tab, click **Configuration** on the vpc\-cni\-controlplane add\-on and enable **Static IP for pods** in the pop\-up window.

4. Click **Confirm** to finish.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If this option does not appear in your cluster or is grayed out and cannot be configured, it indicates that Trunk ENI is not enabled in the cluster or the add\-on is not at the required version. For more information, see the previous content.</div>


<span id=".5q2l6aqk5LiJ77ya5Yib5bu6LXZwY2VuaWRlZmluaXRpb24t5a-56LGh"></span>
### Step 3: Create a VPCENIDefinition object

Create a VPCENIDefinition object. The configuration example and key parameter descriptions are as follows:

```YAML
apiVersion: network.volcengine.com/v1beta1
kind: VPCENIDefinition
metadata:
  name: vpceni-default # custom VPCENIDefinition object name
  namespace: default
spec:
  vpcID: vpc-rr1s2d*** # Required. The ID of the VPC (Virtual Private Cloud) to which the cluster belongs.
  allocateType:
    releaseAfter: 3m0s # Required. The delayed time before reclaiming the IP address after a pod is removed. Setting it to 0 means immediate reclaim. Only effective if releaseStrategy is set to TTL.
    releaseStrategy: TTL # Required, IP reclaim policy, with available values including TTL (delayed reclaim) and Never (never reclaim). If it is set to Never, the parameter releaseAfter becomes ineffective.
    type: Fixed # Required, IP allocation mode, Fixed means static IP
  securityGroupIDs: 
  - sg-rrhowl*** # Required, the default security group for pods
  subnetIDs:
  - subnet-13f64*** # Required. Specify the subnet ID in the VPC.
  - subnet-13fy9***
```


The parameters under `spec` are listed below.


|Parameter ||Required |Description |
|---|---|---|---|
|vpcID |\- |Yes |The ID of the VPC (Virtual Private Cloud) to which the cluster belongs. |
|allocateType |type |Yes |IP allocation mode:<br><br><br>* **Elastic**: elastic IP policy. The IP resources are released as soon as pods are deleted.<br><br>* **Fixed**: static IP policy. |
||releaseStrategy |It is required if the `type` is set to `Fixed` |IP reclaim policy. It is effective only if `type` is set to `Fixed`. Valid values:<br><br><br>* **TTL**: delayed reclaim. The system will reclaim IP addresses based on the configuration of `releaseAfter`.<br><br>* **Never**: never reclaim. The system will not automatically reclaim IP addresses. You need to manually delete the PodENI resource to release the IPs.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If it is set to <code>Never</code>, the <code>releaseAfter</code> parameter becomes ineffective.</div><br> |
||releaseAfter |It is required if the `type` is set to `Fixed` |IP release time. Only effective if `releaseStrategy` is set to `TTL`. The delayed time before reclaiming the IP address after a pod is removed. The time format is Go time type, for example, `2h35m` and `3m0s`. For details on the format of Go time type, see [Go time type](https://pkg.go.dev/time#ParseDuration). A value of `0` indicates immediate reclaim. |
|securityGroupIDs |\- |Yes |Specify security group IDs. Multiple security groups can be configured and will be effective simultaneously. |
|subnetIDs |\- |Yes |Specify one or more subnet IDs within the VPC. They can be some or all of the subnets assigned to cluster pods, or subnets in the specified VPC that are not assigned to any pods. |


<span id=".5q2l6aqk5Zub77ya5Yib5bu6LXBvZG5ldHdvcmtkZWZpbml0aW9uLeWvueixoQ=="></span>
### Step 4: Create the PodNetworkDefinition object

Create a PodNetworkDefinition object. The configuration example and key parameter descriptions are as follows:

```YAML
apiVersion: network.volcengine.com/v1beta1
kind: PodNetworkDefinition
metadata:
  name: vpceni1
  namespace: default
spec:
  ipResource:
    name: vpceni-default # Required, custom VPCENIDefinition object name, consistent with the name in the previous step
    type: VPCENIDefinition  # Required, specify the resource type, fixed value
  selectors:
  - podSelector:
      matchLabels:
        foo: bar # Optional, pod labels defined in PodNetworkDefinition object, used to match pods that need dedicated ENIs and static IPs
    namespaceSelector:
      matchLabels:
        foo: bar # Optional, the namespace labels defined in the PodNetworkDefinition object, used to match namespaces so that all the pods in it can be assigned ENIs and static IPs
```


The parameters under `spec` are listed below.


|Parameter ||Required |Description |
|---|---|---|---|
|ipResource |name |Yes |Specify a name for the network resource, which needs to be consistent with the name of the VPCENIDefinition object. |
||type |Yes |Specify the type of network resource. It needs to be `VPCENIDefinition` in this case. |
|selectors |podSelector |No |Specify the labels used to match Pods. Matching Pods use the network resources specified by `ipResource` during Pod creation. |
||namespaceSelector |No |Specify labels for selecting namespaces. All Pods in the matching namespaces will use the network resources specified by `ipResource` during Pod creation. |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning"><code>podSelector</code> and <code>namespaceSelector</code> are optional parameters that can be configured as needed. At least one of them must be configured so that the feature can take effect.</div>


* <div data-tips="true" data-tips-type="warning">The <code>selectors</code> is a list that may contain multiple namespaces and pod labels. Each individual member in the list can have labels for both namespaces and pods simultaneously.</div>


* <div data-tips="true" data-tips-type="warning">The selectors contained in each member apply <strong>AND</strong> logically with each other. It means only the pod with labels that match the two selectors simultaneously can be assigned with an ENI and a static IP if both selectors are configured.</div>


* <div data-tips="true" data-tips-type="warning">The members in the list apply <strong>OR</strong> logically with each other if there is more than one member in the list. It means a pod that matches the selectors of any member in the list can be assigned an ENI and a static IP.</div>



<span id=".5q2l6aqk5LqU77ya6YWN572uLXBvZC3ni6zljaDlvLnmgKfnvZHljaE="></span>
### Step 5: Configure an ENI dedicated to a pod 

There are several methods to do it:


* **Namespace label**: Use namespace labels to assign ENIs to all the pods under the namespaces.

* **Pod label**: Use pod labels to assign ENIs to specific pods.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can use either one label type or both. If both types are used, pods need to match them simultaneously to get ENIs.</div>



<Tabs>
<Tab zoneid="oqmw0tBvaS" title="Configuring namespace labels">
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
<Tab zoneid="aACkMxC7FU" title="Creating pods and adding labels">
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
<Tab zoneid="oEEOB7uLJI" title="Creating workloads and adding labels">
<TabTitle>Creating workloads and adding labels</TabTitle>

You can add the label defined in the PodNetworkDefinition object (e.g., `foo: bar`) when creating a pod, so that the pod has a dedicated ENI. The example is as follows:

```YAML
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: statefulset-demo # Workload name
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

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For pods running with static IPs, the AZs (availability zones) of ENIs are determined when pods are first created. If pods are rebuilt later, they will automatically relocate to the AZs of the nodes where the original pods were first created. This achieves automatic affinity.</div>


As shown in the following figure, automatically added annotations (such as `k8s.volcengine.com/eni-ip-status`) indicate that the pod has been configured with a dedicated ENI.

The information about ENIs can be found on the **Network interface** tab of the Pod Details page.

After you delete and recreate the Pod, the Pod IP address remains unchanged, indicating that the static IP has been successfully configured for the Pod.

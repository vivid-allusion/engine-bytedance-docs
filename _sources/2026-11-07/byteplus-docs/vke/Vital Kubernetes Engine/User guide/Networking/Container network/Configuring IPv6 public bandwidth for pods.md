---
title: "Configuring IPv6 public bandwidth for pods"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Configuring_IPv6_public_bandwidth_for_pods"
---

In an IPv4/IPv6 dual\-stack cluster, the IPv6 addresses assigned to pods do not have IPv6 public bandwidth enabled by default, preventing communication with the Internet. This topic describes how to enable the IPv6 public bandwidth feature for a pod during creation, enabling it to access the Internet via IPv6.

<span id="aGZ9gUMy"></span>
## Background information

When you create an IPv4/IPv6 dual\-stack VPC and subnets, and then use the VPC and subnets to create a dual\-stack cluster, the system will automatically assign IPv6 addresses to the nodes and pods within the cluster. By default, pods in the cluster have only IPv6 addresses and can only access private networks. To allow a pod to access the public network via its IPv6 address, follow the configuration method described in this topic and enable the IPv6 public bandwidth feature for the pod before it is created.

<span id="fVLBzQrZ"></span>
## Prerequisites


* An IPv4/IPv6 dual\-stack cluster has been created. For details, see [Creating IPv4/IPv6 dual-stack clusters](https://docs.byteplus.com/en/docs/vke/Deploying-an-IPv4_IPv6-dual-stack-cluster-using-VKE).

* VPC and subnet have been bound to an IPv6 gateway. For details, see [Enabling IPv6 for VPC](https://docs.byteplus.com/en/docs/IPv6/Enable_IPv6_for_private_networks). If you cannot access the IPv6 gateway console, please contact your account manager.

* (Optional) If you plan to use a shared bandwidth package, you need to create a shared bandwidth package that supports the IPv4/IPv6 dual\-stack protocol in advance. See [Creating a Shared Bandwidth Package](https://docs.byteplus.com/en/docs/bandwidthpackage/Creating-a-Bandwidth-Package).


<span id="3yCfu9Sg"></span>
## Usage limits


* We recommend that you uniformly configure the **IPv6 public bandwidth** feature for pods through the method described in this topic. After configuration is complete, do not manually modify the settings (e.g., billing method and bandwidth cap) on the IPv6 gateway console. Otherwise, configuration inconsistencies between the two sides may occur, potentially leading to abnormal or unexpected behavior when pods in the cluster access the public network via IPv6.

* The IPv6 public bandwidth feature for a pod can only be configured during its initial creation. Modifying the annotation after successful configuration will not take effect.

* Trunk ENI does not support IPv6 public bandwidth.

* Only clusters using the VPC\-CNI network model support configuring the IPv6 public bandwidth feature for pods.

* A VPC can be configured with only one IPv6 gateway.

* IPv6 gateway instances have the following limitations:

   * A single account can enable public bandwidth for a maximum of 20 IPv6 addresses in a single region.

   * Each IPv6 gateway instance supports a maximum of 200 **outbound\-only rules**.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">For more details on limitations, see <a href="https://docs.byteplus.com/en/docs/IPv6/Limits">Limits</a>.</div>


* <div data-tips="true" data-tips-type="default">To request an increase in the above quota limits, go to <a href="https://console.byteplus.com/quota/productList">Quota Center</a> to submit an application.</div>



<span id="zx0UUjf0"></span>
## Procedure

<span id="KAm5wr6K"></span>
### Step 1: Install an add\-on


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. On the page that appears, click the name of the target cluster to go to the management page of the cluster.

3. On the cluster management page, click **Addons** in the left navigation bar.

4. Select the **Network** tab, hover your mouse over the vpc\-cni\-controlplane add\-on card, click **Deploy**, and enable **Bind EIP to pods** in the configuration dialog that appears.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If an existing cluster already has the vpc\-cni\-controlplane add\-on installed, ensure it has been upgraded to version 1.5.3 or later. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on">Upgrading add\-ons</a>.   </div>
   

<span id="41Nbt5Hx"></span>
### Step 2: Configure IPv6 public network bandwidth for pods

VKE configures IPv6 public bandwidth for pods through instance annotations.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The configuration of IPv6 public bandwidth for a pod applies regardless of whether the pod is scheduled to a regular node or a VCI node.</div>


Taking a stateless Deployment as an example, you can add an annotation during configuration to set up IPv6 public bandwidth for the pods. The following content in YAML is an example with descriptions:


1. Create the YAML file of the workload. The code of the sample file `deployment-demo.yaml` is as follows:

   ```YAML
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: deployment-demo
     namespace: default
   spec: 
     replicas: 1
     selector: 
       matchLabels: 
         app: demo
     template: 
       metadata: 
         labels: 
           app: demo
         annotations:
           vke.volcengine.com/ipv6gateway-bandwidth-attributes: | # Enable IPv6 public bandwidth feature for pods
             {
               "billingType": 2,
               "bandwidth": 100,
               "bandwidthPackageId": "bwp-13g2o0a09***",
               "egressOnlyRule": false
             }
       spec:
         containers:
         - name: demo
           image: doc-cn-beijing.cr.volces.com/vke/nginx-demo:v1.0
           ports:
           - containerPort: 80
   ```
   

   The key parameters are described in the following table.

   
   |Parameter |Type |Required |Description |
   |---|---|---|---|
   |billingType |Integer |Yes |Billing method for IPv6 public bandwidth. Valid values:<br><br><br>* **2**: Pay\-as\-you\-go \- Billing by bandwidth cap.<br><br>* **3**: Pay\-as\-you\-go \- Billing by actual traffic. |
   |bandwidth |Integer |No |The upper bandwidth limit for IPv6 public bandwidth, measured in Mbps.<br><br><br>* When `BillingType` is `2`, the valid range is 1–500.<br><br>* When `BillingType` is `3`: the valid range is 1–200.<br><br>* If not configured, the default value is 1 Mbps.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The bandwidth cap is allowed to exceed the configured upper limit. If needed, please contact your account manager. For details, see <a href="https://docs.byteplus.com/en/docs/IPv6/Limits">Limits</a>.</div><br> |
   |bandwidthPackageId |String |No |IPv6 shared bandwidth package ID. For details about shared bandwidth packages, see [Creating a Shared Bandwidth Package](https://docs.byteplus.com/en/docs/bandwidthpackage/Creating-a-Bandwidth-Package). |
   |egressOnlyRule |Boolean |No |Whether to synchronously create outbound\-only rules. Valid values:<br><br><br>* **true**: Synchronously create outbound\-only rules.<br><br>* **false**: (Default) Do not create outbound\-only rules.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When enabling IPv6 public bandwidth for pods in a cluster, if you do not want the IPv6 address of the pod to be accessible from public IPv6 endpoints, you can configure this parameter to synchronously create outbound\-only rules. These bound\-only rules deny access from public IPv6 endpoints to the pod.</div><br> |
   

2. Run the following command to create the workload.

   ```Bash
   kubectl apply -f deployment-demo.yaml
   ```
   


<span id="VBlOfRcB"></span>
## Result validation

When the pod reaches the `Running` state, you can use the following methods to verify whether the configuration is correct.


1. Click the Pod name to enter the Pod details page. 

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The status annotation ipv6gateway\-bandwidth\-status is added to the pod asynchronously with pod startup. To avoid scenarios where the pod starts normally but its network resources are unavailable, you can use an initContainer to continuously monitor this annotation and start the business pod only after the annotation reaches the expected state.   </div>
   

2. Log in to the [IPv6 Gateway console](https://console.byteplus.com/eip/ipv6s) and click the IPv6 gateway name corresponding to your VPC to enter the gateway details page. On the **IPv6 Internet bandwidth** tab, use the IPv6 address of the Pod to search and confirm that the configuration matches the expected settings.

3. Log in to the pod console and execute the following commands to verify connectivity.

   ```Bash
   ping6 ipv6.baidu.com
   ```
   

   The expected output is as follows:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a4a60d93e239443bb4fb6e97b33bcbd0.png) </span>


&nbsp;

&nbsp;

&nbsp;

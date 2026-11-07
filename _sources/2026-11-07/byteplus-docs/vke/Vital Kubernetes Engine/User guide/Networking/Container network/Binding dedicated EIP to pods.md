---
title: "Binding dedicated EIP to pods"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Associating-an-EIP-with-a-pod"
---

VKE lets you provide dedicated Internet ingress and egress for individual pods. This satisfies the need to expose only one or a few pods to the Internet, and prevents pods from competing for outbound Internet bandwidth. The following content will introduce how to bind a public IP address to a pod.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">[<a href="https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features"><strong>Beta \- apply for trial</strong></a>]: This feature is currently in beta. To use it, submit an application.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The target cluster is connected through kubectl. For details, see [Connecting to a cluster](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

* To bind an existing EIP to a pod, apply for an EIP instance first. For details, see [Applying for EIPs](https://docs.byteplus.com/en/docs/eip/Applying-for-an-EIP).


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage limits


* Only supported in clusters using the VPC\-CNI network model.

* After the EIP feature is enabled, it cannot be disabled. After the vpc\-cni\-controlplane add\-on is installed, it cannot be uninstalled at this time.

* The pod name must not exceed 63 characters.

* The configuration involves resource application and purchase. Therefore, make sure that the account meets the following requirements:

   * Before creating EIP resources, ensure your account balance is no less than 100 yuan (including vouchers) and not zero (excluding vouchers).

   * You can apply for up to 20 EIPs for an account in a single region by default. If more EIPs are required, please go to the [Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=EIP) to request a quota increase.

   * For each account, the maximum requests sent for EIP addresses a day in the same region are twice the maximum number of EIP addresses.

   * For each account, the maximum requests sent for binding EIP addresses a day in the same region are three times the maximum number of EIP addresses.


<span id=".5q2l6aqk5LiA77ya5a6J6KOF57uE5Lu2"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5a6J6KOF57uE5Lu2"></span>
### Step 1: Install an add\-on


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. On the right page, click the target cluster name to open the management page of this cluster.

3. In the left navigation bar, click **Addons**.

4. On the **Network** tab, move the pointer over the vpc\-cni\-controlplane add\-on card and click **Deploy**.

5. Enable the **Bind EIP to pods** in the pop\-up configuration box.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For the clusters already installed with the vpc\-cni\-controlplane add\-on, you need to ensure the add\-on version is not lower than v1.3.0. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on">Upgrade add\-ons</a>.   </div>
   

6. Click **Confirm** to finish the installation.


<span id=".5q2l6aqk5LqM77ya5Li6LXBvZC3nu5Hlrprni6znq4stZWlw"></span>
### Step 2: Bind a dedicated EIP to the pod

Pods running on Vital Kubernetes Engine can have an EIP by using annotations. Either the existing EIPs or newly created ones can be used on pods.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Before binding an existing EIP, make sure that it is available. An EIP that is already bound to another resource cannot be bound to a pod.</div>


* <div data-tips="true" data-tips-type="warning">The EIPs bound to pods by configuring workloads are effective for Deployment, StatefulSet, Job, and CronJob, but not for DaemonSet.</div>


* <div data-tips="true" data-tips-type="warning">When you bind an existing EIP to pods through a workload configuration, if the replica count is greater than 1, only one of the pods will be bound to the EIP.</div>


* <div data-tips="true" data-tips-type="warning">A dedicated EIP can be bound to any single pod on any node, which can be either a conventional or a VCI node.</div>



<span id=".57uR5a6a5bey5pyJLWVpcA=="></span>
#### Method 1: Bind an existing EIP


<Tabs>
<Tab zoneid="wJ0hlkhbHV" title="Binding an existing EIP to a pod when configuring deployment">
<TabTitle>Binding an existing EIP to a pod when configuring deployment</TabTitle>

You can add annotations in the Deployment to bind a dedicated EIP to a pod. The following YAML content provides an example:

```YAML
apiVersion: apps/v1
kind: Deployment
metadata:
  name: deployment-eip-demo # Workload name
  namespace: default # Namespace to which the workload belongs
spec:
  replicas: 1 
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      annotations:
        vke.volcengine.com/primary-eip-id: "eip-rr67***"  # Existing EIP instance ID bound with pod
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx 
        image: doc-cn-beijing.cr.volces.com/vke/nginx-demo:v1.0
        ports:
        - containerPort: 80 
```





</Tab>
<Tab zoneid="ii9s6apQyY" title="Binding an existing EIP when configuring pod">
<TabTitle>Binding an existing EIP when configuring pod</TabTitle>

You can add annotations to the YAML file for the pod to achieve binding. The following YAML content provides an example:

```YAML
apiVersion: v1
kind: Pod
metadata:
  name: pod-eip-demo # Pod name
  namespace: default # the namespace to which the pod belongs
  annotations: 
    vke.volcengine.com/primary-eip-id: "eip-rr67***"  # Existing EIP instance ID bound with pod
spec:
  containers:
    - name: hello-pod 
      image: doc-cn-beijing.cr.volces.com/vke/nginx-demo:v1.0
      ports:
        - containerPort: 80
```



</Tab>
</Tabs>


The following table describes the annotations.


|Field |Type |Required |Description |
|---|---|---|---|
|vke.volcengine.com/primary\-eip\-id |String |Yes |Existing EIP instance ID bound to pod. |


<span id="3BRZfbuk"></span>
#### Method 2: Create an EIP and bind it

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Be cautious when removing pods. The corresponding EIP addresses will be deleted along with them, and the public IP addresses you get by creating new EIP addresses may differ from the original ones.</div>


* <div data-tips="true" data-tips-type="warning">Do not modify the EIP instances that VKE created (such as switching their billing method). Otherwise, VKE may fail to delete those EIP resources, leaving them stranded. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Associating-an-EIP-with-a-pod#.5riF55CGLXZrZS3liJvlu7rnmoQtZWlwLeWunuS-iw==">Removing EIP instances created in VKE</a>.</div>




<Tabs>
<Tab zoneid="MuS44WRWOY" title="Creating an EIP and binding it to a pod when configuring deployment">
<TabTitle>Creating an EIP and binding it to a pod when configuring deployment</TabTitle>

You can add annotations in the deployment to create a new EIP and bind it to a pod. The following YAML content provides an example:

```YAML
apiVersion: apps/v1
kind: Deployment
metadata:
  name: deployment-eip-demo # Workload name
  namespace: default # Namespace to which the workload belongs
spec:
  replicas: 1 
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      annotations: 
        vke.volcengine.com/primary-eip-allocate: '{"type": "Elastic"}' # EIP application policy, fixed value
        vke.volcengine.com/primary-eip-attributes: '{
          "name": "eip-demo",
          "description": "demo for pods eip",
          "isp": "BGP",
          "billingType": 2,
          "bandwidth": 100,
          "projectName": "default",
          "bandwidthPackageId": "bwp-2d63yyj3ki4u858oz***",
          "tags": {    
            "billing-team": "doc",
            "env": "prod"
          }
        }'
        # billingType specifies the EIP billing method. Valid values: 2 (Pay-as-you-go - by bandwidth limit) and 3 (Pay-as-you-go - by actual traffic). Default value: 2.
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx 
        image: doc-cn-beijing.cr.volces.com/vke/nginx-demo:v1.0
        ports:
        - containerPort: 80 
```





</Tab>
<Tab zoneid="tyv7w1FaVV" title="Creating an EIP and binding it to a pod that is being configured.">
<TabTitle>Creating an EIP and binding it to a pod that is being configured.</TabTitle>

You can add annotations to the YAML file for the pod to achieve binding. The following YAML content provides an example:

```YAML
apiVersion: v1
kind: Pod
metadata:
  name: pod-eip-demo # Pod name
  namespace: default # the namespace to which the pod belongs
  annotations: 
    vke.volcengine.com/primary-eip-allocate: '{"type": "Elastic"}' # EIP application policy, fixed value
    vke.volcengine.com/primary-eip-attributes: '{
      "name": "eip-demo",
      "description": "demo for pods eip",
      "isp": "BGP",
      "billingType": 2,
      "bandwidth": 100,
      "projectName": "default",
      "bandwidthPackageId": "bwp-2d63yyj3ki4u858oz***",
      "tags": {    
            "billing-team": "doc",
            "env": "prod"
      }
    }'
    # billingType specifies the EIP billing method. Valid values: 2 (Pay-as-you-go - by bandwidth limit) and 3 (Pay-as-you-go - by actual traffic). Default value: 2.
spec:
  containers:
    - name: hello-pod 
      image: nginx:latest
      ports:
        - containerPort: 80
```



</Tab>
</Tabs>


The following table describes the annotations.


|Field |Type |Required |Description |
|---|---|---|---|
|vke.volcengine.com/primary\-eip\-allocate |String |No |EIP application policy, with a fixed value set to `'{"type": "Elastic"}'`. |
|vke.volcengine.com/primary\-eip\-attributes |String |Yes |Create and bind an EIP. |


The parameters under `primary-eip-attributes` are listed below.


|Field |Type |Required |Description |
|---|---|---|---|
|name |String |No |EIP name. A name is automatically generated by the system if no one is specified. |
|description |String |No |EIP description. |
|isp |String |No |The EIP line type. Valid values:<br><br><br>* **BGP**: (default) BGP (multi\-line).<br><br>* **ChinaMobile**: China Mobile static single line.<br><br>* **ChinaTelecom**: China Telecom static single line.<br><br>* **ChinaUnicom**: China Unicom static single line.<br><br>* **SingleLine_BGP**: BGP single line.<br><br>* **Static_BGP**: Static BGP.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Except for <strong>BGP (multi\-line)</strong>, all other line types are beta features of EIP products. To apply to use these features, please contact your account manager.</div><br> |
|billingType |Integer |No |EIP billing methods:<br><br><br>* **2**: (default) The billing method is "Pay\-as\-you\-go \- Billing by bandwidth limit".<br><br>* **3**: Pay\-as\-you\-go \- Billing by actual traffic. |
|bandwidth |Integer |No |The maximum bandwidth for an EIP measured in Mbps.<br><br><br>* If `billingType` is set to `2`, the bandwidth range is 1 to 500.<br><br>* If `billingType` is set to `3`, the bandwidth range is 1 to 200. |
|projectName |String |No |The name of the project to which the EIP belongs. The project "default" is used by default. |
|bandwidthPackageId |String |No |ID of the shared bandwidth package.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">A shared bandwidth package is a reusable cloud resource for sharing bandwidth. It aggregates multiple public IPs and IPv6 public bandwidths from the same region into a shared bandwidth pool, reducing public bandwidth costs through bandwidth sharing. For details, see <a href="https://docs.byteplus.com/en/docs/bandwidthpackage/What-is-Bandwidth-Package">What is a shared bandwidth package?</a></div><br> |
|tags |Object |No |The EIP tags as key\-value pairs.<br><br><br>* Both the tag key and tag value are strings.<br><br>* It can contain Chinese characters, uppercase and lowercase English letters, digits, spaces, underscores (`_`), periods (`.`), colons (`:`), slashes (`/`), equals signs (`=`), plus signs (`+`), hyphens (`-`), and at signs (`@`).<br><br>* The tag key cannot start with `volc:` or `sys:` in ‌any case variation‌.<br><br>* The tag value is case\-sensitive.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">To use this configuration, upgrade the vpc\-cni\-controlplane add\-on to v1.6.3 or later. For details, see <a href="https://docs.volcengine.com/docs/6460/1699938?lang=zh">vpc\-cni\-controlplane</a>.</div><br> |


<span id="BwcB8qZU"></span>
#### Method 3: Use an IP address pool to assign EIPs to pods

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">To use an IP address pool to assign EIPs to pods, make sure that the following requirements are met:</div>



* <div data-tips="true" data-tips-type="default">The IP address pool feature of VPC is currently in beta. To use it, contact your account manager.</div>


* <div data-tips="true" data-tips-type="default">Confirm that the IP address pool has been created and obtain the ID of the IP address pool. For details, see <a href="https://docs.byteplus.com/en/docs/eip/Create_an_IP_address_pool">Creating IP address pools</a>.</div>


* <div data-tips="true" data-tips-type="default">You need to upgrade the vpc\-cni\-controlplane add\-on to v1.5.2 or later.</div>



You can add an annotation when you configure a pod to use an address pool to assign dedicated EIP addresses to the pod. The following YAML content provides an example:

```YAML
apiVersion: v1
kind: Pod
metadata:
  name: pod-eip-demo # Pod name
  namespace: default # the namespace to which the pod belongs
  annotations: 
    vke.volcengine.com/primary-eip-allocate: '{"type": "Elastic"}' # EIP application policy, fixed value
    vke.volcengine.com/primary-eip-attributes: '{
      "name": "eip-demo",
      "description": "demo for pods eip",
      "isp": "BGP",
      "billingType": 2,
      "projectName": "default",
      "bandwidthPackageId": "bwp-2d63yyj3ki4u858oz***",
      "ipAddressPoolId": "ippool-w0kr0l3rrxmo***",
      "tags": {    
            "billing-team": "doc",
            "env": "prod"
      }
    }'
    # billingType specifies the EIP billing method. Valid values: 2 (Pay-as-you-go - by bandwidth limit) and 3 (Pay-as-you-go - by actual traffic). Default value: 2.
spec:
  containers:
    - name: hello-pod 
      image: doc-cn-beijing.cr.volces.com/vke/nginx-demo:v1.0
      ports:
        - containerPort: 80
```


The following table describes the annotations.


|Field |Type |Required |Description |
|---|---|---|---|
|vke.volcengine.com/primary\-eip\-allocate |String |No |EIP application policy, with a fixed value set to `'{"type": "Elastic"}'`. |
|vke.volcengine.com/primary\-eip\-attributes |String |Yes |Create and bind an EIP. |


The parameters under `primary-eip-attributes` are listed below.


|Field |Type |Required |Description |
|---|---|---|---|
|name |String |No |EIP name. A name is automatically generated by the system if no one is specified. |
|description |String |No |EIP description. |
|isp |String |No |The EIP line type. Default value: BGP. This configuration must be consistent with that of the IP address pool. |
|billingType |Integer |No |The EIP billing method. This configuration must be consistent with that of the IP address pool. Valid values:<br><br><br>* **2**: (default) The billing method is "Pay\-as\-you\-go \- Billing by bandwidth limit".<br><br>* **3**: Pay\-as\-you\-go \- Billing by actual traffic. |
|bandwidth |Integer |No |The maximum bandwidth for an EIP measured in Mbps.<br><br><br>* If `billingType` is set to `2`, the bandwidth range is 1 to 500.<br><br>* If `billingType` is set to `3`, the bandwidth range is 1 to 200. |
|projectName |String |No |The name of the project to which the EIP belongs. The project "default" is used by default. |
|bandwidthPackageId |String |No |ID of the shared bandwidth package.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">A shared bandwidth package is a reusable cloud resource for sharing bandwidth. It aggregates multiple public IPs and IPv6 public bandwidths from the same region into a shared bandwidth pool, reducing public bandwidth costs through bandwidth sharing. For details, see <a href="https://docs.byteplus.com/en/docs/bandwidthpackage/What-is-Bandwidth-Package">What is a shared bandwidth package?</a></div><br> |
|ipAddressPoolId |String |Yes |The ID of the IP address pool. |
|tags |Object |No |The EIP tags in key\-value pairs.<br><br><br>* Both the tag key and tag value are strings.<br><br>* It can contain Chinese characters, uppercase and lowercase English letters, digits, spaces, underscores (`_`), periods (`.`), colons (`:`), slashes (`/`), equals signs (`=`), plus signs (`+`), hyphens (`-`), and at signs (`@`).<br><br>* The tag key cannot start with `volc:` or `sys:` in ‌any case variation‌.<br><br>* The tag value is case\-sensitive.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">To use this configuration, upgrade the vpc\-cni\-controlplane add\-on to v1.6.3 or later. For details, see <a href="https://docs.volcengine.com/docs/6460/1699938?lang=zh">vpc\-cni\-controlplane</a>.</div><br> |


<span id=".5q2l6aqk5LiJ77ya77yI5Y-v6YCJ77yJ5o6n5Yi2LXBvZC1yZWFkeS3nirbmgIE="></span>
### Step 3: (Optional) Monitor status of a pod

The creation of a pod and EIP binding are performed asynchronously and the binding process starts after an IP is allocated to the pod. Therefore, it is possible for the pod to become ready while the binding process is still incomplete. You can configure an init container in the pod to monitor its status and check if the EIP binding process is complete. The following YAML file is provided as a reference.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In this example, a busybox image is used to run as an init container. You can use any image capable of executing commands. A small image is recommended.</div>


```YAML
apiVersion: v1
kind: Pod
metadata:
  name: pod-eip-demo
  annotations:
    vke.volcengine.com/primary-eip-id: "eip-rr67***"
  ...
spec:
  initContainers:
  - command:
    - timeout
    - "60"
    - sh
    - -c
    - until grep -i 'EipAddress' /etc/eipinfo/allocated-eips; do echo waiting for
      allocated-eips; sleep 1; done   
    image: busybox:latest
    imagePullPolicy: Always
    name: init
    volumeMounts:
    - mountPath: /etc/eipinfo
      name: eipinfo
  volumes:    
   - name: eipinfo      
     downwardAPI:        
      items:          
       - path: "allocated-eips"            
         fieldRef:              
          fieldPath: metadata.annotations['vke.volcengine.com/allocated-eips']
...
```


<span id=".57uT5p6c6aqM6K-B"></span>
## Validate results

<span id=".5qOA5p-lLXBvZC3nirbmgIE="></span>
### Checking pod status

After the pod is in the `Running` state, you can start checking whether the binding process is complete. After the binding is done, the system adds annotations such as `vke.volcengine.com/allocated-eips` to the pod, which you can use to confirm that the binding is complete. Here is a screenshot of the annotations.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_20a84b32c168d7737ae67471b94b3d5d.png) </span>

The parameters under `vke.volcengine.com/allocated-eips` are listed below.


|Parameter |Type |Example |Description |
|---|---|---|---|
|EipId |String |eip\-2yynbg1qt\*\*\* |EIP instance ID. |
|EipAddress |String |14.x.x.x |Public IP of the EIP instance. |
|EniId |String |eni\-2yz4c3ppm\*\*\* |ID of the Pod ENI. |
|EniIp |String |192.168.1.10 |The private IPv4 address of the pod ENI (elastic network interface). |


<span id=".5p-l55yLLWVpcC3kv6Hmga8="></span>
### Viewing EIP information

Log in to the [EIP console](https://console.byteplus.com/eip) and click **Access to Internet** \> **EIP** in the left navigation bar. You can see the EIP instances that are already bound to the pods.

<span id=".6YCa6L-HLWVpcC3orr_pl64tcG9k"></span>
### Accessing pods via EIPs

To verify whether the EIP is effective, access the pod over the Internet.

<span id=".5Y-C6ICD5L-h5oGv"></span>
## For your reference

<span id=".5riF55CGLXZrZS3liJvlu7rnmoQtZWlwLeWunuS-iw=="></span>
### Removing EIP instances created on VKE

Manual changes to EIPs created by VKE may leave behind orphaned EIP resources that VKE cannot automatically delete when the corresponding pods are removed. In this case, delete them manually from the EIP console by identifying VKE\-created EIPs. The following table lists EIP labels:


|Label key |Label value |
|---|---|
|volc:vke:cluster\-id\-<cluster\-id\> |cluster\-id |
|volc:vke:createdby\-vke\-flag |true |
|volc:vke:enieip\-name |<enieip\-name\> |
|volc:vke:enieip\-namespace |<enieip\-namespace\> |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The enieip is a CRD resource in VKE clusters. You can view the information about it by selecting <strong>Workload</strong> \> <strong>Resource Explorer</strong> in the left navigation bar on the console page of a cluster. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Resource-explorer">Resource Explorer</a>.</div>

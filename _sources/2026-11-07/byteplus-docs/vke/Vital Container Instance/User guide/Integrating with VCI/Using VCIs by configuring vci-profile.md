---
title: "Using VCIs by configuring vci-profile"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using-VCI-by-configuring-vci-profile"
---

VCI and VKE provide the vci\-profile capability, which enables non\-intrusive delivery of business workloads to VCI pods.

<span id=".5Yqf6IO95LuL57uN"></span>
## Feature introduction

vci\-profile is the configuration file for VCI. It allows you to define unified and globally fixed configurations for VCI resource usage at the cluster or namespace level. This capability reduces the need to modify workload YAML files, enables more convenient, efficient, and non\-intrusive use of VCI, and avoids confusion between operation management and business management.

<span id=".5L2_55So6K-05piO"></span>
## Usage instructions

Selecting and scheduling to VCI resources via vci\-profile is a form of soft scheduling. In other words, the final scheduling result of a pod is jointly affected by mechanisms such as VCI annotations in the cluster and ResourcePolicy scheduling, so in some cases the pod may ultimately not be scheduled onto VCI.

The features interact as follows:​


|Feature |Description |Application scope |Effect |
|---|---|---|---|
|VCI annotation |The annotation is `vke.volcengine.com/burst-to-vci: enforce`, which enforces scheduling to VCI. This feature addresses whether an individual pod is scheduled onto VCI |Workload |Hard scheduling to VCI. ResourcePolicy scheduling is not effective. |
|vci\-profile file |This feature enables non\-intrusive use of VCI. |Cluster |Soft scheduling to VCI. Scheduling is subject to the ResourcePolicy policy. For details, see the main part of this topic. |
|[ResourcePolicy scheduling](https://docs.byteplus.com/en/docs/vke/ResourcePolicy-scheduling) |This feature addresses the aspect of computing resources required by pods. |Workload |Dynamic, hybrid elasticity of ECS and VCI resources. |


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A cluster with the pod network model of VPC\-CNI has been created. For detailed operations, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Only clusters with the VPC\-CNI network model support using a vci\-profile file.   </div>
   

* The vci\-virtual\-kubelet add\-on has been installed and upgraded to v1.26.1 or later. For add\-on details, see [vci-virtual-kubelet](https://docs.byteplus.com/en/docs/vke/vci-virtual-kubelet).


<span id=".6YWN572uLXZjaS1wcm9maWxl"></span>
## Configuring vci\-profile

To use the vci\-profile support, create a vci\-profile file in a cluster that meets corresponding requirements in the **Prerequisites**. You can use the VKE console or kubectl to create one. We recommend using the VKE console.

<span id=".6YCa6L-H5o6n5Yi25Y-w5LiA6ZSu5Yib5bu6"></span>
### Using the console


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. In the cluster list, click the name of the target cluster.

4. In the left navigation bar, select **Nodes** \> **Virtual node**.

5. On the **Virtual node** page, click **VCI Profile**.

   If no vci\-profile file exists in the cluster, click **Create with one click** to create a vci\-profile file for the cluster.

6. On the VCI Profile page, configure parameters as needed and then click **Confirm**.

   
   |Parameter |Option |Description |
   |---|---|---|
   |**VCI Profile** |||
   |Enable log collection by default ||Whether to enable log collection for the VCI pod to collect logs to the BytePlus TLS. |
   |Kubernetes consistency policy |Privileged mode |Compatibility configuration for the privileged mode of VCI pods at both pod and container levels.<br><br><br>* **Keep user configuration**: VCI pods do not ignore your existing configuration.<br><br>* **Ignore user settings**: (Recommended) VCI pods ignore privileged mode configuration.<br><br>   By default, enabling privileged mode for a VCI pod will cause a failure in creating the pod. For clusters containing VCI workloads, we recommend ignoring the privileged mode. |
   ||DNS resolution policy |DNS resolution configuration inside VCI pods.<br><br><br>* **Keep user configuration**: The VCI pod does not ignore your existing configuration.<br><br>* **Ignore user settings**: (Recommended) The VCI pod ignores your existing configuration and automatically converts the DNS resolution behavior from `ClusterFirstWithHostNet` to `ClusterFirst`.<br><br>   By default, the `dnsPolicy` of the VCI pod does not support `ClusterFirstWithHostNet`. Therefore, for clusters containing VCI workloads, we recommend using this method to convert the DNS resolution behavior to `ClusterFirst`. |
   ||Node file directory mount policy |Configuration for mounting node file directories in VCI pods.<br><br><br>* **Keep user configuration**: VCI pods do not ignore your existing configuration.<br><br>* **Ignore user settings**: (Recommended) VCI pods will ignore the configuration for mounting node file directories.<br><br>   By default, the `volumes.hostPath` configuration of VCI pods will cause pod creation to fail. For clusters with VCI workloads, it is recommended to ignore the existing configuration. |
   ||Pod hostIP reverse display policy |The display field of the node IP address parameter `status.hostIP` for VCI pods.<br><br><br>* **Virtual node IP**: `hostIP` shows the IP address of the virtual node.<br><br>* **Pod IP**: `hostIP` shows the IP address of the VCI pod. |
   |**VCI selector settings** |||
   |Hit scheduling policy |Attempt scheduling |Scheduling will be affected by factors such as scheduler extenders, so pods matching the rules are not guaranteed to be scheduled to VCI. |
   ||Forced scheduling |Scheduling will not be affected by factors such as scheduler extenders, so pods matching the rules are guaranteed to be scheduled to VCI. |
   |Rule |Name |The name of the selector object. The default naming format is `selector-N`. You can configure a custom name. The name must be unique within the same cluster. |
   ||Namespace selector |After this option is enabled, pods are filtered by namespace label. You can configure the following parameters as needed:<br><br><br>* **Label selection**: Corresponds to the Kubernetes `matchLabels` parameter. You can specify multiple labels, which are in a **logical AND** relationship.<br><br>* **Expression selection**: Corresponds to the Kubernetes `matchExpressions` parameter. You can specify multiple expressions, which are in a ** logical AND** relationship.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Both <strong>Label selection</strong> and <strong>Expression selection</strong> can be set. They are in a <strong>logical AND</strong> relationship.</div><br> |
   ||Object selector |If this option is enabled, pods are filtered by pod label. You can configure the following parameters as needed:<br><br><br>* **Label selection**: Corresponds to the Kubernetes `matchLabels` parameter. You can specify multiple labels, which are in a **logical AND** relationship.<br><br>* **Expression selection**: Corresponds to the Kubernetes `matchExpressions` parameter. You can specify multiple expressions, which are in a **logical AND** relationship.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Both <strong>Label selection</strong> and <strong>Expression selection</strong> can be set. They are in a <strong>logical AND</strong> relationship.</div><br> |
   ||Hitter |If this feature is enabled, **labels** or **annotations** are dynamically added to the pod. |
   


<span id=".6YCa6L-HLWt1YmVjdGwt5Yib5bu6"></span>
### Using kubectl


1. Connect to the cluster. For details, see [Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

2. Create the YAML file for vci\-profile.

   Create a vci\-profile file as a ConfigMap in the **kube\-system** namespace. When creating pods in the cluster, the system will read the vci\-profile file in the **kube\-system** namespace and create pods according to the configuration data in this file.

   The complete YAML template for the vci\-profile file is as follows:

   ```YAML
   apiVersion: v1
   kind: ConfigMap
   metadata:
     name: vci-profile         # The name of the ConfigMap. It must be vci-profile.
     namespace: kube-system    # The namespace to which the vci-profile file belongs. It must be kube-system.
   data:
     preferredSubnetIds: subnet-3tispp1nai1****, subnet-3tispp1nai2****    # The VPC subnet to which VCI pods belong.
     tlsEnable: "true"    # Whether log collection to BytePlus TLS is enabled for VCI pods.
     securityContextPrivilegedConfig: ignore    # Privileged mode compatibility configuration for VCI pods.
     dnsPolicyClusterFirstWithHostNetConfig: clusterFirst    # DNS resolution configuration inside VCI pods.
     volumesHostPathConfig: ignore    # Configuration for mounting node file directories in VCI pods.
     hostIpConfig: podIp              # The display field of status.hostIP for VCI pods.
     enforceSelectorToVci: "true"     # Whether to forcibly schedule pods selected by selectors to VCI.
     timezone: Asia/Shanghai    # Synchronize the time zone of the virtual node and containers.
     selectors: |
       [
         {
           "name": "selector-demo1",
           "namespaceSelector": {
             "matchLabels": {
               "vci": "true"
             },
             "matchExpressions": [
               {
                 "key": "tier",
                 "operator": "In",
                 "values": ["backend"]
               }
             ]
           },
           "effect": {
             "annotations": {
               "vci.volcengine.com/tls-enable": "true"
             },
             "labels": {
               "created-by-vci": "true"
             }
           }
         }
       ]
   ```
   

   You can modify the `data` field in a vci\-profile.

   
   |Configuration item in data |Description |Details and example |
   |---|---|---|
   |selectors |By configuring `selectors` in the vci\-profile file, matched pods use VCI resources and have the corresponding annotations and labels. |[selectors](https://docs.byteplus.com/en/docs/vke/Using-VCI-by-configuring-vci-profile#.c2VsZWN0b3JzLemFjee9rumhuQ==) |
   |Non\-selectors configuration items such as preferredSubnetIds and tlsEnable |In addition to `selectors`, you can control cluster\-level fixed configuration for VCI pods by updating configuration items such as `preferredSubnetIds` and `tlsEnable`. |[Globally fixed configuration items](https://docs.byteplus.com/en/docs/vke/Using-VCI-by-configuring-vci-profile#.5YWo5bGA5Zu65a6a6YWN572u6aG5) |
   

3. Create the ConfigMap corresponding to the vci\-profile file.

   ```Bash
   kubectl create -f vci-profile.yaml
   ```
   


<span id=".c2VsZWN0b3JzLemFjee9rumhuQ=="></span>
## selectors

During pod creation, the system will use the `selectors` field in the vci\-profile file to match pods. Pods with matching labels will be soft\-scheduled to VCI resources, and VCI\-related annotations and labels will be added to the pods.

<span id=".c2VsZWN0b3JzLeWPguaVsOivtOaYjg=="></span>
### selectors parameters

Multiple selectors can be included in the `selectors` configuration, and each selector consists of `name`, `namespaceSelector`, `objectSelector`, and `effect`. Detailed descriptions are as follows:


|Parameter |Required |Description |
|---|---|---|
|name |Required |The name of the selector object. It cannot be empty. |
|namespaceSelector |Optional |Filter pods by namespace label.<br><br><br>* **matchLabels**: Namespace labels to match. If multiple labels are specified, they have a **logical AND** relationship.<br><br>* **matchExpressions**: Namespace expressions to match. If multiple expressions are specified, they have a **logical AND** relationship.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Both <strong>matchExpressions</strong> and <strong>matchLabels</strong> can be set. They have a <strong>logical AND</strong> relationship.</div><br> |
|objectSelector |Optional |Filter pods by pod label.<br><br><br>* **matchLabels**: Pod labels to match. If multiple labels are specified, they have a **logical AND** relationship.<br><br>* **matchExpressions**: Namespace expressions to match. If multiple expressions are specified, they have a **logical AND** relationship.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Both <strong>matchExpressions</strong> and <strong>matchLabels</strong> can be set. They have a <strong>logical AND</strong> relationship.</div><br> |
|effect |Optional |Annotations and labels dynamically appended to the pods.<br><br><br>* **annotations**: Annotations to be appended to the pods. It is optional.<br><br>* **labels**: Labels to be appended to the pods. It is optional. |


<span id=".c2VsZWN0b3JzLeS9v-eUqOivtOaYjg=="></span>
### selectors usage notes


* If a single selector is configured:

   * It is recommended to configure at least one of `namespaceSelector` and `objectSelector`.

   * If both `namespaceSelector` and `objectSelector` are configured, a pod must satisfy both to be considered a match ( namely, `namespaceSelector` and `objectSelector` have a **logical AND** relationship).

   * If neither `namespaceSelector` nor `objectSelector` is configured, but `effect` is configured, the `effect` setting will apply to all pods scheduled to VCI based on vci\-profile configuration.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">Warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">In this case, ResourcesPolicy scheduling is ignored. However, if a pod has the <code>vke.volcengine.com/burst-to-vci:enforce</code> annotation, it will be affected by this type of <code>effect</code>.      </div>
      

* If multiple selectors are configured:

   * The system matches the selectors in order.

   * After a selector successfully matches a pod, the annotations and labels declared in `effect` will be automatically added to the VCI pod (only the keys are added, without overwriting values).

   * For duplicate annotations and labels, the original values for the pod have the highest priority, followed by the `effect` in the first selector matched in order, and so on.

* If you use `namespaceSelector`, exercise caution when you configure it to schedule all pods in the initial cluster namespaces (default, kube\-system, kube\-node\-lease, and kube\-public) to VCI. This is because some system add\-ons of VKE are deployed as Daemonsets in the above namespaces, and VCI does not provide full Daemonset support.

* After you create a vci\-profile file, it takes effect only for newly created pods or pods of workloads that are restarted from rolling update, and will not affect existing running pods.


<span id=".c2VsZWN0b3JzLemFjee9ruekuuS-iw=="></span>
### selectors configuration example


<Tabs>
<Tab zoneid="zTiRYq7UMM" title="CPU load configuration example">
<TabTitle>CPU load configuration example</TabTitle>

By configuring `namespaceSelector` and `objectSelector`, schedule pods to VCI when both the pods and their namespaces have the `"use-vci": "true"` label.

```YAML
apiVersion: v1
kind: ConfigMap
metadata:
  name: vci-profile         # The name of the ConfigMap. It must be vci-profile.
  namespace: kube-system    # The namespace to which the vci-profile file belongs. It must be kube-system.
data:
  selectors: |
    [
      {
        "name": "selector-demo",
        "namespaceSelector": {
          "matchLabels": {
            "vci": "true"
          }
        },
        "objectSelector":{
          "matchLabels":{
            "use-vci": "true"
          }
        }
      }
    ]
```





</Tab>
<Tab zoneid="MCPMBfWQxt" title="GPU load configuration example">
<TabTitle>GPU load configuration example</TabTitle>

By configuring `namespaceSelector` and `effect`, you can schedule pods whose namespaces carry the label `vci-gpu: "true"` to VCI. Additionally, use `effect` to add the annotation vci.vke.volcengine.com/preferred\-instance\-family: "vci.ini2" to the pods scheduled to VCI to specify the use of the VCI GPU instance specification family.

```YAML
apiVersion: v1
kind: ConfigMap
metadata:
  name: vci-profile         # The name of the ConfigMap. It must be vci-profile.
  namespace: kube-system    # The namespace to which the vci-profile file belongs. It must be kube-system.
data:
  selectors: |
    [
      {
        "name": "selector-demo",
        "namespaceSelector": {
          "matchLabels": {
            "vci-gpu": "true"
          }
        },
        "effect": {
          "annotations": {
            "vci.vke.volcengine.com/preferred-instance-family": "vci.ini2"
           }
        }
      }
    ]
```





</Tab>
</Tabs>


After configuring `selectors`, you can use the following command to confirm whether the `selectors` setting has taken effect.

```bash
kubectl get mutatingwebhookConfiguration general-webhook-mutate-configuration -o yaml
```


If the returned YAML contains the configured `selectors` field, the configuration is successful. If not, check whether the format of `selectors` is incorrect. For example, the following configuration will be added to the YAML content for the **CPU load configuration example**:

```YAML
- admissionReviewVersions:
  - v1
  - v1beta1
  clientConfig:
    caBundle: ...
    url: https://xx-general-webhook:9443/vci-profile
  failurePolicy: Fail
  matchPolicy: Equivalent
  name: vciprofile-0.mutating.ek8s.io
  namespaceSelector:
    matchLabels:
      vci: "true"
  objectSelector:
    matchLabels:
      use-vci: "true"
  reinvocationPolicy: Never
  rules:
  - apiGroups:
    - ""
    apiVersions:
    - '*'
    operations:
    - CREATE
    resources:
    - pods
    scope: '*'
  sideEffects: None
  timeoutSeconds: 10
```


<span id=".5YWo5bGA5Zu65a6a6YWN572u6aG5"></span>
## Globally fixed configuration items

The fixed configuration items included in `data`, such as `preferredSubnetIds` and `tlsEnable`, correspond to the subnets of the VPC, log collection, and other information related to pods. You can update these items as needed. The updated configuration takes effect immediately and does not require a restart of the vci\-virtual\-kubelet add\-on.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The globally fixed configuration in the vci\-profile file applies at the cluster level. This means that, during VCI pod creation:</div>



* <div data-tips="true" data-tips-type="tip">If no other configuration exists, the globally fixed configuration in the vci\-profile file is used.</div>


* <div data-tips="true" data-tips-type="tip">If additional configuration has been set for VCI pods via an annotation, the additional annotation\-based configuration has higher priority than the global fixed configuration priority in the vci\-profile file.</div>



The detailed parameter description is as follows:


|Parameter |Sample value |Description |
|---|---|---|
|preferredSubnetIds |subnet\-3tispp1nai1\*\*\*\*, subnet\-3tispp1nai2\*\*\*\* |The VPC subnets for VCI pods. Subnets in different availability zones can be configured. To specify multiple subnets, separate them with commas (`,`).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the current virtual node can only recognize a single subnet in the current availability zone, selection will follow the order in which the subnets are specified.</div><br> |
|tlsEnable |true |Whether to enable log collection from the VCI pod to BytePlus TLS. Valid values:<br><br><br>* **true**: Enable log collection.<br><br>* **false**: Do not enable log collection. |
|securityContextPrivilegedConfig |ignore |Compatibility configuration for the privileged mode of VCI pods at both pod and container levels.<br><br>By default, enabling privileged mode for a VCI pod will cause pod creation to fail. You can configure globally to ignore privileged mode. Valid values:<br><br>**ignore**: Pods deployed using VCI will ignore privileged mode configuration. |
|dnsPolicyClusterFirstWithHostNetConfig |clusterFirst |DNS resolution configuration inside VCI pods.<br><br>By default, the `dnsPolicy` of VCI pods does not support `ClusterFirstWithHostNet`. You can use global configuration to automatically convert `ClusterFirstWithHostNet` to `ClusterFirst`. Valid values:<br><br>**clusterFirst**: DNS resolution behavior will automatically be converted from `ClusterFirstWithHostNet` to `ClusterFirst` for pods deployed using VCI. |
|volumesHostPathConfig |ignore |Configuration for mounting node file directories in VCI pods.<br><br>By default, the `volumes.hostPath` of VCI pods will cause pod creation to fail. You can configure at the global level to ignore this parameter. Valid values:<br><br>**ignore**: Pods deployed to VCI will ignore the configuration for mounting node file directories. |
|hostIpConfig |podIp |The display field of the node IP address parameter `status.hostIP` for VCI pods.<br><br>By default, `status.hostIP` of VCI pods shows the IP address of the virtual node. You can use global configuration to change it to show the IP address of the VCI pod. Valid values:<br><br>**podIp**: Pods deployed using VCI will use the pod IP as the value for `status.hostIP`. |
|enforceSelectorToVci |true |Whether pods selected by `selectors` in the vci\-profile file are forcibly scheduled to VCI.<br><br>By default, pods selected by `selectors` in the vci\-profile file are more likely to be scheduled to VCI, but they may be affected by the ResourcePolicy settings and other capabilities set by the scheduler, which may result in not all selected pods being scheduled to VCI. You can use global `selectors` settings to enforce scheduling to VCI. Forced scheduling to VCI ignores resource policy settings (such as scheduler settings and ResourcePolicy settings) and ensures that pods are always scheduled to VCI. Valid values:<br><br>**true**: Pods deployed using the vci\-profile file will be forcibly scheduled to VCI, ignoring resource policy settings (such as scheduler settings and ResourcePolicy settings). |
|timezone |Asia/Shanghai |Set the time zone for the virtual node. After the time zone synchronization feature is enabled for VCI pods, the time zone of the virtual node will be used.<br><br>The parameter supports configuring any time zone, with the format identical to the file name of the time zone in the Linux `/usr/share/zoneinfo/` directory, for example, `Asia/Shanghai`. |

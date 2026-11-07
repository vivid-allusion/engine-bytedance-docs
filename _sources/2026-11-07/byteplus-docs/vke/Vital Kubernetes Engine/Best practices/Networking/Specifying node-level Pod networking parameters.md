---
title: "Specifying node-level Pod networking parameters"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Configuring-pod-security-groups-and-subnets-on-a-NodePool-basis"
---

Node\-level Pod networking parameters are used to specify different Pod networking configurations for different nodes, enabling more fine\-grained network isolation and resource management. This topic describes how to configure node\-level Pod networking parameters in a VKE cluster and validate the result.

<span id="H3FSYMfU"></span>
## Background

In VKE clusters, cello within the vpc\-cni add\-on is used for Pod network management, such as assigning IP addresses to Pods and binding elastic network interfaces (ENIs). By default, all network configurations of cello (such as Pod subnets, security groups, ENI quotas, and network modes) are cluster‑scope configurations. All nodes in the cluster share the same network configuration (cello\-config). For more details, see [vpc-cni](https://docs.byteplus.com/en/docs/vke/vpc-cni-add-on?lang=en).

Cluster\-level configurations meet the requirements of most scenarios. However, this unified global configuration can cause many issues when nodes in a cluster run significantly different workloads. For example, some nodes run high\-density Pods and require a more aggressive IP pooling policy to accelerate Pod startup. Some nodes host specific business workloads that need to be assigned to dedicated Pod subnets or bound to exclusive security groups to meet network isolation and security compliance requirements. Nodes of different instance types have different requirements for ENI quotas.

To meet the preceding requirements, VKE supports node\-level network configurations. You only need to create a custom network configuration (ConfigMap) and specify this configuration on the target node pool or node using a label to achieve different node\-level configurations. This solution offers the following advantages:


* **Fine\-grained management**: Adjust network parameters at the per‑node granularity. You do not need to modify the entire cluster configuration for individual nodes. This prevents a minor change from causing a major impact.

* **Flexible adaptation to diverse workloads**: Configure IP pooling policies, Pod subnets, and security groups per node to achieve isolation and compliance in mixed deployments.

* **Smooth compatibility with existing clusters**: Node‑level configurations take effect in overwrite mode, without affecting existing nodes that do not have the required labels. This keeps change risks under control.


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* Only clusters that use the VPC\-CNI network model support configuring node\-level Pod networking parameters.

* By default, this configuration only takes effect for newly created nodes in the node pool. To make it take effect for existing nodes, you need to restart the vpc\-cni add\-on Pod on the corresponding node. Restarting may affect running workloads. Therefore, we do not recommend directly enabling this feature on existing nodes hosting production workloads.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A cluster that uses the VPC\-CNI network model has been created. For details, see [Creating managed clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

* The vpc\-cni add\-on has been upgraded to v1.6.0 or later. For details, see [vpc-cni](https://docs.byteplus.com/en/docs/vke/vpc-cni-add-on?lang=en).

* (Optional) If you need to configure Pod security groups and subnets, they need to reside within the same VPC as the cluster. Custom security groups and subnets have been created. For details, see [Creating security groups](https://docs.byteplus.com/en/docs/vpc/Creating-a-security-group) and [Creating subnets](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Connect to the target cluster using kubectl. For details, see [Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

2. Create a ConfigMap for the node‑level Pod networking parameters. The code of the sample file `node-config.yaml` is as follows:

   ```YAML
   apiVersion: v1
   kind: ConfigMap
   metadata:
     name: node-config1  # The ConfigMap name.
     namespace: kube-system  # The namespace to which the ConfigMap belongs. You can specify a custom namespace. We recommend that you use the kube-system namespace.
   data:
     conf: |
       {
         "subnets": [ # Configure the subnets used by Pods on the node.
           "subnet-2d6w87rhbgnb45********",
           "subnet-zfedjv8bb8r8ob********"
         ],
         "securityGroups": [ # Configure the security groups used by Pods on the node.
           "sg-2bztk3p36bd342dx0********"
         ],
         "poolTarget": 3, # The target number of pre-reserved Pod network resources on the node.
         "poolTargetMin": 5, # The minimum number of pre-reserved Pod network resources on the node.
         "poolTargetLimit": 1  # The maximum proportion of pooled resources to the available quota of the node.
       }
   ```
   

   The following table describes the key network features and parameters.

   
   |Network feature |Configuration examples |Description |
   |---|---|---|
   |Pod subnets |```YAML```<br>```"subnets": [```<br>```  "subnet-2d6w87rhbgnb45********",```<br>```  "subnet-zfedjv8bb8r8ob********"```<br>```  ]```<br> |Configure the subnets used by Pods on the node.<br><br>We recommend keeping this configuration stable throughout the lifecycle of the node. Otherwise, Pods created at different times may use different subnets, increasing network connectivity and O&M complexity. |
   |Pod security group |```YAML```<br>```"securityGroups": [```<br>```  "sg-2bztk3p36bd342dx0********"```<br>```]```<br> |Configure the security groups used by Pods on the node.<br><br>We recommend keeping this configuration stable across the lifecycle of the node. Otherwise, different Pods on the node may use different security groups, resulting in inconsistent access policies.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">For this parameter, you cannot specify a managed security group. Otherwise, exceptions may occur. For more information about managed security groups, see <a href="https://docs.byteplus.com/en/docs/vpc/Security-group-overview">Security group overview</a>.</div><br> |
   |Pooling parameters |```YAML```<br>```"poolTarget": 3,```<br>```"poolTargetMin": 5,```<br>```"poolTargetLimit": 1```<br> |cello IP pooling parameters. The system manages VPC ENIs and IPs through this parameter to accelerate Pod creation. When you configure pooling parameters, you need to balance Pod startup speed and IP resource consumption.  <br><br><br>* `poolTarget`: The target number of pre\-allocated Pod network resources on the node. cello attempts to prepare this number of available IP or ENI resources in advance, reducing the time Pods spend waiting for network resources during creation.<br><br>* `poolTargetMin`: The minimum number of pre\-allocated Pod network resources on the node. When the number of available resources is lower than this value, cello attempts to supplement resources to prevent insufficient resources during high\-frequency Pod creation on the node.<br><br>* `poolTargetLimit`: The percentage of the available quota of the node that can be occupied by pooled resources. Valid values: 0 to 1. A value of 1 indicates that pooled resources can occupy up to 100% of the node quota. cello calculates the resources that can be reserved based on the ENI or IP quota of the node instance type, preventing pooled resources from consuming excessive node network quota. |
   

3. Run the following command to create a ConfigMap.

   ```Bash
   kubectl apply -f node-config.yaml
   ```
   

4. Add a **node label** to the node pool, and set its value to the ConfigMap you created in the previous step. For more information about node pool parameters, see [Editing node pools](https://docs.byteplus.com/en/docs/vke/Managing-NodePools#.57yW6L6R6IqC54K55rGg).

   * The label key is `vke.volcengine.com/vpc-cni-config`.

   * The label value is `kube-system.node-config1`, where `kube-system` and `node-config1` are the namespace and name of the ConfigMap, respectively.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If the error message <strong>The specified ConfigMap is not in the correct format</strong> is returned, use a JSON validator to check the format of the <code>conf</code> field in the ConfigMap.   </div>
   

<span id="nxNRpwKe"></span>
## Validate results

After the configuration is complete, you can scale out the node pool to confirm whether the newly added nodes use the specified node\-level networking configuration. This topic uses node\-level subnets and security groups as examples.


1. Scale out the node pool to enable the ENIs of the newly added nodes to use the security group and subnet configured in the specified ConfigMap. For operations related to node pool scale\-out, see [Scaling node pools](https://docs.byteplus.com/en/docs/vke/Scaling-a-NodePool?lang=en).

   This topic provides an example of how to scale out a new node. As shown in the following figure, a node named **node\-qp6k6s** is scaled out.

2. Check whether the ENI of the newly scaled\-out node uses the specified subnet and security group.

   1. Log in to the [ECS console](https://console.byteplus.com/ecs).

   2. In the left navigation bar, click **Instances & Images** \> **Instances**.

   3. Search for the target instance by node name and then click the instance name.

   4. On the instance details page, check whether the auxiliary ENI with the `volc:vke:created-by=cello` label uses the specified security group and subnet on the **Network Interface** tab.

3. Schedule the business pods to the target node. Use the pod security group and subnet at the node pool level in your business scenarios.

   This topic provides an example of how to configure node affinity scheduling for a Deployment. In this way, pods are scheduled to the **node\-qp6k6s** node in the node pool with the label `vke.volcengine.com/vpc-cni-config: kube-system.node-config1`. For the configuration descriptions of Deployments, see [Managing Deployments](https://docs.byteplus.com/en/docs/vke/Managing-Deployments).

---
title: "Capacity scheduling"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Capacity-scheduling"
---

VKE provides the capacity scheduling feature to support resource elasticity in big data and machine learning scenarios. This topic describes how to use the capacity scheduling feature. 

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">[<a href="https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features"><strong>Beta · Apply for Trial</strong></a>]: This feature is currently in the beta stage. Submit an application if you need to use it.</div>


<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

In some enterprise cluster setups, a single cluster may be shared across multiple departments (or users). Native Kubernetes uses ResourceQuota to allocate fixed resources to each user, thereby isolating their resource capacities. However, this approach has a key limitation: resources cannot be elastically shared between users. For example, if one department faces resource shortages while another has idle resources in the same cluster, the resource\-constrained department cannot utilize the idle resources, leading to suboptimal cluster resource utilization. This inefficiency is especially obvious in big data and machine learning workloads.

VKE implements capacity scheduling by leveraging the extension mechanism of Kubernetes Scheduling Framework and introducing ElasticQuota on the scheduling side. This enhances overall cluster resource utilization through resource sharing while guaranteeing allocated resources of each user.

<span id=".5Yqf6IO95qaC6L-w"></span>
## Feature overview

<span id=".Y2FwYWNpdHkt6LCD5bqm5qC45b-D6IO95Yqb"></span>
### Core capabilities of capacity scheduling

Capacity scheduling has the following capabilities:


* Elastic quota resources can be defined at different levels.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bf915e17b799a028b0857a38ed3611fe.png) </span>

   * A maximum of two levels of ElasticQuota can be set. As shown in the figure above, root.1 and root.2 are the first level, and root.1.1 and root.1.2 are the second level.

   * A leaf\-level ElasticQuota must be associated with a namespace. As shown in the figure, root.2, root.1.1, and root.1.2 are leaf\-level ElasticQuotas, so they must be associated with custom namespaces.

   * A single ElasticQuota can be associated with multiple namespaces.

   * A namespace can only be associated with one leaf\-level ElasticQuota.

   * The hierarchical ElasticQuota relationship is represented by labels.

      
      |Label |Default value |Description |
      |---|---|---|
      |vke.volcengine.com/elasticquota\-is\-parent |false |Whether the ElasticQuota can be attached to a leaf\-level ElasticQuota. Valid values:<br><br><br>* true: Yes.<br><br>* false: No. |
      |vke.volcengine.com/elasticquota\-parent |root |The parent level of the ElasticQuota. Valid values:<br><br><br>* root: The parent of the first\-level ElasticQuota is always root. root is the default root node created by the system.<br><br>* Custom: The parent of the second\-level ElasticQuota is the custom name of the associated first\-level ElasticQuota. |
      

* It supports resource borrowing and reclaiming between different ElasticQuotas.

   * Whether ElasticQuota resources can be borrowed is indicated by a label.

      
      |Label |Default value |Description |
      |---|---|---|
      |vke.volcengine.com/elasticquota\-allow\-lent |true |Whether to allow the ElasticQuota resource to be borrowed. Valid values:<br><br><br>* true: Yes.<br><br>* false: No. |
      

   * By setting the maximum resource limit (Max) and minimum guaranteed resource (Min), resource borrowing and reclaiming policies between different ElasticQuotas are enforced.

      * The sum of the Min values of child ElasticQuotas must be less than or equal to the Min value of the parent ElasticQuota.

      * The system automatically calculates the sum of the Min values of level\-1 ElasticQuotas and the guaranteed resources of the cluster. It keeps the sum of the Min values of level\-1 ElasticQuotas less than or equal to the guaranteed resources of the cluster.

* It supports setting quotas for multiple resources, such as CPU, GPU, and memory.

* Resources can be fairly allocated based on ElasticQuota weights. Unused Min resources from an ElasticQuota are fairly distributed to other ElasticQuotas by weight.


<span id=".6ZuG576k6LWE5rqQ5by55oCn6YWN6aKd5YiS5YiG"></span>
### Elastic quota allocation for cluster resources

The following schematic diagram illustrates the elastic quota allocation of cluster resources.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7f06ce1a5bb2be24834727c5744bea20.png) </span>

In VKE, cluster resources are divided into two parts from the perspective of ElasticQuota:


* User\-defined quota:

   Users create custom ElasticQuotas by configuring level\-1 and level\-2 ElasticQuotas, establishing hierarchical relationships, and associating custom namespaces under leaf\-level quotas (e.g., the three namespaces namespace\-1, namespace\-2, and namespace\-3 in the above diagram).

* System default quota:

   * System group: Refers to the ElasticQuota of the kube\-system namespace. It is automatically calculated by the system and cannot be modified by users.

   * Default group: All resources not belonging to the System group or user\-defined groups are included in the Default group, and their quotas are computed by the system.


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage limits

Currently, you can enable the capacity scheduling feature only when you create a cluster. After it is enabled, its configuration cannot be modified for the time being.

<span id=".5L2_55So5pa55rOV"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5Yib5bu66ZuG576k5bm25byA5ZCvLWNhcGFjaXR5Leiwg-W6pg=="></span>
### Step 1: Create a cluster and enable capacity scheduling

This topic uses two 4\-vCPU 16\-GiB Elastic Compute Service (ECS) instances to demonstrate the implementation principles and usage of capacity scheduling in VKE.


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar of the VKE console, click **Cluster**. On the page that appears, click **Create cluster**.

3. In the **Create cluster** dialog box, click **Create now** in the **Custom managed clusters** section.

4. On the **Create cluster** page, specify cluster parameters based on the on\-screen prompts and your business requirements.

   Specify some parameters based on the following descriptions. For detailed configuration instructions for other parameters, see [Creating managed clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

   * In the **Node pool configuration (Optional)**  step, select a 4\-vCPU and 16\-GiB **Instance type** from any instance family and set the **Number of nodes** to `2`.****

   * In the **Addon configuration** step, find the **scheduler\-plugin** card and click Configuration. In the scheduler\-plugin parameter configuration dialog box, enable **Capacity scheduling**.

4. Confirm the settings and click **Confirm**.


<span id=".5q2l6aqk5LqM77ya6KeE5YiS5by55oCn6YWN6aKd"></span>
### Step 2: Plan elastic quotas

To demonstrate ElasticQuota planning, this example creates four ElasticQuotas (**root.** 1, ** root.** 2, ** root.1.** 1, and ** root.1.** 2) and associates them with three namespaces (**namespace\-1**,  ** namespace\-2**, and ** namespace\-3**).


1. Connect to the cluster via kubectl. For details, see [Connecting to a cluster](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

2. Run the following command to create the three namespaces.

   ```bash
   kubectl create ns namespace-1
   kubectl create ns namespace-2
   kubectl create ns namespace-3
   ```
   

3. Run the command to create YAML files for defining the four ElasticQuotas.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The ElasticQuotas must be created within the kube\-system namespace, and leaf\-level ElasticQuotas must be associated with custom namespaces.   </div>
   

   * root.1

      ```yaml
      apiVersion: scheduling.vke.volcengine.com/v1beta1
      kind: ElasticQuota
      metadata:
        labels:
          vke.volcengine.com/elasticquota-allow-lent: "true" # Whether guaranteed resources during an idle window can be lent to other ElasticQuotas.
          vke.volcengine.com/elasticquota-is-parent: "true" # Leaf-level quotas can be attached to this ElasticQuota.
          vke.volcengine.com/elasticquota-parent: root # The parent of this ElasticQuota is root.
        name: root.1
        namespace: kube-system # The configuration takes effect only if the value is set to kube-system.
      spec:
        max:
          cpu: 4
          memory: 40Gi
          nvidia.com/gpu: 2
        min:
          cpu: 2
          memory: 40Gi
          nvidia.com/gpu: 2
      ```
      

   * root.2

      ```yaml
      apiVersion: scheduling.vke.volcengine.com/v1beta1
      kind: ElasticQuota
      metadata:
        labels:
          vke.volcengine.com/elasticquota-allow-lent: "true" # Whether guaranteed resources during an idle window can be lent to other ElasticQuotas.
          vke.volcengine.com/elasticquota-is-parent: "false" # Leaf-level quotas cannot be attached to this ElasticQuota.
          vke.volcengine.com/elasticquota-parent: root # The parent of this ElasticQuota is root.
        name: root.2
        namespace: kube-system # The configuration takes effect only if the value is set to kube-system.
      spec:
        max:
          cpu: 6
          memory: 40Gi
          nvidia.com/gpu: 2
        min:
          cpu: 4
          memory: 20Gi
          nvidia.com/gpu: 1
        namespaces:        # The namespace associated with the ElasticQuota.
        - namespace-3        
      ```
      

   * root.1.1

      ```yaml
      apiVersion: scheduling.vke.volcengine.com/v1beta1
      kind: ElasticQuota
      metadata:
        labels:
          vke.volcengine.com/elasticquota-allow-lent: "true" # Whether guaranteed resources during an idle window can be lent to other ElasticQuotas.
          vke.volcengine.com/elasticquota-is-parent: "false" # Leaf-level quotas cannot be attached to this ElasticQuota.
          vke.volcengine.com/elasticquota-parent: root.1 # The parent of this ElasticQuota is root.1.
        name: root.1.1
        namespace: kube-system # The configuration takes effect only if the value is set to kube-system.
      spec:
        max:
          cpu: 4
          memory: 40Gi
          nvidia.com/gpu: 2
        min:
          cpu: 1
          memory: 20Gi
          nvidia.com/gpu: 1
        namespaces:        # The namespace associated with the ElasticQuota.
        - namespace-1   
      ```
      

   * root.1.2

      ```yaml
      apiVersion: scheduling.vke.volcengine.com/v1beta1
      kind: ElasticQuota
      metadata:
        labels:
          vke.volcengine.com/elasticquota-allow-lent: "true" # Whether guaranteed resources during an idle window can be lent to other ElasticQuotas.
          vke.volcengine.com/elasticquota-is-parent: "false" # Leaf-level quotas cannot be attached to this ElasticQuota.
          vke.volcengine.com/elasticquota-parent: root.1 # The parent of this ElasticQuota is root.1.
        name: root.1.2
        namespace: kube-system # The configuration takes effect only if the value is set to kube-system.
      spec:
        max:
          cpu: 4
          memory: 40Gi
          nvidia.com/gpu: 2
        min:
          cpu: 1
          memory: 20Gi
          nvidia.com/gpu: 1
        namespaces:        # The namespace associated with the ElasticQuota.
        - namespace-2
      ```
      

4. After creating the four ElasticQuotas, view the resource information related to capacity scheduling.

   * Run the following command to view the generated quota tree (ElasticQuotaTree).

      ```bash
       kubectl get ElasticQuotaTree -n kube-system system-elasticquota-tree -o yaml
      ```
      

      The expected response is as follows:

      ```yaml
      apiVersion: scheduling.vke.volcengine.com/v1beta1
      kind: ElasticQuotaTree
      metadata:
        annotations:
          cluster-capacity-resource: '{"cpu":"7800m","ephemeral-storage":"189273916718","hugepages-1Gi":"0","hugepages-2Mi":"0","memory":"26811077427200m","pods":"126"}'
          default-quota-used-resource: '{"cpu":"200m","memory":"128Mi"}'
          guaranteed-sum-min-resource: '{"cpu":"7160m","ephemeral-storage":"189273916718","hugepages-1Gi":"0","hugepages-2Mi":"0","memory":"26058199859200m","pods":"126"}'
          root-children-sum-min-resource: '{"cpu":"6","memory":"60Gi","nvidia.com/gpu":"3"}'
          system-quota-used-resource: '{"cpu":"440m","memory":"590Mi"}'
        name: system-elasticquota-tree
        namespace: kube-system
      spec:  # Hierarchical relationship of ElasticQuotas and resource configuration.
        root:
        - name: root.1
          children:
          - name: root.1.1
            max: '{"cpu":"4","memory":"40Gi","nvidia.com/gpu":"2"}'
            min: '{"cpu":"1","memory":"20Gi","nvidia.com/gpu":"1"}'
            other: '{"is_parent":false,"namespaces":["namespace-1"]}'
          - name: root.1.2
            max: '{"cpu":"4","memory":"40Gi","nvidia.com/gpu":"2"}'
            min: '{"cpu":"1","memory":"20Gi","nvidia.com/gpu":"1"}'
            other: '{"is_parent":false,"namespaces":["namespace-2"]}'
          max: '{"cpu":"4","memory":"40Gi","nvidia.com/gpu":"2"}'
          min: '{"cpu":"2","memory":"40Gi","nvidia.com/gpu":"2"}'
          other: '{"is_parent":true}'
        - name: root.2
          max: '{"cpu":"6","memory":"40Gi","nvidia.com/gpu":"2"}'
          min: '{"cpu":"4","memory":"20Gi","nvidia.com/gpu":"1"}'
          other: '{"is_parent":false,"namespaces":["namespace-3"]}'
      ```
      

      The following table describes key parameters.

      
      |Parameters |Description |
      |---|---|
      |cluster\-capacity\-resource |The total ResourceQuota available to the cluster. |
      |default\-quota\-used\-resource |The resource quota already used by the Default group. |
      |root\-children\-sum\-min\-resource |The sum of the Min values of level\-1 ElasticQuotas. |
      |system\-quota\-used\-resource |The resource quota already used by the System group. |
      |guaranteed\-sum\-min\-resource |The guaranteed resource quota automatically calculated by the system.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">The guaranteed\-sum\-min\-resource is calculated by using the following formula: <code>guaranteed-sum-min-resource</code> = <code>cluster-capacity-resource</code> \- <code>system-quota-used-resource</code> \- <code>default-quota-used-resource</code>.</div><br><br><br>   <div data-tips="true" data-tips-type="warning">After capacity scheduling is enabled for a cluster, you can view the Quota tree to obtain the values of the above parameters.   </div><br>   <br><br>* <div data-tips="true" data-tips-type="warning">The value of <code>root-children-sum-min-resource</code> must be less than or equal to the value of <code>guaranteed-sum-min-resource</code>. The cluster can guarantee the resource quota only after you define the Min value of the ElasticQuota.</div><br> |
      

   * View the YAML content of the four ElasticQuotas: **root.1**, **root.2**, **root.1.1**, and **root.1.2**. The system will automatically add capacity scheduling\-related annotations to ElasticQuotas.

      The following YAML example is for the **root.1** resource.

      ```yaml
      apiVersion: scheduling.vke.volcengine.com/v1beta1
      kind: ElasticQuota
      metadata:
        annotations:
          vke.volcengine.com/elasticquota-fair-share: '{"cpu":"3160m"}' # The eventually allocatable resources calculated for the ElasticQuota based on fairness settings.
          vke.volcengine.com/elasticquota-request: '{"cpu":"4"}' # The total requests of pods in the namespace associated with this ElasticQuota.
        labels:
          vke.volcengine.com/elasticquota-allow-lent: "true" # Whether guaranteed resources during an idle window can be lent to other ElasticQuotas.
          vke.volcengine.com/elasticquota-is-parent: "true" # Leaf-level quotas can be attached to this ElasticQuota.
          vke.volcengine.com/elasticquota-parent: root # The parent of this ElasticQuota is root.
        name: root.1
        namespace: kube-system
      spec:
        max:      # Maximum resources available.
          cpu: 4
          memory: 40Gi
          nvidia.com/gpu: "2"
        min:      # Minimum resources available. The sum of the Min values used by all users must be less than the total amount of resources in the cluster.
          cpu: "2"
          memory: 40Gi
          nvidia.com/gpu: "2"
        weight:   # The weight of the ElasticQuota. A greater weight indicates lower probability of being allocated the remaining resources. Max is used by default. We recommend against setting a custom weight in most cases.
          cpu: 4
          memory: 40Gi
          nvidia.com/gpu: "2"
      status:
        used:
          cpu: "2"        
      ```
      


<span id=".5q2l6aqk5LiJ77ya6YOo572y5bqU55So"></span>
### Step 3: Deploy an application

In this example, an NGINX Deployment is deployed to verify from the CPU perspective whether capacity scheduling is functioning normally.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can upload the NGINX image to BytePlus Container Registry in advance by following the instructions in <a href="https://docs.byteplus.com/en/docs/cr/push-and-pull-images">Pushing and pulling images</a>.</div>



1. Create a Deployment named **nginx\-in\-ns1** under the **namespace\-1** namespace.

   In this example, some parameters need to be configured according to the following description. For information on how to configure other parameters, see [Creating Deployments](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment).

   * In the **Basic information** step, for **Namespace**, select the created **namespace\-1**, and set **Number of instances** to `2`.

   * In the **Container configuration** step, go to the **ResourceQuota** section and set **CPU request** to `2` cores, and **CPU limit** to `2` cores.

2. After **nginx\-in\-ns1** is created successfully, click the workload name to enter the details page, then click the **List of instances** tab to view the status of the pod instances.

   Because resources on the node are sufficient, the status of both pod instances is **Running**.

3. Create a Deployment named **nginx\-in\-ns3** in the **namespace\-3** namespace.

   In this example, some parameters need to be configured according to the following description. For information on how to configure other parameters, see [Creating Deployments](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment).

   * In the **Basic information** step, for **Namespace**, select the created **namespace\-3**, and set **Number of instances** to `4`.

   * In the **Container configuration** step, go to the **ResourceQuota** section and set **CPU request** to `1` core, and **CPU limit** to `1` core.

4. After **nginx\-in\-ns3** is created successfully, click the workload name to enter the details page, then click the **List of instances** tab to view the status of the pod instances.

   Because the previously created **nginx\-in\-ns1** used cluster resources, insufficient resources remain. Therefore, only two out of the four pod instances are in the **Running** state, while the other two are in the **Pending** state.

   After two or three minutes, the resource usage of pod instances in the namespaces associated with the four ElasticQuotas will change. This is because capacity scheduling is enabled for the cluster, and the four ElasticQuotas are defined.

   * **nginx\-in\-ns1** starts evicting pod instances to release borrowed resources.

   * **nginx\-in\-ns3** acquires the resources released from **nginx\-in\-ns1** and is able to successfully run the four pod instances.

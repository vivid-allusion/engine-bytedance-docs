---
title: "ResourcePolicy scheduling"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/ResourcePolicy-scheduling"
---

VKE provides the ResourcePolicy scheduling policy, which allows you to specify a custom ResourcePolicy to set the order in which pods of a workload are flexibly scheduled to different types of nodes, such as subscription ECS instances, pay\-as\-you\-go ECS instances, and virtual nodes. This topic describes how to configure custom ResourcePolicies to achieve ResourcePolicy scheduling.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The scheduler\-plugin add\-on has been installed in the target cluster and **ResourcePolicy scheduling** has been enabled. For detailed operations, see [scheduler-plugin add-on](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on#.c2NoZWR1bGVyLXBsdWdpbi3nu4Tku7Y=).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To use ResourcePolicy scheduling when Vital Container Instance (VCI) is used, make sure that a cluster related to VCI workloads has been created, the scheduler\-plugin add\-on has been installed in the cluster, and <strong>ResourcePolicy scheduling</strong> is enabled for the cluster. For VCI\-related cluster operations, see <a href="https://docs.byteplus.com/en/docs/vke/Integrating-with-VCI">Connecting to VCI</a>.   </div>
   

* When you use this capability in VCI workloads, we recommend that you enable the VCI inventory\-aware scheduling feature. For detailed operations, see [VCI inventory-aware scheduling](https://docs.byteplus.com/en/docs/vke/VCI-inventory-aware-scheduling).


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage limits


* The ResourcePolicy scheduling feature is only available in clusters of the following Kubernetes versions. If the cluster version does not meet the requirements, upgrade the cluster version. For details, see [Upgrading clusters](https://docs.byteplus.com/en/docs/vke/Upgrading-a-cluster).

   * [Kubernetes v1.24](https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v-1_24): 1.24.15\-vke.21 and later

   * [Kubernetes v1.26](https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v-1_26): 1.26.10\-vke.10 and later

   * Other later [Kubernetes versions](https://docs.byteplus.com/en/docs/vke/Kubernetes-version-release-notes) released by VKE

* This feature cannot be used with pod\-deletion\-cost of Kubernetes at the same time. For information about pod\-deletion\-cost, see [pod-deletion-cost](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/#pod-deletion-cost).

* When you create a ResourcePolicy, make sure that the scheduled pods in the target namespace are not managed by the ResourcePolicy. Otherwise, the scheduled pods will be preferentially scaled in.

* After you modify an existing ResourcePolicy, scheduled pods will be scaled in according to the order of the original ResourcePolicy and newly added pods will be scaled in according to the order of the updated ResourcePolicy.

* Only Deployments support reverse scale\-in through ResourcePolicies.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Reverse scale\-in: When a workload for which a ResourcePolicy is configured is being scaled in, the resource pool with the lowest priority specified in the ResourcePolicy will be scaled in first.   </div>
   

* Before you use this feature when VCI is used, see [What is VCI](https://docs.byteplus.com/en/docs/vke/What-is-Vital-Container-Instance) and [VCI usage restrictions](https://docs.byteplus.com/en/docs/vke/VCI-limits).


<span id=".5L2_55So5pa55rOV"></span>
## Procedure

Specify the priority of elastic resources in a ResourcePolicy.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">A ResourcePolicy only applies to the pods that are related to all workloads with the specified label in the namespace of the ResourcePolicy.</div>


* <div data-tips="true" data-tips-type="warning">The <strong>resource pool</strong> mentioned below is not the <strong>node pool</strong> defined in VKE. The <strong>resource pool</strong> is the collection of all nodes in a cluster that meet a specific filter condition.</div>


   <div data-tips="true" data-tips-type="warning">For example, <code>vci-pool</code> in the following content is the collection of nodes in the current cluster that meet the <code>type=virtual-kubelet</code> condition.   </div>
   


```YAML
apiVersion: scheduling.vke.volcengine.com/v1beta1
kind: ResourcePolicy
metadata:
  name: vke-resourcepolicy   # The ResourcePolicy object name.
  namespace: default   # The namespace to which the ResourcePolicy belongs. The namespace must be the same as the namespace of the scheduled pods.
spec:
  selector:   # The label selector of pods that are managed by the ResourcePolicy.
    app: nginx
  subsets:   # The resource pool configurations.
  - name: pool-1   # The resource pool name.
    maxReplicas: 100   # The maximum number of pods scheduled to the resource pool.
    maxReplicasRatio: "0.1"  # The threshold of the ratio of pods scheduled to the resource pool to all pods. When this threshold is exceeded, no more pods will be scheduled to the resource pool.
    whenNotReachMax: ScheduleAnyWay   # The scheduling policy. Valid values: DoNotSchedule and ScheduleAnyWay.
    nodeSelectorTerm: 
    - key: cluster.vke.volcengine.com/machinepool-name   # The label key of the resource pool. machinepool-name in this example indicates the label key of the resource pool (node pool) ID.
      operator: In
      values:   # The label value of the resource pool, which is the ID of the resource pool (node pool).
      - pcgc1omersf******
      - ncljdfq33h3******
  - name: vci-pool   # The resource pool name.
    maxReplicas: 100 
    maxReplicasRatio: "0.1" 
    nodeSelectorTerm:
    - key: type
      operator: In
      values:
      - virtual-kubelet  # Match the virtual nodes that correspond to the VCI resources.
    tolerations: # If a pod is scheduled to the resource pool, an additional toleration needs to be added to the pod.
    - effect: NoSchedule
      key: vci.vke.volcengine.com/node-type
      operator: Equal
      value: vci

status:   # The current status of the ResourcePolicy.
  policyStatuses:  # The status of schedulable pods that correspond to each resource pool.
  - name: pool-1
    missingReplicas: 50
  - name: vci-pool
    missingReplicas: "-"
```


The following table describes key parameters.


|Parameters |Description |
|---|---|
|selector |The label selector of pods that are managed by the ResourcePolicy. It indicates that the ResourcePolicy applies to the pods with the specified label in the namespace of the ResourcePolicy. |
|subsets |The target resource pool. Pods will be first scheduled to the resource pool node that appears earliest in the sequence. When pods are being scaled in, the pods in the resource pool node that appears last in the sequence will be first scaled in.<br><br>The descriptions of sub\-parameters are as follows:<br><br><br>* name: the name of the resource pool<br><br>* maxReplicas: the maximum number of pods scheduled to the resource pool. If you do not specify this parameter, it indicates that the maximum number of pods is not limited. The value of the `maxReplicas` field can be estimated based on the ECS resource capacity or the VCI resource quota and the resource requirements of pods.<br><br>* maxReplicasRatio: The threshold of the ratio of pods scheduled to the resource pool to all pods managed by the ResourcePolicy. When this threshold is exceeded, no more pods will be scheduled to the resource pool. Valid value: [0,1].<br><br>* whenNotReachMax: the scheduling policy. Two policies are available.<br><br>   * DoNotSchedule: If the resource node pool has not reached the `maxReplicasRatio` or `maxReplicas` threshold, the pods can only be scheduled to the resource node pool or to a resource node pool with higher priority.<br><br>   * ScheduleAnyWay: If the resource node pool does not have any schedulable resources, regardless of whether the `maxReplicasRatio` or `maxReplicas` threshold has been reached, pods will be preferentially scheduled to the resource node pool with lower priority.<br><br>* nodeSelectorTerm: Select the resource node pool that pods can be scheduled by label.<br><br>* tolerations: If a pod is scheduled to the resource pool, an additional toleration needs to be added to the pod. The format of the value is the same as that of `pod.spec.tolerations` in Kubernetes. If you do not specify this parameter, you do not need to add additional tolerations to pods. |
|policyStatuses |The status of schedulable pods that correspond to each resource pool.<br><br><br>* name: the name of the resource pool<br><br>* missingReplicas: the number of remaining schedulable pods in the resource pool `missingReplicas: "-"` indicates that you did not specify maxReplicas when creating the ResourcePolicy. |


<span id=".5L2_55So56S65L6L"></span>
## Examples

This topic provides an example of how to create a ResourcePolicy and define the priority of elastic resources in the following scenario.

Your cluster contains a fixed number of ECS resources, which means that autoscaling is not configured for the node pool where the nodes are located. Your cluster also contains VCI resources. To reduce resource usage costs when you deploy a workload, such as Deployment, in the cluster, you need to deliver the following results:


* Deployed pods are preferentially scheduled to the fixed ECS resources. When the ECS resources are insufficient, the elastic VCI resources are used as supplementary resources.

* During scale\-in, pods on the VCI resources are preferentially deleted to release the VCI resources. Then, pods on the ECS resources are deleted to release the ECS resources.


This method primarily applies to workloads with steady and sustained traffic, which occasionally experience sudden traffic spikes. Fixed ECS resources can be used to handle long\-term stable traffic and the quick autoscaling capability of VCI can be used to handle sudden traffic spikes. For more sample scenarios, see the [Sample scenarios](https://docs.byteplus.com/en/docs/vke/ResourcePolicy-scheduling#.5Zy65pmv56S65L6L) section of this topic.

<span id=".5q2l6aqk5LiA77ya77yI5Y-v6YCJ77yJ5Yib5bu66ZuG576k5bm25byA5ZCv5by55oCn6LWE5rqQ5LyY5YWI57qn6LCD5bqm"></span>
### Step 1: (Optional) Create a cluster and enable ResourcePolicy scheduling

If you have an available cluster, install the scheduler\-plugin add\-on in the cluster, and enable ResourcePolicy scheduling, you can skip this step.


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar of the VKE console, click **Cluster**. On the page that appears, click **Create cluster**.

3. In the **Create cluster** dialog box, click **Create now** in the **Custom managed clusters** section.

4. On the **Create cluster** page, specify cluster parameters based on the on\-screen prompts and your business requirements.

   Specify some parameters based on the following descriptions. For detailed configuration instructions for other parameters, see [Creating managed clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

   * In this example, both ECS and VCI resources exist in the cluster. Therefore, select **VPC\-CNI** for the **Network model** parameter in the **Cluster configuration** step.

   * In the **Addon configuration** step, find the **scheduler\-plugin** card and click Configuration. In the scheduler\-plugin parameter configuration dialog box, enable **ResourcePolicy scheduling** and configure the scheduling weight.

4. Confirm the configurations and then click **Confirm** to create the cluster.


<span id=".5q2l6aqk5LqM77ya5Yib5bu6LXJlc291cmNlcG9saWN5"></span>
### Step 2: Create a ResourcePolicy


1. Connect to the VPC\-CNI cluster created in **Step 1** by using kubectl. For details, see [Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

2. Create a YAML file for the ResourcePolicy. The following `vke-resourcepolicy-nginx.yaml` file serves as an example:

   ```yaml
   apiVersion: scheduling.vke.volcengine.com/v1beta1
   kind: ResourcePolicy
   metadata:
     name: vke-resourcepolicy-nginx   
     namespace: default   # The namespace to which the ResourcePolicy belongs. The namespace must be the same as the namespace of the scheduled pods.
   spec:
     selector:
       app: demo-nginx   # The pods with the app:demo-nginx label will be managed by the ResourcePolicy.
     subsets:
     - name: pool-ecs    # The first subset is the ECS resource pool.
       maxReplicas: 2  # The maximum number of pods to be scheduled to the resource pool. In this example, the value is set to 2 to schedule pods to VCI resources when ECS resources are insufficient or the number of pods reaches the upper limit. Estimate the value based on the parameter description in the actual scenario.
       whenNotReachMax: ScheduleAnyWay  # Set the value to ScheduleAnyWay. This makes sure that pods can be directly scheduled to VCI resources when ECS resources are insufficient.
       nodeSelectorTerm: 
       - key: cluster.vke.volcengine.com/machinepool-name   
         operator: In
         values:
         - pcm5pq1r5i7aqm******   # The ID of the matched node pool that corresponds to the ECS resources. Make sure that the node pool ID is valid. You can specify multiple node pool IDs.
     - name: pool-vci   # The second subset is the VCI resource pool.
       maxReplicas: 100  # We recommend that you specify the maximum number of pods that can be scheduled to the VCI resource pool. This prevents the VCI ResourceQuota from being exhausted.
       nodeSelectorTerm:
       - key: type
         operator: In
         values:
         - virtual-kubelet  # Match the VCI virtual node.
       tolerations: # If a pod is scheduled to the resource pool, an additional toleration needs to be added to the pod.
       - effect: NoSchedule
         key: vci.vke.volcengine.com/node-type
         operator: Equal
         value: vci
   ```
   

3. Run the following command to create the ResourcePolicy.

   ```bash
   kubectl apply -f vke-resourcepolicy-nginx.yaml
   ```
   


<span id=".5q2l6aqk5LiJ77ya5Yib5bu65bel5L2c6LSf6L29"></span>
### Step 3: Create a workload

This topic provides an example of how to create a Deployment. For more workload\-related operations, see [Workloads](https://docs.byteplus.com/en/docs/vke/Workloads).


1. Create a YAML file for the Deployment. The following `demo-nginx.yaml` file serves as an example:

   ```yaml
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: demo-nginx
     namespace: default  # The namespace of the Deployment, which is consistent with that of the ResourcePolicy.
   spec:
     replicas: 5  # The number of pods.
     selector:
       matchLabels:
         app: demo-nginx
     template:
       metadata:
         labels:
           app: demo-nginx  # The pod label, which matches the label configured in the selector of the ResourcePolicy.
       spec:
         schedulerName: default-scheduler
         containers:
         - image: nginx:1.14.2  # The container image address and tag of the pod. Replace the values with those used in your business scenario.
           imagePullPolicy: IfNotPresent
           name: nginx-container
           resources:
             requests:
               cpu: 10m
               memory: 10Mi
         dnsPolicy: ClusterFirst
         restartPolicy: Always
         securityContext: {}
   ```
   

2. Run the following command to create the Deployment.

   ```bash
   kubectl apply -f demo-nginx.yaml
   ```
   


<span id=".5q2l6aqk5Zub77ya5p-l55yL6LCD5bqm57uT5p6c"></span>
### Step 4: View the scheduling result


1. Run the following command to view the scheduling result.

   ```bash
   kubectl get po -n default -o wide
   ```
   

   The expected output is as follows: Two pods are scheduled to ECS resources, and the remaining three pods are scheduled to VCI resources.

   ```bash
   NAME                          READY   STATUS    RESTARTS   AGE   IP               NODE                      NOMINATED NODE   READINESS GATES
   demo-nginx-6b6bfc8b7f-62qls   1/1     Running   0          66m   192.168.**.**    vci-node1-cn-shanghai-a   <none>           <none>
   demo-nginx-6b6bfc8b7f-97md6   1/1     Running   0          66m   192.168.**.**    192.168.**.**             <none>           <none>
   demo-nginx-6b6bfc8b7f-bzdnw   1/1     Running   0          66m   192.168.**.**    vci-node1-cn-shanghai-b   <none>           <none>
   demo-nginx-6b6bfc8b7f-rjrnx   1/1     Running   0          66m   192.168.**.**    vci-node1-cn-shanghai-a   <none>           <none>
   demo-nginx-6b6bfc8b7f-tjc5p   1/1     Running   0          31m   192.168.**.**    192.168.**.**             <none>           <none>
   ```
   

2. (Optional) View the status of resource release when a pod is being scaled in.

   1. Run the following command to reduce the number of pods in the Deployment to 3, which is the value of the **replicas** parameter.

      ```bash
      kubectl scale --replicas=3 deployment/demo-nginx -n default
      ```
      

   2. View the scheduling result.

      ```bash
      kubectl get po -n default -o wide
      ```
      

      The expected output is as follows: Two pods on VCI resources are scaled in first to release VCI resources.

      ```bash
      NAME                          READY   STATUS    RESTARTS   AGE   IP               NODE                      NOMINATED NODE   READINESS GATES
      demo-nginx-6b6bfc8b7f-97md6   1/1     Running   0          70m   192.168.**.**    192.168.**.**             <none>           <none>
      demo-nginx-6b6bfc8b7f-bzdnw   1/1     Running   0          70m   192.168.**.**    vci-node1-cn-shanghai-b   <none>           <none>
      demo-nginx-6b6bfc8b7f-tjc5p   1/1     Running   0          35m   192.168.**.**    192.168.**.**             <none>           <none>
      ```
      


<span id=".5Zy65pmv56S65L6L"></span>
## Sample scenarios

<span id=".5Zy65pmv5LiA77yadmNpLei1hOa6kC3oh6rliqjkvLjnvKnnmoQtZWNzLei1hOa6kA=="></span>
### Scenario 1: VCI resources and automatically scaled ECS resources


* **Scenario description**

   VCI resources are preferentially used when both VCI resources and automatically scaled ECS resources exist in the target namespace of the cluster. When the VCI resource quota is insufficient, pods will be scheduled to the ECS resources, and autoscaling will be triggered to scale out the ECS resource pool. This method mainly applies to workloads such as batch jobs that experience sudden, high resource usage. You do not need to maintain fixed ECS resource costs, and VCI is preferentially used to obtain cost\-effective elastic resources. When the VCI capacity is insufficient, ECS resources can be autoscaled to ensure sufficient resource supply.

* **Configuration description**

   1. Configure the virtual node that corresponds to the VCI resources as the first `subset.`

      We recommend that you specify the `maxReplicas` field under `subset` to prevent the VCI ResourceQuota from being exhausted. The value of the `maxReplicas` field can be estimated based on the VCI resource quota and the resource requirements of pods.

   2. Configure the node pool that corresponds to the ECS resources as the second `subset`.

        &nbsp;

      * You need to specify the `maxReplicas` field under `subset` to control the maximum number of ECS resources that can be used. The value of the `maxReplicas` field can be estimated based on the ECS resource capacity and the resource requirements of pods.

      * Set the `whenNotReachMax` field under `subset` to `DoNotSchedule`. In this way, when ECS resources are insufficient, scheduled pods will be in the Pending state for a short period of time, and then autoscaling will be triggered to scale out the ECS resource node pool.

      * Make sure that autoscaling is enabled for the corresponding ECS node pool. For details, see [Creating cluster autoscalers](https://docs.byteplus.com/en/docs/vke/Creating-a-Cluster-Autoscaler).

* **Sample configurations**

   ```yaml
   apiVersion: scheduling.vke.volcengine.com/v1beta1
   kind: ResourcePolicy
   metadata:
     name: vke-resourcepolicy-nginx   
     namespace: default
   spec:
     selector:
       app: nginx   # The pods with the app: nginx label will be managed by the ResourcePolicy.
     subsets:
     - name: pool-vci   # The first subset is the VCI resource pool, which means that VCI resources are preferentially used.
       maxReplicas: 100  # We recommend that you specify the maxReplicas field to prevent the VCI ResourceQuota from being exhausted.
       nodeSelectorTerm:
       - key: type
         operator: In
         values:
         - virtual-kubelet  # Match the VCI virtual node.
     - name: pool-ecs    # The second subset is the ECS resource pool, which serves as a supplement when the VCI resources are insufficient.
       maxReplicas: 1000  # You need to specify the maxReplicas field to control the maximum number of ECS resources that can be used.
       whenNotReachMax: DoNotSchedule  # If you set the value to DoNotSchedule, if the ECS node pool has insufficient resources, the pod will temporarily remain in the Pending state and wait for the node pool to be autoscaled.
       nodeSelectorTerm: 
       - key: cluster.vke.volcengine.com/machinepool-name   
         operator: In
         values:
         - pcgc1omersf******   # The ID of the matched ECS node pool. You can configure multiple node pools.
         - ncljdfq33h3******
       tolerations: # If a pod is scheduled to the resource pool, an additional toleration needs to be added to the pod.
       - effect: NoSchedule
         key: vci.vke.volcengine.com/node-type
         operator: Equal
         value: vci   
   ```
   


<span id=".5Zy65pmv5LqM77ya5oyJ5q-U5L6L5bCGLXBvZC3osIPluqbliLAtZWNzLei1hOa6kOWSjC12Y2kt6LWE5rqQ"></span>
### Scenario 2: Schedule pods to ECS resources and VCI resources by proportion


* **Scenario description**

   Schedule the pods in the workload to ECS resources and VCI resources based on the specified ratio to maintain the balance between fixed resources and elastic resources. This method is applicable when the workload is being switched from ECS resources to elastic VCI resources. You can use this method to gradually switch the workload by adjusting the scheduling ratio.

* **Configuration description**

   1. Configure the node pool that corresponds to the ECS resources as the `first` subset.

      You need to specify the `maxReplicasRatio` field under `subset` to schedule pods to the ECS resources based on the specified ratio.

   2. Configure the virtual node that corresponds to the VCI resources as the second `subset`.

      You need to specify the `maxReplicasRatio` field under `subset` to schedule pods to the VCI resources based on the specified ratio. We recommend that you keep the sum of the ratio thresholds of the `maxReplicasRatio` field for all `subsets` to 1.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">A deviation exists for the calculation of the scheduling ratio when a small number of pods exist. We do not recommend that you specify both <code>maxReplicasRatio</code> and <code>whenNotReachMax: DoNotSchedule</code>. Otherwise, some pods may be in the Pending state unexpectedly.   </div>
   

* **Sample configurations**

   ```yaml
   apiVersion: scheduling.vke.volcengine.com/v1beta1
   kind: ResourcePolicy
   metadata:
     name: vke-resourcepolicy-nginx   
     namespace: default
   spec:
     selector:
       app: nginx   # The pods with the app: nginx label will be managed by the ResourcePolicy.
     subsets:
     - name: pool-ecs    # The first subset is the ECS resource pool.
       maxReplicasRatio: "0.6"  # Set the scheduling ratio for the first resource pool to 0.6.
       whenNotReachMax: ScheduleAnyWay  # We recommend that you set the value to ScheduleAnyWay.
       nodeSelectorTerm: 
       - key: cluster.vke.volcengine.com/machinepool-name   
         operator: In
         values:
         - pcgc1omersf******   # The ID of the matched ECS node pool. You can configure multiple node pools.
         - ncljdfq33h3******
     - name: pool-vci   # The second subset is the VCI resource pool.
       maxReplicasRatio: "0.4"  # Set the scheduling ratio for the second resource pool to 0.4.
       whenNotReachMax: ScheduleAnyWay  # We recommend that you set the value to ScheduleAnyWay.
       nodeSelectorTerm:
       - key: type
         operator: In
         values:
         - virtual-kubelet  # Match the VCI virtual node.
       tolerations: # If a pod is scheduled to the resource pool, an additional toleration needs to be added to the pod.
       - effect: NoSchedule
         key: vci.vke.volcengine.com/node-type
         operator: Equal
         value: vci
   ```

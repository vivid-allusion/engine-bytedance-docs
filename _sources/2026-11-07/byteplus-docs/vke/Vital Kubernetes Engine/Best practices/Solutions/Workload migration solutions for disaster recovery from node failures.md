---
title: "Workload migration solutions for disaster recovery from node failures"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Node_failure_and_load_disaster_recovery_migration_solution"
---

This topic describes solutions for disaster recovery and migration of workloads in case of node failures.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

Your container workloads run on Kubernetes nodes. A recommended VKE best practice is to deploy workloads with multiple replicas distributed across multiple nodes to avoid situations where a single node failure causes overall business unavailability due to the inability to migrate pods instantly.

An example YAML for multiple\-replica and multi\-node workload deployment is shown below. For more information, see the [official Kubernetes documentation](https://kubernetes.io/zh-cn/docs/concepts/scheduling-eviction/topology-spread-constraints/).

```YAML
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  selector:
    matchLabels:
      app: nginx
  replicas: 3    # Deploy multiple replicas.
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
      topologySpreadConstraints:  # Control the distribution of pods across cluster topology.
      - maxSkew: 1   # Control the maximum allowed pod count difference. The value 1 indicates that the difference in the number of pods with app=nginx between any two nodes must not exceed 1.
        topologyKey: "kubernetes.io/hostname"  # TopologyKey. The current configuration indicates node-level distribution. topology.kubernetes.io/zone indicates region-level distribution.
        whenUnsatisfiable: ScheduleAnyway # Set the behavior when pod distribution cannot meet the constraints. Possible values: DoNotSchedule (do not schedule) or ScheduleAnyway (schedule anyway, even if the constraints are not satisfied).
        labelSelector:  # Indicate pod matching by label.
          matchLabels:
            app: nginx
```


However, in actual business scenarios, node failures may result in pods being unable to migrate for various reasons and consequent business losses. This topic provides disaster recovery and migration solutions for various workloads (especially StatefulSets) to help minimize impacts and losses in case of node failures.

<span id=".a3ViZXJuZXRlcy3nirbmgIHmnLrlj5jljJbmg4XlhrU="></span>
## Kubernetes state machine changes

When a node fails (before manual intervention and recovery), different Kubernetes resources exhibit distinct behaviors.

<span id=".6IqC54K56KGo546w"></span>
### Node behavior


1. After a node fails, the kubelet cannot report its heartbeat status, causing the node to become unreachable.

2. Forty seconds after the node becomes unreachable, the kube\-controller\-manager (KCM) marks it as NotReady and adds the `node.kubernetes.io/unreachable` taint.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The duration of node statuses is controlled by the following KCM parameters:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>node\-monitor\-period</strong>: The interval at which the node controller checks the status of each node. The default is 5 seconds.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>node\-monitor\-grace\-period</strong>: The time window for the node controller to consider a node failed. The default is 40 seconds, meaning a node is considered failed if no status updates are received within 40 seconds.   </div>
   


<span id=".5peg54q25oCB6LSf6L296KGo546w"></span>
### Deployment behavior


1. When a node is marked as NotReady, the KCM simultaneously marks all pods on that node as NotReady.

2. If the node remains in the NotReady state for five minutes, the KCM triggers pod recreation.

   * If the pod recreation policy is RollingUpdate, a new pod is created first, and then the original pod in the NotReady state (hereinafter referred to as the original pod) is deleted. However, due to node failure, the kubelet cannot delete the original pod on the node, so the original pod will remain indefinitely in the Terminating state (unless the node recovers or the pod is forcibly deleted).

   * If the pod recreation policy is ReCreate, the original pod is deleted first, and then a new pod is created. However, because the original pod cannot be deleted, the new pod cannot be created.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The duration of node statuses is controlled by the following kube\-apiserver parameters:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>default\-not\-ready\-toleration\-seconds</strong>: The tolerance duration for the <code>NotReady:NoExecute</code> taint, in seconds. The default is 300 seconds. By default, this toleration is added to every pod that does not already have this toleration.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>default\-unreachable\-toleration\-seconds</strong>: The toleration duration for the taint <code>Unreachable:NoExecute</code>, in seconds. The default is 300 seconds. By default, this toleration is added to every pod that does not already have this toleration.   </div>
   


<span id=".5pyJ54q25oCB6LSf6L296KGo546w"></span>
### StatefulSet behavior


1. When a node is marked as NotReady, the KCM simultaneously marks all pods on that node as NotReady.

2. If the node remains in the NotReady state for five minutes, the KCM triggers pod recreation. For a StatefulSet, the original pod is deleted first and then a new pod is created. However, due to node failure, the kubelet cannot delete the original pod on the node, so the original pod is stuck in the Terminating state and the new pod cannot be created.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the pod is bound to a PersistentVolumeClaim (PVC), migration of the StatefulSet will involve releasing and rebinding the PersistentVolume (PV). In case of a node failure, the associated PV cannot be disassociated from the node.   </div>
   

<span id=".5pyN5Yqh77yIc2VydmljZe-8ieihqOeOsA=="></span>
### Service behavior


1. In case of a node failure, pods on the node may not be accessible. If the pod is associated with a Service, the pod will not be removed from the Endpoints immediately. When requests are routed to the pod through the Service, the requests will fail.

2. After the node remains in the NotReady state for 40 seconds, as the pod is marked as NotReady, the corresponding Service\-related Endpoints will add NotReady pod information via the `subsets.notReadyAddresses` parameter. At this point, Service traffic will not reach the NotReady pods.


<span id=".5Lq65bel5LuL5YWl5oGi5aSN5q2l6aqk"></span>
## Manual recovery steps

<span id=".5L2_55So6ZmQ5Yi2"></span>
### Limits

Before performing manual recovery, pay attention to the following restrictions:


* The cluster must have other available nodes (in addition to the failed node) that can sufficiently accommodate the workloads to be migrated.

* Do not operate on virtual nodes during manual intervention. Otherwise, VCI pods will be evicted. If you must operate on a virtual node, [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000210) to get professional technical support.

* Node failures are generally categorized into three types: ‌**graceful node shutdown‌** , ‌**non\-graceful node shutdown‌** , and **kubelet exception**. Among these types, **graceful node shutdown** does not require manual intervention. This topic provides load migration solutions for the other two types of node failure:

   * **Graceful node shutdown**: If the [graceful node shutdown feature](https://kubernetes.io/zh-cn/docs/concepts/cluster-administration/node-shutdown/) is enabled, when the system shuts down, the kubelet will attempt to detect this event and gracefully shut down the pods running on the node. This enables automatic load migration without requiring manual intervention. Enabling this feature requires certain conditions to be met. For details, see the [Kubernetes documentation](https://kubernetes.io/zh-cn/docs/concepts/cluster-administration/node-shutdown/).

   * **Non\-graceful node shutdown**: The node shutdown event cannot be detected by kubelet (for example, node crashes or disabled graceful shutdown). This leads to the [Kubernetes state machine changes](https://docs.byteplus.com/en/docs/vke/Node_failure_and_load_disaster_recovery_migration_solution#.a3ViZXJuZXRlcy3nirbmgIHmnLrlj5jljJbmg4XlhrU=) described earlier.

   * **Kubelet exception:**  The node loses connection with the control plane, but the workloads on the node may still run normally. For this scenario, it is recommended to first try to restart kubelet or attempt to restore the node. If restoration is not possible, remove the node from the cluster via the VKE console to prevent workloads on the node from interfering with business operations when they are out of Kubernetes management (for example, for RPC frameworks with independent service discovery like Dubbo).


<span id=".5peg54q25oCB6LSf6L29"></span>
### Deployments


1. Ensure that the update policy of these workloads is `RollingUpdate`.

   ```yaml
   strategy:
     type: RollingUpdate
     rollingUpdate:
       maxUnavailable: 25%
       maxSurge: 25%
   ```
   

2. Manually run the `rollout` command to quickly recreate pods under the Deployment.

   ```bash
   kubectl rollout restart deployment/nginx
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><code>deployment/nginx</code> is the <code>Deployment name or the pod name within the Deployment</code>. You need to replace it with your actual information.   </div>
   

   The expected response is as follows:

   ```bash
   deployment.apps/nginx restarted
   ```
   


<span id=".5pyJ54q25oCB6LSf6L29"></span>
### StatefulSets

<span id=".a3ViZXJuZXRlcy12MS0yNi3kuYvliY0="></span>
#### Before Kubernetes v1.26

Implement load migration by forcibly deleting the pod and waiting for exclusive resources to be disassociated and released. The detailed steps are as follows:


1. Forcibly delete the original pod on the failed node so that exclusive resources are disassociated from the original pod.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If exclusive resources are not disassociated from the original pod, the new pod will be stuck in the Creating state.   </div>
   

   ```bash
   kubectl delete pod nginx-1 --force
   ```
   

   The expected response is as follows:

   ```bash
   Warning: Immediate deletion does not wait for confirmation that the running resource has been terminated. The resource may continue to run on the cluster indefinitely.
   pod "nginx-1" force deleted
   ```
   

2. Wait for exclusive resources (if any) to be released.

   1. PVs associated with the pod: After six minutes, the KCM automatically disassociate PVCs from the pod. The csi\-controller will watch this action and then call the [DetachVolume API](https://docs.byteplus.com/en/docs/ecs/Detachvolume) to disassociate the cloud disk, completing resource release.

   2. Static IP for the pod (Trunk ENI): The static IP of a pod is released immediately.

   3. View pod information.

      ```bash
      kubectl get pod -o wide
      ```
      

      The expected response is as follows:

      ```bash
      NAME                              READY   STATUS              RESTARTS   AGE     IP              NODE           NOMINATED NODE   READINESS GATES
      nginx-0                           1/1     Running             0          100m    192.168.0.108   192.168.0.12   <none>           <none>
      nginx-1                           0/1     ContainerCreating   0          8s      <none>          192.168.0.13   <none>           <none>
      ```
      

3. After resources are released, the new pod successfully has these resource bound and its status changes to Running.  At this point, load migration is completed.

   ```bash
   kubectl get pod -o wide
   ```
   

   The expected response is as follows:

   ```bash
   NAME                              READY   STATUS        RESTARTS   AGE    IP              NODE           NOMINATED NODE   READINESS GATES
   nginx-1                           1/1     Running       0          6m     192.168.0.63    192.168.0.13   <none>           <none>
   nginx-0                           1/1     Running       0          114m   192.168.0.108   192.168.0.12   <none>           <none>
   ```
   


<span id=".a3ViZXJuZXRlcy12MS0yNi3lj4rkuYvlkI4="></span>
#### Kubernetes v1.26 and later

Implement load migration by adding a specific taint to the failed node to trigger the [NodeOutOfServiceVolumeDetach](https://kubernetes.io/zh-cn/docs/reference/command-line-tools-reference/feature-gates/) feature gate. The detailed steps are as follows:


1. Ensure that the ECS instance (the target node) is in the **closed** or **powered off** state, and that the target node is not a virtual node.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The node state must not be <strong>Running</strong> and the ECS instance state corresponding to the node must not be <strong>Restarting</strong>. Otherwise, it may lead to unpredictable behaviors such as residual mount points on the node and pod read/write anomalies.   </div>
   

2. Ensure that the workload (Pod) to be migrated does not tolerate the `node.kubernetes.io/out-of-service` taint.

   ```bash
   kubectl get statefulset <sts-name> -o jsonpath="{.spec.template.spec.tolerations}"
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><code><sts-name></code> is the name of the StatefulSet. You need to replace it with your actual workload name.   </div>
   

   The following content is the expected response, where the value of `key` indicates the taint tolerated by the pod (in this example, the `temp` taint). If the response is empty, it means that no taint is tolerated.

   ```bash
   [{"key":"temp","effect":"NoSchedule","operator":"Exists"}]
   ```
   

3. Run the following command to specify a taint for the failed node.

   ```bash
   kubectl taint nodes <node-name> node.kubernetes.io/out-of-service=nodeshutdown:NoExecute
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Replace <code><node-name></code> with the name of the failed node.   </div>
   

4. After the taint is successfully specified, the original pod will be deleted by the KCM, and the associated exclusive resources will be immediately disassociated. A new pod will be recreated on a different node to replace the deleted one, completing migration.

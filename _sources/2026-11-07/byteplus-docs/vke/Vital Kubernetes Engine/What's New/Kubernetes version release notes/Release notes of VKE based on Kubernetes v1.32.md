---
title: "Release notes of VKE based on Kubernetes v1.32"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v1_32"
---

Vital Kubernetes Engine (VKE) strictly adheres to the Certified Kubernetes Conformance Program. This topic describes the changes introduced in the VKE release based on Kubernetes v1.32.

<span id="YIRe4qod"></span>
## Release notes

Table 1: Core components and descriptions


|Core component |Current version |Considerations |
|---|---|---|
|Kubernetes |1.32.3 |Kubernetes v1.31 and v1.32 have deprecated and removed beta API versions. You need to check compatibility before using new versions. For details, see the following sections of this topic: **Deprecated and removed features** and **Deprecated API versions**. |
|ETCD |v3.5.16 |None |
|Containerd Runtime |v1.6.38 |None |
|CoreDNS |v1.11.3 |None |
|Ingress\-nginx |v1.11.5\-vke.2 |None |


Table 2: Kubernetes versions and the corresponding VKE versions


|**Kubernetes version** |**VKE version** |**Release notes** |
|---|---|---|
|v1.32.3 |vke.16 |The kube\-apiserver supports the Seat rate limiter feature. |
|v1.32.3 |vke.15 |The expansion scheduler is enhanced to support image\-aware scheduling. |
|v1.32.3 |vke.14 |* Added the following metrics to the kube\-apiserver audit log:<br><br>   * `apiserver.response.k8s.io/object-count`: Indicates the number of objects returned by a LIST request.<br><br>   * `apiserver.response.k8s.io/size-bytes`: Indicates the actual size of the HTTP response body written by a LIST request, measured in bytes.<br><br>* The expansion scheduler is enhanced to support the node resource amplification capability. |
|v1.32.3 |vke.13 |Fixed an issue in the scheduler where pod scheduling failed when using an NPU card that does not support micro\-topology scheduling. |
|v1.32.3 |vke.12 |* Fixed an issue in the scheduler where the RDMANetworkTopology add\-on did not implement the PreBind interface.<br><br>* Optimized the kube\-apiserver cache bypass feature. |
|v1.32.3 |vke.11 |Optimized the scheduler controller and adjusted the NodeMonitor CR update interval. |
|v1.32.3 |vke.10 |Optimized the container change detection method in Kubelet. |
|v1.32.3 |vke.9 |Added the AcceleratorTopology add\-on in the scheduler to support NPU\-A2 topology awareness. |
|v1.32.3 |vke.8 |* Added a rate\-limiting queue and improved the re\-queuing logic upon PV\-PVC binding failures for the PV controller.<br><br>* The expansion scheduler supports scheduling with open\-local storage. |
|v1.32.3 |vke.7 |vke.8<br><br>Added a rate\-limiting queue and improved the re\-queuing logic upon PV\-PVC binding failures for the PV controller.<br><br>The expansion scheduler supports scheduling with open\-local storage.<br><br>vke.7<br><br>Enabled collecting control plane metrics through self\-managed Prometheus.<br><br> |
|v1.32.3 |vke.6 |The expansion scheduler load awareness plugin is available at the cluster or pod level. |


<span id="Ojiq1tEb"></span>
## About Kubernetes community versions

<span id="LNk0UAjY"></span>
### Major updates

<span id="aXRTRds3"></span>
#### In Kubernetes v1.32


* Support for selectable fields for custom resources has entered the GA stage. This support allows selectableFields to be configured in CustomResourceDefinition (CRD) configuration to declare which other fields in custom resources can be used in field selectors. The supported requests include List, Watch, and DeleteCollection requests for efficient filtering of CRD resources. For details, see [Selectable fields for custom resources](https://kubernetes.io/docs/tasks/extend-kubernetes/custom-resources/custom-resource-definitions/#crd-selectable-fields).

* The StatefulSet auto\-delete PVC feature has reached the GA (General Availability) stage. It allows you to control whether PVCs created via the StatefulSet's volumeClaimTemplate field are retained when pods are deleted. During StatefulSet deletion or scale\-in, the default policy is retention. For details, see [PersistentVolumeClaim retention](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/#persistentvolumeclaim-retention).

* The JobManagedBy feature has entered the beta stage. You can configure the `.spec.managedBy` field to specify an external controller to take over Job reconciliation. For details, see [Delegation of managing a Job object to external controller](https://kubernetes.io/docs/concepts/workloads/controllers/job/#delegation-of-managing-a-job-object-to-external-controller).

* The scheduler plugin now includes a QueueingHint callback function. Based on cluster event changes and the reason the plugin previously rejected scheduling, it determines whether to requeue the pod to the active queue or backoff queue (delayed retry). This reduces unnecessary scheduling retries and improves scheduler throughput. For details, see [QueueingHint Brings a New Possibility to Optimize Pod Scheduling](https://kubernetes.io/blog/2024/12/12/scheduler-queueinghint/).

* The WatchList feature has entered the beta stage. The client\-go client can use streaming requests instead of List requests, optimizing memory usage in List request responses. The kube\-controller\-manager add\-on enables this feature by default. For details, see [Enhancing Kubernetes API Server Efficiency with API Streaming](https://kubernetes.io/blog/2024/12/17/kube-apiserver-api-streaming/).

* The feature for handling volume expansion failures has reached the beta stage. It supports retrying PVC expansion by adjusting the `.spec.resources` of the PVC to a smaller value when the initial expansion fails. This reduces the operational complexity of recovery operations when expansion fails due to insufficient underlying storage. For details, see [Recovering from Failure when Expanding Volumes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#recovering-from-failure-when-expanding-volumes).

* The AuthorizeWithSelectors and AuthorizeNodeWithSelectors features have entered the beta stage. They allow the node authorizer to use more granular selectors for authorization, such as fieldSelector and labelSelector.  The kubelet now has minimal permissions: it can only read its own Node object and the pods bound to its Node. For details, see [Using Node Authorization](https://kubernetes.io/docs/reference/access-authn-authz/node/).

* The pod\-level resource feature has reached the alpha stage. It supports configuring pod\-level resources for pods (instead of just for individual containers) through the `.spec.resources` field, simplifying resource management and improving resource utilization.


<span id="XaNcIoPN"></span>
#### In Kubernetes v1.31


* The pod disruption status feature has reached the GA stage. A dedicated pod DisruptionTarget condition is added to indicate that the pod is about to be deleted due to a disruption. For a Job or CronJob, this condition can be used in the job pod failure policy to define the behavior when the pod fails due to disruption. For details, see [Pod disruption conditions](https://kubernetes.io/docs/concepts/workloads/pods/disruptions/#pod-disruption-conditions).

* The pod failure policy feature has reached the GA stage. Jobs now support using the `.spec.podFailurePolicy` field to control how pod failures are handled (either retried or ignored) based on container exit codes and pod conditions. This avoids unnecessary pod restarts and ensures Jobs complete even when pods are interrupted. For details, see [Pod failure policy](https://kubernetes.io/docs/concepts/workloads/controllers/job/#pod-failure-policy).

* The Job success policy feature has entered the beta stage. It enables defining when an indexed Job is declared successful based on the number of successful pods. For details, see [Success policy ](https://kubernetes.io/docs/concepts/workloads/controllers/job/#success-policy).

* The MatchLabelKeysInPodAffinity feature has reached the beta stage. The podAffinity and podAntiAffinity fields now support matchLabelKeys and mismatchLabelKeys for configuring pod affinity/anti\-affinity. This resolves the issue where the scheduler cannot distinguish between new and old pods during Deployment rolling updates, thereby preventing affinity/anti\-affinity features from failing. For details, see [matchLabelKeys](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#matchlabelkeys).

* The recursive read\-only mount feature has entered the beta stage. It allows setting a recursive read\-only attribute on pod volume mounts. Any volume mounted this way, along with all its subdirectories and files, will be in a read\-only state. For details, see [Recursive read-only mounts](https://kubernetes.io/docs/concepts/storage/volumes/#recursive-read-only-mounts).

* The Service traffic distribution feature has entered the beta stage. It allows defining traffic routing preferences to backend endpoints in a Service. For example, PreferClose means prioritizing traffic to topologically closest endpoints to the client. For details, see [Traffic distribution](https://kubernetes.io/docs/concepts/services-networking/service/#traffic-distribution).

* The HonorPVReclaimPolicy feature has reached the beta stage. It supports adding a Finalizer to PersistentVolumes (PVs) to ensure that, regardless of the deletion order of PVs and PVCs, PVs with the Delete reclaim policy are only deleted after the corresponding underlying storage resources are removed. For details, see [PersistentVolume deletion protection finalizer](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolume-deletion-protection-finalizer).

* The cache\-based consistent read feature has entered the beta stage. The Kube\-apiserver handles consistent read requests using a cache. This reduces requests to ETCD and improves request processing efficiency. For details, see [Consistent reads from cache](https://kubernetes.io/blog/2024/08/15/consistent-read-from-cache-beta/).

* The ServiceAccountTokenNodeBinding feature has reached the beta stage. It supports creating a Service Account Token that is directly bound to a Node. The Token will become invalid if it expires or the associated Node or Service Account is deleted.

* The Kubernetes client and Kube\-apiserver use the WebSocket protocol by default instead of SPDY/3.1 for streaming and executing commands such as kubectl exec, kubectl attach, kubectl cp, and kubectl port\-forward. For details, see [Streaming Transitions from SPDY to WebSockets](https://kubernetes.io/blog/2024/08/20/websockets-transition/).

* The ImageVolume feature has entered the alpha stage, allowing users to specify an OCI image reference as a read\-only volume in a pod and mount it as a volume inside containers for reuse. Multiple containers in a pod can share a configuration file without including this file in the main image. This minimizes security risks and reduces the overall image size. For details, see [Read Only Volumes Based On OCI Artifacts](https://kubernetes.io/blog/2024/08/16/kubernetes-1-31-image-volume-source/).


<span id="xjc6iUoC"></span>
### Deprecated and removed features


* In Kubernetes v1.32, the service account annotation `kubernetes.io/enforce-mountable-secrets` is deprecated. It is recommended to use a separate namespace to isolate access to Secrets. For details, see [Restricting access to Secrets (deprecated) ](https://kubernetes.io/docs/concepts/security/service-accounts/#enforce-mountable-secrets).

* In Kubernetes v1.32, kube\-scheduler has removed the AzureDiskLimits, CinderLimits, EBSLimits, and GCEPDLimits plugins.

* In Kubernetes v1.31, you will no longer be able to run the `kubectl exec [POD] [COMMAND]` command without the `--` separator. Instead, use the `kubectl exec [POD] -- [COMMAND]` command.

* In Kubernetes v1.31, the built\-in CephFS volume plugin `kubernetes.io/cephfs` has been removed and replaced by the [CephFS CSI driver](https://github.com/ceph/ceph-csi/).

* In Kubernetes v1.31, the built\-in CephRBD volume plugin `kubernetes.io/rbd` has been removed and replaced by the [RBD CSI driver](https://github.com/ceph/ceph-csi/).

* In Kubernetes v1.31, with Portworx CSI migration, all operations no longer use the built\-in Portworx volume plugin and instead rely on the CSI plugin: `pxd.portworx.com`. For details, see [Portworx CSI migration](https://kubernetes.io/docs/concepts/storage/volumes/#portworx-csi-migration).


<span id="C2axrnrL"></span>
### Deprecated API versions


* In Kubernetes v1.32, the FlowSchema and PriorityLevelConfiguration objects have been removed from `flowcontrol.apiserver.k8s.io/v1beta3`. Instead, you should use `flowcontrol.apiserver.k8s.io/v1` (available since v1.29).  

* For `flowcontrol.apiserver.k8s.io/v1`, the `spec.limited.nominalConcurrencyShares` field of PriorityLevelConfiguration defaults to 30 (if explicitly set to 0, it will not be changed to 30).

* In Kubernetes v1.32, `coordination.k8s.io/v1alpha1` has been removed and replaced by `coordination.k8s.io/v1alpha2`.

* In Kubernetes v1.31, if you create a CustomResourceDefinition (CRD) object and specify a non\-empty con`version webhook caBundle`  field with invalid content, the CRD will not be able to function. Once the caBundle of a CRD is set to a valid state, updates that would make it invalid or empty are no longer allowed. This prevents disruption to the normal operation of the CRD.

* In Kubernetes v1.31, the `kubeadm.k8s.io/v1beta3` version is deprecated. You need to migrate to `kubeadm.k8s.io/v1beta4`.


<span id="lHswXbdQ"></span>
### Reference links

For more information on the performance and feature evolution of Kubernetes version 1.32, see:


* [CHANGELOG-1.32.md](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.32.md)

* [CHANGELOG-1.31.md](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.31.md)

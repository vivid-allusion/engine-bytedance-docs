---
title: "Release notes for VKE based on Kubernetes v1.36"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v1_36"
---

Vital Kubernetes Engine (VKE) strictly adheres to the Certified Kubernetes Conformance Program. This topic describes the changes introduced in the VKE release based on Kubernetes v1.36.

<span id="apS1Gww2"></span>
## Release notes

Table 1: Core components and descriptions


|Core component |Current version |Considerations |
|---|---|---|
|Kubernetes |1.36.1 |Kubernetes v1.35 and v1.36 have deprecated and removed beta/alpha APIs. Compatibility checks are required when upgrading to these versions. For details, see the following sections of this topic: **Deprecated and removed features** and **Deprecated API versions**. |
|ETCD |v3.6.8 |None |
|Containerd Runtime |v2.1.9 |None |
|CoreDNS |v1.12.4 |None |


Table 2: Kubernetes versions and the corresponding VKE versions


|**Kubernetes version** |**VKE version** |**Release notes** |
|---|---|---|
|v1.36.1 |vke.4 |The kube\-apiserver supports the Seat rate limiter feature. |
|v1.36.1 |vke.3 |The expansion scheduler is enhanced to support image\-aware scheduling. |
|v1.36.1 |vke.2 |The expansion scheduler is enhanced to support the node resource amplification capability. |


<span id="YAsVWvge"></span>
## About Kubernetes community versions

<span id="TrJZ0Wra"></span>
### Major updates

<span id="CbLhDd8K"></span>
#### In Kubernetes v1.36


* The Mutable CSINode allocatable feature has entered the GA stage. It allows updates to the mounted volume upper limit reported by a node. This prevents scheduling decisions from using outdated data, which will lead to inaccurate scheduling or failed mounting.

* The ImageVolume feature has entered the GA stage. It allows users to specify an OCI image reference as a read‑only volume in a pod and mount it for reuse within containers. Multiple containers within a pod can share a single configuration file without including it in the main image, thereby minimizing security risks and reducing overall image size. For details, see [Image Volumes](https://kubernetes.io/docs/concepts/storage/volumes/#image).

* The CSIServiceAccountTokenSecrets feature has entered the GA stage. CSIDriver supports obtaining the service account tokens of a Pod through the Secret field. This prevents token leakage in logs and other outputs caused by configuration in `volumeContext`. For details, see [A Better Way to Pass Service Account Tokens to CSI Drivers](https://kubernetes.io/blog/2026/01/07/kubernetes-v1-35-csi-sa-tokens-secrets-field-beta/).

* Fine\-grained API authorization of Kubelet has entered the GA stage. Node authorization subresources, including configz, healthz, and pods, are added. In this way, no additional permissions are required for log collection, monitoring, and other add\-ons to communicate with Kubelet. For details, see [Fine-grained authorization](https://kubernetes.io/docs/reference/access-authn-authz/kubelet-authn-authz/#fine-grained-authorization).

* The mutating admission policy has entered the GA stage. It allows users to configure MutatingAdmissionPolicy resource declarations for resource changes, which can be used to replace mutating admission webhooks. For details, see [Mutating Admission Policy](https://kubernetes.io/docs/reference/access-authn-authz/mutating-admission-policy/).

* The Volume Group Snapshot feature has entered the GA stage. It supports the use of label selectors to group multiple PersistentVolumeClaim objects for snapshots. This allows you to restore that group of snapshots to new volumes and recover your workload based on a crash\-consistent recovery point. For details, see [Volume Group Snapshot](https://kubernetes.io/blog/2026/05/08/kubernetes-v1-36-volume-group-snapshot-ga/).

* The UserNamespacesSupport feature has entered the GA stage, enabling pods to utilize Linux User Namespaces for enhanced container security.

* The KubeletPSI feature has entered the GA stage. It allows Kubelet to use Pressure Stall Information (PSI) metrics in the Summary API and Prometheus metrics. For details, see [PSI Metrics](https://kubernetes.io/blog/2026/05/12/kubernetes-v1-36-psi-metrics-ga/).

* Dynamic Resource Allocation\-related features DRAPrioritizedList and DRAAdminAccess have been promoted to GA. The DRAPrioritizedList feature allows you to specify a priority\-ordered list of alternative devices, enabling workloads to use alternative devices when the preferred device is unavailable. The DRAAdminAccess feature allows a request in a ResourceClaim or ResourceClaimTemplate to be marked as having admin access. For details, see [Dynamic Resource Allocation](https://kubernetes.io/docs/concepts/scheduling-eviction/dynamic-resource-allocation/).

* Dynamic Resource Allocation (DRA)\-related features DRAPrioritizedList and DRAAdminAccess are generally available. The DRAPrioritizedList feature allows you to specify a priority\-ordered list of alternative devices, enabling workloads to use alternative devices when the preferred device is unavailable. The DRAAdminAccess feature allows a request with administrative access to be marked in a ResourceClaim or ResourceClaimTemplate. For details, see [Dynamic Resource Allocation](https://kubernetes.io/docs/concepts/scheduling-eviction/dynamic-resource-allocation/).

* The mixed version proxy feature has entered the Beta stage. It allows the API Server to proxy requests for unknown versions or unrecognized API resources to another API Server in the cluster that may support the versions. This maintains API compatibility during rolling upgrades and reduces unexpected 404 errors caused by version differences during the upgrades. For details, see [Mixed Version Proxy](https://kubernetes.io/blog/2026/05/15/kubernetes-1-36-feature-mixed-version-proxy-beta/).

* The feature of updating the resources of suspended Jobs has entered the Beta stage. When a Job is suspended, you can modify the `requests` and `limits` configuration for CPU, memory, GPU, and various extended resources in the Pod template.

* The RestartAllContainers feature has entered the Beta stage. When a source container in a Pod exits due to the restart policy, all containers will be restarted. You can reset the Pod status at a lower cost by rerunning all containers (including init containers) in the Pod from scratch, without the need to delete and recreate the Pod. For details, see [New level of efficiency with in-place Pod restart](https://kubernetes.io/blog/2026/01/02/kubernetes-v1-35-restart-all-containers/).

* The strictIPCIDRValidation feature has entered the Beta stage. The API Server will strictly validate IP addresses and CIDR formats. Previous configurations (such as leading zeros in IP/CIDR addresses and subnet masks with ambiguous CIDR semantics) will not be allowed in v1.36.

* The impersonation access control feature has entered the Beta stage. It adds fine\-grained access control to the existing impersonation mechanism **.**  It supports configuring access permissions on resources. This means that, with this feature, you can impersonate a specific identity to perform specific operations. When the feature is not enabled, all permissions of the impersonated identity are granted.

* The node declaration feature has entered the Beta stage. Kubelet reports the feature gates supported by nodes through `.status`. This helps control plane add\-ons to use this information to make better decisions.

* The ComponentStatusz and ComponentFlagz features have entered the Beta stage. It supports exposing basic add\-on information and effective command parameter information through the `/statusz` and `/flagz` endpoints.


<span id="MD3HfxQ1"></span>
#### In Kubernetes v1.35


* The In‑Place Pod Resource Adjustment feature has entered the GA stage. It supports adjusting the CPU and memory values under the `resources` field of pod containers. This avoids restarting the pod or its containers, enabling vertical autoscaling in place. For details, see [In-Place Pod Resize](https://kubernetes.io/blog/2025/12/19/kubernetes-v1-35-in-place-pod-resize-ga/).

* The PodObservedGenerationTracking feature has entered the GA stage. It allows the `observedGeneration` field to be set in the Pod status and allows other add\-ons to include `observedGeneration` in Pod Conditions, reflecting the `metadata.generation` of pods at the time the state or condition was recorded.

* The JobManagedBy feature has entered the GA stage. You can configure the `.spec.managedBy` field to specify an external controller to take over Job reconciliation. For details, see [Job Managed By](https://kubernetes.io/blog/2025/12/18/kubernetes-v1-35-job-managedby-for-jobs-goes-ga/).

* The SupplementalGroups feature has entered the GA stage, enabling fine‑grained control over SupplementalGroups for pods via the `.spec.securityContext.supplementalGroupsPolicy` field. For details, see [Fine-grained Supplemental Groups Control](https://kubernetes.io/blog/2025/12/23/kubernetes-v1-35-fine-grained-supplementalgroups-control-ga/).

* The PodCertificateRequest feature has entered the Beta stage and is disabled by default. After `PodCertificateRequest` and `PodCertificate` projected volumes are introduced, certificate lifecycle management is delegated to the Kubelet layer. For details, see [PodCertificate projected volumes](https://kubernetes.io/docs/concepts/storage/projected-volumes/#podcertificate).

* The configurable CrashLoopBackOff feature has entered the Beta stage. It supports node\-level configuration of the restart backoff time for containers in the `CrashLoopBackOff` state. The backoff time can be set to 1 to 300 seconds, with a default value of 300 seconds.

* The Downward API injection of node topology labels feature has entered the Beta stage. The labels of the node where a Pod resides: `topology.k8s.io/zone`, `topology.k8s.io/region`, and `kubernetes.io/hostname` are copied to the labels of the Pod. This enables the Pod to obtain topology information via the downward API. For details, see [PodTopologyLabels](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/#podtopologylabels).

* The container startup feature has entered the Beta stage, which supports configuring container\-level startup policies. Each container can have its own `restartPolicy` set individually, and `restartPolicyRules` can be used to control restart behavior based on exit codes.

* The feature of configuring maximum unavailable StatefulSet replicas has entered the Beta stage. StatefulSets support configuration of the `maxUnavailable` field. This enables concurrent updates of multiple Pods to improve deployment efficiency.

* The configurable HorizontalPodAutoscaler (HPA) Tolerance feature has entered the Beta stage. HPA introduces the `tolerance` field. This supports configuration of Pod autoscaling tolerance for fine\-grained management in large\-scale clusters. For details, see [Tolerance](https://kubernetes.io/docs/concepts/workloads/autoscaling/horizontal-pod-autoscale/#tolerance).

* The KubeletEnsureSecretPulledImages feature has entered the Beta stage. When Kubelet pre\-pulls images, it checks whether the target Pod is authorized to use images that already exist on the node for IfNotPresent/Never pull policies. For details, see [Ensure image pull credential verification](https://kubernetes.io/docs/concepts/containers/images/#ensureimagepullcredentialverification).

* The NominatedNodeNameForExpectation feature has entered the Beta stage. The scheduler explicitly writes its decision "The node is chosen for the Pod while binding is in progress or preemption is pending" into the `status.nominatedNodeName` field of a Pod. It allows external add\-ons (such as Cluster Autoscaler) and the restarted scheduler to view the node that the Pod is intended for. This prevents unintended operations and carries forward existing scheduling decisions.

* The feature of displaying the number of replicas that are being terminated in Deployments and ReplicaSets has entered the Beta stage. The `.status.terminatingReplicas` field in Deployments and ReplicaSets displays the current number of Pods that are being terminated.

* KYAML has entered the Beta stage. It adds the kyaml output format (`-o kyaml`) to kubectl, which is compatible with standard YAML parsers.

* The GenericWorkload feature has entered the Alpha stage. It supports gang scheduling to ensure a group of Pods can be scheduled in an all\-or\-nothing manner. A Workload resource is added under `scheduling.k8s.io/v1alpha1` to declare the scheduling requirements and policies of a group of Pods. For details, see [Workload API](https://kubernetes.io/docs/concepts/workloads/workload-api/).

* The in‑place Pod resource adjustment feature has entered the Alpha stage. It supports adjusting the CPU and Memory values under the `resources` field of Pods. This prevents Pod or its containers from restarting.


<span id="PMPb3e5r"></span>
### Deprecated and removed features


* The Git\-Repo volume add\-on is disabled by default and cannot be enabled.

* Kubernetes v1.35 will be the last Kubernetes version that supports containerd 1.x. Before upgrading to Kubernetes v1.36, you need to upgrade the runtime to containerd 2.0+, and you can use the `kubelet_cri_losing_support` metric to check at\-risk nodes. Starting from v1.36, VKE clusters use containerd 2.x by default. Before upgrading VKE clusters to v1.36 or later versions, you need to upgrade containerd to 2.x.

* Starting from Kubernetes v1.35, cgroup v1 is no longer supported. The node operating system must be upgraded to support cgroup v2. Otherwise, Kubelet will not start.

* In Kubernetes v1.35, the Kube\-proxy ipvs mode is deprecated and is expected to be removed in later versions. We recommend migrating to nftables mode.

* In Kubernetes v1.35, Kubelet has removed the deprecated startup parameter `--pod-infra-container-image`.


<span id="Na1fhgZf"></span>
### Deprecated API versions


* The `Service.spec.externalIPs` field is deprecated.

* In Kubernetes v1.35, StorageVersionMigration v1alpha1 is removed and replaced by StorageVersionMigration v1beta1.


<span id="yzT2I05X"></span>
### Reference links

For more information about the performance and feature evolution in Kubernetes v1.36, see


* [CHANGELOG-1.36.md](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.36.md)

* [CHANGELOG-1.35.md](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.35.md)

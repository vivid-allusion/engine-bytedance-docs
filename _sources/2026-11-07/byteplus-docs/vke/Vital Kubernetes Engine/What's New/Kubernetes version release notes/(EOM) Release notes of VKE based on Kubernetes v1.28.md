---
title: "(EOM) Release notes of VKE based on Kubernetes v1.28"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v-1_28"
---

Vital Kubernetes Engine (VKE) strictly adheres to the Certified Kubernetes Conformance Program. This topic describes the changes introduced in the VKE release based on Kubernetes v1.28.

<span id=".54mI5pys5Y-R5biD6K-05piO"></span>
## Release notes

Table 1: Core components and descriptions


|Core component |Current version |Considerations |
|---|---|---|
|Kubernetes |v1.28.15 |Kubernetes v1.27 and v1.28 have deprecated and removed beta API versions. You need to check compatibility before using new versions. For details, see the following sections of this topic: [Deprecated and removed features](https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v-1_28#.5bqf5byD5ZKM56e76Zmk5Yqf6IO9) and [Deprecated API versions](https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v-1_28#.YXBpLeeJiOacrOW8g-eUqA==). |
|ETCD |v3.5.9 |None |
|Containerd Runtime |1.6.38 |None |
|CoreDNS |1.10.1 |None |
|Ingress\-nginx |1.9.5\-vke.1 |None |


Table 2: Kubernetes versions and the corresponding VKE versions


|Kubernetes version |VKE version |Release notes |
|---|---|---|
|v1.28.15 |vke.33 |Fixed an issue where the pvcprotection controller in kube\-controller\-manager caused PVCs to remain in the Terminating state for an extended period during deletion and fail to be released. |
|v1.28.15 |vke.32 |* Added the following metrics to the kube\-apiserver audit log:<br><br>   * `apiserver.response.k8s.io/object-count` indicates the number of objects returned by a LIST request.<br><br>   * `apiserver.response.k8s.io/size-bytes` indicates the actual size of the HTTP response body written for a LIST request, in bytes.<br><br>* The extended scheduler is enhanced to support node overcommitment. |
|v1.28.15 |vke.31 |Fixed an issue in the scheduler where pod scheduling failed when using an NPU card that does not support micro\-topology scheduling. |
|v1.28.15 |vke.30 |Optimized the scheduler controller and adjusted the NodeMonitor CR update interval. |
|v1.28.15 |vke.29 |Added the AcceleratorTopology add\-on in the scheduler to support NPU\-A2 topology awareness. |
|v1.28.15 |vke.28 |Added a rate\-limiting queue and improved the re\-queuing logic upon PV\-PVC binding failures for the PV controller. |
|v1.28.15 |vke.27 |vke.8<br><br>Added a rate\-limiting queue and improved the re\-queuing logic upon PV\-PVC binding failures for the PV controller.<br><br>The expansion scheduler supports scheduling with open\-local storage.<br><br>vke.7<br><br>Enabled collecting control plane metrics through self\-managed Prometheus.<br><br> |
|v1.28.15 |vke.26 |The expansion scheduler load awareness plugin is available at the cluster or pod level. |
|v1.28.15 |vke.25 |A new configuration protocol is supported in scenarios where a container uses multiple GPUs. |
|v1.28.15 |vke.24 |You can configure the hugepage cgroup limits for pods by using pod annotations. |
|v1.28.15 |vke.23 |Optimized the logic when the kube\-apiserver requests an etcd resource over 2 GiB. |
|v1.28.15 |vke.22 |* Mount options for memory type of EmptyDir volume are available.<br><br>* mGPU scheduling results can be transmitted to container environment variables. |
|v1.28.15 |vke.21 |Improved the handling of GPU card failure in mGPU scheduling scenarios. |
|v1.28.15 |vke.20 |The enhanced API server can inject sidecar containers into VCI pods. |
|v1.28.15 |vke.19 |The enhanced expansion scheduler supports online and offline hybrid deployment of mGPU. |
|v1.28.15 |vke.18 |The code from the Kubernetes community v1.28.15 is synchronized. |
|v1.28.3 |vke.17 |* Enhanced the expansion scheduler, which can detect changes in virtual kubelet services.<br><br>* The in\-place VerticalPodAutoscaler (VPA) feature is supported. |
|v1.28.3 |vke.16 |The expansion scheduler is enhanced, which supports local storage\-aware scheduling. |
|v1.28.3 |vke.15 |The expansion scheduler is enhanced, which supports NUMA\-aware scheduling and RDMA topology\-aware scheduling. |
|v1.28.3 |vke.14 |The issue where Local Path Provisioner is not supported when the expansion scheduler detects vePFS storage is fixed. |
|v1.28.3 |vke.13 |* The expansion scheduler is enhanced, and the mGPU cross\-GPU sharing feature supports the full computing power allocation strategy.<br><br>* The expansion scheduler is enhanced, which can detect vePFS storage. |
|v1.28.3 |vke.12 |Fixed the issue that occurs during initialization of the extended scheduler add\-on. |
|v1.28.3 |vke.11 |Optimized the release specifications for core components. |
|v1.28.3 |vke.10 |The issue where the Ready state of containers changes when kubelet restarts is fixed. |
|v1.28.3 |vke.9 |The expansion scheduler is enhanced, which supports mGPU preemptive scheduling. |
|v1.28.3 |vke.8 |The expansion scheduler is enhanced, which supports VCI resource inventory awareness. |
|v1.28.3 |vke.7 |The self\-signed certificate of the API server is optimized. |
|v1.28.3 |vke.6 |* Kubelet is enhanced, which allows you to configure container resource views.<br><br>* Kubelet is enhanced, which allows you to configure the graceful shutdown period for evicted pods by using annotations.<br><br>* The load\-aware scheduling issue of the expansion scheduler is fixed. |


<span id=".a3ViZXJuZXRlcy3npL7ljLrniYjmnKzop6Por7s="></span>
## About Kubernetes community versions

<span id=".6YeN5aSn5pu05paw"></span>
### Major updates


* In Kubernetes v1.28, the scheduling framework optimizes add\-on invocation to reduce unnecessary retries. If custom scheduler add\-ons are used in a cluster, we recommend that you optimize the add\-ons to improve the overall scheduling performance. For details, see [Scheduling framework optimization](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.28.md#urgent-upgrade-notes).

* In Kubernetes v1.28, the CephFS and RBD in\-tree storage driver add\-ons are deprecated and are planned to be deleted in Kubernetes v1.31. We recommend that you use the third\-party storage driver [CephFS CSI](https://github.com/ceph/ceph-csi/).


<span id=".5aKe6YeP5Yqf6IO95ZKM54m55oCn"></span>
### Incremental features

<span id=".5ZyoLWt1YmVybmV0ZXMtdjEtMjgt54mI5pys"></span>
#### In Kubernetes v1.28


* The supported version skew between the control plane and nodes has changed from n\-2 to n\-3. This increases the number of compatible versions and thereby reduces upgrade interruptions during node upgrades. For details, see [Version Skew Policy](https://kubernetes.io/releases/version-skew-policy/).

* The non\-graceful node shutdown feature moves to GA. When a node is shut down due to failures such as power outages, stateful applications need to be promptly restarted on nodes that are running as expected to ensure normal business operations. For details, see [Non-graceful node shutdown](https://kubernetes.io/docs/concepts/architecture/nodes/#non-graceful-node-shutdown).

* The traceable default StorageClass feature moves to GA. Users do not need to create a default StorageClass first and then create a PersistentVolumeClaim (PVC). All PVCs that do not have a StorageClass assigned automatically use the default StorageClass. For details, see [Retroactive default StorageClass assignment](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#retroactive-default-storageclass-assignment).

* Two new features have been added for Job failure handling:

   * Pod replacement policy: The JobPodReplacementPolicy feature gate is added. After it is enabled, you can set `podReplacementPolicy` to `Failed` in the pod spec. After you configure this policy, the pod will be replaced only if it reaches the `Failed` stage instead of the `Terminating` stage. This prevents two pods from simultaneously occupying index and node resources. For details, see [Delayed creation of replacement pods](https://kubernetes.io/docs/concepts/workloads/controllers/job/#pod-replacement-policy).

   * Index\-based fallback mechanism: The JobBackoffLimitPerIndex feature gate is added. If it is enabled, you can configure `.spec.backoffLimitPerIndex` when you create an Indexed Job. This prevents the failure of the whole Job when a single index continuously fails until it reaches the `.spec.backoffLimit` limit. For details, see  [Index-based fallback limits ](https://kubernetes.io/docs/concepts/workloads/controllers/job/#backoff-limit-per-index).

* NodeSwap moves to Beta. After you enable the NodeSwap feature gate, you can configure swap memory for running workloads. For details, see [Beta support for using swap on Linux](https://kubernetes.io/blog/2023/08/24/swap-linux-beta/).

* Native sidecar containers move to Alpha. The SidecarContainers feature gate has been added. If this feature is enabled, you can configure the `restartPolicy` field in Init containers. For details, see [Introducing native sidecar containers](https://kubernetes.io/blog/2023/08/25/native-sidecar-containers/).

* The podresources API has moved to GA. It is an API served locally by the kubelet on the node. Originally used for [monitoring device information](https://kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/device-plugins/#monitoring-device-plugin-resources), it now exposes compute resources exclusively allocated to containers. For details, see [podresource API](https://kubernetes.io/blog/2023/08/23/kubelet-podresources-api-ga/).

* Multiple new features have been added for CEL expression capabilities:

   * The CEL\-based CRD validation feature has moved to Beta. CEL is integrated with CRD to apply to most CR validation scenarios during development without webhooks. For details, see [CRD validation expression language](https://github.com/kubernetes/enhancements/tree/master/keps/sig-api-machinery/2876-crd-validation-expression-language).

   * CEL\-based admission control moves to Beta. It supports declarative validation of resource requests and allows you to use [CEL expressions](https://kubernetes.io/docs/reference/using-api/cel/#cel-community-libraries) to define complex validation rules without the need to deploy webhook\-based admission controllers. For details, see [Validating Admission Policy](https://kubernetes.io/docs/reference/access-authn-authz/validating-admission-policy/).

* The ServiceNodePortStatic feature moves to Beta, which allows you to retain a static port range to prevent conflicts with dynamically allocated ports. For details, see [Avoid collisions assigning ports to NodePort services](https://kubernetes.io/blog/2023/05/11/nodeport-dynamic-and-static-allocation/).

* The mixed version proxy feature moves to Alpha. If multiple versions of API servers exist in a cluster, the mixed version proxy ensures that an HTTP request for a resource is served by the correct API server. For details, see [Mixed version proxy](https://kubernetes.io/blog/2023/08/28/kubernetes-1-28-feature-mixed-version-proxy-alpha/).

* The consistent reads from cache feature moves to Alpha. The ConsistentListFromCache feature gate is added, which achieves consistent list reads through the watch cache. For details, see [Consistent Reads from Cache](https://github.com/kubernetes/enhancements/tree/master/keps/sig-api-machinery/2340-Consistent-reads-from-cache).

* The configuration of a drop\-in directory for kubelet moves to Alpha. The `--config-dir` configuration is added, which allows you to specify a directory to override the original `/etc/kubernetes/kubelet.conf` configuration.

* The in\-place VPA feature of pods moves to Beta. This allows you to modify the CPU and memory requests and limits without restarting pods by upgrading the API server, scheduler, and kubelet. For details,  see [Resize CPU and memory resources assigned to containers](https://kubernetes.io/docs/tasks/configure-pod-container/resize-container-resources/).


<span id=".5ZyoLWt1YmVybmV0ZXMtdjEtMjct54mI5pys"></span>
#### In Kubernetes v1.27


* The SeccompDefault feature moves to GA, which allows you to enable RuntimeDefault as the default seccomp configuration file for all workloads by using the kubelet command line argument `--seccomp-default`. For details, see [kubelet startup parameters](https://kubernetes.io/docs/reference/command-line-tools-reference/kubelet/).

* Multiple features of pod topology spread constraints move to Beta, including: spreading pods over a minimum number of domains, involving the affinity and taint during topology constraint scheduling, and resolving issues of being unable to constrain topology spread during rolling updates. For details, see [More fine-grained pod topology spread policies](https://kubernetes.io/blog/2023/04/17/fine-grained-pod-topology-spread-features-beta/).

* Multiple features of StatefulSets move to Beta. For example, the ordinals of pods can start from arbitrary non\-negative numbers. You can specify associated PVCs to be deleted. Associated PVCs can be automatically deleted during scale\-in. For details, see [StatefulSet start ordinal simplifies migration](https://kubernetes.io/blog/2023/04/28/statefulset-start-ordinal/) and [StatefulSet PVC auto-deletion](https://kubernetes.io/blog/2023/05/04/kubernetes-1-27-statefulset-pvc-auto-deletion-beta/).

* The `maxParallelImagePulls` field of kubelet is added, which specifies the maximum number of images pulled in parallel to prevent excessive consumption of network bandwidth or disk I/O. For details, see [maxParallelImagePulls](https://kubernetes.io/docs/concepts/containers/images/#maximum-parallel-image-pulls).

* The mutable scheduling directives of Jobs move to GA. You can modify the scheduling part of a pod when a Job is being suspended, including the node selector, node affinity, anti\-affinity, and toleration. For details, see [Job Mutable Scheduling Directives](https://kubernetes.io/docs/concepts/workloads/controllers/job/#mutable-scheduling-directives).

* Downward API HugePages moves to GA, which allows you to configure HugePages limits in the `spec.resources` field of pods by using the resource `hugepages-2Mi` or `hugepages-1Gi`. To configure multiple types of HugePages, you need to configure a volume of the HugePages type. For details, see [Manage HugePages](https://kubernetes.io/docs/tasks/manage-hugepages/scheduling-hugepages/).

* The pod readiness state for scheduling moves to Beta. The `.spec.schedulingGates` field of pods is added, which controls when a pod is ready to be considered for scheduling.

* The ReadWriteOncePod access mode has graduated to Beta. This access mode restricts PV access from a single pod on a single node. The ReadWriteOnce mode restricts volume access to a single node, but does not restrict access to a single node from multiple pods. For details, see [Single pod access mode for PersistentVolumes graduates to Beta](https://kubernetes.io/blog/2023/04/20/read-write-once-pod-access-mode-beta/).

* The quick SELinux volume relabeling feature moves to Beta, which optimizes the use of SELinux labels during volume mounting and accelerates container startup. For details, see [Speed up SELinux volume relabeling using mounts](https://github.com/kubernetes/enhancements/tree/master/keps/sig-storage/1710-selinux-relabeling).

* The VolumeManager reconstruction moves to Beta. It allows the kubelet to carry additional information about how existing volumes are mounted during start.

* Server\-side field validation and the latest OpenAPI standard, OpenAPI v3, move to GA. For details, see [Server-side field validation and OpenAPI v3 move to GA](https://kubernetes.io/blog/2023/04/24/openapi-v3-field-validation-ga/).

* The feature of controlling the startup order of StatefulSets moves to Beta. By default, you can configure the startup ordinal in StatefulSets by using `spec.ordinals.start`. For details, see [StatefulSet start ordinal simplifies migration](https://kubernetes.io/blog/2023/04/28/statefulset-start-ordinal/).

* The automatic deletion feature for StatefulSet PVCs moves to Beta. You can configure whenDeleted or whenScaled to trigger the Retain or Delete operation. Retain is the default behavior. The PVC deletion operation will be triggered only if the corresponding StatefulSet is configured with a deletion policy and then deleted. For details, see [KEP-1847](https://kubernetes.io/blog/2023/05/04/kubernetes-1-27-statefulset-pvc-auto-deletion-beta/) and [PersistentVolumeClaim retention](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/#persistentvolumeclaim-retention).

* The volume **group snapshot** feature moves to Alpha. It is available for all volume at the pod level. You do not need to worry about time differences when you back up different volumes. For details, see [KEP-3476](https://github.com/kubernetes/enhancements/issues/3476) and [Introducing an API for Volume Group Snapshots](https://kubernetes.io/blog/2023/05/08/kubernetes-1-27-volume-group-snapshot-alpha/).

* `kubectl apply --prune` is reconstructed to improve performance, and a pruning method is added to `kubectl apply --prune --applyset`. For details, see [Declarative Management of Kubernetes Objects Using Configuration Files](https://kubernetes.io/docs/tasks/manage-kubernetes-objects/declarative-config/#%E6%9B%BF%E4%BB%A3%E6%96%B9%E5%BC%8F-kubectl-apply-f-%E7%9B%AE%E5%BD%95-prune).

* The ServiceNodePortStaticSubrange feature gate is added. After it is enabled, you can use a different port allocation strategy for NodePort Services.

* The in\-place pod resource resize feature moves to Alpha. The InPlacePodVerticalScaling feature gate is added. It allows you to vertically autoscale CPU and memory resources under the `resources` field of pod containers without restarting pods or containers. For details, see [KEP-1287](https://github.com/kubernetes/enhancements/issues/1287) and [In-place pod resource adjustment](https://kubernetes.io/blog/2023/05/12/in-place-pod-resize-alpha/).

* KMS V2 moves to Beta. It optimizes the performance of the KMS provider. For details, see [Using a KMS provider for data encryption](https://kubernetes.io/docs/tasks/administer-cluster/kms-provider/).


<span id=".5bqf5byD5ZKM56e76Zmk5Yqf6IO9"></span>
### Deprecated and removed features

<span id=".5ZyoLWt1YmVybmV0ZXMtdjEtMjgt54mI5pys"></span>
#### In Kubernetes v1.28


* The CephFS and RBD in\-tree storage add\-ons are deprecated. We recommend that you use the third\-party storage driver [CephFS CSI](https://github.com/ceph/ceph-csi/).

* The kube\-scheduler replaces the command line arguments`--lock-object-namespace` and `--lock-object-name` with `--leader-elect-resource-namespace` and `--leader-elect-resource-name`.

* kubectl removes the command line argument `--short`, and the default output of `kubectl version` is the same as `kubectl version --short`.

* The kube\-controller\-manager starts deprecating the command line arguments `--volume-host-cidr-denylist` and `--volume-host-allow-local-loopback`.

* The kubelet starts replacing the command line argument `--azure-container-registry-config` with `--image-credential-provider-config` and `--image-credential-provider-bin-dir`.

* KMSv1 has been deprecated. If you still need to use KMSv1, you need to configure the `--feature-gates=KMSv1=true` feature gate. We recommend that you use KMSv2.

* The `--concurrent-cron-job-syncs` parameter is added to kube\-controller\-manager to configure the concurrency of the CronJob controller. The `--concurrent-job-syncs` parameter is added to configure the concurrency of the Job controller. For details, see [#117550](https://github.com/kubernetes/kubernetes/pull/117550/files) and [#117138](https://github.com/kubernetes/kubernetes/pull/117138/files).

* The following feature gates are removed: DelegateFSGroupToCSIDriver, DevicePlugins, KubeletCredentialProviders, MixedProtocolLBService, ServiceInternalTrafficPolicy, ServiceIPStaticSubrange, and EndpointSliceTerminatingCondition.


<span id=".5ZyoLWt1YmVybmV0ZXMtdjEtMjct54mI5pys"></span>
#### In Kubernetes v1.27


* The kube\-controller\-manager removes the command line arguments `--pod-eviction-timeout` and `--enable-taint-manager`.

* The kubelet removes the command line arguments `--container-runtime`, `--container-runtime-endpoint`, and `--image-service-endpoint`.

* The kube\-apiserver removes the command line argument `--master-service-namespace`.

* The kube\-controller\-manager removes the command line arguments `--enable-taint-manager` and `--pod-eviction-timeout`.

* The kubelet removes the command line arguments `--container-runtime` and `--master-service-namespace`.

* The following changes are made to metrics: `node_collector_evictions_number` is replaced by `node_collector_evictions_total`, and `scheduler_e2e_scheduling_duration_seconds` is replaced by `scheduler_scheduling_attempt_duration_seconds`.

* The following feature gates are removed: IPv6DualStack, ExpandCSIVolumes, ExpandInUsePersistentVolumes, ExpandPersistentVolumes, ControllerManagerLeaderMigration, CSI Migration, CSIInlineVolume, EphemeralContainers, LocalStorageCapacityIsolation, NetworkPolicyEndPort, StatefulSetMinReadySeconds, IdentifyPodOS, and DaemonSetUpdateSurge. For details, see [Kubernetes v1.27 removal](https://kubernetes.io/blog/2023/03/17/upcoming-changes-in-kubernetes-v1-27/#api-removals-and-other-changes-for-kubernetes-v1-27).


<span id=".YXBpLeeJiOacrOW8g-eUqA=="></span>
### Deprecated API versions


* Starting from Kubernetes v1.28 released by VKE, the PodGroup CRD APIGroup of the expansion scheduler in VKE clusters uses `scheduling.x-k8s.io` instead of `scheduling.sigs.k8s.io`. For details, see [BREAKING CHANGE: switch API group to x-k8s.io](https://github.com/kubernetes-sigs/scheduler-plugins/pull/526).

* In Kubernetes v1.29, the `kubescheduler.config.k8s.io/v1beta2` API of KubeSchedulerConfiguration was removed, and we recommend that you use `kubescheduler.config.k8s.io/v1`. For details, see [Remove v1beta2 KubeSchedulerConfiguration](https://github.com/kubernetes/kubernetes/pull/117649).

* In Kubernetes v1.28, the `.status.resizeStatus` field of a PVC is replaced with the `.status.allocatedResourceStatus`  map field to store the states of resources that are being resized for the PVC. For details, see [PersistentVolumeClaimStatus](https://kubernetes.io/docs/reference/kubernetes-api/config-and-storage-resources/persistent-volume-claim-v1/#PersistentVolumeClaimStatus).

* In Kubernetes v1.28, the NetworkPolicyStatus feature was removed. Network policy no longer has the Status attribute.

* In Kubernetes v1.27, the CSIStorageCapacity API of the `storage.k8s.io/v1beta1` version is removed. We recommend that you use `storage.k8s.io/v1`.


<span id=".5Y-C6ICD6ZO-5o6l"></span>
## Reference links

For more information on the performance and feature evolution of Kubernetes version v1.28, see:


* [CHANGELOG-1.28.md](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.28.md)

* [CHANGELOG-1.27.md](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.27.md)

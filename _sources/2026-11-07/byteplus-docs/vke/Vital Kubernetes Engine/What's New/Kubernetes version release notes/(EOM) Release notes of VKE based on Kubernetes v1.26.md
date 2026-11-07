---
title: "(EOM) Release notes of VKE based on Kubernetes v1.26"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v-1_26"
---

Vital Kubernetes Engine (VKE) strictly adheres to the Certified Kubernetes Conformance Program. This topic describes the changes introduced in the VKE release based on Kubernetes v1.26.

<span id=".54mI5pys5Y-R5biD6K-05piO"></span>
## Release notes

Table 1: Core components and descriptions


|Core component |Current version |Considerations |
|---|---|---|
|Kubernetes |v1.26.15 |Kubernetes v1.25 and v1.26 have deprecated and removed beta API versions. You need to check compatibility before using new versions. For details, see the [API version changes](https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v-1_26#.YXBpLeeJiOacrOWPmOabtA==) section in this topic. |
|Containerd Runtime |1.6.38 |In Kubernetes v1.26, the runtime version needs to be version 1.6 or later. |
|ETCD |3.5.5 |None |
|CoreDNS |1.9.3 |None |


Table 2: Kubernetes versions and the corresponding VKE versions


|Kubernetes version |VKE version |Release notes |
|---|---|---|
|v1.26.15 |vke.39 |Fixed an issue where the pvcprotection controller in kube\-controller\-manager caused PVCs to remain in the Terminating state for an extended period during deletion and fail to be released. |
|v1.26.15 |vke.38 |Added the AcceleratorTopology add\-on in the scheduler to support NPU\-A2 topology awareness. |
|v1.26.15 |vke.37 |Enhanced kube\-apiserver with extended request rate limiting capabilities. |
|v1.26.15 |vke.36 |Added Informer metrics to kube\-controller\-manager. |
|v1.26.15 |vke.35 |Added a rate\-limiting queue and improved the re\-queuing logic upon PV\-PVC binding failures for the PV controller. |
|v1.26.15 |vke.34 |vke.8<br><br>Added a rate\-limiting queue and improved the re\-queuing logic upon PV\-PVC binding failures for the PV controller.<br><br>The expansion scheduler supports scheduling with open\-local storage.<br><br>vke.7<br><br>Enabled collecting control plane metrics through self\-managed Prometheus.<br><br> |
|v1.26.15 |vke.33 |The expansion scheduler load awareness plugin is available at the cluster or pod level. |
|v1.26.15 |vke.32 |A new configuration protocol is supported in scenarios where a container uses multiple GPUs. |
|v1.26.15 |vke.31 |You can configure the hugepage cgroup limits for pods by using pod annotations. |
|v1.26.15 |vke.30 |Optimized the logic when the kube\-apiserver requests an etcd resource over 2 GiB. |
|v1.26.15 |vke.29 |* Mount options for memory type of EmptyDir volume are available.<br><br>* mGPU scheduling results can be transmitted to container environment variables. |
|v1.26.15 |vke.28 |Improved the handling of GPU card failure in mGPU scheduling scenarios. |
|v1.26.15 |vke.27 |The enhanced API server can inject sidecar containers into VCI pods. |
|v1.26.15 |vke.26 |The enhanced expansion scheduler supports online and offline hybrid deployment of mGPU. |
|v1.26.15 |vke.25 |The vulnerability [CVE-2024-10220](https://docs.byteplus.com/en/docs/vke/Kubernetes-security-vulnerability-announcement-CVE-2024-10220) is fixed. |
|v1.26.15 |vke.24 |The code from the Kubernetes community v1.26.15 has been synchronized. |
|v1.26.10 |vke.23 |Enhanced the expansion scheduler, which can detect changes in virtual kubelet services. |
|v1.26.10 |vke.22 |The expansion scheduler is enhanced, which supports local storage\-aware scheduling. |
|v1.26.10 |vke.21 |The expansion scheduler is enhanced, which supports NUMA\-aware scheduling and RDMA topology\-aware scheduling. |
|v1.26.10 |vke.20 |The issue where Local Path Provisioner is not supported when the expansion scheduler detects vePFS storage is fixed. |
|v1.26.10 |vke.19 |* The expansion scheduler is enhanced, and the mGPU cross\-GPU sharing feature supports the full computing power allocation strategy.<br><br>* The expansion scheduler is enhanced, which can detect vePFS storage. |
|v1.26.10 |vke.18 |Fixed the issue that occurs during initialization of the extended scheduler add\-on. |
|v1.26.10 |vke.17 |Optimized the release specifications for core components. |
|v1.26.10 |vke.16 |The issue where the Ready state of containers changes when kubelet restarts is fixed. |
|v1.26.10 |vke.15 |The expansion scheduler is enhanced, which supports mGPU preemptive scheduling. |
|v1.26.10 |vke.14 |The expansion scheduler is enhanced, which supports VCI resource inventory awareness. |
|v1.26.10 |vke.13 |The self\-signed certificate of the API server is optimized. |
|v1.26.10 |vke.12 |* Kubelet is enhanced, which allows you to configure container resource views.<br><br>* Kubelet is enhanced, which allows you to configure the graceful shutdown period for evicted pods by using annotations.<br><br>* The load\-aware scheduling issue of the expansion scheduler is fixed. |
|v1.26.10 |vke.11 |The runc container escape vulnerability [CVE-2024-21626](https://docs.byteplus.com/en/docs/vke/Kubernetes-security-vulnerability-announcement-CVE-2024-21626) is fixed. |
|v1.26.10 |vke.10 |Enhanced the elastic resource priority scheduling feature to support proportional scheduling and to trigger scale\-out by Cluster Autoscaler. |
|v1.26.10 |vke.9 |The issue where pods occasionally cannot be scheduled when the expansion scheduler is configuring the MultiPoint add\-on is fixed. |
|v1.26.10 |vke.8 |The API server parameter configuration is enhanced to ensure consistency with the community version. |
|v1.26.10 |vke.7 |The code from the native Kubernetes community v1.26.10 is synchronized. |
|v1.26.6 |vke.6 |The API server is strengthened and the vulnerabilities [CVE-2023-44487](https://github.com/advisories/GHSA-qppj-fm5r-hxr3) and [CVE-2023-39325](https://github.com/advisories/GHSA-4374-p667-p6c8) are fixed. |
|v1.26.6 |vke.5 |Enhanced the extended scheduler to avoid cache penetration to etcd. |
|v1.26.6 |vke.4 |The issue with synchronization of the actual load when the expansion scheduler reschedules pods is fixed. |
|v1.26.6 |vke.3 |The expansion scheduler is enhanced, which can inject node information into pods during scheduling. |


<span id=".a3ViZXJuZXRlcy3npL7ljLrniYjmnKzop6Por7s="></span>
## About Kubernetes community versions

<span id=".6YeN5aSn5pu05paw"></span>
### Major updates


* PodSecurityPolicy is removed in Kubernetes v1.25. For clusters that have used PodSecurityPolicy, you can use the built\-in Pod Security admission controller. For details, see [Pod Security Admission](https://kubernetes.io/docs/concepts/security/pod-security-admission/) and [Migrate from PodSecurityPolicy to the Built-In PodSecurity Admission Controller](https://kubernetes.io/docs/tasks/configure-pod-container/migrate-from-psp/).

* The ephemeral container feature has entered the Stable phase. Ephemeral containers can run temporarily in an existing pod when kubectl exec becomes unavailable because a container has crashed or a container image does not include debugging utilities. For details, see [Ephemeral Containers](https://kubernetes.io/docs/concepts/workloads/pods/ephemeral-containers/?spm=a2c4g.11186623.0.0.511d52e9bp6Pgx).

* Cgroups v2 has entered the stable phase. This feature constrains resources allocated to processes. For details, see [About cgroup v2](https://kubernetes.io/docs/concepts/architecture/cgroups/).

* In Kubernetes v1.25, support for Windows systems is optimized.

* In Kubernetes v1.25, the container image repository `k8s.gcr.io` is redirected to `registry.k8s.io`. For details, see [k8s.gcr.io redirect to registry.k8s.io](https://kubernetes.io/blog/2023/03/10/image-registry-redirect/).

* In Kubernetes v1.25, the EndPort field of network policies moves to GA. For details, see [Network policy port range](https://kubernetes.io/docs/concepts/services-networking/network-policies/#targeting-a-range-of-ports).

* In Kubernetes v1.25, local ephemeral storage capacity isolation has reached the GA phase, which achieves the capacity isolation between pods and local ephemeral storage. For details, see [Local ephemeral storage capacity isolation](https://github.com/kubernetes/enhancements/tree/master/keps/sig-storage/361-local-ephemeral-storage-isolation).

* In Kubernetes Version 1.25, ephemeral Inline CSI volumes have entered the Stable phase, which do not allow you to directly specify CSI data volumes in a pod by using a PersistentVolume (PV) or a PersistentVolumeClaim (PVC). For details, see [Ephemeral Inline CSI volumes](https://github.com/kubernetes/enhancements/tree/master/keps/sig-storage/596-csi-inline-volumes).

* In Kubernetes v1.25, the KMS v2 alpha1 API was introduced to improve performance. It enables key rotation and enhances observability. This API replaces AES\-CBC with AES\-GCM, uses a data encryption key (DEK) to achieve static data encryption (Kubernetes Secrets), and supports reading through both AES\-GCM and AES\-CBC. For details, see [Using a KMS provider for data encryption](https://kubernetes.io/docs/tasks/administer-cluster/kms-provider/).

* In Kubernetes v1.25, a standard interface is added: Container Object Storage Interface (COSI), which is in the Alpha phase. For details, see [Container Object Storage Interface (COSI)](https://kubernetes.io/blog/2022/09/02/cosi-kubernetes-object-storage-management/?spm=a2c4g.11186623.0.0.511d52e9bp6Pgx).

* In Kubernetes v1.25, if `PodHasNetwork` in the `pod status` field is set to `True`, it indicates that the pod runtime sandbox is initialized with networking configured. Kubelet begins pulling container images only if `PodHasNetwork` is set to `True`. Therefore, this field can be used to accurately generate Service Level Indicators (SLIs) for container initialization latency. For details, see [Differences between PodHasNetwork and Initialized Condition](https://kubernetes.io/blog/2022/09/14/pod-has-network-condition/?spm=a2c4g.11186623.0.0.511d52e9bp6Pgx#how-is-this-different-from-the-existing-initialized-condition-reported-for-pods).

* In Kubernetes v1.25, the minReadySeconds feature of StatefulSets has entered the Stable phase, which allows each pod to wait for a specified period to slow down the rolling update of StatefulSets. For details, see [Minimum ready seconds](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/?spm=a2c4g.11186623.0.0.511d52e9bp6Pgx#minimum-ready-seconds).

* In Kubernetes v1.25, the maxSurge feature of DaemonSets has entered the Stable phase, which allows a DaemonSet to run multiple DaemonSet pods on a node during a rolling update to reduce DaemonSet downtime during the update. For details, see [Perform a rolling update on a DaemonSet](https://kubernetes.io/docs/tasks/manage-daemon/update-daemon-set/?spm=a2c4g.11186623.0.0.511d52e9bp6Pgx).

* Kubernetes v1.25 provides alpha support for running pods with user namespaces. This maps root users inside pods to non\-zero IDs outside containers. From the host's perspective, containers run with regular unprivileged IDs even though they appear to be running as root. For more information, see [Alpha support for running pods with user namespaces](https://kubernetes.io/blog/2022/10/03/userns-alpha/?spm=a2c4g.11186623.0.0.511d52e9bp6Pgx).

* In Kubernetes v1.25, the RetroactiveDefaultStorageClass feature gate is added, which changes the method of allocating the default StorageClass to a PVC. After you enable this feature, PVCs without an assigned StorageClass will automatically be assigned the corresponding StorageClass, and you do not need to delete and recreate them.

* In Kubernetes v1.25, the JobPodFailurePolicy feature was added. It allows you to configure Jobs to specify how to handle pod failures based on container exit codes and pod statuses. This feature moved to Beta in v1.26. For details, see [Configuring pod failure policies for Jobs](https://v1-26.docs.kubernetes.io/docs/tasks/job/pod-failure-policy/?spm=a2c4g.11186623.0.0.511d52e9bp6Pgx#using-pod-failure-policy-to-ignore-pod-disruptions).

* In Kubernetes v1.25, the issue of the PodTopologySpread feature, where pods are unexpectedly unevenly distributed during rolling updates, is fixed.

* In Kubernetes v1.25, `KUBE-MARK-DROP`, `KUBE-MARK-MASQ`, and `KUBE-POSTROUTING` are no longer created, which optimizes the performance of kube\-proxy. For details, see [Cleaning up IPTables Chain Ownership](https://github.com/kubernetes/enhancements/issues/3178) and [Kubernetes’s IPTables Chains Are Not API](https://kubernetes.io/blog/2022/09/07/iptables-chains-not-api/).

* In Kubernetes v1.26, CRI v1alpha2 is no longer supported, and the container runtime needs to support CRI v1. This means that the containerd needs to be upgraded to version 1.6.0 or later before you upgrade nodes to Kubernetes v1.26.

* In Kubernetes v1.26, the dynamic resource allocation feature is added, which is used for requesting and sharing resources between pods and between pod containers, and allows you to provide parameters to initialize resources. This feature is in the Alpha phase, and you need to enable the DynamicResourceAllocation feature gate and the ` resource.k8s.io/v1alpha1` API group and install drivers for the specific resources to be managed. For details, see [Alpha API for Dynamic Resource Allocation](https://kubernetes.io/blog/2022/12/15/dynamic-resource-allocation/?spm=a2c4g.11186623.0.0.511d52e9bp6Pgx).

* In Kubernetes v1.26, non\-graceful node shutdown moves to Beta. Before you use this feature, you need to enable the NodeOutOfServiceVolumeDetach feature gate. When a node fails, the pods on the failed node remain in Terminating state, and VolumeAttachments cannot be deleted. To resolve this issue, you need to manually add the `out-of-service` taint to the node and evict the pods to a new healthy node. After the node is restored, you also need to manually remove the taint.

* In Kubernetes v1.26, pod fsGroup can be delegated to CSI driver during mounting, which replaces Kubelet in changing file and directory permissions in volumes. For details, see [CSI Driver fspGroup Support](https://kubernetes-csi.github.io/docs/support-fsgroup.html?spm=a2c4g.11186623.0.0.511d52e9bp6Pgx).

* In Kubernetes v1.26, the Pod Scheduling Readiness feature gate is added, which specifies the time when the scheduler begins scheduling pods. After you configure SchedulingGated for a pod, the scheduler will ignore the pod and no longer schedule the pod.

* In Kubernetes v1.26, CPU Manager moves to GA, and Kubelet allocates exclusive CPUs to containers by using CPU Manager. Three different policy options are supported. see [Control CPU management policies on the node](https://kubernetes.io/docs/tasks/administer-cluster/cpu-management-policies/).

* In Kubernetes v1.26, cross\-namespace storage data sources move to Alpha, which allows you to specify a data source for a PVC, even where the source data belongs to a different namespace.

* In Kubernetes v1.26, you can configure eviction policies for unhealthy pods for PodDisruptionBudget. You can specify `.spec.unhealthyPodEvictionPolicy=AlwaysAllow` to evict unhealthy pods without being affected by a PDB. This feature is in the Alpha phase, and you need to enable the PDBUnhealthyPodEvictionPolicy feature gate. For details, see [Unhealthy Pod Eviction Policy](https://kubernetes.io/docs/tasks/run-application/configure-pdb/?spm=a2c4g.11186623.0.0.511d52e9bp6Pgx#unhealthy-pod-eviction-policy).

* In Kubernetes v1.26, two `spec` fields are added for the API Priority and Fairness (APF) PriorityLevelConfigurations resources. These fields allow borrowing throttling seats from other priority levels. For details, see [PriorityLevelConfigurations](https://kubernetes.io/docs/reference/kubernetes-api/cluster-resources/priority-level-configuration-v1beta3/).

* In Kubernetes v1.26, httpGet for container lifecycle hooks preStop and postStart conforms to the settings of the `scheme` and `headers` fields. You can configure custom headers and enable HTTPS. You can specify `--feature-gates=ConsistentHTTPGetHandlers=false` on the kubelet to disable this feature.

* In Kubernetes v1.26, you can configure multiple StorageClasses by using the annotation `storageclass.kubernetes.io/is-default-class`, and the admission plugin will select the latest StorageClass as the default value and will no longer throw an exception.

* In Kubernetes v1.26, you can specify `--concurrent-horizontal-pod-autoscaler-syncs` to set the number of workers for the HorizontalPodAutoscaler (HPA) controller in kube\-controller\-manager.

* In Kubernetes v1.26, label selectors are verified for HPAs. When multiple HPAs point to the same pod, the HPAs do not take effect, and an AmbiguousSelector event is generated.


<span id=".5bqf5byD5ZKM56e76Zmk5Yqf6IO9"></span>
### Deprecated and removed features


* In Kubernetes v1.25, the migration of in\-tree [core plugins](https://github.com/kubernetes/enhancements/tree/master/keps/sig-storage/625-csi-migration?spm=a2c4g.11186623.0.0.511d52e9bp6Pgx) to CSI reaches the Stable phase. The [GlusterFS](https://github.com/kubernetes/enhancements/issues/3446) and [Portworx in-tree storage](https://github.com/kubernetes/enhancements/issues/2589) plug\-ins are deprecated, and the [Flocker](https://github.com/kubernetes/kubernetes/pull/111618), [Quobyte](https://github.com/kubernetes/kubernetes/pull/111619), and [StorageOS](https://github.com/kubernetes/kubernetes/pull/111620) in\-tree storage plug\-ins are removed.

* In Kubernetes v1.25, Kubelet cleans up IPTables chain ownership by using the IPTablesCleanup feature gate. For details, see [Cleaning up IPTables Chain Ownership](https://github.com/kubernetes/enhancements/issues/3178?spm=a2c4g.11186623.0.0.511d52e9bp6Pgx).

* In Kubernetes v1.25, the kube\-controller\-manager removes the `deleting-pods-qps`, `deleting-pods-burst`, and `register-retry-count` command\-line parameters.

* In Kubernetes v1.25, kube\-apiserver replaces the `--service-account-api-audiences` startup parameter with `--api-audiences`.

* In Kubernetes v1.26, the GlusterFS driver is removed, and the [OpenStack](https://github.com/kubernetes/enhancements/issues/1489?spm=a2c4g.11186623.0.0.511d52e9bp6Pgx) Cinder in\-tree storage driver code that uses CSI is removed.

* In Kubernetes v1.26, the nested authentication code for specific cloud providers is removed from client\-go and kubectl. It can be replaced by [authentication plug-ins](https://kubernetes.io/docs/reference/access-authn-authz/authentication/#client-go-credential-plugins).

* In Kubernetes v1.26, kubectl replaces the `--prune-whitelist` parameter with `--prune-allowlist`.

* In Kubernetes v1.26, the [Dynamic Kubelet Configuration](https://github.com/kubernetes/enhancements/tree/2cd758cc6ab617a93f578b40e97728261ab886ed/keps/sig-node/281-dynamic-kubelet-configuration) feature gate and its code in kube\-apiserver are removed.

* In Kubernetes v1.26, the kube\-apiserver command line argument begins deprecating the `--master-service-namespace` parameter.

* In Kubernetes v1.26, the following parameters for the kubectl run command have been officially deprecated: `--cascade`, `--filename`, `--force`, `--grace-period`, `--kustomize`, `--recursive`, `--timeout`, and `--wait`.

* In Kubernetes v1.26, the kube\-proxy userspace modes have been removed. The `userspace` proxy mode, which has been deprecated for over a year, is no longer supported on either Linux or Windows. For details, see [Remove kube-proxy userspace modes](https://github.com/kubernetes/kubernetes/pull/112133). Linux users need to use `iptables` or `ipvs`, and Windows users need to use `kernelspace`. Using `--mode userspace` will fail. Windows winkernel kube\-proxy no longer supports Windows HNS v1 APIs.


<span id=".YXBpLeeJiOacrOWPmOabtA=="></span>
### API version changes


* In Kubernetes v1.25, the CronJob API of the `batch/v1beta1` version is removed, and the API of the `batch/v1` version that is available starting from Kubernetes v1.21 continues to be provided.

* In Kubernetes v1.25, the EndpointSlice API of the `discovery.k8s.io/v1beta1` version is removed, and the API of the `discovery.k8s.io/v1` version that is available starting from Kubernetes v1.21 continues to be provided.

* In Kubernetes v1.25, the `events.k8s.io/v1beta1` Event API version is removed. The batch/v1 API version (available since Kubernetes `v1.21`) continues to be provided. Field changes are as follows:

   * The `type` field can only be set to either `Normal` or `Warning`.

   * The `involvedObject` field has been renamed to `regarding`.

   * The `action`, `reason`, `reportingController`, and `reportingInstance` fields are required when you create an `events.k8s.io/v1` event.

   * `eventTime` is used instead of the deprecated `firstTimestamp` field (This field has been renamed `deprecatedFirstTimestamp` and is not allowed in new `events.k8s.io/v1` Event objects).

   * `series.lastObservedTime` is used instead of the deprecated `lastTimestamp` field (This field has been renamed `deprecatedLastTimestamp` and is not allowed in new `events.k8s.io/v1` Event objects).

   * `series.count` is used instead of the deprecated `count` field (This field has been renamed `deprecatedCount` and is not allowed in new `events.k8s.io/v1` Event objects).

   * `reportingController` is used instead of the deprecated `source.component` field (This field has been renamed `deprecatedSource.component` and is not allowed in new `events.k8s.io/v1` Event objects).

   * `reportingInstance` is used instead of the deprecated `source.host` field (This field has been renamed `deprecatedSource.host` and is not allowed in new `events.k8s.io/v1` Event objects).

* In Kubernetes v1.25, the `autoscaling/v2beta2` HorizontalPodAutoscaler API was removed.

* In Kubernetes v1.25, the PodDisruptionBudget API of the `policy/v1beta1` version is removed, and the API of the `policy/v1` version continues to be provided.

* In Kubernetes v1.25, the `node.k8s.io/v1beta1` API for RuntimeClass is removed, and the `node.k8s.io/v1` API continues to be provided.

* In Kubernetes v1.26, the `flowcontrol.apiserver.k8s.io/v1beta1` API for FlowSchema and PriorityLevelConfiguration is removed, and the `flowcontrol.apiserver.k8s.io/v1beta2` and `flowcontrol.apiserver.k8s.io/v1beta3` APIs continue to be provided.

* In Kubernetes v1.26, the `DisableCompression` field is added to kubeconfig, which is disabled by default.


<span id=".5Y-C6ICD6ZO-5o6l"></span>
## Reference links

For more information on the performance and feature evolution of Kubernetes version v1.26, see:


* [CHANGELOG-1.26.md](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.26.md)

* [CHANGELOG-1.25.md](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.25.md)

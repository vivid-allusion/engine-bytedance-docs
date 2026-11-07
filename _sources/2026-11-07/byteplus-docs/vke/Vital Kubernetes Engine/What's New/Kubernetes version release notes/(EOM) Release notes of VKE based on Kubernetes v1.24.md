---
title: "(EOM) Release notes of VKE based on Kubernetes v1.24"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v-1_24"
---

Vital Kubernetes Engine (VKE) strictly adheres to the Certified Kubernetes Conformance Program. This topic describes the changes introduced in the VKE release based on Kubernetes v1.24.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">VKE will no longer provide technical support for Kubernetes v1.24 as of <strong>April 30, 2025</strong> (UTC+08). For more information, see <a href="https://docs.byteplus.com/en/docs/vke/Kubernetes_Version_1-24_cluster_EOM_announcement">Product announcement</a>.</div>


<span id=".54mI5pys5Y-R5biD6K-05piO"></span>
## Release notes

Table 1: Core components and descriptions


|Core component |Current version |Considerations |
|---|---|---|
|Kubernetes |v1.24.17 |None |
|Containerd Runtime |1.6.21 |None |
|ETCD |3.5.5 |None |
|CoreDNS |1.8.6 |None |


Table 2: Kubernetes versions and the corresponding VKE versions


|Kubernetes version |VKE version |Release notes |
|---|---|---|
|v1.24.17 |vke.45 |Fixed an issue where the pvcprotection controller in kube\-controller\-manager caused PVCs to remain in the Terminating state for an extended period during deletion and fail to be released. |
|v1.24.17 |vke.44 |kube\-apiserver supports collecting control\-plane metrics using self\-managed Prometheus. |
|v1.24.17 |vke.42 |The logic based on which kube\-apiserver requests over 2 GB of etcd resources is optimized. |
|v1.24.17 |vke.41 |* Mount options for memory type of EmptyDir volume are available.<br><br>* mGPU scheduling results can be transmitted to container environment variables. |
|v1.24.17 |vke.40 |Improved the handling of GPU card failure in mGPU scheduling scenarios. |
|v1.24.17 |vke.39 |The enhanced API server can inject sidecar containers into VCI pods. |
|v1.24.17 |vke.38 |Enhanced the extended scheduler to support mGPU online/offline colocation. |
|v1.24.17 |vke.37 |The vulnerability [CVE-2024-10220](https://docs.byteplus.com/en/docs/vke/Kubernetes-security-vulnerability-announcement-CVE-2024-10220) is fixed. |
|v1.24.17 |vke.36 |The code from the Kubernetes community v1.24.17 is synchronized. |
|v1.24.15 |vke.35 |Enhanced the expansion scheduler, which can detect changes in virtual kubelet services. |
|v1.24.15 |vke.34 |The expansion scheduler is enhanced, which supports NUMA\-aware scheduling and RDMA topology\-aware scheduling. |
|v1.24.15 |vke.33 |The issue where Local Path Provisioner is not supported when the expansion scheduler detects vePFS storage is fixed. |
|v1.24.15 |vke.32 |* The expansion scheduler is enhanced, and the mGPU cross\-GPU sharing feature supports the full computing power allocation strategy.<br><br>* The expansion scheduler is enhanced, which can detect vePFS storage. |
|v1.24.15 |vke.31 |Fixed the issue that occurs during initialization of the extended scheduler add\-on. |
|v1.24.15 |vke.30 |Optimized the release specifications for core components. |
|v1.24.15 |vke.29 |The issue where the Ready state of containers changes when kubelet restarts is fixed. |
|v1.24.15 |vke.28 |The expansion scheduler is enhanced, which supports mGPU preemptive scheduling. |
|v1.24.15 |vke.27 |The expansion scheduler is enhanced, which supports VCI resource inventory awareness. |
|v1.24.15 |vke.26 |The self\-signed certificate of the API server is optimized. |
|v1.24.15 |vke.25 |* Kubelet is enhanced, which allows you to configure container resource views.<br><br>* Kubelet is enhanced, which allows you to configure the graceful shutdown period for evicted pods by using annotations.<br><br>* The load\-aware scheduling issue of the expansion scheduler is fixed. |
|v1.24.15 |vke.24 |The runc container escape vulnerability [CVE-2024-21626](https://docs.byteplus.com/en/docs/vke/Kubernetes-security-vulnerability-announcement-CVE-2024-21626) is fixed. |
|v1.24.15 |vke.23 |* Kubelet is enhanced, which performs device allocation based on the scheduler allocation results.<br><br>* The expansion scheduler is enhanced, which supports RDMA topology\-aware scheduling. |
|v1.24.15 |vke.21 |Enhanced the elastic resource priority scheduling feature to support proportional scheduling and to trigger scale\-out by Cluster Autoscaler. |
|v1.24.15 |vke.20 |The issue where pods occasionally cannot be scheduled when the expansion scheduler is configuring the MultiPoint add\-on is fixed. |
|v1.24.15 |vke.19 |The API server parameter configuration is enhanced to ensure consistency with the community version. |
|v1.24.15 |vke.18 |Enhanced the API Server and optimized the way parameters are configured. |
|v1.24.15 |vke.17 |The API server is strengthened and the vulnerabilities [CVE-2023-44487](https://github.com/advisories/GHSA-qppj-fm5r-hxr3) and [CVE-2023-39325](https://github.com/advisories/GHSA-4374-p667-p6c8) are fixed. |
|v1.24.15 |vke.16 |Enhanced the extended scheduler to avoid cache penetration to etcd. |
|v1.24.15 |vke.15 |Fixed the issue that occurs when volumes are unmounted after Kubelet is upgraded. |
|v1.24.15 |vke.14 |The expansion scheduler is enhanced, with the load\-aware scheduling feature improved. |
|v1.24.15 |vke.13 |* The expansion scheduler is enhanced, which supports NUMA\-aware scheduling.<br><br>* The issue with synchronization of the actual load when the expansion scheduler reschedules pods is fixed. |
|v1.24.15 |vke.12 |* The expansion scheduler is enhanced, which achieves load\-aware hotspot descheduling.<br><br>* The expansion scheduler is enhanced, which can inject node information into pods during scheduling. |
|v1.24.10 |vke.11 |Kubelet is enhanced, with the initialization logic of the node network add\-on optimized. |
|v1.24.10 |vke.10 |The Kubernetes cluster installation process is optimized. |
|v1.24.10 |vke.9 |The issue that occurred during the expansion scheduler initialization is fixed. |
|v1.24.10 |vke.8 |The expansion scheduler configuration is optimized. |
|v1.24.10 |vke.7 |* The expansion scheduler is enhanced, which supports the mGPU cross\-GPU sharing feature.<br><br>* Kubelet is enhanced, with the NetworkUnavailable Condition issue fixed. |
|v1.24.10 |vke.6 |The API server is enhanced to prevent cache penetration into ETCD. |
|v1.24.10 |vke.5 |* The expansion scheduler is enhanced, which supports load\-aware scheduling.<br><br>* The fine\-grained request observability capability of the API server is enhanced.<br><br>* The expansion scheduler is enhanced, which supports capacity scheduling.<br><br>* The vulnerabilities [CVE-2022-3162](https://github.com/kubernetes/kubernetes/issues/113756) and [CVE-2022-3294](https://github.com/kubernetes/kubernetes/issues/113757?spm=a2c4g.11186623.0.0.72362060ruCrcI) are fixed. |


<span id=".a3ViZXJuZXRlcy3npL7ljLrniYjmnKzop6Por7s="></span>
## About Kubernetes community versions

<span id=".6YeN5aSn5pu05paw"></span>
### Major updates


* Dockershim is removed.

   The Dockershim add\-on is deprecated in Kubernetes v1.20 and removed from the kubelet in Kubernetes v1.24. For more information about the removal of the support of Dockershim for Docker, see [Dockershim Removal FAQ](https://kubernetes.io/blog/2022/02/17/dockershim-faq/). For the impact and feedback of Dockershim's removal, see [GitHub issue](https://github.com/kubernetes/kubernetes/issues/106917).

* Beta APIs are disabled by default.

   New beta APIs are not enabled in clusters by default. Existing beta APIs and their updated versions will continue to be enabled by default.

* Released artifacts are signed.

   Cosign is used to sign container images and verify signed container images when artifacts are being released, which improves the security of the software release process.

* The performance of the API server is optimized.

   As of v1.24.10, Kubernetes is compiled with Go 1.19.5, of which the garbage collection algorithm is optimized. In this way, the P99 call latency of the API server has significantly decreased, and the supported load has increased by approximately 25%.

* Structured logging enters Beta. Components such as kube\-scheduler and kubelet use structured logs in `key="value"` format to facilitate parsing and analysis. For detailed information, see [Introducing Structured Logs](https://kubernetes.io/blog/2020/09/04/kubernetes-1-19-introducing-structured-logs/?spm=a2c4g.11186623.0.0.484122c6IfsorC).

* Secrets cannot be automatically created.

   By default, LegacyServiceAccountTokenNoAutoGeneration is enabled, and secrets are no longer automatically created for ServiceAccounts.

* OpenAPI V3 is enabled by default.

* You can display the available storage capacity by using CSIStorageCapacity objects, which reduces scheduling latencies caused by failures to create or mount PersistentVolumes (PVs) for pods.

* NonPreemptingPriority, which supports pod priority preemption, moves to GA.

* In\-tree storage plugin to Container Storage Interface (CSI) migration is steadily progressing. For detailed information, see [In-tree Storage Plugin to CSI Migration Design Doc](https://github.com/kubernetes/design-proposals-archive/blob/main/storage/csi-migration.md#background-and-motivations).

* The gRPC probe has been upgraded to the Beta phase and can be enabled through the feature gate parameter GRPCContainerProbe. You can configure native Kubernetes startup, liveness, and readiness probes for gRPC applications without the need to expose an HTTP endpoint or execute additional executable files.

* The image credential provider configuration of kubelet has been upgraded to the Beta phase. The kubelet can dynamically retrieve credentials for a container image registry by using exec plugins instead of storing credentials in the file system of a node.

* The [contextual logging](https://github.com/kubernetes/enhancements/issues/3077) feature is supported.

* You can soft\-reserve a range of static IP addresses for services to prevent IP allocation conflicts.

* Dynamic kubelet configuration is removed.

* The `.spec.minReadySeconds` parameter is supported by StatefulSets by default, and the StatefulSetMinReadySeconds feature gate moves to Beta. For detailed information, see [Minimum Ready Seconds for StatefulSets](https://kubernetes.io/blog/2021/08/27/minreadyseconds-statefulsets/).

* You can specify the `maxUnavailable` parameter for StatefulSets, which can stop pods faster during rolling updates.

* The JobReadyPods feature is enabled by default. After this feature is enabled, the number of pods in the `Ready` state is displayed in the status field of a Job.

* If you specify the `.spec.OS` parameter of a pod and the node label that indicates the node OS does not match the value of the .Spec.OS parameter, the kubelet of the node rejects the pod.

* The `Service.spec.ipFamilyPolicy` parameter is required when you create or update IPv4/IPv6 dual\-stack Services. When you use an IPv4/IPv6 dual\-stack Service, you need to set `ipFamilyPolicy` to `PreferDualStack` or `RequireDualStack`.

* Client\-go adds the following new workqueue state: Processing. When you shut down a workqueue in the Processing state, the shutdown process starts after all ongoing tasks in the workqueue are complete.

* All controllers are included in the health checks of kube\-controller\-manager.

* Certificates signed through the SHA\-1 hash algorithm cannot be verified by default.

* Kubelet creates an iptables chain named KUBE\-IPTABLES\-HINT in the mangle table. Containerized add\-ons that need to modify iptables rules in the host network namespace can use this chain to check whether the system is using `iptables-legacy` or `iptables-nft` in a more reliable manner.

* The following two parameters are added to kube\-proxy. This way, kube\-proxy can run on Windows.

   * `--forward-healthcheck-vip`: forwards the health check requests destined for the virtual IP address (VIP) of a service to the health check service of kube\-proxy.

   * `--root-hnsendpoint-name`: specifies the name of the Host Networking Service (HNS) endpoint for the root network namespace.

* The optional field `timeZone` is added for CronJobs. After you enable the CronJobTimeZone feature, you can run a CronJob in a specific time zone.

* Monitoring metrics for all add\-ons are enriched:

   * The `webhook_fail_open_count` metric is added to monitor webhook failures.

   * The `admission_webhook_request_total` metric is added to monitor webhook information, such as the webhook name, admission type, request action, HTTP status code, whether the request was rejected, and the namespace of the requested resource.

   * The `sync_proxy_rules_no_local_endpoints_total` metric is added for kube\-proxy, which displays the number of services without internal endpoints.

   * The `kubelet_volume_stats_health_abnormal` metric is added for kubelet to record the health status of volumes.

   * The following metrics are added to the API server, including `controller_admission_duration_seconds`, `step_admission_duration_seconds`, `webhook_admission_duration_seconds`, `apiserver_current_inflight_requests`, and `apiserver_response_sizes`. In addition, metrics related to LIST requests are added to the API server.

   * The following metrics are added to the kube\-scheduler, including `pending_pods`, `preemption_attempts_total`, `preemption_victims`, `schedule_attempts_total`, `scheduling_attempt_duration_seconds` (formerly `e2e_scheduling_duration_seconds`), `pod_scheduling_duration_seconds`, `pod_scheduling_attempts`, `framework_extension_point_duration_seconds`, `plugin_execution_duration_seconds`, and `queue_incoming_pods_total`.

   * The `evictions_number` metric is replaced with `evictions_total`.


<span id=".5bqf5byD5Yqf6IO9"></span>
### Deprecated features


* FlexVolume is deprecated. We recommend that you use the out\-of\-tree CSI driver. For detailed information, see [Kubernetes Volume Plugin FAQ](https://github.com/kubernetes/community/blob/master/sig-storage/volume-plugin-faq.md?spm=a2c4g.11186623.0.0.484139b8nCImvq#kubernetes-volume-plugin-faq-for-storage-vendors).

* Klog has deprecated some command line arguments, and Kubernetes is streamlining add\-on logs. For detailed information, see [System Logs](https://kubernetes.io/docs/concepts/cluster-administration/system-logs/#klog).

* Kubeadm has deprecated the `--experimental-patches` parameter in the `init`, `join`, and `upgrade` commands, and `--patches` and `--config` cannot be used together.

* kube\-log\-runner is included in the tar package of the release to replace the deprecated `--log-file` parameter. For detailed information, see [kube-log-runner](https://github.com/kubernetes/kubernetes/tree/master/staging/src/k8s.io/component-base/logs/kube-log-runner).

* The `scheduler_volume_scheduling_duration_seconds` metric is deprecated.

* The `apiserver_longrunning_requests` metric is used instead of the deprecated `apiserver_longrunning_gauge` metric.

* You need to specify `--dry-run=(server|client|none)` for `kubectl --dry-run`.

* The `Service.Spec.LoadBalancerIP` parameter is deprecated because this parameter does not support IPv4/IPv6 dual stack.

* kube\-apiserver removes the `--address`, `--insecure-bind-address`, `--port`, and `--insecure-port=0` parameters.

* kube\-controller\-manager and kube\-scheduler remove the `--port=0` and `--address` startup parameters.

* The kube\-apiserver startup parameters `--audit-log-version` and `--audit-webhook-version` only support `audit.k8s.io/v1`.

* Kubelet removes the startup parameter `--network-plugin`, which is only effective when the container runtime environment is set to Docker, and will be deleted together with Dockershim.

* The dynamic log sanitization feature is deprecated and removed. For detailed information, see [Dynamic log sanitization](https://github.com/kubernetes/kubernetes/pull/107207) and [KEP-1753](https://github.com/kubernetes/enhancements/tree/master/keps/sig-instrumentation/1753-logs-sanitization#deprecation).

* VolumeSnapshot v1beta1 CRD is deprecated in Kubernetes v1.20 and removed in Kubernetes v1.24. You need to use v1 instead.

* The `service annotation tolerate-unready-endpoints`, which has been deprecated since Kubernetes v1.11, is removed. `Service.spec.publishNotReadyAddresses` is used instead.

* The `metadata.clusterName` field is deprecated, and will be deleted in the later version.

* The logic based on which kube\-proxy listens on NodePort is removed. After the logic is removed, TCP connections may occasionally fail if the port of a NodePort Service conflicts with the port range specified by the kernel parameter `net.ipv4.ip_local_port_range` of a node. This leads to health check failures and service exceptions on the node. Before you update the Kubernetes version, make sure that the ports of all NodePort Services in the cluster do not conflict with the port range specified by the kernel parameter `net.ipv4.ip_local_port_range` of each node. For more information, see [Kubernetes community PR](https://github.com/kubernetes/kubernetes/pull/108496).

* The `node-role.kubernetes.io/master` label for master nodes is deprecated and replaced by `node-role.kubernetes.io/control-plane` (introduced in Kubernetes v1.20).

* The `node-role.kubernetes.io/control-plane:NoSchedule` taint is added for master nodes, and the old taint `node-role.kubernetes.io/master:NoSchedule` (which will be removed in Kubernetes v1.25) is retained.


<span id=".YXBpLeeJiOacrOWPmOabtA=="></span>
### API version changes

<span id=".5ZyoLWt1YmVybmV0ZXMtdjEtMjMt54mI5pys5ZCO"></span>
#### After Kubernetes v1.23


* `rbac.authorization.k8s.io/v1alpha1` is removed and `rbac.authorization.k8s.io/v1` is used.

* `scheduling.k8s.io/v1alpha1` is removed and `scheduling.k8s.io/v1` is used.

* `autoscaling/v2beta2` is deprecated, and HorizontalPodAutoscaler v2 moves to GA.

* `client.authentication.k8s.io/v1alpha1` is removed and `client.authentication.k8s.io/v1` is used.

* `CSIStorageCapacity.storage.k8s.io/v1beta1` is deprecated and `CSIStorageCapacity.storage.k8s.io/v1` is used.

* The `networking.k8s.io/v1alpha1` network API is removed.


<span id=".5ZyoLWt1YmVybmV0ZXMtdjEtMjIt54mI5pys5ZCO"></span>
#### After Kubernetes v1.22


* MutatingWebhookConfiguration and ValidatingWebhookConfiguration resources no longer support the `admissionregistration.k8s.io/v1beta1` API version. For WebhookConfigurations created using this version, promptly migrate them to the `admissionregistration.k8s.io/v1` API version. Otherwise, configuration creation will fail.

* CustomResourceDefinition no longer supports the `apiextensions.k8s.io/v1beta1` API version. For custom resources that are created with this version, you need to promptly replace this version with the `apiextensions.k8s.io/v1` API version. Otherwise, custom controller tuning will fail.

* APIService resources no longer support the `apiregistration.k8s.io/v1beta1` API version. For APIService resources that are created with this version, you need to promptly replace this version with the `apiregistration.k8s.io/v1` version. Otherwise, expansion API services will fail.

* TokenReview resources no longer support the `authentication.k8s.io/v1beta1` API version. For resources created with this version, promptly replace them with the `authentication.k8s.io/v1` version. Otherwise, authorization will fail.

* SubjectAccessReview resources no longer support the `authorization.k8s.io/v1beta1` API version. For resources created with this version, promptly replace them with the `authorization.k8s.io/v1` version. Otherwise, authorization will fail.

* CertificateSigningRequest resources no longer support the `certificate.k8s.io/v1beta1` API version. For resources created with this version, promptly replace them with the `certificate.k8s.io/v1` version. Otherwise, authorization will fail.

* Lease resources no longer support the `coordination.k8s.io/v1beta1` API version. For resources that are created with this version, you need to promptly replace the version with the `coordination.k8s.io/v1` version. Otherwise, leader election will fail, and normal service operation will be affected.

* Ingress and IngressClass resources no longer support the `networking.k8s.io/v1beta1` and `extensions/v1beta1` API versions. For resources created with this version, you need to promptly replace them with the `networking.k8s.io/v1` version. Otherwise, the application may be unable to expose services externally.

* ClusterRole, ClusterRoleBinding, Role, and RoleBinding resources no longer support the `rbac.authorization.k8s.io/v1beta1` API version. For RBAC resources that are created with this version, you need to promptly replace this version with the `rbac.authorization.k8s.io/v1` version. Otherwise, the permissions service within the application cluster will be affected.

* CSIDriver, CSINode, StorageClass, and VolumeAttachment resources no longer support the `storage.k8s.io/v1beta1` API version. For CSI resources created with this version, you need to promptly upgrade them to the `storage.k8s.io/v1 version`. Otherwise, the provision of storage services within the cluster will be affected, and CSI will be unavailable in the cluster.

* PriorityClass resources no longer support the `scheduling.k8s.io/v1beta1` API version. For PriorityClass resources that are created with this version, you need to promptly replace this version with `scheduling.k8s.io/v1`. Otherwise, operations may fail.


<span id=".5ZyoLWt1YmVybmV0ZXMtdjEtMjEt54mI5pys5ZCO"></span>
#### After Kubernetes v1.21


* The deprecated PodSecurityPolicy (PSP) is planned to be removed in v1.25.

* The service traffic topology awareness feature via the `Service topologyKeys` field is deprecated. Use the topology awareness feature instead.


<span id=".5Y-C6ICD6ZO-5o6l"></span>
## Reference links

For more information on the performance and feature evolution of Kubernetes version v1.24, see:


* [CHANGELOG-1.24.md](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.24.md)

* [CHANGELOG-1.23.md](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.23.md)

* [CHANGELOG-1.22.md](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.22.md)

* [CHANGELOG-1.21.md](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.21.md)

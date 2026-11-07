---
title: "(Scheduled for EOM) Release notes of VKE based on Kubernetes v1.30"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v1_30"
---

Vital Kubernetes Engine (VKE) strictly adheres to the Certified Kubernetes Conformance Program. This topic describes the changes introduced in the VKE release based on Kubernetes v1.30.

<span id=".54mI5pys5Y-R5biD6K-05piO"></span>
## Release notes

Table 1: Core components and descriptions


|Core component |Current version |Considerations |
|---|---|---|
|Kubernetes |1.30.4 |Kubernetes v1.29 and v1.30 have removed deprecated APIs in the test version. Do not forget to check compatibility before using new versions. For details, see the following sections of this topic: [Deprecated and removed features](https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v1_30#.5bqf5byD5ZKM56e76Zmk5Yqf6IO9) and [Deprecated API versions](https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v1_30#.YXBpLeeJiOacrOW8g-eUqA==). |
|ETCD |v3.5.9 |None |
|Containerd Runtime |v1.6.38 |None |
|CoreDNS |v1.11.1 |None |
|Ingress\-nginx |v1.10.4\-vke.1 |None |


Table 2: Kubernetes versions and the corresponding VKE versions


|Kubernetes version |VKE version |Release notes |
|---|---|---|
|v1.30.4 |vke.19 |Fixed an issue where the pvcprotection controller in kube\-controller\-manager caused PVCs to remain in the Terminating state for an extended period during deletion and fail to be released. |
|v1.30.4 |vke.18 |The expansion scheduler is enhanced to support image\-aware scheduling. |
|v1.30.4 |vke.17 |* kube\-apiserver audit logs now include the following new metrics:<br><br>   * `apiserver.response.k8s.io/object-count`: Indicates the number of objects returned by a LIST request.<br><br>   * `apiserver.response.k8s.io/size-bytes`: Indicates the actual size of the HTTP response body written for a LIST request, in bytes.<br><br>* The expansion scheduler is enhanced to support the node resource amplification capability. |
|v1.30.4 |vke.16 |Fixed an issue in the scheduler where pod scheduling failed when using an NPU card that does not support micro\-topology scheduling. |
|v1.30.4 |vke.15 |Optimized the scheduler controller and adjusted the NodeMonitor CR update interval. |
|v1.30.4 |vke.14 |Added the AcceleratorTopology add\-on in the scheduler to support NPU\-A2 topology awareness. |
|v1.30.4 |vke.13 |Added a rate\-limiting queue and improved the re\-queuing logic upon PV\-PVC binding failures for the PV controller. |
|v1.30.4 |vke.12 |vke.8<br><br>Added a rate\-limiting queue and improved the re\-queuing logic upon PV\-PVC binding failures for the PV controller.<br><br>The expansion scheduler supports scheduling with open\-local storage.<br><br>vke.7<br><br>Enabled collecting control plane metrics through self\-managed Prometheus.<br><br> |
|v1.30.4 |vke.11 |The expansion scheduler load awareness plugin is available at the cluster or pod level. |
|v1.30.4 |vke.10 |A new configuration protocol is supported in scenarios where a container uses multiple GPUs. |
|v1.30.4 |vke.9 |* You can configure the hugepage cgroup limits for pods by using pod annotations.<br><br>* You can set the timeout for Device Plugin gRPC interfaces to 30 seconds by using kubelet feature gates. |
|v1.30.4 |vke.8 |NUMA\-aware scheduling and RDMA topology\-aware scheduling are supported. |
|v1.30.4 |vke.7 |Optimized the logic when the kube\-apiserver requests an etcd resource over 2 GiB. |
|v1.30.4 |vke.6 |* Mount options for memory type of EmptyDir volume are available.<br><br>* mGPU scheduling results can be transmitted to container environment variables. |
|v1.30.4 |vke.5 |Improved the handling of GPU card failure in mGPU scheduling scenarios. |
|v1.30.4 |vke.4 |The enhanced API server can inject sidecar containers into VCI pods. |
|v1.30.4 |vke.3 |The enhanced expansion scheduler supports online and offline hybrid deployment of mGPU. |


<span id=".a3ViZXJuZXRlcy3npL7ljLrniYjmnKzop6Por7s="></span>
## About Kubernetes community versions

<span id=".6YeN5aSn5pu05paw"></span>
### Major updates

<span id=".5ZyoLWt1YmVybmV0ZXMtdjEtMzAt54mI5pys"></span>
#### Kubernetes v1.30


* The Legacy ServiceAccount Token Cleaner moves to GA. The legacy ServiceAccount tokens generated automatically will be marked as invalid by the Cleaner if they remain unused for a certain period of time (one year by default) and have not been mounted by any pods. An invalid token will be removed by the cleaner if it remains unused for a specific period of time (one year by default). For details, see[Legacy ServiceAccount token cleaner ](https://kubernetes.io/docs/reference/access-authn-authz/service-accounts-admin/#legacy-serviceaccount-token-cleaner).

* The Pod\-level auto\-scaling feature based on the ContainerResource metric moves to GA stage, allowing the HPA to implement auto\-scaling based on the resource usage of each container in the Pod instead of the overall resource usage of the Pod, making it easy to set scale\-out/in threshold for the most important containers in the Pod. For details, see [Container resource metrics ](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/#container-resource-metrics).

* The Webhook matching conditions feature has entered the GA phase. It allows Webhook matching based on specific conditions, enabling more precise Webhook triggering. For details, see [Dynamic Admission Control ](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/#matching-requests-matchconditions).

* The ready state of Pod scheduling enters the GA phase. The field `.spec.schedulingGates `is introduced to control the timing when the Pod allows scheduling. For details, see [Pod Scheduling Readiness ](https://kubernetes.io/docs/concepts/scheduling-eviction/pod-scheduling-readiness/).

* The minimum domain in the Pod topology distribution enters the GA phase, allowing the `minDomains` field to confine the minimum number of qualified domains when the Pod topology constraint is set to `whenUnsatisfiable: DoNotSchedule`. For details, see [minDomains ](https://kubernetes.io/docs/concepts/scheduling-eviction/topology-spread-constraints/#spread-constraint-definition).

* Preventing unauthorized volume mode conversion moves to GA. When creating a PersistentVolumeClaim based on VolumeSnapshot, the mode of the original volume used to create the snapshot needs to match that of the newly created volume to avoid security issues caused by volume mode changes. For details, see [KEP-3141 ](https://github.com/kubernetes/enhancements/issues/3141), [Preventing unauthorized volume mode conversion ](https://kubernetes.io/blog/2024/04/30/prevent-unauthorized-volume-mode-conversion-ga/).

* The VolumeManager reconstruction moves to GA. It allows the kubelet to carry additional information about how existing volumes are mounted during start.

* Service LoadBalancer IP mode moves to Beta. The new field `.status.loadBalancer.ingress.ipMode ` is added to the LoadBalancer Service to specify how the LoadBalancer IP behaves. For details, see [Load balancer IP address mode ](https://kubernetes.io/docs/concepts/services-networking/service/#load-balancer-ip-mode).

* Garbage collection for unused container images moves to Beta. The `imageMaximumGCAge` field specifies the maximum time that local images can remain unused, after which kubelet garbage\-collects them. For details, see [Garbage collection for unused container images ](https://kubernetes.io/docs/concepts/architecture/garbage-collection/#image-maximum-age-gc).

* CRDValidationRatcheting feature moves to Beta. The API server accepts updates to resources that become invalid after the update. This is allowed only if the update doesn't modify any invalid part of the resource. This won't affect existing resources or users. For details, see [CRD Validation ratcheting ](https://kubernetes.io/docs/tasks/extend-kubernetes/custom-resources/custom-resource-definitions/#validation-ratcheting).

* The NodeLogQuery feature moves to Beta. It allows fetching logs of services running on the node through the `/logs `endpoints. For details, see [log-query ](https://kubernetes.io/docs/concepts/cluster-administration/system-logs/#log-query).

* A new monitoring metric named `image_pull_duration_seconds ` is added to kubelet to track the time of pulling images. For details, see [List of Kubernetes metrics for the Alpha phase ](https://kubernetes.io/docs/reference/instrumentation/metrics/#list-of-alpha-kubernetes-metrics).

* The JobSuccessPolicy feature moves to Alpha. When creating an Indexed Job, you can define when a Job can be declared as succeeded using a `.spec.successPolicy` For details, see [Success policy ](https://kubernetes.io/docs/concepts/workloads/controllers/job/#success-policy).


<span id=".5ZyoLWt1YmVybmV0ZXMtdjEtMjkt54mI5pys"></span>
#### Kubernetes v1.29


* ReadWriteOncePod access mode moves to the GA phase. This access mode enables you to restrict PV access to a single pod in the cluster. ReadWriteOnce mode restricts volume access to a single node, but does not restrict simultaneous access to multiple pods on the same node. For details, see [ReadWriteOncePod ](https://kubernetes.io/docs/tasks/administer-cluster/change-pv-access-mode-readwriteoncepod/).

* The CSI NodeExpandSecret feature moves to GA. It allows secret credentials to be sent to the CSI driver in the process of NodeExpandVolume. For details, see [KEP-3107](https://github.com/kubernetes/enhancements/issues/3107) and [Use Secrets for node-driven expansion of CSI volume](https://kubernetes.io/blog/2022/09/21/kubernetes-1-25-use-secrets-while-expanding-csi-volumes-on-node-alpha/).

* KMS V2 moves to GA. It optimizes the performance of the KMS. For details, see [Use KMS driver for data encryption ](https://kubernetes.io/zh-cn/docs/tasks/administer-cluster/kms-provider/).

* PodReadyToStartContainersCondition feature moves to Beta. The new field `PodReadyToStartContainers `  accurately surfaces the initialization state of a Pod, from the perspective of Pod sandbox creation and network configuration. For details, see [Pod network readiness ](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/#pod-has-network).

* The native sidecar container moves to Beta. It allows you to specify a `restartPolicy` for an init container to enable the sidecar container. The sidecar containers are independent of other Init containers and the main application containers within the same Pod. For details, see [Sidecar containers](https://kubernetes.io/docs/concepts/workloads/pods/sidecar-containers/).

* The index\-based fallback mechanism moves to Beta. Once the JobBackoffLimitPerIndex is enabled in your cluster, you can create an Indexed Job with the `.spec.backoffLimitPerIndex` field specified to avoid the failure of the whole job because a single index reaches the `.spec.backoffLimit` limit repeatedly. For details, see  [Index-based fallback limits ](https://kubernetes.io/zh-cn/docs/concepts/workloads/controllers/job/#backoff-limit-per-index).

* The PodHostIPs feature moves to Beta. It adds a `status.hostIPs `field for Pod and downward APIs to expose the node IP to the workload. The `status.hostIPs` is a dual\-stack version of `status.hostIP`, and the first IP is always the same as `status.hostIP`. 

* Pod affinity/anti\-affinity with matchLabelKeys/mismatchLabelKeys has moved to Alpha. This feature can control the scope of Pod affinity/anti\-affinity more finely. It solves the issue where the scheduler cannot distinguish between new and old Pods during Deployment rolling updates, leading to unexpected scheduling results. For details, see [matchLabelKeys/mismatchLabelKeys ](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#matchlabelkeys).

* NFTables proxy mode moves to Alpha stage. It allows kube\-proxy to use the nftables API of the kernel netfilters subsystem to configure data packet forwarding rules. For details, see [nftables proxy mode ](https://kubernetes.io/docs/reference/networking/virtual-ips/#proxy-mode-nftables).

* Extended Service IP Range moves to Alpha. It allows the new ServiceCIDR object to dynamically configure the allocated range of Service ClusterIP addresses. For details, see [KEP-1880 ](https://github.com/kubernetes/enhancements/tree/master/keps/sig-network/1880-multiple-service-cidrs).

* Image pull based on RuntimeClass moves to Alpha. The kubelet will reference container images by a tuple ( `image name `, `runtime handle `) rather than just image names or image summaries. For details, see [Image pull per runtime class ](https://kubernetes.io/docs/concepts/containers/images/#image-pull-per-runtime-class).

* The PodLifecycleSleepAction feature has moved to Alpha. PreStop now has a new Sleep callback handler, which supports pausing the container for a specified duration. For details, see [Container lifecycle hooks](https://kubernetes.io/docs/concepts/containers/container-lifecycle-hooks/).

* KubeletSeparateDiskGC feature moves to Alpha. The kubelet is able to perform garbage reclaim on images (read\-only layer) and/or containers (writable layer) deployed on different file systems. For details, see [KEP-4191 ](https://github.com/kubernetes/enhancements/blob/master/keps/sig-node/4191-split-image-filesystem/README.md).


<span id=".5bqf5byD5ZKM56e76Zmk5Yqf6IO9"></span>
### Deprecated and removed features

<span id=".5ZyoLWt1YmVybmV0ZXMtdjEtMzAt54mI5pys"></span>
#### Kubernetes v1.30


* The command "kubectl apply" now uses the `--prune-allowlist` flag, instead of `--prune-whitelist`.

* The `SecurityContextDeny` admission plugin, which was deprecated in v1.27, has been removed. We recommend using `[PodSecurity] (https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/#podsecurity)` instead.


<span id=".5ZyoLWt1YmVybmV0ZXMtdjEtMjkt54mI5pys"></span>
#### Kubernetes v1.29


* By default, the built\-in `cloud providers` are disabled and can be enabled through feature gates `DisableCloudProviders` and `DisableKubeletCloudCredentialProvider`. For details, see [Removed In-Tree Cloud Providers ](https://github.com/kubernetes/enhancements/issues/2395).

* `selectorSpread `add\-on is removed from Kube\-Scheduler and uses `podTopologySpread `instead.

* CronJob does not support `.spec.schedule `field with `TZ `or `CRON_TZ ` inside. Use `.spec.timeZone `instead.


<span id=".YXBpLeeJiOacrOW8g-eUqA=="></span>
### Deprecated API versions


* In Kubernetes v1.29, the `flowcontrol.apiserver.k8s.io/v1beta3` API version for FlowSchema and PriorityLevelConfiguration was upgraded to `flowcontrol.apiserver.k8s.io/v1`. `V1beta3 `is deprecated and no longer supported in v1.32.

* In Kubernetes v1.29, the `kubescheduler.config.k8s.io/v1beta3` API version for KubeSchedulerConfiguration was removed. Migration to `kubescheduler.config.k8s.io/v1` is needed.

* In Kubernetes v1.29, the PVC `.spec.Resource` field type was switched from ResourceRequirements to VolumeResourceRequirements.

* In Kubernetes v1.29, the `OnPodConditions `field in the PodFailurePolicyRule was changed to an optional field.

* In Kubernetes v1.29, the alpha API ClusterCIDR was removed.


<span id=".5Y-C6ICD6ZO-5o6l"></span>
### Reference links

For more information on the performance and feature evolution of Kubernetes version 1.30, see:

[CHANGELOG-1.30.md](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.30.md)

[CHANGELOG-1.29.md](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.29.md)

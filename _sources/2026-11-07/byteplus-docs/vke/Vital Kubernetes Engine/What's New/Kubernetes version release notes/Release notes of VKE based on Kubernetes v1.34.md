---
title: "Release notes of VKE based on Kubernetes v1.34"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v1_34"
---

Vital Kubernetes Engine (VKE) strictly adheres to the Certified Kubernetes Conformance Program. This topic describes the changes introduced in the VKE release based on Kubernetes v1.34.

<span id="gPT1ACKN"></span>
## Release notes

Table 1: Core components and descriptions


|Core component |Current version |Considerations |
|---|---|---|
|Kubernetes |1.34.1 |Kubernetes v1.33 and v1.34 have deprecated and removed beta/alpha APIs. Compatibility checks are required when upgrading to these versions. For details, see the following sections of this topic: **Deprecated and removed features** and **Deprecated API versions**. |
|ETCD |v3.6.4 |None |
|Containerd Runtime |v2.1.9 |None |
|CoreDNS |v1.12.4 |None |
|Ingress\-nginx |v1.11.5\-vke.2 |None |


Table 2: Kubernetes versions and the corresponding VKE versions


|**Kubernetes version** |**VKE version** |**Release notes** |
|---|---|---|
|v1.34.6 |vke.12 |The issue where Kubelet ignores the userNamespaces.idsPerPod configuration is fixed. |
|v1.34.6 |vke.11 |The expansion scheduler is enhanced to support image\-aware scheduling. |
|v1.34.6 |vke.10 |The rate limiter for the kube\-apiserver is optimized. |
|v1.34.6 |vke.9 |* The expansion scheduler is enhanced to support the node resource amplification capability.<br><br>* The kube\-apiserver supports rate limiting. |
|v1.34.6 |vke.8 |* Fixed an issue in the scheduler where pod scheduling failed when using an NPU card that does not support micro\-topology scheduling.<br><br>* Added the following metrics to the kube\-apiserver audit log:<br><br>   * `apiserver.response.k8s.io/object-count`: Indicates the number of objects returned by a LIST request.<br><br>   * `apiserver.response.k8s.io/size-bytes`: Indicates the actual size of the HTTP response body written by a LIST request, measured in bytes. |
|v1.34.6 |vke.7 |* Fixed an issue in the scheduler where the RDMANetworkTopology add\-on did not implement the PreBind interface.<br><br>* Optimized the kube\-apiserver cache bypass feature. |
|v1.34.6 |vke.6 |Fixed a panic issue that occurs when the scheduler's ElasticQuota add\-on performs preemption. |
|v1.34.6 |vke.5 |* Optimized the scheduler controller and adjusted the NodeMonitor CR update interval.<br><br>* Synchronized community v1.34.6 code. |
|v1.34.1 |vke.4 |Added the AcceleratorTopology add\-on in the scheduler to support NPU\-A2 topology awareness. |
|v1.34.1 |vke.3 |* Added a rate\-limiting queue and improved the re\-queuing logic upon PV\-PVC binding failures for the PV controller.<br><br>* The expansion scheduler supports scheduling with open\-local storage. |


<span id="ViFF0vyk"></span>
## About Kubernetes community versions

<span id="pHAbtGgt"></span>
### Major updates

<span id="9UPmFT4p"></span>
#### In Kubernetes v1.34


* The Dynamic Resource Allocation (DRA) feature has entered the GA stage. DRA provides a richer set of descriptors for devices (requirements), supporting more advanced scheduling policies and flexible utilization of device resources. For details, see [Dynamic Resource Allocation](https://kubernetes.io/blog/2025/09/01/kubernetes-v1-34-dra-updates/).

* The Volume Attributes Class feature has reached the GA stage, allowing dynamic adjustment of volume performance attributes by modifying the volumeAttributesClassName field after PVC creation. For details, see [Volume Attributes Classes](https://kubernetes.io/docs/concepts/storage/volume-attributes-classes/).

* The ResilientWatchCacheInitialization feature has reached the GA stage. When the APIServer starts up, the watchCache must be fully initialized. Otherwise, the APIServer startup will fail. To improve system performance and stability, during watchCache initialization, watch requests and most list requests are rejected to prevent control‑plane overload and ensure successful startup. For details, see [Resilient watchcache initialization](https://github.com/kubernetes/enhancements/tree/master/keps/sig-api-machinery/4568-resilient-watchcache-initialization).

* The Streaming List responses feature is promoted to GA. The APIServer now encodes List response bodies in a streaming manner (using `protobuf` or `JSON` request formats). This avoids allocating all memory at once, preventing excessive memory consumption when handling List requests. For details, see [Streaming Encoding for LIST Responses](https://github.com/kubernetes/enhancements/blob/master/keps/sig-api-machinery/5116-streaming-response-encoding/README.md).

* The Cache‑Based Consistent Read feature has reached the GA stage. The APIServer now supports consistent reads served directly from its cache. By leveraging the [progress notification](https://etcd.io/docs/v3.5/dev-guide/interacting_v3/#watch-progress) mechanism of ETCD, the cache is kept consistent with ETCD, and consistent read requests are handled based on the cache. This reduces direct queries to ETCD (avoiding cache penetration) and improves request processing efficiency. For details, see [Consistent reads from cache](https://kubernetes.io/blog/2024/08/15/consistent-read-from-cache-beta/).

* The RelaxedDNSSearchValidation feature has reached the GA stage. It relaxes the validation rules for container DNS search strings (`.spec.dnsConfig.searches`), allowing underscores (`_`) and periods (`.`) to be included in DNS search strings.

* The RelaxedEnvironmentVariableValidation feature has reached the GA stage. The `pod env name` can now contain any printable ASCII character except "`=`". The range of printable ASCII characters is 32–126.

* The ListFromCacheSnapshot feature has entered the Beta stage. It allows the APIServer to create snapshots of the Watch cache storage and use these snapshots to handle LIST requests. For details, see [Snapshottable API server cache](https://github.com/kubernetes/enhancements/blob/master/keps/sig-api-machinery/4988-snapshottable-api-server-cache/README.md).

* Pod‑level resources have entered the Beta stage, enabling the specification of resource requests and limits at the pod level. For details, see [Pod Level Resources](https://kubernetes.io/blog/2025/09/22/kubernetes-v1-34-pod-level-resources/).

* The Pod Generation feature has entered the Beta stage. It allows the `observedGeneration` field to be set in the Pod status and allows other add\-ons to include `observedGeneration` in Pod Conditions, reflecting the metadata.generation of pods at the time the state or condition was recorded.

* The Watch‑List feature has entered the Beta stage. It converts LIST requests into Watch‑List requests for streaming processing, transmitting each item individually in a stream rather than returning the entire dataset at once, thereby reducing memory consumption. This feature is enabled by default for both the APIServer and the Kube‑controller‑manager. The WatchListClient FeatureGate is explicitly enabled on the client side. For details, see [Allow informers for getting a stream of data instead of chunking](https://github.com/kubernetes/enhancements/blob/master/keps/sig-api-machinery/3157-watch-list/README.md).

* The PreferSameTrafficDistribution feature has entered the Beta stage. Service now supports setting the `spec.trafficDistribution` value to `PreferSameZone` or `PreferSameNode`. `PreferSameNode` prioritizes sending traffic to endpoints that reside on the same node as the client. The legacy `PreferClose` option has been deprecated. For details, see [Traffic Distribution](https://kubernetes.io/docs/reference/networking/virtual-ips/#traffic-distribution).

* The container restart policy feature has entered the Alpha stage, enabling the configuration of restart policies at the container level. Each container can have its own `restartPolicy` set individually, and restartPolicyRules can be used to control restart behavior based on exit codes. For details, see [Finer-Grained Control Over Container Restarts](https://kubernetes.io/blog/2025/08/29/kubernetes-v1-34-per-container-restart-policy/).


<span id="4IQWUUFl"></span>
#### In Kubernetes v1.33


* The Extended Service IP Range feature has reached the GA stage. It introduces the ServiceCIDR and IPAddress resources to track the allocation of Service ClusterIPs and supports dynamically expanding the assignable ClusterIP range through ServiceCIDR. For details, see [Extend Service IP Ranges](https://kubernetes.io/docs/tasks/network/extend-service-ip-ranges/).

* The Service Traffic Distribution feature has reached the GA stage. By configuring the `.spec.trafficDistribution` field of a Service, you can define the preference for how traffic is routed to back\-end endpoints. For details, see [Traffic distribution control](https://kubernetes.io/docs/reference/networking/virtual-ips/#traffic-distribution).

* The HonorPVReclaimPolicy feature has reached the GA stage. When the `reclaimPolicy` of a PV is set to `Delete`, it ensures that the underlying storage resources are deleted strictly according to the policy, regardless of the deletion order of the PV or PVC, thereby preventing storage resource leaks. For details, see [PersistentVolume deletion protection finalizer](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolume-deletion-protection-finalizer).

* The Native Sidecar Containers feature has reached the GA stage. It enables sidecar containers by configuring the `restartPolicy` field within Init containers. Sidecar containers operate independently of other Init containers and the main application containers within the same pod. For details, see [Sidecar containers](https://kubernetes.io/docs/concepts/workloads/pods/sidecar-containers/).

* The CPUManagerPolicyOptions feature has reached the GA stage, enabling fine‑tuning of the resource allocation policies of CPU Manager. For details, see [Static policy options](https://kubernetes.io/docs/tasks/administer-cluster/cpu-management-policies/#cpu-policy-static--options).

* The ImageVolume feature has entered the Beta stage and is disabled by default. It allows users to specify an OCI image reference as a read‑only volume in a pod and mount it for reuse within containers. Multiple containers within a pod can share a single configuration file without including it in the main image, thereby minimizing security risks and reducing overall image size. For details, see [Image Volumes](https://kubernetes.io/blog/2025/04/29/kubernetes-v1-33-image-volume-beta/).

* The ProcMountType feature has entered the Beta stage. It allows customization of the mount type for the` /proc` filesystem inside containers via the `securityContext.procMount` field of a pod, enabling fine‑grained control over `/proc` filesystem access and improving pod security and isolation.

* The UserNamespacesSupport feature has entered the Beta stage, enabling pods to utilize Linux User Namespaces for enhanced container security. For details, see [User Namespaces enabled by default](https://kubernetes.io/blog/2025/04/25/userns-enabled-by-default/).

* The In‑Place Pod Resource Adjustment feature has entered the Beta stage. With the new `InPlacePodVerticalScaling` feature gate enabled, it supports adjusting the CPU and memory values under the `resources` field of pod containers. This avoids restarting the pod or its containers, enabling vertical autoscaling in place. For details, see [In-Place Pod Resize](https://kubernetes.io/blog/2025/05/16/kubernetes-v1-33-in-place-pod-resize-beta/).

* The SupplementalGroupsPolicy feature has entered the Beta stage, enabling fine‑grained control over SupplementalGroups for pods via the `.spec.securityContext.supplementalGroupsPolicy` field. For details, see [Configure fine-grained SupplementalGroups control for a Pod](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/#supplementalgroupspolicy).

* The Custom Container Stop Signal feature has entered the Alpha stage, allowing users to define the signal sent by the container runtime when stopping a container within the pod spec. For details, see [Defining custom stop signals](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/#defining-custom-stop-signals).


<span id="KyAmMcOK"></span>
### Deprecated and removed features


* In Kubernetes v1.34, Kubelet has removed the deprecated startup flag `--register-schedulable`. It no longer supports marking a node as `unschedulable` during registration, and recommends using `registerWithTaints` instead.

* In Kubernetes v1.33, the Git\-Repo volume add\-on is disabled by default. If you need to retain it, you can manually enable the `GitRepoVolumeDriver` feature gate.

* In Kubernetes v1.33, `DisableNodeKubeProxyVersion` is enabled by default and cannot be disabled. kubelet no longer sets the node's `status.kubeProxyVersion` field.


<span id="uxxifZ2f"></span>
### Deprecated API versions


* In Kubernetes v1.33, the Endpoints API v1 is deprecated and replaced with the EndpointSlices API. The EndpointSlice API has been stable since v1.21 and introduced features such as dual‑stack network support.  For details, see [Continuing the transition from Endpoints to EndpointSlices](https://kubernetes.io/blog/2025/04/24/endpoints-deprecation/).

* In Kubernetes v1.33, the v1alpha1 versions of ValidatingAdmissionPolicy and ValidatingAdmissionPolicyBinding have been removed.

* In Kubernetes v1.33, `resource.k8s.io/v1beta1` is deprecated, and using v1beta2 instead is recommended.

* In Kubernetes v1.33, the `apidiscovery.k8s.io/v2beta1` API group is disabled. This API is used by clients to query all registered API resources in the cluster. We recommend migrating to the stable v2 version.

* In Kubernetes v1.33, the `Pod status.resize` field is deprecated and replaced by the PodResizeInProgress and PodResizePending conditions, which indicate the status of resource adjustments during vertical scaling of pods.

* In Kubernetes v1.33, the EndpointSlice annotation `service.kubernetes.io/topology-mode` is deprecated. Using `spec.trafficDistribution` instead is recommended.


<span id="3qOgjyXn"></span>
### Reference links

For more information about the performance and feature evolution in Kubernetes v1.34, see

[CHANGELOG-1.34.md](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.34.md)

[CHANGELOG-1.33.md](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.33.md)

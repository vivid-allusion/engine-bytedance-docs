---
title: "Best practices for VCI troubleshooting"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Best_practices_for_VCI_troubleshooting"
---

This topic is intended for technical and operations teams deploying services on VCIs. It systematically covers best practices, from issue identification and troubleshooting to monitoring, alerting, and architecture optimization. These best practices can help your workloads run on VCIs reliably.

## 1. Understanding VCI

Before proceeding to best practices for VCI troubleshooting, quickly address some common VCI misconceptions. For more information about basic concepts, application scenarios, and positioning of VCI, see [VCI overview](https://docs.byteplus.com/en/docs/vke/VCI-Overview?lang=zh).

* **Misconception 1**: Kubernetes knowledge is not required to use VCI.

   **Fact**: This is not correct. While VCI eliminates node O&M efforts, it operates within the orchestration framework of Kubernetes. You need knowledge of core Kubernetes concepts (such as Pod, Deployment, Service, and Annotation) to effectively define and manage applications. VCI only manages nodes in the data plane.

* **Misconception 2**: VCI applies to all applications.

   **Fact**: Not necessarily. VCI is a nodeless service that eliminates node O&M, so applications requiring node\-related features (such as DaemonSet and NodePort) cannot run in VCIs.

* **Misconception 3**: VCI does not apply to scenarios featuring fixed resource consumption over a long period.

   **Fact**: This is not correct. Some users mistakenly believe that for long\-running applications that operate stably for extended periods, with fixed resource requirements and high resource utilization, using traditional ECS node pools is more cost\-effective. In fact, VCI supports the Reserved Container Instance (RCI) feature, which allows its usage costs to be aligned with those of ECS node pools. VCI not only provides extreme elasticity to handle fluctuating demands, but also meets business requirements in steady\-state scenarios through yearly/monthly subscriptions.

* **Misconception 4**: The vci\-profile configuration implements enforced scheduling.

   **Fact**: It is soft scheduling, not forced scheduling. vci\-profile is a convenient, non\-intrusive global configuration method to influence Pod scheduling preferences. Final scheduling results are jointly affected by multiple factors, including Pod annotations, cluster\-level resource policies, and more. Therefore, a Pod may still not be scheduled to a VCI.

## 2. Locating issues: Layering and determination

A clearly layered model is critical to troubleshooting VCI issues. It helps you quickly narrow down the scope of the issue and avoid wasting time on irrelevant factors. The recommended troubleshooting sequence is "**top\-down, inside\-out**", where you start from business performance, move to the application itself, then to the VCI instance, and finally extend to the network and external dependencies.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e9f0864335258a261a2822ace94ddd78.png)

The following are the core focus points for each layer:

**Card**

1. Application layer

This is the layer where you should begin with the troubleshooting flow. At this layer, you focus on observability metrics of your application.

* **Core questions**: Are there any abnormalities observed in the application? Are there any errors recorded in application logs?

* **Key metrics**: Application SLI/SLO (success rate/latency), error codes, and custom monitoring metrics.

* **Troubleshooting tools**: APMPlus, application logging services, and custom monitoring dashboards.

**Card**

2. Kubernetes and VCI resource Layer

If an abnormality occurs on the business application side, immediately drill down to the Kubernetes resource layer to check the Pod lifecycle and configuration.

* **Core questions**: Is the Pod running normally? Is the Pod configuration valid?

* **Key indicators**: Pod events (using the "kubectl describe pod" command), container logs (using the "kubectl logs" command), and Pod annotations.

* **Common states**: Pending, Terminating, CrashLoopBackOff, ImagePullBackOff, and FailedCreate.

**Card**

3. VCI data plane layer

The health of a VCI significantly affects the Pods running on it.

* **Core questions**: Is the virtual node where the VCI instance resides healthy? Are the relevant resources sufficient?

* **Key metrics**: Virtual node status, kubelet/containerd health, and GPU\-related metrics (DCGM).

* **Troubleshooting tools**: The "kubectl get node" command and Cloud Monitor.

**Card**

4. Network routing layer

Networking is essential for distributed systems, and VCI is no exception.

* **Core questions**: Is the network connected? Is DNS resolution working properly? Is traffic flow allowed by security policies?

* **Key components**: VPC routing, security groups, network ACLs, and CoreDNS.

* **Troubleshooting tools**: ping, curl, nslookup, tcpdump, and VPC/CLB console.

**Card**

5. Control plane and dependency service layer

When a large number of VCI instances encounter common issues, there is probably a problem with the upstream control plane or dependent services.

* **Core questions**: Is the VCI control plane stable? Are the dependent monitoring and storage services normal?

* **Key metrics**: Success rates of core VCI APIs and Virtual Kubelet interfaces.

* **Troubleshooting tools**: Cloud Monitor, VMP, and alerting platforms.

**Card**

6. Resource and quota layer

Pending states or creation failures are often related to resource availability.

* **Core questions**: Does the account have sufficient quotas? Is the resource inventory in the target availability zone sufficient?

* **Key indicators**: FailedScheduling events, Quota Center alerts, quota abnormalities (usually indicating insufficient quotas), and sold\-out abnormalities (indicating resource shortages).

* **Troubleshooting tools**: The Quota center console and tickets for technical consultation.

## 3. Handling high\-frequency failures: SOP

This section compiles common high\-frequency issues from real\-world cases and presents them in a standard operating procedure (SOP) format: "Issue phenomenon → Possible cause → Issue identification → Recommended fix."

**Note**: Stay calm when encountering issues. The `kubectl describe pod <pod-name>` command is your primary diagnostic tool, and 90% of issue clues reside in the Events section of the command output.

### 3.1 Abnormal Pod states

|**Issue phenomenon** |**Possible cause** |**Issue identification** |**Recommended fix** |
|---|---|---|---|
|Pod stuck in the Pending state |* Insufficient resource quotas or stock: The vCPU, memory, or GPU quota for VCI in the account is exhausted, or the resource stock in the availability zone is insufficient.<br><br>* No match for scheduling conditions: The resource specifications (such as specific CPU or GPU models), availability zone, subnet, and other factors requested by the Pod cannot be satisfied.<br><br>* Invalid vci\-profile settings: Selectors or other items in the vci\-profile configuration are invalid, preventing the Pod from correctly matching VCI scheduling rules.<br><br>* Control\-plane component abnormalities: The VCI scheduler or Virtual Kubelet is abnormal. |1. Run `kubectl describe pod <pod-name>` to view events. Pay special attention to the FailedScheduling event, which clearly indicates the cause (for example, `Insufficient quota`or `No nodes available to schedule pods`).<br><br>2. In the [Quota Center](https://console.byteplus.com/quota) console, check the quota usage of VCI\-related resources.<br><br>3. Check the Pod YAML configuration for errors in scheduling\-related settings (such as `annotations` and `nodeSelector`).<br><br>4. Check whether the ConfigMap configuration corresponding to `vci-profile` in the `kube-system` namespace meets expectations. |1. Increase the quota: Request an increase in the corresponding resource quota in the [Quota Center](https://console.byteplus.com/quota). For details, see [Viewing and requesting quotas](https://docs.byteplus.com/en/docs/vke/VCI-limits#.6YWN6aKd5p-l55yL5ZKM55Sz6K-3).<br><br>2. Adjust the scheduling policy: Relax the scheduling restrictions of the Pod, for example, by deploying the VCI Pod in another availability zone or updating the VCI instance specification.<br><br>3. Check stock status:  Contact your account manager or technical support to confirm the resource stock status in the target availability zone.<br><br>4. Fix configuration errors: Correct invalid settings in the Pod YAML or vci\-profile configuration based on information such as the Message field of the failure or event. |
|Pod stuck in the Terminating state |* Abnormal application process status: The application process inside the container is blocked in the kernel state (Disk Sleep) and cannot respond to the SIGTERM signal. This is common when storage clients (such as JuiceFS) are not unmounted normally, resulting in application I/O blocking.<br><br>* Volume unmount failure: The unmount operation of underlying volumes, such as EBS or FileNAS filesystems, is stuck for a long time.<br><br>* Abnormal network resource reclamation: An exception occurs during the unbinding or reclamation of network resources, such as ENIs.<br><br>* Data\-plane node abnormalities of VCI: The underlying physical server or MicroVM has failed and cannot complete the cleanup work. |1. Log in to the Pod corresponding to the VCI and run the `ps aux \| grep 'D'` command to check for any processes in the D state. For information about how to log in to a Pod, see [Managing Pods](https://docs.byteplus.com/en/docs/vke/Managing-pods).<br><br>2. Check containerd or kubelet logs of data\-plane nodes for errors related to Pod cleanup.<br><br>3. Check logs in `/var/log/bytedrive` for storage issues.<br><br>4. If you suspect an application process issue, enter the container before deleting the Pod to check the process status and resource handle occupancy. For details, see [Viewing Pod information](https://docs.byteplus.com/en/docs/vke/Viewing-pod-details). |1. Fix logic: Ensure the application can correctly process the SIGTERM signal and clean up all resources before exiting, especially the storage client `umount` operation.<br><br>2. Force deletion: Run `kubectl delete pod <pod-name> --grace-period=0 --force` to forcibly delete the Pod.<br><br>   > **warning**<br>   <br><br>   > Forced Pod deletion may result in data inconsistency or resource leakage. Proceed with caution.<br>   <br><br>3. Submit a support ticket: If you cannot resolve the issue yourself, provide the Pod name, namespace, and time when the issue occurred, and contact the after\-sales support team for assistance. |
|Pod in the CrashLoopBackOff state |* Application start failure: The causes include application bugs, incorrect configuration, or dependent services not being ready.<br><br>* Insufficient resources: The `requests` or `limits` of the Pod are set too low. As a result, the application is terminated during startup due to OOM (Out of Memory) or insufficient CPU resources.<br><br>* Health check failure: The `livenessProbe` or `readinessProbe` configuration contains invalid settings, such as a wrong port or path, or a short timeout, causing the kubelet to misjudge the application as abnormal and restart it repeatedly.<br><br>* Permission issue: The process inside the container has no read or write access to the required files or directories. |1. Run the `kubectl logs <pod-name>` command to view the logs of the current container, where you can usually find the cause of the application startup failure.<br><br>2. Run the `kubectl logs <pod-name> --previous` command to view the logs of the previously terminated container. This check is critical for troubleshooting OOM and similar issues.<br><br>3. Run the `kubectl describe pod <pod-name>` command to view events. In the output, pay attention to information such as `Back-off restarting failed container` and check the Last State in the State section to identify the reason for exit (for example, `Exit Code: 137` indicates OOMKilled). |1. Fix application code bugs and configuration errors.<br><br>2. Add resources: Appropriately increase the values of `resources.requests` and `resources.limits` in the Pod spec configuration. <br><br>3. Adjust health check settings: Check and correct the `livenessProbe` and `readinessProbe` settings.<br><br>4. Fix permissions: Adjust the securityContext of the container or file permissions in the image. For details, see [Configuring security context](https://docs.byteplus.com/en/docs/vke/Configuring-a-security-context). |

### 3.2 Image and storage issues

|**Issue phenomenon** |**Possible cause** |**Issue identification** |**Recommended fix** |
|---|---|---|---|
|Slow or failed image pull (ImagePullBackOff)<br><br> |* Network unreachable: The VCI cannot access the target CR instance (public or private).<br><br>* Credential error (ImagePullSecrets): The `imagePullSecrets` field is incorrectly configured, or the specified credentials have expired, resulting in authentication failure.<br><br>* Missing image or insufficient permissions: The image address or tag is incorrect, or the current account does not have permission to pull the image.<br><br>* Image cache issues:<br><br>   * Automatic image cache is enabled, but the specified system volume capacity (via `vci.vke.volcengine.com/system-storage-size`) is too small to accommodate the cache.<br><br>   * The image cache itself is corrupted or expired.<br><br>* Proxy registry configuration error: The image proxy configured via `vci.volcengine.com/registry-mirror-config` has an incorrect address or credentials. |1. Run `kubectl describe pod <pod-name>` to view events, which usually contain error details, such as `Failed to pull image ...` `rpc error: code = Unknown desc = ...`.<br><br>2. Log in to a machine that can access the target repository and try to run `docker pull <image-name>:<tag>` to verify that the image and credentials are valid.<br><br>3. Check the `imagePullSecrets` setting in the YAML manifest for the Pod to confirm that the content of the corresponding Secret is correct.<br><br>4. If you use image cache, check whether the annotation for system disk size is configured as required according to the official documentation (for example, no less than 2 to 2.5 times the image size) For details, see [VCI image caching](https://docs.byteplus.com/en/docs/vke/VCI-Image-Cache). |1. Check network connectivity: Ensure that the subnet where the VCI resides has a correct public network egress (NAT gateway) or a network path to the private repository.<br><br>2. Update credentials: Create a valid imagePullSecrets or fix the current imagePullSecrets setting.<br><br>3. Correct image information: Use the correct image repository address and tag.<br><br>4. Adjust system volume size: Add or modify the `vci.vke.volcengine.com/system-storage-size` annotation for Pods using image cache<br><br>5. P2P acceleration: For large images, consider using the P2P acceleration solution. For details, see [P2P acceleration](https://docs.byteplus.com/en/docs/vke/P2P-acceleration-solution). |
|ProviderFailed or FailedCreateSystemDisk reported during Pod creation |1. Insufficient system volume capacity: The system volume of a VCI  (with a default size of 40 GiB) does not have enough space to accommodate the operating system, system components, and container images. This issue is especially prone to occur when you use a large image.<br><br>2. Underlying resource allocation failure: Allocating compute, storage (EBS volumes), or network resources failed in the data plane.<br><br>3. Account in arrears: The account balance is insufficient to create new billable resources. |1. Run the `kubectl describe pod <pod-name>` command to view events. Error information usually includes keywords such as `"ProviderFailed"` or `"FailedCreateSystemDisk"`.<br><br>2. Check the image size used by the Pod. If the image is too large, for example, more than 15 GiB, the issue is probably caused by insufficient system volume capacity.<br><br>3. In the [Billing center](https://console.byteplus.com/finance/account-overview/), confirm whether the account balance is sufficient. |1. Increase system volume capacity: Add `vci.vke.volcengine.com/system-storage-size: "80"`(unit: GiB) to the `metadata.annotations` field of the Pod configuration to explicitly specify a larger system volume. You can also specify a different appropriate system volume capacity.<br><br>2. Confirm your account balance:  Ensure that your account balance is not zero when vouchers are excluded. For details, see [Billing overview](https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview-2).<br><br>3. Retry: If the underlying resource allocation occasionally fails, simply delete the Pod and recreate it. If creation continues to fail, contact your BytePlus account manager or [submit a ticket](https://console.byteplus.com/workorder/create?step=1) to obtain technical support. |
|Volume mount failure (FailedMount) |1. EBS volume mounting: An attempt is made to mount an EBS volume from availability zone A to a VCI located in availability zone B.<br><br>2. Unreachable NAS/file storage network: The network between the VCI and the mount point of the NAS file system is unreachable or blocked by a security group or ACL.<br><br>3. Incorrect PV or PVC configuration: The PersistentVolume (PV) or PersistentVolumeClaim (PVC) configuration is incorrect. For example, it has a mismatching `storageClassName` or insufficient storage capacity.<br><br>4. Abnormal volume status: The volume itself is in the **Abnormal**, **Mounted**, or another state other than **Available**. |1. Run the `kubectl describe pod <pod-name>` command to view the details of `FailedMount` in the Events.<br><br>2. Check the PV manifest to confirm the volume ID corresponding to `spec.csi.volumeHandle`. Then, go to the [Volumes page in the ECS console](https://console.byteplus.com/ebs) to query the status and availability zone of the volume.<br><br>3. Run the `kubectl get pod <pod-name> -o wide` command to check the scheduling result of the Pod, and confirm whether the node and availability zone where it is scheduled are consistent with those of the volume.<br><br>4. If the storage type of the volume is FileNAS, check the routing and security policies between the VCI subnet and the FileNAS mount point. |1. Ensure the same availability zone: Use `nodeSelector` or the `vci.vke.volcengine.com/preferred-availability-zones` annotation to schedule the Pod to the same availability zone as the EBS volume.<br><br>2. Enable network connectivity: Correctly configure network access policies for FileNAS storage. For details, see [FileNAS](https://docs.byteplus.com/en/docs/vke/NAS-Volumes).<br><br>3. Fix PV or PVC configuration: Check and fix the PV or PVC configuration. |

### 3.3 Networking and service discovery issues

|**Issue phenomenon** |**Possible cause** |**Issue identification** |**Recommended fix** |
|---|---|---|---|
|DNS resolution failure |* CoreDNS failure or resource shortage: The CoreDNS Pod in the cluster is abnormal, or CPU or memory resources are insufficient due to excessive requests, resulting in response timeouts.<br><br>* Network policy (NetworkPolicy): A configured network policy blocks access from business Pods to port 53/UDP of the CoreDNS Pod in the kube\-system namespace.<br><br>* Incorrect Pod dnsPolicy configuration: The dnsPolicy of the Pod is incorrectly set to Default or None, which causes the in\-cluster DNS service not to be used.<br><br>* Upstream DNS issue: If you resolve a public domain name, the upstream DNS server used by CoreDNS may be faulty. |1. Enter the application Pod by running the `kubectl exec -it <pod-name> -- /bin/sh` command.<br><br>2. In the Pod, run the `cat /etc/resolv.conf` command to confirm whether the `nameserver` points to the service IP of the CoreDNS in the cluster.<br><br>3. Use `nslookup <service-name>` or `dig <external-domain.com>` to test domain resolution. If it times out or fails, try requesting the CoreDNS IP directly: `dig @<coredns-pod-ip> <domain-name>`.<br><br>4. Check the logs and resource usage of the CoreDNS Pod. |1. Scale out CoreDNS: Increase the number of replicas of CoreDNS or its resource `limits` value. For details, see [FAQ](https://docs.byteplus.com/en/docs/vke/How-do-I-update-the-CoreDNS-replica-count-and-resource-quotas).<br><br>2. Use NodeLocal DNSCache: Enable NodeLocal DNSCache for the cluster to reduce direct requests to CoreDNS and improve resolution performance. For details, see [Using NodeLocal DNSCache as a DNS caching agent](https://docs.byteplus.com/en/docs/vke/Using-NodeLocal-DNSCache).<br><br>3. Check network policies: Ensure that a policy allows the application Pod to access CoreDNS.<br><br>4. Fix `dnsPolicy`: Ensure that `dnsPolicy` is set to `ClusterFirst` (default) or `ClusterFirstWithHostNet`. |
|Cross\-network segment or cross\-service access failure |* Access blocked by security groups: The inbound and outbound rules of the security group that governs the source or destination VCI or ECS instance do not allow the corresponding protocol and port.<br><br>* VPC route table conflict or missing routes:<br><br>   * When multiple VPCs are connected via CEN, custom routes conflict with system routes (for example, a conflict in the `100.64.0.0/11` network segment).<br><br>   * No explicit route pointing to the peer end exists.<br><br>* Network ACL restriction: The network ACL associated with the subnet blocks traffic.<br><br>* CLB backend health check failure: The VCI serving as the CLB backend is removed due to the application process not listening or the health check failure. |1. VPC traffic path analysis: In the [VPC console](https://console.byteplus.com/vpc), open the "Path Analysis" tool and enter the source and destination IP addresses to check the connectivity of routes, security groups, and ACLs in a visualized manner. For details, see [Path analysis](https://docs.byteplus.com/en/docs/NetworkAdvisor/User-guide-Path-Analysis).<br><br>2. Check security groups: Check all security groups associated with the source and destination instances, respectively, to verify that both inbound and outbound rules are correctly configured For details, see [Configuring security groups](https://docs.byteplus.com/en/docs/vke/Security-group-settings).<br><br>3. Review the route table: Check the route table associated with the subnet where the VCI resides, focusing on whether custom routes overwrite or conflict with system routes. For details, see [Ingresses](https://docs.byteplus.com/en/docs/vke/Ingresses).<br><br>4. Check the backend server group of the CLB: In the [Load Balancer console](https://console.byteplus.com/clb), confirm whether the VCI is in the **Healthy** state. |1. Precisely allow traffic through security groups: Follow the principle of least privilege to modify security group rules to allow only necessary source or destination IP segments and ports. For details, see [Security group settings](https://docs.byteplus.com/en/docs/vke/Security-group-settings) and [Cluster access rules](https://docs.byteplus.com/en/docs/vke/Cluster-access-rules).<br><br>2. Fix routes: Adjust or delete conflicting route entries.<br><br>3. Adjust network ACL: Modify ACL rules to allow required traffic.<br><br>4. Fix business applications or adjust health check settings: Ensure that the application process on the CLB backend is listening normally and that health checking is configured correctly. |

## 4. Configure monitoring and alerting: Preventing issues before they occur

Proactive prevention is always preferable to reactive troubleshooting. Establishing a robust, comprehensive monitoring and alerting system is critical to ensuring the stability of VCI services. This section provides an actionable monitoring and alerting checklist, along with implementation suggestions.

### 4.1 Recommendations for monitoring and alerting subscription

The table in this subsection aggregates key metrics and events from BytePlus Cloud Monitor, VMP, APMPlus, and self\-managed alerting platforms. It offers a reference for building a panoramic monitoring view of VCI.

**Core principle for configuring alerting**: Alert quality is more important than quantity. Prioritize configuring alerts that directly indicate impaired user experience or signal major risks (such as SLI decline or a large number of Pending Pods) and establish clear SOPs for such alerts. For metrics prone to excessive alert noise (for example, transient high CPU load), set higher trigger thresholds or longer durations to prevent alert fatigue.

|**Category** |**Metric/Event name** |**Recommended threshold/condition** |**Corresponding platform** |**Description and applicable scenario** |
|---|---|---|---|---|
|VCI and Pod basics |pod_cpu_usage_seconds_total (Counter)<br><br>container_cpu_usage_seconds_total (Counter) |`rate(...) > 85%` for 5 consecutive minutes |VMP |CPU utilization of VCIs (at the Pod level) or individual containers. Persistently high levels may indicate resource bottlenecks or application logic issues. |
||pod_memory_working_set_bytes (Gauge)<br><br>container_memory_working_set_bytes (Gauge) | Pod/Container Limit \> 90% |VMP |Physical memory usage. When it approaches the configured Limit, the Pod faces the risk of OOMKilled. |
||container_network_receive_bytes_total (Counter)<br><br>container_network_transmit_bytes_total (Counter) |An abnormal surge or drop in `rate(...)` |VMP |Network throughput. This metric tracks drastic traffic fluctuations, which may indicate potential attacks, business anomalies, or network issues. |
|Core Kubernetes events |Event: Pod Pending |The number of Pending Pods in the same namespace is greater than 5  for 3 consecutive minutes |Self\-managed alerting platforms or Cloud Monitor |Widespread Pod scheduling failures. This event indicates insufficient cluster resources or scheduler abnormalities and signals critical failures. |
||Event: Pod Terminating |Number of terminating Pods in the same namespace \> 3 for 10 consecutive minutes |Self\-managed alerting platforms or Cloud Monitor |Pods fail to terminate properly, which will disrupt service rollouts and scaling operations. |
||Event: Node NotReady |Virtual node status changes to NotReady |Self\-managed alerting platforms or Cloud Monitor |Indicates a severe communication failure between the VCI data plane or Virtual Kubelet and the control plane. |
|GPU monitoring |DCGM_FI_DEV_GPU_TEMP (Gauge) |\> 85 (degrees Celsius) |VMP (DCGM Exporter) |High GPU temperature. Too high GPU temperature will trigger GPU throttling and may even cause hardware damage. |
||DCGM_FI_DEV_POWER_USAGE (Gauge) |`rate(...)` remains below the expected value |VMP (DCGM Exporter) |Persistently low GPU power during training jobs indicates that the GPU may not be properly utilized. |
||DCGM_FI_DEV_GPU_UTIL (Gauge)<br><br>DCGM_FI_DEV_MEM_COPY_UTIL (Gauge) |`avg_over_time(...) < 10%` for 10 consecutive minutes |VMP (DCGM Exporter) |Persistently low GPU utilization or GPU memory bandwidth utilization indicates idle GPU resources and the need for troubleshooting application settings. |
||DCGM_FI_DEV_XID_ERRORS (Gauge) |\> 0 |VMP (DCGM Exporter) |NVIDIA XID errors indicate critical GPU hardware or driver errors and require immediate attention. |
|Storage and volumes |kubelet_volume_stats_used_bytes / kubelet_volume_stats_capacity_bytes |Disk usage \> 90% |VMP |The capacity of the data volumes or system volume is nearly exhausted. This issue will cause data write failures and application crashes. |
||kubelet_volume_stats_inodes_used / kubelet_volume_stats_inodes |Inode usage \> 90% |VMP |Inode exhaustion will prevent the creation of new files. This metric applies to scenarios where a large number of small files are stored. |
||EBS IO metrics (such as DiskReadBandwidth, DiskWriteBandwidth) |Reaching 95% of the upper IO limit for the volume specification |Cloud Monitor |Storage IO reaching its bottleneck will cause a surge in application read/write latency. |
|Control plane and dependencies |Core VCI API SLIs (such as CreateContainerInstance) |Success rate < 99% for 5 consecutive minutes |Self\-managed alerting platforms |Abnormalities in the core APIs of the VCI control plane. This will cause widespread disruption to Pod creation and management operations. |
||Events related to Quota Center |Quota utilization exceeds 80% |Quota Center or Cloud Monitor |VCI resource quota is nearly exhausted. You need to apply for a quota increase in advance to avoid affecting business elasticity. |
|Subhealthy and faulty machines |Search for the issue keyword “InstanceReady” in the pod Condition or pod Label box.<br><br> |`kubectl get po -A -l vci.vke.volcengine.com/instance-fault=NodeNotReady`<br><br> |Self\-managed alerting platforms<br><br> |Node downtime: A physical server failure has occurred, and instances on the node can no longer run properly. |
||Filter by fault keyword "VciOps" in the pod Condition/pod Label box. |`kubectl get po -A-l vci.vke.volcengine.com/VciOps=PreVciNodeOffline` |Self\-managed alerting platforms<br><br> |Prepare sub\-healthy nodes for being offline. O&M actions will be performed by VCI later. This will impact the running of the VCI. |

### 4.2 Recommendations for alert subscription and management

* **Using built\-in templates**:

   * **VMP**: Use the built\-in alert templates provided by VMP for VKE to quickly create monitoring and alert rules for VCIs.

* **Alert noise reduction and aggregation**:

   * **Spike filtering**: To filter out invalid alerts, configure a policy that sends an alert only after it is triggered the specified number of times within the given number of minutes.

   * **Alert sending throttling**: Enable alert sending throttling to avoid being flooded with excessive alerts.

   * **Alert aggregation**: Set a reasonable aggregation interval to make alert information more organized and legible.

* **Alert grading and notification**:

   * **Alert grading**: Clearly define alert levels (such as `P0 / Fatal`, `P1 / Warning`, and `P2 / Notice`) to improve alert handling efficiency.

* **Alert\-to\-ticket automation and SOP integration**:

   * **Automation**: Establish automated workflows for closed\-loop handling of critical alerts.

   * **SOP integration**: To help on\-call response personnel quickly locate and resolve issues, attach the troubleshooting guide for the corresponding failure scenario to the alert content.

## 5. Preventing failures and optimizing design: Graceful VCI usage

Sound system design can eliminate a large number of failures at the source. The following are best practices that product and R&D teams should consider during the design phase.

**Card**

Keep images lightweight and warmed up

* **Lightweight design**: Image size is a key factor that affects Pod startup speed. Follow the best practices of VCI to build a multi\-stage Dockerfile. Package only the necessary runtime and binary files into the final image and avoid including non\-essential content (such as compilation tools, source code, and documentation).

* **Image caching**: For applications requiring large\-scale, rapid deployment, enable automatic or manual image caching. You can enable image caching using the annotation. Image caching allows VCI to pre\-cache image data to the specified volume in the target availability zone. For details, see [VCI image caching](https://docs.byteplus.com/en/docs/vke/VCI-Image-Cache-overview).

* **Image cache warmup**: New images or images not used for a long time may experience slow pulls, or failed pulls due to expired cache upon first use. Therefore, we recommend creating a small number of Pods to trigger and warm up the image cache before large\-scale deployment. After the cache status changes to **Ready.Ok**, you can proceed with full\-scale deployment.

**Card**

Reasonably estimating and configuring capacity

* **System volume capacity**: The default system volume for VCI is 40 GiB. For scenarios using large images, image caching, or writing significant temporary files to containers, this capacity may be insufficient. In these scenarios, use the \`vci.vke.volcengine.com/system-storage-size\` annotation to specify a reasonably larger system volume capacity to avoid Pod creation failure due to FailedCreateSystemDisk. For more information, see [VCI image caching](https://docs.byteplus.com/en/docs/vke/VCI-Image-Cache-overview).

* **Unified configurations with vci\-profile**: We recommend using vci\-profile to centrally manage VCI configurations at the namespace or cluster level, rather than specifying them individually in the YAML manifest of each workload. vci\-profile ensures consistency in configuration items (such as subnets, log collection, and security context) and reduces failures caused by missing or incorrect individual configurations. For details, see [Using VCI by configuring vci-profile](https://docs.byteplus.com/en/docs/vke/Using-VCI-by-configuring-vci-profile).

**Card**

Plan networking and governance proactively

* **Clear network planning**: Clear network topology planning should be established during the application design phase. Avoid using overlapping or conflicting network segments in the production environment, especially when using CEN to connect multiple VPCs. Prevent conflicts between custom routes and IP ranges for BytePlus public\-facing services (such as \`100.XX.XX.XX/11\`). For more information about VKE networking, see [Network overview](https://docs.byteplus.com/en/docs/vke/Container-networks).

* **Least\-privilege security groups**: We recommend configuring dedicated security groups for VCI. When doing so, follow the principle of least privilege to open only the protocols and ports necessary for the application. Avoid using \`0.0.0.0/0\` (this setting allows all traffic). For more information, see [Security group settings](https://docs.byteplus.com/en/docs/vke/Security-group-settings) and [Cluster access rules](https://docs.byteplus.com/en/docs/vke/Cluster-access-rules).

* **DNS governance**: For high\-concurrency applications or those sensitive to DNS resolution latency, we recommend enabling NodeLocal DNSCache in the cluster. This effectively reduces the request pressure on CoreDNS and improves the stability and performance of service discovery. For details, see [Using NodeLocal DNSCache as a DNS caching agent](https://docs.byteplus.com/en/docs/vke/Using-NodeLocal-DNSCache).

## 6. Implementation checklist

Before your product or project launch or after failure troubleshooting, you can go through the following checklist to ensure that key practices are in place:

|No. |Check item |Check content |
|---|---|---|
|1 |- [ ] Core alerts subscribed |Have you configured alerts for Pending Pods, Terminating Pods, memory/disk utilization, and core business SLIs? |
|2 |- [ ] System volume capacity evaluated |Have you allocated sufficient system volume capacity via the annotation for Pods using large images or image caches? |
|3 |- [ ] Resource limits configured |Have you set reasonable CPU and memory limits for all containers (especially in production environments) to prevent resource contention and OOM events? |
|4 |- [ ] Health checks configured |Have you configured accurate livenessProbe and readinessProbe for all long\-running services? |
|5 |- [ ] vci\-profile adopted |Have you implemented unified management of VCI configurations via vci\-profile? |
|6 |- [ ] Security group rules hardened |Do security groups only open required ports to avoid exposure to `0.0.0.0/0`? |
|7 |- [ ] DNS caching considered |For applications sensitive to DNS resolution, have you evaluated or enabled NodeLocal DNSCache? |

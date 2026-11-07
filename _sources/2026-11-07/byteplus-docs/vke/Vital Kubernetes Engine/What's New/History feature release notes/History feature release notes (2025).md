---
title: "History feature release notes (2025)"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/History_feature_release_notes_2025"
---

Vital Kubernetes Engine (VKE) feature updates released in 2025. 

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">For the latest release notes for VKE, refer to <a href="https://docs.byteplus.com/en/docs/vke/Release-notes">release notes</a>.</div>


<span id="4BjmOXrt"></span>
## Notes


* **Release region** refers to the region where the feature was first released. The release regions coming up afterward will not affect the historical release notes. For the regions where features are actually available, please refer to the information on the console pages.

* Historical **beta** records are not updated after a feature becomes generally available. For subsequent iterations of a feature, refer to the latest relevant release entry.


<span id="uwxwbGbT"></span>
## December 2025


|**Feature name** |**Description** |**Region** |**Related documentation** |
|---|---|---|---|
|New version of the RBAC authorization system |More permission management capabilities are added and optimized based on the original RBAC authorization system, which improves the flexibility and efficiency of permission management. |All |* [Using the new RBAC authorization system of VKE](https://docs.byteplus.com/en/docs/vke/Use_the_new_VKE_RBAC_authorization_system)<br><br>* [Granting RBAC permissions](https://docs.byteplus.com/en/docs/vke/Configuring-RBAC-permissions) |
|Checking and self\-healing |Custom node check items can be specified. This allows you to specify node failures based on NodeCondition information and achieves automatic checks and self\-healing. |All |* [Configuring node check and self-healing](https://docs.byteplus.com/en/docs/vke/NodePool-health-check-and-auto-repair)<br><br>* [Custom node check items](https://docs.byteplus.com/en/docs/vke/Custom_Node_check_and_self-healing) |
|Subscription node pools supporting automatic binding of EIPs to nodes |EIPs can be automatically bound to nodes during the scale\-out of subscription node pools, which reduces constraints in scenarios such as a pay\-as\-you\-go node pool being switched to a subscription node pool. |All |[Managing node pools](https://docs.byteplus.com/en/docs/vke/Managing-NodePools) |
|Load\-aware scheduling takes effect at the cluster level |Load\-aware scheduling can apply to all pods in a cluster. This reduces the need to modify pod configurations and improves your user experience. |All |* [Load-aware scheduling](https://docs.byteplus.com/en/docs/vke/Load-aware-scheduling)<br><br>* [Installing add-ons](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on) |
|LoadBalancer service integrating with NLB |When you configure a LoadBalancer service, you can use an annotation to integrate with NLB. This achieves higher\-performance elastic forwarding. |All |[Configuring an NLB service using annotations](https://docs.byteplus.com/en/docs/vke/Configuring_an_NLB_Service_using_annotations) |


<span id="8xuXE2Vo"></span>
## November 2025


|**Feature name** |**Description** |**Region** |**Related documentation** |
|---|---|---|---|
|RBAC supporting account cluster\-level authorization |[[Beta · Apply for Trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] The RBAC authorization system supports cluster account\-level authorization, which improves the flexibility and efficiency of permission management. |All |* [Granting RBAC permissions](https://docs.byteplus.com/en/docs/vke/Configuring-RBAC-permissions)<br><br>* [Using the new RBAC authorization system of VKE](https://docs.byteplus.com/en/docs/vke/Use_the_new_VKE_RBAC_authorization_system) |
|Custom metric collection |The custom metric collection feature is added, which allows clusters to expose metrics of control plane add\-ons. This helps you use self\-built Prometheus to collect metrics and build a cluster control plane monitoring dashboard, which integrates the metrics with your self\-built monitoring system. |All |* [Operation and maintenance configuration](https://docs.byteplus.com/en/docs/vke/Operation-and-maintenance-configuration)<br><br>* [Using self-built Prometheus to collect control plane add-on metrics](https://docs.byteplus.com/en/docs/vke/Using_self-managed_Prometheus_to_collect_control_plane_metrics) |
|Full release of Kubernetes v1.32 |Kubernetes v1.32 released by VKE has exited the beta stage and is officially released, which keeps pace with the native community. |All |[Release notes of VKE based on Kubernetes v1.32](https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v1_32) |
|Cluster public access |You can disable the cluster public access feature and simultaneously clean up the managed NAT gateways. After you disable this feature, you can use a custom public NAT gateway to achieve cluster public access. |All |* [Cluster basics](https://docs.byteplus.com/en/docs/vke/Cluster-basics)<br><br>* [How do I manually enable Public NAT for Internet endpoint for a cluster?](https://docs.byteplus.com/en/docs/vke/How-do-I-manually-enable-internet-facing-access-for-a-cluster) |
|Updating node pool billing types |The billing type of nodes within existing node pools can be updated, which improves your user experience and meets various billing change requirements. |All |[Managing node pools](https://docs.byteplus.com/en/docs/vke/Managing-NodePools) |
|CLB and ALB Ingresses supporting cross\-project certificate selection |For CLB and ALB Ingresses, when you configure HTTPS certificates, you can select certificates from the Certificate Center of another project. |All |* [Creating an ALB Ingress through the console](https://docs.byteplus.com/en/docs/vke/Creating-an-ALB-Ingress-in-the-console)<br><br>* [Creating CLB Ingresses through the console](https://docs.byteplus.com/en/docs/vke/Creating-a-CLB-Ingress-in-the-console) |
|Upgrading the node Kubernetes version at the node pool level |[[Beta · Apply for Trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] When you upgrade the Kubernetes version of a cluster, you can upgrade nodes either at the node level or the node pool level. This improves the efficiency of node upgrades in large\-scale clusters. |All |* [Upgrading clusters](https://docs.byteplus.com/en/docs/vke/Upgrading-a-cluster)<br><br>* [Best practices of cluster upgrade](https://docs.byteplus.com/en/docs/vke/Cluster-upgrade-best-practices) |
|FSX authentication |In VKE clusters, when you use FSX to integrate with TOS, you can achieve authentication through IRSA. This achieves pod\-level isolation in terms of access to OpenAPIs, which achieves fine\-grained isolation of access permissions on cloud resources and reduces security risks. |All |* [FSX authentication methods](https://docs.byteplus.com/en/docs/vke/FSX_authentication_method)<br><br>* [Using IRSA to implement authentication for storage mounting](https://docs.byteplus.com/en/docs/vke/Create_an_IAM_role_and_bind_it_to_csi-fsx)<br><br>* [Accessing TOS static PersistentVolume through the FSX client](https://docs.byteplus.com/en/docs/vke/Using_static_TOS_Volumes_through_the_FSX_client) |
|Cloud\-native basic observability |The period\-over\-period comparison and statement copying features are added to the observability dashboard of cloud\-native basic observability. These features help you understand data definitions in preset dashboards. You can use these statements to build custom monitoring dashboards in systems like Grafana. |All |[Using dashboards](https://docs.byteplus.com/en/docs/vke/Using_dashboard) |


<span id="G8BeTx08"></span>
## October 2025


|**Feature name** |**Description** |**Region** |**Related documentation** |
|---|---|---|---|
|Official commercialization of the pod\-identity\-webhook add\-on |The pod\-identity\-webhook add\-on is officially available for commercial use, which can automatically inject OIDC\-related environment variables into pods that use the IRSA feature. |All |* [pod-identity-webhook](https://docs.byteplus.com/en/docs/vke/pod-identity-webhook)<br><br>* [Using IRSA in clusters](https://docs.byteplus.com/en/docs/vke/Using_IRSA_in_clusters)<br><br>* [Add-on overview](https://docs.byteplus.com/en/docs/vke/Add-on-overview) |
|ALB Ingress |The HTTPS mutual authentication feature is added, which allows you to enable ALB listener mutual authentication during the configuration of the ALB Ingress. This ensures server and client security in HTTPS scenarios. |All |[Configuring mutual authentication on HTTPS listeners for ALB Ingresses](https://docs.byteplus.com/en/docs/vke/Configure_HTTPS_mutual_authentication_for_ALB_Ingress) |
|Instant snapshot availability of EBS |The instant snapshot availability feature of EBS is supported. After this feature is enabled, you do not need to wait for the snapshot creation to complete before using the snapshot to create a cloud disk. |All |[Using EBS snapshots](https://docs.byteplus.com/en/docs/vke/Using-EBS-volume-snapshots) |


<span id="HNbmWxJq"></span>
## September 2025


|**Feature name** |**Description** |**Region** |**Related documentation** |
|---|---|---|---|
|Full release of Kubernetes v1.30 |Kubernetes v1.30 released by VKE has ended public beta and is officially fully released, which keeps pace with the native community. |All |[Release notes of VKE based on Kubernetes v1.30](https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v1_30) |
|ALB Ingress |When configuring ALB Ingress through the console or YAML, you can configure WAF protection and access log delivery for ALB instances, as well as access control (ACL) and personalization configuration of listeners. |All |* [Creating an ALB Ingress through the console](https://docs.byteplus.com/en/docs/vke/Creating-an-ALB-Ingress-in-the-console)<br><br>* [Creating an ALB Ingress through kubectl](https://docs.byteplus.com/en/docs/vke/Creating-an-ALB-Ingress-using-kubectl) |
|Access static PersistentVolume through the FSX client |TOS and PFS storage allow access to static PersistentVolumes through the FSX client. Unlike the method of directly using native storage, the FSX client provides high\-performance capabilities with better applicability, providing greater flexibility and improved compatibility. |All |* [Accessing static TOS PersistentVolume through the FSX client](https://docs.byteplus.com/en/docs/vke/Using_static_TOS_Volumes_through_the_FSX_client)<br><br>* [Accessing static PFS PersistentVolume through the FSX client](https://docs.byteplus.com/en/docs/vke/Using_static_PFS_Volumes_through_FSX_client) |
|Node pool supports RDMA communication mode |[[Beta · Apply for Trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] RDMA is now available as a new network communication mode for node pools, allowing nodes to exchange data based on RDMA. This enables faster data transmission and improved communication efficiency, which is applicable to applications that require large\-scale data transfer and high\-performance network communication. |All |* [Creating a node pool](https://docs.byteplus.com/en/docs/vke/Creating-a-NodePool)<br><br>* [Creating a managed node pool](https://docs.byteplus.com/en/docs/vke/Creating-a-managed-NodePool) |
|Optimizing multi\-card sharing configuration |When using mGPU multi\-card sharing, the number of GPU cards is configured based on container names instead of containers themselves. This can eliminate the issue that the number of GPU cards needs to be modified frequently because the number of containers in pods keeps changing. |All |[mGPU multi-GPU sharing](https://docs.byteplus.com/en/docs/vke/Multiple-GPU-sharing) |
|PersistentVolume backup and restoration |Backup Center now supports PersistentVolumes backup and recovery. CSI snapshots can be backed up to TOS and used for restoration in a specified cluster with one click. |All |[Creating backup plans](https://docs.byteplus.com/en/docs/vke/Create_backup_plan) |
|AI profiling |The AI profiling feature is added for the observability feature of VKE. When you deploy LLMs in a VKE cluster, you can analyze the AI profiling results of specified containers. This facilitates detection and optimization throughout the LLM life cycle, including training, inference, and optimization. |All |[AI profiling](https://docs.byteplus.com/en/docs/vke/AI_Profiling) |
|Pod event |VKE clusters can be integrated with TLS, which provides event persistence capabilities and supports the generation of charts that record pod events based on log indexes. The charts help you view the events of a specified pod. |All |[Configuring and viewing persistent events](https://docs.byteplus.com/en/docs/vke/Configuring-and-viewing-persistent-events) |
|RDMA resource allocation mode |[[Beta · Apply for Trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] When you use RDMA resources in RoCE high\-performance computing clusters, the shared\-host mode is added. This mode allows all RDMA NICs on a host to be inserted into containers as IPVLAN sub\-interfaces. These NICs are then available for pods within the container cluster. |All |[Using RDMA resources (RoCE) in VKE clusters](https://docs.byteplus.com/en/docs/vke/Using-RDMA-resources-in-VKE-clusters) |
|Registered clusters supporting cloud\-native observability |[[Beta · Apply for Trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] The high\-availability collector deployed in the registered cluster provides basic observability capabilities by using VMP. |All |[Observability of registered clusters](https://docs.byteplus.com/en/docs/vke/Enable_observation) |


<span id="uLLGBCLv"></span>
## August 2025


|**Feature name** |**Description** |**Region** |**Related documentation** |
|---|---|---|---|
|Optimized upgrade checks |Optimized the check process for cluster upgrade, allowing performing checks for both control plane and node upgrade simultaneously. Optimized the upgrade report content, making it easier for users to quickly address anomalies and complete the upgrade process for clusters. |All |* [Upgrading clusters](https://docs.byteplus.com/en/docs/vke/Upgrading-a-cluster)<br><br>* [Cluster upgrade checks](https://docs.byteplus.com/en/docs/vke/Cluster_upgrade_checks)<br><br>* [Best practices of cluster upgrade](https://docs.byteplus.com/en/docs/vke/Cluster-upgrade-best-practices) |
|Allows custom containerd configurations |Node pools support custom containerd configuration, which includes the Container Registry proxy address for container images and disabling self\-signed certificate verification. This can meet the custom requirements of user business. |All |* [Configuring containerd for node pools](https://docs.byteplus.com/en/docs/vke/Configuring_containerd_for_node_pools)<br><br>* [Creating a cluster.](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster)<br><br>* [Creating a node pool](https://docs.byteplus.com/en/docs/vke/Creating-a-NodePool)<br><br>* [Creating a managed node pool](https://docs.byteplus.com/en/docs/vke/Creating-a-managed-NodePool) |
|RBAC allows cluster\-level permissions under an account |Grant RBAC permissions at the **cluster level under your account** to IAM users or roles. These users or roles can access all existing clusters and any future clusters created under your root user. |All |[Granting RBAC permissions](https://docs.byteplus.com/en/docs/vke/Configuring-RBAC-permissions) |
|Compatible with veLinux 2.0 and Ubuntu 22.04 series images at public beta stage |[Public beta] Vital Kubernetes Engine now supports veLinux 2.0 and Ubuntu 22.04 series images. All CPU instance families, including General\-purpose, Compute\-optimized, and Memory\-optimized, can work with these images. |All |[Overview of operating system (OS) images](https://docs.byteplus.com/en/docs/vke/Overview-of-operating-system-images) |
|Backup center |[Public beta] The Vital Kubernetes Engine (VKE) has newly added a Backup center. It can back up container application metadata to TOS and restore backup data to the specified cluster with one click. This feature meets the needs of scenarios including container business disaster recovery, IDC\-hosted cloud applications, and cross\-cloud application migration. |* China (Beijing)<br><br>* Asia Pacific (Johor) |[Backup center overview](https://docs.byteplus.com/en/docs/vke/Backup_center_overview) |


<span id="3iMt1YIi"></span>
## July 2025


|**Feature name** |**Description** |**Region** |**Related documentation** |
|---|---|---|---|
|The node pool supports selecting multiple specifications |When you are creating or updating node pools, this feature allows you to select multiple computing specifications, thus improving the success rate of scaling. |All |* [Creating a node pool](https://docs.byteplus.com/en/docs/vke/Creating-a-NodePool)<br><br>* [Creating a managed node pool](https://docs.byteplus.com/en/docs/vke/Creating-a-managed-NodePool) |
|Instant node elasticity (Karpenter) |This feature supports the instant autoscaler of Karpenter\-based nodes, achieving the autoscaler feature of multiple specifications. |All |* [Cluster autoscaler overview](https://docs.byteplus.com/en/docs/vke/How-Cluster-Autoscaler-works)<br><br>* [Configuring the instant elasticity of nodes (Karpenter)](https://docs.byteplus.com/en/docs/vke/Configure_node_instant_autoscaler_Karpenter) |
|kubelet parameters of nodes |Supports new kubelet parameters for customizing nodes such as `max-pods` and `cpu-manager-policy`. |All |[Configuring kubelet parameters for nodes](https://docs.byteplus.com/en/docs/vke/Configuring-kubelet-parameters-for-a-NodePool) |
|The Kubernetes version 1.30 clusters support NUMA and RDMA |Kubernetes version 1.30 clusters support NUMA\-aware scheduling and RDMA topology\-aware scheduling. This feature perfects the capabilities of Kubernetes version 1.30 and enhances user experience. |All |* [NUMA-aware scheduling](https://docs.byteplus.com/en/docs/vke/NUMA-aware-scheduling)<br><br>* [RDMA topology-aware scheduling](https://docs.byteplus.com/en/docs/vke/RDMA-topology-aware-scheduling) |
|veLinux 2.0 images are now supported for node operating systems |[**Beta·Apply for Trial**] For clusters running Kubernetes v1.30 and later, new nodes can use veLinux 2.0 images and veLinux 2.0 CentOS\-compatible images. These newer veLinux images provide compatibility with more upstream Kubernetes ecosystem capabilities. |All |[Overview of operating system (OS) images](https://docs.byteplus.com/en/docs/vke/Overview-of-operating-system-images) |


<span id="XgOQUers"></span>
## May 2025


|**Feature name** |**Description** |**Region** |**Related documentation** |
|---|---|---|---|
|Custom node names are allowed in node pools |Custom node names and increment expressions are allowed in node pools. The node metadata can be named with the `hostname`. Interactive guidance is available on the console page to help configure node names, hostnames, and metadata. It provides a better experience in the configurations of nodes. |All |* [Creating a cluster.](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster)<br><br>* [Creating a node pool](https://docs.byteplus.com/en/docs/vke/Creating-a-NodePool)<br><br>* [Creating a managed node pool](https://docs.byteplus.com/en/docs/vke/Creating-a-managed-NodePool) |
|Monitoring Center now supports observability for registered clusters |Registered clusters can now integrate with cloud\-native observability to provide cluster resource observability, improving the observability capabilities of registered clusters. |All |No |
|IRSA officially online |IRSA (IAM Roles for Service Accounts), based on Identity and Access Management (IAM), is released in VKE, allowing access control at pod\-level in multi\-tenant scenarios. |All |[IRSA overview](https://docs.byteplus.com/en/docs/vke/IRSA-overview) |
|Specified data volumes allowed to be mounted when adding existing nodes to a custom node pool |Verification is no longer required when adding existing nodes to a custom node pool. Data volumes can be mounted by using device names. It facilitates resource migration and allocation with high efficiency by eliminating the concern of data volume size. |All |[Managing node pools](https://docs.byteplus.com/en/docs/vke/Managing-NodePools#.5re75Yqg5bey5pyJ6IqC54K5) |
|Diagnosis of failures when scaling out a node pool is now officially released. |Diagnosis of failures when scaling out a node pool is now available. It provides abundant diagnosis scenarios to help clients increase maintenance efficiency. |All |[Scaling out/in node pools](https://docs.byteplus.com/en/docs/vke/Scaling-a-NodePool) |
|Node resource reservation on the console page |Reservation of resources such as CPUs and memory for nodes can be configured on the console page, increasing resource management efficiency. |All |[Configuring kubelet parameters for nodes](https://docs.byteplus.com/en/docs/vke/Configuring-kubelet-parameters-for-a-NodePool) |
|User\-defined domain names are allowed when issuing KubeConfig |User\-defined domain names are allowed when issuing KubeConfig, which facilitates cross\-cloud access and provides strong security. |All |[Creating a cluster.](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster) |


<span id="qUX7CEgG"></span>
## April 2025


|**Feature name** |**Description** |**Region** |**Related documentation** |
|---|---|---|---|
|Enhanced node checking and self\-healing |The node checking and self\-healing feature can detect typical ECS failures and activate related protocols (e.g., cold migration). It encapsulates troubleshooting policies based on failure types and intervenes with auto\-fix protocols. |All |[Node check and self-healing](https://docs.byteplus.com/en/docs/vke/NodePool-health-check-and-auto-repair) |
|Ubuntu 22.04 operating system supported |[ [Beta · Apply for Trial ](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] Ubuntu 22.04 operating system is supported now in clusters based on Kubernetes v1.30 and above, with cgroupv2 to implement isolation of container resources. This feature brings a new version of the operating system to the image family supported by VKE. |All |[Overview of operating system (OS) images](https://docs.byteplus.com/en/docs/vke/Overview-of-operating-system-images) |


<span id="hqfkzaNT"></span>
## March 2025


|**Feature name** |**Description** |**Region** |**Related documentation** |
|---|---|---|---|
|ALB Ingress allows native certificates in Secret  |[ [Beta · Apply for Trial ](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] certificate information can be configured directly in Secret. The ALB Controller in the Certificate Center will create a certificate according to that information and then bind the certificate ID on the ALB side. It simplifies certificate configurations. |All |[Enabling HTTPS for ALB Ingress](https://docs.byteplus.com/en/docs/vke/ALB_Ingress_configuring_the_HTTPS_protocol) |
|Multiple listening ports on an ALB Ingress |[ [Beta · Apply for Trial ](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] A single ALB Ingress allows multiple listening ports, which reduces the number of Ingress and management cost. |All |[Configuring ALB Ingress using annotation](https://docs.byteplus.com/en/docs/vke/Configuring-an-ALB-Ingress-using-annotations) |
|Optimized layout for container commands on the console |It provides a better layout for typing container commands on the console page for deployment, allowing each command to be put in a separate textbox and ensuring bash commands can be parsed correctly. |All |[Workload](https://docs.byteplus.com/en/docs/vke/Workloads) |
|Service with support for 7\-layer CLB |The service can work with 7\-layer CLBs and HTTPS listeners. Additionally, it can automatically create and maintain the back\-end server groups to which the listeners are attached. It satisfies the scenarios that need to expose 7\-layer services outside of nginx\-ingress and configure SSL/TLS certificates for 7\-layer web services for secured communication between clients and CLBs. |All |[Configuring CLB services by using annotations](https://docs.byteplus.com/en/docs/vke/Configuring-a-LoadBalancer-Service-using-annotations) |
|Custom ECS hostnames are allowed in node pools. |Custom ECS hostnames are allowed in node pools. It provides a flexible configuration for hostnames. |All |* [Creating a cluster.](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster)<br><br>* [Creating a node pool](https://docs.byteplus.com/en/docs/vke/Creating-a-NodePool)<br><br>* [Creating a managed node pool](https://docs.byteplus.com/en/docs/vke/Creating-a-managed-NodePool) |
|CR password\-free add\-on applicable to repositories in multiple regions |The password\-free add\-on (cr\-credential\-controller) is applicable to Container Registry (CR) in multiple regions. It meets the needs for cross\-region use of the password\-free add\-on. |All |* [Using password-free add-on to pull private images to create workloads](https://docs.byteplus.com/en/docs/vke/Pulling-private-images-to-create-workloads-by-using-cr-credential-controller)<br><br>* [cr-credential-controller](https://docs.byteplus.com/en/docs/vke/cr-credential-controller)<br><br>* [Installing add-on](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on#.Y3ItY3JlZGVudGlhbC1jb250cm9sbGVyLee7hOS7tg==) |
|Tags allowed to be added when creating LoadBalancer services |User tags can be added to the annotations of the LoadBalancer service by CCM (Cloud Controller Manager) of the VKE when creating that service. It expands the capabilities of the LoadBalancer service. |All |[Configuring CLB services by using annotations](https://docs.byteplus.com/en/docs/vke/Configuring-a-LoadBalancer-Service-using-annotations) |
|ACL is available at the access endpoint of APIServer for registered clusters |ACL is available at the access endpoint of APIServer for registered clusters, providing a higher security level for registered cluster access and permission control. |All |[Registration of existing clusters through proxy](https://docs.byteplus.com/en/docs/vke/Register_the_cluster_by_proxy) |


<span id="9r2g3yDM"></span>
## February 2025


|**Feature name** |**Description** |**Region** |**Related documentation** |
|---|---|---|---|
|CLB Ingress allows certificates in Certificate Center |CLB Ingress can work with the certificates in the Certificate Center with the current BytePlus root user. It expands the scope of certificates that CLB Ingress can work with and meets the needs in more scenarios. |All |[Certificate management](https://docs.byteplus.com/en/docs/vke/Configuring-HTTPS-for-a-CLB-Ingress#.6K-B5Lmm566h55CG) |
|Creating data volumes using snapshots |The feature of creating data volumes using snapshots now goes online officially. It realizes quick start of nodes from snapshots, providing a higher efficiency. |All |[Creating node pools](https://docs.byteplus.com/en/docs/vke/Creating-a-NodePool) |
|Batch deletion of Pods |Batch deletion of pods from the pod list on the console page is allowed, increasing resource management efficiency. |All |[Managing pods](https://docs.byteplus.com/en/docs/vke/Managing-pods) |
|An allowlist of public IPs is supported for login to pods through terminals. |[Public beta] An allowlist of public IPs is supported for login to pods through terminals, providing more specific security control for terminal login.  |All |[Access control based on IAM for the VKE console](https://docs.byteplus.com/en/docs/vke/Access_control_based_on_IAM_for_VKE_console) |
|Optimized interaction when creating clusters |It provides default values, tips and guidance when creating clusters on the console page, delivering a better experience. |All |[Creating a cluster.](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster) |
|IPVS is supported for clusters that use the VPC\-CNI network model  |[ [Beta · Apply for Trial ](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] You can specify a PVS LoadBalancer when creating a cluster with the VPC\-CNI network model. In autoscaling scenarios, the least\-connections algorithm helps direct new connections to newly scaled\-out pods whenever possible. |All |[Creating a cluster.](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster) |
|Taint configuration available for node pool autoscaler |Two taint parameters for node pool autoscaler (CA) are available to meet various scheduling requirements in scale\-out scenarios:<br><br><br>* Startup taint: if a node has this taint, the node is considered not yet initialized.<br><br>* Ignore taint: the taint scheduling attribute of a node or node pool will be ignored during scaling out. |All |[Creating a cluster autoscaler](https://docs.byteplus.com/en/docs/vke/Creating-a-Cluster-Autoscaler) |
|TSSD TL0 cloud disk for container storage |TSSD TL0 cloud disk is available for container storage to meet the needs for more cloud storage scenarios. |All |* [Using static PersistentVolume of cloud disks](https://docs.byteplus.com/en/docs/vke/Using-static-EBS-Volumes)<br><br>* [Using dynamic PersistentVolume of cloud disks](https://docs.byteplus.com/en/docs/vke/Using-static-EBS-Volumes) |
|Optimization of the Deployment list page |The deployment list page is optimized in terms of display and the search tool, allowing sorting by creation date and filtering by label. It provides a better experience on the console page. |All |[Deployments](https://docs.byteplus.com/en/docs/vke/Deployments) |
|Console configuration load\-aware scheduling parameter |[ [Beta · Apply for Trial ](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] Load\-aware scheduling can be configured on the console page with parameters such as usage threshold and scoring weight. It provides a better experience and higher efficiency during configuration. |All |* [Load-aware scheduling](https://docs.byteplus.com/en/docs/vke/Load-aware-scheduling)<br><br>* [Scheduler-plugin add-on](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on#.c2NoZWR1bGVyLXBsdWdpbi3nu4Tku7Y=) |
|Supports Kruise add\-on |[ [Beta · Apply for Trial ](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] A Kruise add\-on built based on OpenKruise is available in the Add\-on Center, allowing automatic deployment, release, and maintenance of native cloud applications. It meets the requirements for enhanced add\-on management capabilities for workloads. |All |* [kruise](https://docs.byteplus.com/en/docs/vke/kruise)<br><br>* [Add-on overview](https://docs.byteplus.com/en/docs/vke/Add-on-overview)<br><br>* [Installing add-ons](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on#.a3J1aXNlLee7hOS7tg==) |
|Cluster with shared VPC |[ [Beta · Apply for Trial ](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] Clusters can be created based on shared VPC. It allows a single account to manage network resources and meets the requirements of communication and isolation between business networks. |All |[Using a shared VPC to create clusters](https://docs.byteplus.com/en/docs/vke/Using_a_shared_VPC_to_create_clusters) |
|Capability of working with KEDA add\-on |The KEDA add\-on is available in the add\-on hub, providing an autoscaler driven by Kubernetes events to enhance the capability of elastic scaling. |All |* [Add-on overview](https://docs.byteplus.com/en/docs/vke/Add-on-overview)<br><br>* [keda](https://docs.byteplus.com/en/docs/vke/keda) |
|Online/offline hybrid deployment with mGPU |[ [Beta · Apply for Trial ](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] mGPU allows hybrid deployment of online and offline services based on the same GPU card, increasing utilization of GPU resources. |All |[Using mGPU to implement online-offline hybrid deployment](https://docs.byteplus.com/en/docs/vke/Using_mGPU_for_online-offline_hybrid_deployment) |
|Public beta based on Kubernetes v1.30 version |[Public beta] Vital Kubernetes Engine based on Kubernetes v1.30 is available at public beta stage. |All |[Release notes of VKE based on Kubernetes v1.30](https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v1_30) |
|Deployment set for node pool |ECS instances for nodes in node pools can be deployed using the deployment set. The deployment set is a policy that controls distributed ECS at the hardware layer and provides secure physical isolation, ensuring underlying fault tolerance and high availability.  |All |* [Creating a cluster.](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster)<br><br>* [Creating a node pool](https://docs.byteplus.com/en/docs/vke/Creating-a-NodePool)<br><br>* [Creating a managed node pool](https://docs.byteplus.com/en/docs/vke/Creating-a-managed-NodePool) |

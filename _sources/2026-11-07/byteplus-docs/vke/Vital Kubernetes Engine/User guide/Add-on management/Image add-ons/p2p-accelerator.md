---
title: "p2p-accelerator"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/p2p-accelerator-add-on"
---

p2p\-accelerator is a P2P\-based image acceleration add\-on designed to reduce the time required to pull large container images in large\-scale clusters or high\-concurrency scenarios. This topic describes the functionality, core resources, and installation and upgrade instructions of this add\-on.

<span id="waFjJnO9"></span>
## Add\-on overview

p2p\-accelerator is an image acceleration and distribution proxy add\-on provided by VKE. It distributes downloaded image data chunks across worker nodes over P2P networks. When a large\-scale cluster is scaled out or multiple nodes pull large images concurrently, this add\-on reduces the outbound bandwidth pressure on the central CR service and shortens image pull and application startup times.

After the add\-on is installed in a cluster, the system will create the following Kubernetes resources under the kube\-system namespace.


|Resource name |**Resource type** |**Resource description** |
|---|---|---|
|p2p\-accelerator\-scheduler |StatefulSet |The Dragonfly Scheduler add\-on schedules an optimal set of parent nodes for download nodes. |
|p2p\-accelerator\-dfdaemon\-controller |Deployment |A cluster\-side component for service discovery and configuration control. It monitors changes to dfdaemon Pods and nodes and maintains Endpoints, ConfigMaps, and PrivateZone DNS resolution records in some scenarios. |
|p2p\-accelerator\-dfdaemon\-proxy |StatefulSet |The Dragonfly Seed Peer component provides a centralized dfdaemon access entry and cache service for Nydus scenarios. In some deployment modes, it also acts as a Seed Peer, fetching data from the origin and providing it to other Peers. |
|p2p\-accelerator\-dfdaemon |DaemonSet |The Dragonfly Peer component is deployed on nodes to provide the P2P download client and proxy service. It handles image layer download requests from the container runtime. |
|p2p\-accelerator\-watcher |DaemonSet |A node\-side configuration listener component. It monitors ConfigMaps and updates the node\-side runtime configuration as appropriate. |
|p2p\-accelerator\-preheat\-controller |Deployment |The preheat task control component. It orchestrates preheat tasks, scores and selects target nodes, and distributes tasks to the preheat\-agent on the corresponding nodes. |
|p2p\-accelerator\-preheat\-agent |DaemonSet |The execution component deployed on target preheat nodes. It runs preheat tasks and pulls images to nodes in advance. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The preceding table only lists the main resources of the add\-on, as well as resources that may be used when the add\-on or the corresponding feature is configured. This helps you understand the main components of this add\-on. Other resources, such as ConfigMap and Secret, related to the add\-on are not described here. You should refer to the actual resources in the cluster.</div>


<span id="ox7ZrV6C"></span>
## Add\-on versions

For information about the historical release records of the add\-on, as well as new features and optimization descriptions for each version, see [Add-on release records](https://docs.byteplus.com/en/docs/vke/p2p-accelerator).

<span id="uiLfFmR8"></span>
## Install the add\-on


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. Click the name of the target cluster to go to the management page of this cluster.

3. In the left navigation pane, choose **Image acceleration** to open the image acceleration configuration page.

4. In the add\-on installation section of the image acceleration configuration page, click **Install** to install the add\-on and configure its parameters.

   
   |Parameter |Subparameter |Description |
   |---|---|---|
   |CR Standard Edition instance ||Select a CR Enterprise Standard Edition instance with P2P acceleration enabled. |
   |Image lazy loading ||Specify whether to enable P2P\-accelerated origin fetching for Nydus image lazy loading.<br><br><br>* Enabled: Nydus fetches data from the origin through P2P Seed Peers. This applies to large\-scale scale\-out scenarios or situations where multiple nodes pull the same image at the same time. This solution reduces the back\-to\-origin request pressure on CR.<br><br>* Disabled: Nydus fetches data directly from CR.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This configuration provides P2P\-accelerated origin fetching only for the image lazy loading feature. When you enable this feature, ensure the following conditions are met so that image lazy loading can function properly.</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The image\-accelerator add\-on is installed in the cluster. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Container-image-lazy-loading-solution?lang=en">Lazy loading of container images</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Lazy loading is enabled for the CR instance. For details, see <a href="https://docs.byteplus.com/en/docs/cr/create-image-lazy-loading-conversion-rules?lang=en">Creating rules for conversion to lazy\-loaded images</a>.</div><br> |
   |Pod scheduling based on taints and tolerations ||After it is enabled, you can configure taint tolerations, allowing the core workloads of the add\-on to be scheduled to nodes with the specified taints. |
   |Node Label Selector ||After you enable this feature, you can specify node labels, and the core workloads of the add\-on will be scheduled onto nodes with the specified labels. |
   |VCI deployment (extended) ||After you enable this feature, you can deploy the add\-on on VCI.<br><br><br>* **Deployment method**: Select the deployment method for the add\-on on VCI. The default value is **Custom StatefulSet deployment** and cannot be modified.<br><br>* **Number of instances**: Specify the number of add\-on instances. |
   |**Advanced settings** |||
   |Scheduler |Number of instances |The number of Scheduler replicas. The system uses an anti\-affinity deployment policy to prevent a single point of failure from affecting image pull scheduling across the cluster.<br><br><br>* When the cluster has many nodes or image pull concurrency is high, increase the number of replicas appropriately to improve scheduling throughput.<br><br>* Reducing the number of replicas lowers the high availability level of the Scheduler. |
   ||Pod scheduling based on taints and tolerations |Configure the taint toleration rules for the Scheduler.<br><br><br>* After this feature is enabled, you can configure taint toleration rules for the core workloads of the add\-on, allowing them to be scheduled to nodes with specified taints.<br><br>* When this feature is disabled, the core workloads cannot be scheduled to nodes with NoSchedule or NoExecute taints. |
   ||Node forced scheduling |Configure the node label matching rules that the Scheduler must satisfy. After this feature is enabled, you can set node label selection conditions. The core workloads of the add\-on are scheduled only to nodes that satisfy all specified labels. If no node in the cluster meets the conditions, the core workloads cannot be scheduled. |
   ||Node priority scheduling |Configure the node labels and weights preferred by the Scheduler. After this feature is enabled, you can set node label selection conditions and priority weights. The core workloads of the add\-on are scheduled preferentially to nodes that match the specified labels and have higher weights. If no node meets the conditions, the workloads can still be scheduled to nodes that meet other conditions. |
   ||Resource configuration |* CPU: The CPU request and limit for the Scheduler component. When the cluster has many nodes, many concurrent image pulls, or preheat tasks, increase this value appropriately to prevent slow processing of scheduling requests or task queuing caused by insufficient CPU resources.<br><br>* Memory: The memory limit for the Scheduler component. When the cluster is large or when many download events and scheduling requests are processed at the same time, increase this value appropriately. This prevents the component from restarting unexpectedly due to insufficient memory, which would affect the scheduling of image data sources. |
   |Seed Peer |Number of instances |The number of Seed Peer replicas. The system uses an anti\-affinity deployment policy to ensure that cache data sources remain available even when some nodes are unavailable.<br><br><br>* When image pull concurrency in the cluster stays high and Seed Peer origin traffic becomes a bottleneck, increase the number of replicas appropriately to distribute the origin\-fetching pressure.<br><br>* Reducing the number of replicas lowers cache data availability. In extreme cases, it may increase traffic from direct CR access. |
   ||Pod scheduling based on taints and tolerations |Configure the taint toleration rules for the Seed Peer.<br><br><br>* After this feature is enabled, you can configure taint toleration rules for the core workloads of the add\-on, allowing them to be scheduled to nodes with specified taints.<br><br>* When this feature is disabled, the core workloads cannot be scheduled to nodes with NoSchedule or NoExecute taints. |
   ||Node forced scheduling |Configure the node label matching rules that the Seed Peer must satisfy. After this feature is enabled, you can set node label selection conditions. The core workloads of the add\-on are scheduled only to nodes that satisfy all specified labels. If no node in the cluster meets the conditions, the core workloads cannot be scheduled. |
   ||Node priority scheduling |Configure the node labels and weights preferred by the Seed Peer. After this feature is enabled, you can set node label selection conditions and priority weights. The core workloads of the add\-on are scheduled preferentially to nodes that match the specified labels and have higher weights. If no node meets the conditions, the workloads can still be scheduled to nodes that meet other conditions. |
   ||StorageClass |The storage type used by the Seed Peer to persistently cache image data. The Seed Peer caches the original image data pulled from CR to a local persistent volume for reuse by other nodes in the cluster, avoiding repeated back\-to\-origin pulls.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">We recommend selecting a StorageClass with high I/O performance, such as a local volume or an EBS volume. This improves the read and write speeds of cached data and reduces image distribution latency.</div><br> |
   ||Capacity |The maximum capacity of the persistent storage volume for the Seed Peer. The default is 512 GiB. This capacity determines the total amount of image data that the Seed Peer can cache. When the cluster involves many image types or large images, increase this value appropriately. This prevents frequent eviction of cached data and increased origin pulls caused by insufficient cache space. |
   ||Resource configuration |* CPU: The CPU request and limit for the Seed Peer component. When the cluster has many concurrent image pulls, segmented requests, or prefetch requests, increase this value appropriately. This prevents slow cache data processing, origin pulls, or data distribution caused by insufficient CPU resources.<br><br>* Memory: The memory limit for the Seed Peer component. When the Seed Peer must process many cache read/write, origin pull, or data distribution requests at the same time, increase this value appropriately. This prevents the component from restarting unexpectedly due to insufficient memory, which would affect the reuse of the image cache and the efficiency of origin pulls in the cluster. |
   ||Retain cache |Specify whether to retain existing cache data after the Seed Peer restarts.<br><br><br>* Enabled: After the Seed Peer restarts, it continues to use the cached image data without affecting image pulls by other nodes.<br><br>* Disabled: When the Seed Peer restarts, its cache is lost, but image data can still be obtained from the cache of other Peer nodes in the cluster. An origin pull from CR is triggered only when none of the nodes have cached data. We recommend using this option only when you must forcibly clear the Seed Peer cache. |
   ||Cache Time\-To\-Live |The expiration time of the Seed Peer cache. Cache data that is not accessed within this period is marked as reclaimable.<br><br><br>* When images are updated infrequently, or you want to retain cached data for a long time to reduce origin traffic, increase this value appropriately.<br><br>* When disk space is tight, decrease this value to speed up old cache cleanup. |
   ||Disk usage high watermark |The high disk usage threshold, in percentage. When disk usage reaches this threshold, cache reclamation is triggered to clear data until usage drops below the low watermark.<br><br><br>* When disk capacity is small or the cache grows quickly, lower this value appropriately to trigger cache reclamation early and prevent disk space exhaustion.<br><br>* Increasing this value retains more cached data but risks exhausting disk space. |
   ||Disk usage low watermark |The low disk usage threshold, in percentage. After reclamation is triggered, the system keeps clearing the cache until disk usage drops below this threshold. A lower value causes more data to be reclaimed in each cleanup cycle, which reduces reclamation frequency but deletes more potentially valid cache. Keep a reasonable gap from the high threshold to avoid frequent small\-scale reclamation. |
   |Peer |HostPath |The mount path of the Peer on the node. It is fixed to `/mnt/p2pcache` and cannot be modified. |
   ||Resource configuration |* CPU: The CPU request and limit for the Peer component. When many containers on a node pull images concurrently, or cached image data must be provided to other nodes at the same time, increase this value appropriately to prevent slow image data processing and transmission caused by insufficient CPU resources.<br><br>* Memory: The memory limit for the Peer component. When multiple image pull requests occur on a node at the same time, or a large amount of data needs to be transmitted concurrently, increase this value appropriately. This prevents the Peer from restarting unexpectedly or image pulls from being interrupted due to insufficient memory. |
   ||Retain cache |Specify whether to retain cache data on the node after the Peer restarts.<br><br><br>* Enabled: After the Peer restarts, it continues to use the cached image data without affecting normal pulls on the node.<br><br>* Disabled: When the Peer restarts, its cache is lost, but image data can still be obtained from the Seed Peer or the cache of other Peer nodes in the cluster. An origin pull from CR is triggered only when none of the nodes have cached data. We recommend using this option only when you must forcibly clear the cache on the node. |
   ||Cache Time\-To\-Live |The expiration time of the Peer cache. Cache data that is not accessed within this period is marked as reclaimable.<br><br><br>* When images are updated infrequently or node disk space is sufficient, increase this value to extend the retention time of the local node cache and reduce repeated pulls from the Seed Peer or CR.<br><br>* When node disk space is tight, decrease this value to speed up old cache cleanup. |
   ||Disk usage high watermark |The high threshold for cache disks on nodes, in percentage. When disk usage reaches this threshold, cache reclamation is triggered to clear data until usage drops below the low watermark. This configuration takes effect on each node. Changes affect the cache reclamation behavior of all Peers in the cluster.<br><br><br>* When the node cache disk capacity is small, lower this value appropriately to trigger cache reclamation early and prevent disk space exhaustion.<br><br>* Increasing this value retains more cached data but risks exhausting disk space. |
   ||Disk usage low watermark |The low threshold for cache disks on nodes, in percentage. After reclamation is triggered, the system keeps clearing the cache until disk usage drops below this threshold. A lower value causes more data to be reclaimed in each cleanup cycle, which reduces reclamation trigger frequency but deletes more potentially valid cache. Keep a reasonable gap from the high threshold to avoid frequent small\-scale reclamation. |
   |Preheater Controller |Number of instances |The number of Preheat Controller replicas. When the cluster has many preheat tasks or the control add\-on needs higher concurrent processing capability, increase the replica count appropriately. Setting it to 1 reduces the high availability of the control add\-on, and no new preheat tasks can be triggered while the single replica is down. |
   ||Resource configuration |* CPU: The CPU request and limit for the Preheat Controller component. When there are many preheat tasks or preheat tasks are triggered frequently, increase this value appropriately to prevent preheat tasks from queuing or timing out due to insufficient CPU resources.<br><br>* Memory: The memory limit for the Preheat Controller component. When many preheat tasks run at the same time, increase this value appropriately to prevent the Preheat Controller from restarting unexpectedly or tasks from being interrupted due to insufficient memory. |
   |Preheater Agent |Resource configuration |* CPU: The CPU request and limit for the Preheater Agent component. When a node runs multiple preheat tasks concurrently or preheat tasks are triggered frequently, increase this value appropriately to prevent slow image preheating or task timeouts due to insufficient CPU resources.<br><br>* Memory: The memory limit for the Preheater Agent component. When a node runs many preheat tasks concurrently or must process a large volume of image data, increase this value appropriately. This prevents the Preheater Agent component from restarting unexpectedly or preheat tasks from being interrupted due to insufficient memory. |
   

5. Click **Confirm** to finish configuration.


<span id="Wt6W40PZ"></span>
## Upgrade the add\-on

New versions of the add\-on are released at irregular intervals to provide new features or fix known issues. When the add\-on card displays that a new version is available, we recommend upgrading the add\-on promptly. To ensure a smooth service transition, perform the upgrade **during off\-peak hours** whenever possible. For the upgrade procedure and considerations, see [Upgrading the add-on](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

<span id="p3c1982w"></span>
## Monitoring and alerting

<span id="aTiYo23V"></span>
### Add\-on observability

The stability and performance of the p2p\-accelerator add\-on directly affect the functionality and effectiveness of your cluster. We recommend enabling add\-on observability in your cluster to monitor add\-on health in real time. For details, see [Image acceleration observability](https://docs.byteplus.com/en/docs/vke/Image-acceleration-observability?lang=en).

<span id="Iam7eHgn"></span>
### Configuring alerts

VKE provides comprehensive cluster monitoring and alerting capabilities based on [VMP](https://docs.byteplus.com/en/docs/vmp/what-is-vital-managed-service-for-prometheus). You can quickly create alert rule groups by using preset templates or configure custom alert rules by using PromQL statements based on your business requirements. You can also export preset templates in YAML format, adjust the rules, and save them as custom alert templates for reuse across multiple clusters. For details, see the following topics:


* [Configuring alerts through preset templates](https://docs.byteplus.com/en/docs/vke/Configuring_alerts_through_preset_templates?lang=en)

* [Configuring alerts based on custom templates](https://docs.byteplus.com/en/docs/vke/Configuring_alerts_based_on_custom_templates?lang=en)

* [Custom alert rules](https://docs.byteplus.com/en/docs/vke/Configure_custom_alert_rules?lang=en)


Preset alert templates are provided by the system based on common O&M scenarios. They are applicable to building an alert system for the first time or quickly supplementing basic monitoring items. This helps you promptly detect insufficient resources or abnormal operation of add\-ons. For details about the alert rules in preset alert templates, see [Preset alert templates](https://docs.byteplus.com/en/docs/vke/Preset_alert_templates?lang=en).

<span id="93apWNPG"></span>
## Related documentation


* [Overview of P2P acceleration](https://docs.byteplus.com/en/docs/vke/Overview-of-P2P-acceleration?lang=en)

* [Configuring P2P acceleration](https://docs.byteplus.com/en/docs/vke/P2P-acceleration-solution)

* [Reference performance of P2P acceleration](https://docs.byteplus.com/en/docs/vke/P2P_Performance_Testing?lang=en)

* [Image acceleration observability](https://docs.byteplus.com/en/docs/vke/Image-acceleration-observability)

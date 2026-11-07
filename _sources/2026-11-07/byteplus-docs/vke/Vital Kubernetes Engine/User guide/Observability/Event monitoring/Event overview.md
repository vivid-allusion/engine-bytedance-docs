---
title: "Event overview"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Event-monitoring-overview"
---

VKE integrates with **C**[loud Monitor](https://docs.byteplus.com/en/docs/cloudmonitor/What-is-Vitality-Cloud-Monitor)**C**to record and notify you of cluster resource events. When system events are triggered by resources such as clusters, node pools, nodes, or add\-ons, you can promptly view event details and take appropriate actions.

<span id="leXzNuIa"></span>
## Event types

When you use a VKE cluster, the cluster and the resources within it generate event records in certain critical statuses. These events directly affect whether the cluster can function as expected and thus require your special attention.

<span id="njqZdVg9"></span>
### VKE event types

The supported event types and event names in a VKE cluster are shown in the table below.


|Resource type |Event description |Event name |
|---|---|---|
|Cluster |Cluster failed |vke:Cluster:ClusterStatus.Failed |
||Cluster suspended due to account arrears |vke:Cluster:ClusterStatus.Stoped |
|Node pool |Node pool failed |vke:NodePool:NodePoolStatus.Failed |
||Node pool scale\-in failed |vke:NodePool:ScaleDown.Failed |
||Node pool scale\-in started |vke:NodePool:ScaleDown.Start |
||Node pool scale\-in succeeded |vke:NodePool:ScaleDown.Succeeded |
||Node pool scale\-out failed |vke:NodePool:ScaleUp.Failed |
||Node pool scale\-out started |vke:NodePool:ScaleUp.Start |
||Node pool scale\-out succeeded |vke:NodePool:ScaleUp.Succeeded |
||Node pool scaling failed |vke:NodePool:ScalingProcess.Failed |
|Node |Node failed |vke:Node:NodeStatus.Failed |
||Node scale\-in failed |vke:Node:ScaleDown.Failed |
||Node scale\-in started |vke:Node:ScaleDown.Start |
||Node scale\-in succeeded |vke:Node:ScaleDown.Succeeded |
||Node scale\-out failed |vke:Node:ScaleUp.Failed |
||Node scale\-out started |vke:Node:ScaleUp.Start |
||Node scale\-out succeeded |vke:Node:ScaleUp.Succeeded |
|Add\-on |Add\-on failed |vke:Addon:AddonStatus.Failed |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For resource suspension, abnormality, or failure events in a cluster, you can view the reasons for abnormal resource statuses and take action accordingly. If a resource cannot return to its normal status, <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000210">submit a ticket</a> for technical support.</div>


<span id="Nnpt22OL"></span>
### VCI event types

For details of VCI event types, see [Summary of VCI event types](https://docs.byteplus.com/en/docs/vke/VCI-event-types?lang=en).

<span id=".5LqL5Lu254q25oCB"></span>
## Event status

The following table describes the supported event statuses in a VKE cluster.


|Status |Displayed in the console |Attribute |Description |
|---|---|---|---|
|Start |Start |Unstable status |Execution started. |
|Succeeded |Succeeded |Stable status |Execution succeeded. |
|Stoped |Stopped |Stable status |Only the `vke:Cluster:ClusterStatus.Stoped` event has this status, which indicates that the cluster was suspended due to account arrears. |
|Failed |Failed/Abnormal |Stable status |* Resource status changed from a non\-failure one to failure.<br><br>* Execution failed. |


&nbsp;

&nbsp;

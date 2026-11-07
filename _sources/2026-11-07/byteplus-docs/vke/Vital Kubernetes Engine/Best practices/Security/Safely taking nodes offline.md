---
title: "Safely taking nodes offline"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Safely-undeploying-nodes"
---

This topic describes how to safely take nodes offline in a cluster by using the console, Kubectl, and other methods.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

In the daily maintenance of applications running on VKE, it is sometimes necessary to take a specific cluster node offline, for example, for version upgrades, scaling, modifications, maintenance, or node recycling.

VKE supports taking specified nodes in the cluster offline. After a node is offline, all pods on the node, except those managed by DaemonSets, will be evicted to other nodes in the cluster. Newly created pods cannot be scheduled to this node.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Considerations


* Removing a node will cause pod migration, which may impact business. Please perform this operation during off\-peak hours.

* Unexpected risks may arise during the operation. Please back up data in advance.

* Taking nodes offline will reduce the available and schedulable CPU, memory, and other resources in the cluster. If reserved available resources of the cluster are insufficient, it will affect the scheduling of subsequent workloads and the operation of existing workloads.


<span id=".5YmN572u5qOA5p-l"></span>
## Pre\-checks

Before taking a node offline, check its status to ensure that services are not affected by this operation. The main check items are as follows.


|**Check item** |**Check details** |**Solution** |
|---|---|---|
|Whether an ingress\-controller pod is running on the node |Restarting or migrating Ingresses will inevitably disconnect long connections from clients, which may result in 502 requests. |If business interruption is unavoidable, perform the operation during off\-peak hours.<br><br>If the Ingress uses a Service of type LoadBalancer or NodePort for external exposure, ensure that there are Ingress replicas on other nodes besides the node to be taken offline.<br><br>If the Ingress uses HostNetwork for external exposure, first delete the corresponding IP address on the caller side (for example, external load balancer and external gateway). |
|Whether the node has workloads that are strongly bound to it |1. Check the node binding method, for example, label selectors or node names.<br><br>2. Confirm the reason for node binding, for example, allowlisting or resource isolation. |Migrate strongly bound workloads on the node to other nodes and then take the node offline. |
|Whether single\-replica workloads exist on the node |Confirm the reason for using single\-replica deployment (such as concurrency conflicts or resource saving). |If scale\-out is possible, first scale out the service to ensure that available replicas of the service exist on other nodes before taking the node offline.<br><br>If scaling out is not possible, evaluate whether the business loss caused by the node going offline is acceptable. |
|Whether a static pod exists on the node |1. Confirm the reason for using the static pod for deployment.<br><br>2. Confirm whether migration is needed and whether concurrent operation is possible. |Perform an evaluation and respond accordingly. |
|Whether the remaining resources of the cluster are sufficient to handle the workloads on the node to be taken offline. |Query node details via the console, OpenAPI, or kubectl, and view the current resource usage of the node and the remaining resources in the cluster.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If the node to be taken offline has services with many requests, the total cluster resources may be sufficient, but scheduling may fail due to significant resource fragmentation.</div><br> |Perform an evaluation and respond accordingly. |
|Whether the workloads deployed on the node support smooth migration |Smooth service migration includes the following:<br><br>1. The terminated replica no longer accepts new requests and exits after all received requests are processed normally.<br><br>2. The newly started service begins accepting requests only after it is ready. |If the service is exposed externally via a Service, the terminated replica no longer accepts new requests. If the service exposes endpoints directly (that is, end\-to\-end access, such as having an additional service registry and discovery center), the service must proactively remove itself from the list upon receiving the exit signal.<br><br>To ensure proper handling of all received requests, the program must receive and intercept the termination signal SIGTERM (the default termination signal, which can be specified in the Dockerfile). After receiving the signal, the program must ensure that all requests are processed before exiting. The service needs to self\-assess the time required to process all requests and set the `terminationGracePeriodSeconds` parameter of the pod appropriately.<br><br>Ensure that the new service does not accept requests before it is ready. If the service is exposed externally via a Service, configure appropriate program readiness checking. If the service directly exposes endpoints externally (for example, with an additional service registration and discovery center), the service must register itself with the registration center only after it is ready. |


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

After all pre\-checks pass, you can begin taking the node offline. Currently, the cluster supports the following methods for taking nodes offline:


* Using the VKE console.

* Writing kubectl code.


<span id=".6YCa6L-H5a655Zmo5pyN5Yqh6aG16Z2i5pON5L2c6IqC54K55LiL57q_"></span>
### Taking nodes offline via the VKE console


2. Log in to the [VKE console](https://console.byteplus.com/vke). In the left navigation bar, click **Cluster**.

2. Click the target cluster name, and click **Node** in the left navigation bar of the cluster management page.

3. Ensure that the status of the target node is normal and that taking the node offline does not affect your service. Then click **Go offline** in the **Actions** column.

4. In the pop\-up window, click **Confirm** to proceed.

   When a node goes offline, all pods except for those of system components and DaemonSets will enter the **Terminating** state. Check the **List of pods** on the node. After all business pods have been successfully evicted, the node will switch to the **Offline** state and become unschedulable. At this point, the node is offline. You can then perform node operations, such as removing the node or changing its configuration.


<span id=".6YCa6L-HLWt1YmVjdGwt6Ieq6KGM5a6e546w5Luj56CB5LiL57q_6IqC54K5"></span>
### Taking nodes offline by using kubectl code

For details, see the official topic [Safely drain a node](https://kubernetes.io/docs/tasks/administer-cluster/safely-drain-node/).

---
title: "How do I schedule a VCI pod to a specified availability zone?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/How-do-I-schedule-a-VCI-pod-to-a-specified-Availability-Zone"
---

You can schedule a VCI pod to a specified availability zone using two methods:


* Method 1: Use node affinity of the VCI pod to schedule it to a node in the specified availability zone.

   1. Confirm the target availability zone. The label key related to availability zones on a node is `topology.kubernetes.io/zone`. The value of this label is the specific availability zone ID. For the availability zone IDs supported by VCI, see [Regions and availability zones](https://docs.byteplus.com/en/docs/vke/VCI-Regions-and-Availability-Zones).

   2. When creating the VCI pod, use node affinity to schedule the pod to a node with the label `topology.kubernetes.io/zone=<specific availability zone ID>`. For details on node affinity\-based scheduling, see the [official Kubernetes documentation](https://kubernetes.io/docs/tasks/configure-pod-container/assign-pods-nodes-using-node-affinity/).

* Method 2: Specify a subnet in the target availability zone for the VCI pod so that it is scheduled to that availability zone.

   When creating the VCI pod, use the `vke.volcengine.com/preferred-subnet-ids` annotation to specify a subnet in a particular availability zone. This schedules the pod to the specified availability zone. For details, see [Creating instances with specified subnets](https://docs.byteplus.com/en/docs/vke/Creating-an-instance-based-on-specified-subnets).

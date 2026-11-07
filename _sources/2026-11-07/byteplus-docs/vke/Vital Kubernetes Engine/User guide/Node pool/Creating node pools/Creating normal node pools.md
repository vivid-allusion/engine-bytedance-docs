---
title: "Creating normal node pools"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Creating-a-NodePool"
---

This topic describes the characteristics of normal node pools as well as the procedure and parameter configuration for creating a normal node pool. 

<span id="lI0s3g2H"></span>
## Background

A normal node pool refers to a node pool where the managed capability is not enabled during creation. The following table describes the differences between a normal node pool and a managed node pool.


|Comparison dimension |Normal node pool |Managed node pool |
|---|---|---|
|O&M entity |Users perform O&M and management. |The VKE platform performs O&M and management. |
|Check and self\-healing |Not supported. |Supported and enabled by default. It provides recommended self\-healing rules (for CPU/GPU nodes) and custom self\-healing rules, and supports self‑healing for failures such as Kubelet failures, runtime failures, and abnormal GPU status. |
|Node diagnosis |Not supported. |Supports node diagnosis and node pool diagnosis. |
|Default autoscaling behavior |By default, autoscaling is disabled. You can enable it based on your business requirements. |The autoscaling capability is enabled for pay\-as\-you\-go and spot instances by default. |
|Application scenario |Scenarios that require full control over node O&M |Scenarios that require lower O&M cost, automatic failure detection and recovery, and higher resource utilization |
|Other capabilities |The basic configuration is fully custom, and the capabilities for scaling out/in and adding nodes are the same as those of a managed node pool. |The basic configuration is fully custom, and the capabilities for scaling out/in and adding nodes are the same as those of a normal node pool. |


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The target cluster is in the **Running** state.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [VKE console ](https://console.byteplus.com/vke).

2. In the left navigation bar of the VKE console, click **Cluster**.

3. In the cluster list, click the name of the target cluster for which you need to create a node pool.

4. In the left navigation bar of the cluster management page, click **Nodes** \> **Node pool**.

5. Click **Create node pool** above the node pool list.

6. Specify parameters related to the node pool on the  Specify parameters related to the node pool and switch off **Enable managing** on the **Create node pool** page. For descriptions of other parameters, see [Creating managed node pools](https://docs.byteplus.com/en/docs/vke/Creating-a-managed-NodePool).

7. Click **Next: Confirm configuration** in the lower\-right corner of the page to enter the configuration confirmation step.

   * Check whether the configurations meet your expectations. If you need to update the configurations, click **Previous: Node pool configuration** in the lower\-right corner of the page.

   * Check the configuration cost. You can click the help icon next to the cost to view the cost details, including billable items, billing method, quantity, original price, and discounted price.****

8. Carefully read **Vital Kubernetes Engine Specific Terms of Service** and select the checkbox to agree to the terms. Then, click **Confirm** in the lower\-right corner of the page to create the node pool and add the related configurations.

   On the **Node pool** page, if **Running** appears in the Status column for the created node pool, the node pool has been successfully created.


<span id="6ivyXXz6"></span>
## What to do next

After the node pool is created, you can add nodes to it or manage its configurations. For detailed operations, refer to [Managing node pools](https://docs.byteplus.com/en/docs/vke/Managing-NodePools).

<span id="6ivyXXz6"></span>
## Related documentation

[CreateNodePool](https://docs.byteplus.com/en/docs/vke/CreateNodePool)

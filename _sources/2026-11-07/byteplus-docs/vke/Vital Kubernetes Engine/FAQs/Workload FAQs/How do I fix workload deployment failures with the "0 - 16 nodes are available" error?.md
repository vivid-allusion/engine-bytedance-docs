---
title: "How do I fix workload deployment failures with the \"0/16 nodes are available\" error?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/How-do-I-resolve-the-0_16-nodes-are-available-error-when-deploying-a-workload"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Issue description

A workload fails to be deployed in the cluster due to the `0/16 nodes are available` error, which means that the number of available nodes in the cluster is 0.

<span id=".5Y6f5Zug5YiG5p6Q"></span>
## Cause analysis

Possible reasons for workload deployment failure are as follows:


* The existing resources in the cluster do not meet the requirements of the workload. Typical error messages include:

   * `Insufficient CPU`: Indicates that the CPU resource on the node is insufficient.

   * `Insufficient memory`: Indicates that the memory resource on the node is insufficient.

* The node has taints that cannot be tolerated by the workload. The typical error message is `node(s) had taint{}, that the pod did not tolerate`.


<span id=".6Kej5Yaz5pa55qGI"></span>
## Solution

When your workload deployment fails, view the error event to confirm the cause of the failure:


1. If the deployment fails due to insufficient cluster resources, we recommend increasing the available resources by adding nodes to the cluster. For details, see [Adding nodes](https://docs.byteplus.com/en/docs/vke/Adding-nodes). 

2. The deployment fails due to node taints. In this case, you can:

   * Configure the **scheduling policy** of the workload to tolerate the taints. For details, see [Creating Deployments](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment).

   * Modify the existing node pool to remove the taints from the node. For details, see [Modify node pool settings](https://docs.byteplus.com/en/docs/vke/Managing-NodePools#.57yW6L6R6IqC54K55rGg).

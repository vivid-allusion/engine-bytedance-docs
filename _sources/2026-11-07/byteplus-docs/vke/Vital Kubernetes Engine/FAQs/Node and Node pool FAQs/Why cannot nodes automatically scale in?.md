---
title: "Why cannot nodes automatically scale in?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Why-cannot-nodes-be-automatically-removed"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Issue description

After you configure autoscaling for a node pool, nodes in the node pool do not automatically scale in based on the configured rule.

<span id=".5Y6f5Zug5YiG5p6Q"></span>
## Cause analysis

Check whether anti\-affinity is configured for the pods on your nodes. If pods configured with anti\-affinity exist on a node that is about to scale in, the node cannot scale in. If the node scales in, the pods will be in the Pending state.

<span id=".6Kej5Yaz5pa55rOV"></span>
## Solution

Update the anti\-affinity configurations of the workload where the pods reside based on your business requirements. For detailed operations, see [Managing workloads](https://docs.byteplus.com/en/docs/vke/Managing-Deployments).

---
title: "How do I handle add-on scheduling failures?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/What-can-I-do-with-add-on-scheduling-failures"
---

<span id=".6Zeu6aKY5o-P6L-w"></span>
## Issue description

After you install an add\-on in the [VKE console](https://console.byteplus.com/vke), the add\-on remains in the scheduling failed state, as shown in the following figure.

<span id=".5Y6f5Zug5YiG5p6Q"></span>
## Cause analysis

In most cases, add\-on scheduling failures are caused by the following four reasons:


* No available nodes exist in the cluster.

* Available nodes exist in the cluster, but they are in an abnormal status, or the CPU or memory of the nodes is insufficient.

* Available nodes exist in the cluster. The nodes are in a normal status, and sufficient resources exist on the nodes. However, taints exist on the nodes that the add\-on pods cannot tolerate.

* Available nodes exist in the cluster. The nodes are in a normal status, and sufficient resources exist on the nodes. However, these nodes cannot satisfy the affinity scheduling requirements of the add\-on pods.


<span id=".6Kej5Yaz5pa55rOV"></span>
## Solution


* Non\-system managed add\-ons: Troubleshoot the scheduling issue, uninstall the add\-on, and then reinstall it based on the description in [How do I fix a failure in scheduling a pod in the Pending state](https://docs.byteplus.com/en/docs/vke/Pod-in-the-Pending-state_not-successfully-scheduled)?

* System\-managed add\-ons: You cannot independently resolve scheduling failures for this type of add\-on. Contact the technical support of BytePlus, or [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000210) to obtain technical support. 

   Add\-ons with the identifier shown in the following figure are system\-managed add\-ons. You can also obtain the information about system\-managed add\-ons based on the description in [Add-on overview](https://docs.byteplus.com/en/docs/vke/Add-on-overview).

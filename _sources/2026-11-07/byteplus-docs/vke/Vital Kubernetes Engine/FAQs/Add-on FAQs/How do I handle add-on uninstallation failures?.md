---
title: "How do I handle add-on uninstallation failures?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/What-can-I-do-with-add-on-uninstallation-failures"
---

<span id=".6Zeu6aKY5o-P6L-w"></span>
## Issue description

When you uninstall an installed add\-on in the [VKE console](https://console.byteplus.com/vke), the operation fails, as shown in the following figure.

<span id=".6Kej5Yaz5pa55rOV"></span>
## Solution

Try uninstalling the add\-on again. For detailed operations, see [Uninstalling add-ons](https://docs.byteplus.com/en/docs/vke/Uninstalling-an-add-on).


* If the add\-on is uninstalled, the issue is resolved, and no further operation is required.

* After you try uninstalling the add\-on, if resources still exist in the namespace of the add\-on within 5 minutes, the add\-on will enter the **Uninstallation failed** state. In this case, resolve the issue by performing the following steps. The csi\-nas add\-on in the preceding figure is used as an example.

   1. On the management page of the cluster where the add\-on is located, click **Workload** \> **Pod** in the left navigation bar.

   2. Under the **kube\-system** namespace, search for **csi\-nas**, find the resources related to the add\-on, and then manually delete the remaining resources.

      After you delete the remaining resources of the add\-on, the add\-on will automatically enter the Not installed state.

   3. (Optional) If you still cannot uninstall the add\-on by using the preceding solution, [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000210) to  and provide a detailed description of the issue and related information, such as logs, to obtain technical support.

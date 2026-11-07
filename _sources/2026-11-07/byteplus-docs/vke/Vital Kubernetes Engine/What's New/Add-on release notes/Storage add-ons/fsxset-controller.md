---
title: "fsxset-controller"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/fsxset-controller"
---

The fsxset\-controller is a scheduling add\-on used to achieve fine\-grained O&M for the FSX client (fsx\-agent). This topic describes the change history of the fsxset\-controller add\-on.

For more information about add\-ons and how to use them, see [Add-on overview](https://docs.byteplus.com/en/docs/vke/Add-on-overview).

<span id="m61bGXjW"></span>
## June 2026


|**Version** |**Compatibility with Kubernetes version** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v0.1.0 |v1.24 ≤ Cluster version ≤ v1.36 |Maintained |* All FSX client management features of the fsx\-service add\-on have been migrated to this add\-on.<br><br>* Supports environment isolation. Different resources can be configured for the FSX client.<br><br>* Supports hot upgrade of the FSX client based on policies.<br><br>* Allows FSX to use vRDMA NICs for communication. |None |

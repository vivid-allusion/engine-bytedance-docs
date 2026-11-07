---
title: "After a workload is unbound from a Service, why is it still accessible through the Service address?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Can-access-the-workload-through-the-endpoint-provided-by-a-Service"
---

<span id=".6Zeu6aKY5o-P6L-w"></span>
## Issue description


1. In a VKE cluster, a workload is unbound from a Service (Kubernetes Service) in the console, or the associated selector labels of the Service are cleared.

2. Accessing the address of the Service can still reach the previously associated workload.


<span id=".6Zeu6aKY5Y6f5Zug"></span>
## Cause

This issue occurs due to unreasonable design logic in the native Kubernetes EndpointSlice controller. For more information, see the [Community documentation](https://github.com/kubernetes/kubernetes/issues/103576).

<span id=".6Kej5Yaz5pa55rOV"></span>
## Solution


* If you no longer need the Service, delete it. For details, see [Deleting Services](https://docs.byteplus.com/en/docs/vke/Managing-Services).

* To change the association between a Service and a workload, replace the original workload with a new workload directly. For details, see [Updating Services](https://docs.byteplus.com/en/docs/vke/Managing-Services) and [Editing Service YAML files](https://docs.byteplus.com/en/docs/vke/Managing-Services).

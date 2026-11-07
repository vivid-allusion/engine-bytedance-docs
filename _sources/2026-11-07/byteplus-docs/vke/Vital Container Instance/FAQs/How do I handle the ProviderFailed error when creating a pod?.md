---
title: "How do I handle the ProviderFailed error when creating a pod?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/How-do-I-handle-the-ProviderFailed-error-when-creating-a-pod"
---

<span id=".6Zeu6aKY5o-P6L-w"></span>
## Problem description

The **ProviderFailed** error occurs during pod creation: `disk status is not available`.

<span id=".6Kej5Yaz5pa55rOV"></span>
## Solution

When using EBS as the volume (data disk) of the pod, VCI does not support mounting the same volume on multiple pods simultaneously. Check the status of the data volume mounted on the VCI. If the data volume is already mounted on another VCI, you can unmount it first or use another data volume. If the problem persists, [submit a ticket](https://console.byteplus.com/ticket/createTicketV2/?step=2&Service=ecs) to obtain technical support.

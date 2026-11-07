---
title: "How do I handle add-on startup failures?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/What-can-I-do-with-add-on-startup-failures"
---

<span id=".6Zeu6aKY5o-P6L-w"></span>
## Issue description

After you install an add\-on in the [VKE console](https://console.byteplus.com/vke), the add\-on is in the **Abnormal** state with the error message **Addon startup failed**.

<span id=".5Y6f5Zug5YiG5p6Q"></span>
## Cause analysis

An add\-on startup failure indicates that one of the add\-on pods is in the CrashLoopBackOff state. This issue is usually caused by add\-on startup parameter modification or internal defects.

<span id=".6Kej5Yaz5pa55rOV"></span>
## Solution


* If an add\-on enters the Addon startup failed state because you modified its YAML configurations, try restoring the original configurations of the add\-on.

* If you have not modified the add\-on YAML configurations, see [How do I fix a Pod remaining in the CrashLoopBackOff state](https://docs.byteplus.com/en/docs/vke/Pod-in-the-CrashLoopBackOff-state) for troubleshooting.

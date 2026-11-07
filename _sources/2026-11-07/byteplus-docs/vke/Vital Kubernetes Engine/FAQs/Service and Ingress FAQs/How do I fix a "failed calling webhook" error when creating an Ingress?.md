---
title: "How do I fix a \"failed calling webhook\" error when creating an Ingress?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Failed-calling-webhook-error-when-creating-an-Ingress"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Issue description

The "xxx failed calling webhook xxx" error occurs during Ingress creation or addition.

<span id=".5Y6f5Zug5YiG5p6Q"></span>
## Cause analysis

When creating or adding an Ingress, you need to verify the validity of the Ingress by a Service (the default is ingress\-nginx\-controller\-admission). If a problem exists in the validation chain (for example, the Service is deleted or the Ingress controller is deleted), validity verification will fail and the Ingress resource will be rejected.

<span id=".6Kej5Yaz5pa55qGI"></span>
## Solution


* Check if all resources in the Webhook chain (ValidatingWebhookConfiguration \> Service \> Pod) exist and are functioning properly: 

* Confirm that the admission feature of the Ingress Controller pod is enabled and that the pod can be accessed externally.

* If the Ingress Controller has been deleted or the webhook feature is not required, delete the ValidatingWebhookConfiguration resource.

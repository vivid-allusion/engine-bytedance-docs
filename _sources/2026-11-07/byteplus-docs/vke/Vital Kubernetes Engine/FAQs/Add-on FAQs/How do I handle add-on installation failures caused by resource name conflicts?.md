---
title: "How do I handle add-on installation failures caused by resource name conflicts?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/What-can-I-do-with-add-on-installation-failures-that-are-caused-by-resource-name-conflicts"
---

<span id=".6Zeu6aKY5o-P6L-w"></span>
## Issue description

When you install an add\-on in the [VKE console](https://console.byteplus.com/vke), the operation fails, with an error message indicating a conflict with an existing resource name.

<span id=".5Y6f5Zug5YiG5p6Q"></span>
## Cause analysis

In most cases, add\-ons are installed in the **kube\-system** namespace. If a resource with the same name as the add\-on already exists in the namespace, the preceding issue will occur.

<span id=".6Kej5Yaz5pa55rOV"></span>
## Solution

Perform the following steps to resolve this issue:


1. Uninstall the add\-on that fails to install. For detailed operations, see [Uninstalling add-ons](https://docs.byteplus.com/en/docs/vke/Uninstalling-an-add-on).

2. In the namespace where the add\-on will be installed (generally the **kube\-system** namespace), find the resource with the same name as the add\-on. Rename or delete it. For detailed operations, see [Managing namespaces](https://docs.byteplus.com/en/docs/vke/Managing-namespaces).

3. Reinstall the target add\-on. For details, see [Installing add-ons](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on).

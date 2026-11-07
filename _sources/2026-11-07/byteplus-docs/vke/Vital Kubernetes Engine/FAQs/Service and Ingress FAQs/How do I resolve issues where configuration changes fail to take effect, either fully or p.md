---
title: "How do I resolve issues where configuration changes fail to take effect, either fully or partially?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Configuration-changes-do-not-take-effect-or-only-partially-take-effect"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Issue description

After I modify the ConfigMap of ingress\-nginx\-controller or the annotations in the Ingress, the corresponding configuration does not take effect.

<span id=".6Kej5Yaz5pa55qGI"></span>
## Solution


1. Check whether the ConfigMap after the modification is valid.

2. If long connection settings are modified, check whether the connection was established after the configuration change.

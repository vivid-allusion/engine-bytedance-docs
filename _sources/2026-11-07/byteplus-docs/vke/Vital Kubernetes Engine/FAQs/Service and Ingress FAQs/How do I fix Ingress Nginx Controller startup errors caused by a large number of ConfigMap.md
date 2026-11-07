---
title: "How do I fix Ingress Nginx Controller startup errors caused by a large number of ConfigMaps?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Large-numbers-of-business-ConfigMaps-prevent-the-Ingress-Nginx-controller-from-starting"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Issue description

The cluster has a large number of ConfigMaps, which causes the Nginx Ingress add\-on to fail to be created.

<span id=".5Y6f5Zug5YiG5p6Q"></span>
## Cause analysis

By default, the Ingress Nginx Controller listens to all ConfigMaps in a cluster, and when the add\-on starts, it loads all ConfigMap resources into memory. If too many ConfigMaps are created, the add\-on will load an excessive number of resources during startup, resulting in high memory usage and triggering an OOM error.

<span id=".6Kej5Yaz5pa55qGI"></span>
## Solution

Restrict the namespaces that the Ingress Nginx Controller listens to. Modify the startup parameter `--watch-namespace=xxx-system`, where the specified namespace is that of the current controller.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">This solution causes the Ingress Nginx Controller to monitor Ingress resources only in the specified namespace. To use Ingress resources in multiple namespaces, deploy an Ingress Nginx Controller in each namespace and modify the startup parameter so that it listens only to the namespace where the controller is located.</div>

---
title: "How do I fix an Nginx Ingress add-on installation failure?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Failed-to-install-the-ingress-nginx-add-on"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Issue description

The installation of the nginx\-ingress add\-on in the cluster failed. The add\-on remains in the "Creating" state.

The pod corresponding to Nginx Ingress remains in the "Pending" state. Further investigation of the status reveals that the root cause is insufficient resources.

<span id=".5Y6f5Zug5YiG5p6Q"></span>
## Cause analysis

The basic configuration of existing nodes in the cluster is 2C4G, and each node already runs kubelet, kube\-proxy, containerd, and other related programs that consume system resources. As a result, the available resources on each node are less than 2000m, which does not meet the requirements of the nginx\-ingress add\-on and prevents installation.

<span id=".6Kej5Yaz5pa55qGI"></span>
## Solution

Purchase new nodes with resource specifications greater than or equal to 4C8G.

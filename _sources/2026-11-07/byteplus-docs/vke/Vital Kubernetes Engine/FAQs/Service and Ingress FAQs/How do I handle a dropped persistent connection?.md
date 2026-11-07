---
title: "How do I handle a dropped persistent connection?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/a-persistent-connection-is-closed"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Issue description

Services that require a persistent connection (for example, live streaming and online meetings) experience brief connection interruptions.

<span id=".5Y6f5Zug5YiG5p6Q"></span>
## Cause analysis


* The persistent connection is disrupted when Nginx restarts or reloads its configuration.

* During an Nginx Ingress Controller scale\-in, requests may exit before they are fully processed due to a lack of graceful shutdown support.


<span id=".6Kej5Yaz5pa55qGI"></span>
## Solution


* For connection disruptions caused by an Nginx restart or configuration reload, configure worker\-shutdown\-timeout to set the connection timeout for persistent connections after the reload. Modify the ConfigMap of the ingress\-nginx\-controller.

   ```Bash
   kubectl edit configmap -n ingress-nginx ingress-nginx-controller
   ```
   

   ```YAML
   apiVersion: v1
   data:
     disable-access-log: "true"
     enable-multi-accept: "true"
     enable-underscores-in-headers: "true"
     ignore-invalid-headers: "false"
     max-worker-connections: "500000"
     max-worker-open-files: "1000000"
     worker-cpu-affinity: auto
     worker-shutdown-timeout: "240"
   ```
   

* For dropped persistent connections caused by an Nginx Ingress Controller scale\-in, if the client has a retry mechanism, it can recover automatically.

---
title: "Why does the \"InvalidServerGroupListener.InUse\" event occur when I delete a Service?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Event-InvalidServerGroupListener_InUse-occurs-when-deleting-a-Service"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Issue description

During Service deletion, the "InvalidServerGroupListener.InUse: The specified ServerGroup has dependent resources Listener is in use" event occurs.

<span id=".5Y6f5Zug5YiG5p6Q"></span>
## Cause analysis

This event indicates that the back\-end server group created via Annotation is being used by another listener.

<span id=".6Kej5Yaz5pa55qGI"></span>
## Solution

In the [Load Balancer console](https://console.byteplus.com/clb), check whether the back\-end server group of the corresponding CLB instance for this Service is used by a custom listener. If so, disassociate the custom listener and back\-end server group, and then delete the Service.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">Do not reuse back\-end server groups created via Annotation (these are usually prefixed with <strong>k8s_{{cluster_id}}</strong>).</div>

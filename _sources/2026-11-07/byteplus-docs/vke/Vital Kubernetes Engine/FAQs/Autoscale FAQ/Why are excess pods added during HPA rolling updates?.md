---
title: "Why are excess pods added during HPA rolling updates?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/HPA_rolling_update_leads_to_the_creation_of_excess_Pods"
---

<span id=".6Zeu6aKY5o-P6L-w"></span>
## Issue description

During a rolling update, kube\-controller\-manager performs zero filling on pods whose monitoring data cannot be collected. This may add excess pods. You can prevent this issue by configuring an annotation for workloads.

<span id=".6Kej5Yaz5pa55qGI"></span>
## Solution

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To use this feature, you need to upgrade the metrics\-server add\-on of clusters to v0.7.1\-vke.2. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on">Upgrading add\-ons</a>.</div>


You can add the `HPARollingUpdateSkipped` configuration when configuring workloads to skip HPA during rolling updates to prevent extra pods from being created. Sample configurations:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: demo-workload
  annotations: 
    HPARollingUpdateSkipped: "true"# Skip HPA during rolling updates
spec:
  replicas: 1
  selector:
    matchLabels:
      app: demo-workload
  template:
    metadata:
      labels:
        app: demo-workload
    spec:
      containers:
      - name: workload
        image: doc-cn-beijing.cr.volces.com/vke/nginx-demo:v1.0
        resources:
          requests: 
            cpu: "500m" 
            memory: "1024Mi"
          limits:
            cpu: "1" 
            memory: "2Gi"
```

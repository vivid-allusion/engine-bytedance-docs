---
title: "Collecting VCI container logs via TLS"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Collecting-VCI-container-logs-using-Torch-Log-Service"
---

VCI supports collecting container logs via BytePlus TLS. This topic describes how to collect the standard output logs and file\-based logs of VCI containers to TLS.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A **log project** and **log topic** have been created in TLS. For detailed operations, see [Log projects](https://docs.byteplus.com/en/docs/tls/Managing_projects) and [Log topics](https://docs.byteplus.com/en/docs/tls/Managing_topics).

* The [log-collector](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on#.bG9nLWNvbGxlY3Rvci3nu4Tku7Y=) add\-on has been installed in the VKE cluster, or a [host group](https://docs.byteplus.com/en/docs/tls/Create_a_label-based_host_group) with the identifier `k8s-vke-${cluster_id}` has been created.


<span id=".5by55oCn5a655Zmo5a6e5L6L5byA5ZCv5pel5b-X6YeH6ZuG"></span>
## Enabling log collection for VCI

VCI supports two log collection methods:


* Add a Kubernetes pod annotation to enable log collection. You need to redeploy existing VCIs after adding the pod annotation to them.

* Enable log collection when creating a workload in the console.


<span id=".a3ViZXJuZXRlcy3mlrnlvI_phY3nva4="></span>
### Using Kubernetes configuration

When creating pods or workloads (including Deployments, StatefulSets, Jobs, and CronJobs), enable log collection by adding the specified pod annotation.

The annotation description is as follows.


|**Annotation Key** |**Annotation sample value** |**Description** |
|---|---|---|
|vci.volcengine.com/tls\-enable |true |Whether to collect VCI logs to TLS. Valid values:<br><br><br>* **false**: Disable log collection.<br><br>* **true**: Enable log collection. |


The following sample code shows how to create a Deployment.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      annotations:
        vke.volcengine.com/burst-to-vci: enforce  # Force use of VCI
        vci.volcengine.com/tls-enable: "true"  # Enable log collection to collect logs to TLS
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: cr-cn-beijing.volces.com/tw/nginx:1.0  # The address and version of the application image. Replace it with your own image address and version.
        ports:
        - containerPort: 80
        resources:
          requests:  # Specify the vCPU and memory for the container.
            cpu: "500m"      
            memory: "1024Mi"
          limits:
            cpu: "1"      
            memory: "2048Mi"
```


<span id=".5o6n5Yi25Y-w5pa55byP6YWN572u"></span>
### Using the console


1. Create a cluster that uses VCI. For detailed operations, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

2. When [creating a workload](https://docs.byteplus.com/en/docs/vke/Workload-overview), in the **Basic information** step, select **Vital Container Instance** for **Computing power type** and switch on **Log collection** to collect VCI logs into TLS.


<span id=".5p-l55yL5pel5b-X"></span>
## Viewing logs

Log in to the [TLS console](https://console.byteplus.com/tls) to query and analyze the collected log data. For a detailed description, see [Analysis overview](https://docs.byteplus.com/en/docs/tls/Analysis-overview).

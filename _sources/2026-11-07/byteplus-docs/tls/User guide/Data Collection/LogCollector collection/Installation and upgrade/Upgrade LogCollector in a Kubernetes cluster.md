---
title: "Upgrade LogCollector in a Kubernetes cluster"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/upgrade_logcollector_in_a_kubernetes_cluster"
---

To ensure the stability and efficiency of log collection, it is recommended that you upgrade LogCollector in a timely manner and always use the latest version of LogCollector to collect Kubernetes cluster logs. LogCollector installed in a Kubernetes cluster only supports manual upgrades. This document describes how to upgrade the LogCollector version in a Kubernetes cluster.

<span id=".5omL5Yqo5L-u5pS56ZWc5YOP54mI5pys"></span>
## Manual upgrade

You can execute the following commands in the Kubernetes cluster to upgrade the LogCollector version.

```shell
kubectl -n <namespace> set image <workload-type> <workload-name> <container-name>=<image>
```


The parameter description is as follows:


|Parameter |Example |Description |
|---|---|---|
|namespace |kube\-system |The LogCollector namespace. |
|workload\-type |daemonsets |The workload type of LogCollector.<br><br><br>* If LogCollector is installed according to [Install LogCollector using a DaemonSet](https://docs.byteplus.com/docs/tls/install_logCollector_use_a_daemonSet), it should be set to daemonsets.<br><br>* If LogCollector is installed according to [Install LogCollector using a sidecar](https://docs.byteplus.com/docs/tls/install_logcollector_use_a_sidecar), it should be set to the specific workload type. |
|workload\-name |logcollector |The workload name of LogCollector.<br><br><br>* If LogCollector is installed according to [Install LogCollector using a DaemonSet](https://docs.byteplus.com/docs/tls/install_logCollector_use_a_daemonSet), it should be set to "logcollector".<br><br>* If LogCollector is installed according to [Install LogCollector using a sidecar](https://docs.byteplus.com/docs/tls/install_logcollector_use_a_sidecar), it should be set to the specific workload name. |
|workload\-name |logcollector |The container name of LogCollector. If LogCollector is installed according to [Install LogCollector using a DaemonSet](https://docs.byteplus.com/docs/tls/install_logCollector_use_a_daemonSet), or [Install LogCollector using a sidecar](https://docs.byteplus.com/docs/tls/install_logcollector_use_a_sidecar), it should be set to logcollector. |
|image |logcollector\-bp\-ap\-southeast\-1.cr.bytepluses.com/logcollector/logcollector:latest |The image address of LogCollector. For the latest version of the image address, please refer to [LogCollector image URLs](https://docs.byteplus.com/docs/tls/install_logCollector_use_a_daemonSet#89454489). |


<span id=".6YeN5ZCvLWxvZ2NvbGxlY3RvcuacjeWKoQ=="></span>
## Verify the upgrade result


1. Run the following command to check the pod status. LogCollectors installed on all pods are upgraded with the rolling upgrade method. After all pods are in the Running status, the upgrade is successful.

   ```shell
   kubectl get pod -n ${namespace}
   ```
   

2. Go to the console to check the version of LogCollector installed on the specified host in the host group. If it is the latest version, the upgrade is successful.

---
title: "How do I create CRD resources such as ServiceMonitor in a cluster?"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/How-do-I-create-Custom-Resource-Definition-resources-such-as-ServiceMonitor-in-a-cluster"
---

This article introduces how to create CRD resources such as ServiceMonitor or PodMonitor in a cluster.

<span id=".6Zeu6aKY546w6LGh"></span>
## Issue Description

After you install the collector in the cluster, you can use CRD resources such as ServiceMonitor and PodMonitor to meet custom service discovery requirements. However, these CRD resources may not be built into the cluster, and an error is reported when creating the CRD resources.

In this case, you need to first configure CRD resources such as ServiceMonitor and PodMonitor in the cluster. This topic describes how to create these CRD resources in a cluster.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A BytePlus root user is created and Vital Kubernetes Engine (VKE) is activated.

* A cluster is created. For more details, see [Creating A Cluster](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

* The kubectl tool is installed locally. For details, see [Installing and Setting Up kubectl](https://kubernetes.io/docs/tasks/tools/).

* kubectl has been used to connect to the target cluster. For details, see [Connecting Clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).


<span id=".6YWN572u5q2l6aqk"></span>
## Configuration Procedure

<span id=".5Yib5bu6IFNlcnZpY2VNb25pdG9yIENSRCDotYTmupA="></span>
### Create ServiceMonitor CRD resources


1. Use kubectl to connect to the target cluster.

2. Based on the region where your cluster resides, run the corresponding command to create the ServiceMonitor CRD resources in the cluster.



<Tabs>
<Tab zoneid="YUcXCIPK8Q" title="North China 2 (Beijing)">
<TabTitle>North China 2 (Beijing)</TabTitle>

```Bash
kubectl apply -f https://vmp-release-cn-beijing.tos-cn-beijing.volces.com/manifests/crds/promopeartor-crd-servicemonitors.yaml
```





</Tab>
<Tab zoneid="fus6wUEME3" title="East China 2 (Shanghai)">
<TabTitle>East China 2 (Shanghai)</TabTitle>

```Bash
kubectl apply -f https://vmp-release-cn-shanghai.tos-cn-shanghai.volces.com/manifests/crds/promopeartor-crd-servicemonitors.yaml
```





</Tab>
<Tab zoneid="Po62umhn3I" title="South China 1 (Guangzhou)">
<TabTitle>South China 1 (Guangzhou)</TabTitle>

```Bash
kubectl apply -f https://vmp-release-cn-guangzhou.tos-cn-guangzhou.volces.com/manifests/crds/promopeartor-crd-servicemonitors.yaml
```





</Tab>
</Tabs>


<span id=".5Yib5bu6IFBvZE1vbml0b3IgQ1JEIOi1hOa6kA=="></span>
### Create PodMonitor CRD resources


1. Use kubectl to connect to the target cluster.

2. According to the region where your cluster is located, select the corresponding command to create PodMonitor CRD resources in the cluster.



<Tabs>
<Tab zoneid="uZWf94Rj3D" title="North China 2 (Beijing)">
<TabTitle>North China 2 (Beijing)</TabTitle>

```Bash
kubectl apply -f https://vmp-release-cn-beijing.tos-cn-beijing.volces.com/manifests/crds/promopeartor-crd-podmonitors.yaml
```





</Tab>
<Tab zoneid="WMaaJk6RxW" title="East China 2 (Shanghai)">
<TabTitle>East China 2 (Shanghai)</TabTitle>

```Bash
kubectl apply -f https://vmp-release-cn-shanghai.tos-cn-shanghai.volces.com/manifests/crds/promopeartor-crd-podmonitors.yaml
```





</Tab>
<Tab zoneid="ETWMzZLO0O" title="South China 1 (Guangzhou)">
<TabTitle>South China 1 (Guangzhou)</TabTitle>

```Bash
kubectl apply -f https://vmp-release-cn-guangzhou.tos-cn-guangzhou.volces.com/manifests/crds/promopeartor-crd-podmonitors.yaml
```





</Tab>
</Tabs>


<span id=".5Yib5bu6IFByb2JlIENSRCDotYTmupA="></span>
### Create Probe CRD resources


1. Use kubectl to connect to the target cluster.

2. Based on the region where your cluster resides, run the corresponding command to create the Probe CRD resources in the cluster.



<Tabs>
<Tab zoneid="rxiIA1wLg4" title="North China 2 (Beijing)">
<TabTitle>North China 2 (Beijing)</TabTitle>

```Bash
kubectl apply -f https://vmp-release-cn-beijing.tos-cn-beijing.volces.com/manifests/crds/promopeartor-crd-probes.yaml
```





</Tab>
<Tab zoneid="NymRvXQ8Cv" title="East China 2 (Shanghai)">
<TabTitle>East China 2 (Shanghai)</TabTitle>

```Bash
kubectl apply -f https://vmp-release-cn-shanghai.tos-cn-shanghai.volces.com/manifests/crds/promopeartor-crd-probes.yaml
```





</Tab>
<Tab zoneid="R12TSae4XJ" title="South China 1 (Guangzhou)">
<TabTitle>South China 1 (Guangzhou)</TabTitle>

```Bash
kubectl apply -f https://vmp-release-cn-guangzhou.tos-cn-guangzhou.volces.com/manifests/crds/promopeartor-crd-probes.yaml
```





</Tab>
</Tabs>


<span id=".5p-l55yL57uT5p6c"></span>
## View Results

After you create the CRD resources in VKE, you can follow these steps to view the CRD information and verify that the configuration is correct:


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. On the left menu bar, click **Cluster**. In the cluster list on the right side, select the target cluster.

3. Click the name of the cluster to go to the cluster configuration page.

4. In the left navigation pane, click **Workload ** \> **Resource Explorer**, and then select **CRD ** from the **Category ** drop\-down list to view the created CRD resources.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_01604ed4972a8e2b2fa73ff7310a4c72.png) </span>


&nbsp;

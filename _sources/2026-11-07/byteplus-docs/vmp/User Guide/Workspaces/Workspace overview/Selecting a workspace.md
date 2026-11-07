---
title: "Selecting a workspace"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Selecting-a-workspace"
---

Before you create a workspace, you need to estimate the quantity of metrics and select appropriate workspace specifications based on your business requirements. This topic describes how to estimate specifications and select a workspace.

<span id=".6YCJ5oup5pWw5o2u5a2Y5YKo5aSp5pWw"></span>
## Select the number of data storage days

You need to choose an appropriate time range for data storage based on your business requirements.

<span id=".5Lyw566X5pyA5aSn5rS76LeD5pe25bqP5pWw"></span>
## Estimate the maximum number of active time series

Active time series refer to time series that are being actively written into a workspace. Each metric generates an active time series on each monitoring object. Active time series serve as the primary criteria for evaluating data volume. For more details, refer to [Prometheus time series data format](https://docs.byteplus.com/en/docs/vmp/Format-of-Prometheus-time-series-data).

It is recommended to evaluate and select workspace specifications based on the upper limit of active time series. You can estimate the maximum number of active time series by using one of the following methods:

<span id=".5pa55qGI5LiA77ya5qC55o2u6ZuG576k5ZKM5Lia5Yqh6KeE5qih6L-b6KGM5Lyw566X"></span>
### Method 1: Estimate the upper limit based on the cluster and business scale.


* **Cluster metrics**


When you use Vital Kubernetes Engine (VKE) of BytePlus or build your own Kubernetes cluster environment, the data volume of metrics related to container resources, virtual machine resources, and native Kubernetes resources can be estimated based on the cluster size. If the metrics that you collect include node\-exporter, kubelet, cadvisor, and kube\-state\-metrics, which are all the data plane metrics collected by Kubernetes by default, the estimation formula is as follows:

```Plain Text
nodeMax × 15,000 + podMax × 200 + podInc × 200
```



|**Parameter** |**Note** |**Obtaining method** |
|---|---|---|
|nodeMax |The maximum number of nodes in the cluster. |You can run the command `kubectl get node -A \| wc -l` to obtain the number of nodes in the current cluster.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The current number of nodes in your cluster is the result of the value obtained from the preceding command minus 1.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If your cluster has scaling requirements, use the maximum number of nodes.</div><br> |
|podMax |The maximum number of pods in the cluster. |You can use the command `kubectl get pod -A \| wc -l` to obtain the current number of pods in the cluster.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The value obtained from the preceding command minus 1 is the current number of pods in your cluster.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If pods in your cluster are frequently created and deleted, set the value to the maximum number of pods.</div><br> |
|podInc |The maximum number of pods added per hour in the cluster, including **re\-created** pods. |If pods in your cluster are frequently created and deleted, estimate the maximum number of pods added per hour. The number includes the **number of created pods** and the **number of pods re\-recreated after deletion**. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The preceding estimation formula does not include <strong>control plane metrics</strong> and <strong>custom metrics</strong>.</div>



* **Business metrics**

   Business metrics refer to the metrics exposed by businesses deployed in the cluster. The metrics are related to your business situation, including:

   * The number of business pods.

   * The maximum number of active time series exposed by each pod.

   * The creation and deletion situation of business pods, such as whether business pods are frequently deleted and created.


You need to evaluate the maximum active time series of business metrics based on the preceding situations and add them to the maximum active time series of cluster metrics. The sum is the maximum active time series that are required when you select a workspace.

<span id=".5pa55qGI5LqM77ya5LuO5bey5pyJIFByb21ldGhldXMg6L-B5YWl"></span>
### Method 2: Migrate from an existing Prometheus

In native Prometheus, the collection side automatically generates `scrape_samples_scraped` (the total number of samples that are collected each time) and `scrape_series_added` (the number of time series added compared to the last collection). You can use the following PromQL statement in the existing Prometheus system to query these metrics and estimate the maximum active time series.

```promql
sum (scrape_samples_scraped{} offset 1h) + sum (sum_over_time(scrape_series_added{}[1h]))
```


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_57c972482a9717e57f24a6d66890caee.png) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In other monitoring systems, the names of the corresponding metrics may not be exactly the same. You can replace the metrics based on their actual meaning.</div>


<span id=".5pa55qGI5LiJ77ya6K-V55So5qCH5YeG54mI5bel5L2c5Yy6"></span>
### Method 3: Try a Standard Edition workspace.

If you cannot accurately estimate the maximum active time series of the workspace, you can try using a workspace to obtain the metric scale in your environment. VMP offers a Standard Edition workspace with a storage duration of 15 days. The basic cloud service metrics of the workspace are free of charge, which makes the workspace suitable for trial use. 

You can perform the following steps to try a Standard Edition workspace:


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus).

2. On the top navigation bar, select the target region.

3. On the left navigation bar, click **Workspace** to go to the workspace list page.

4. Click **Create**, and choose to create and purchase a Standard Edition workspace.

5. Click **Create Now** to create the workspace.

6. Integrate your clusters and businesses into the new workspace. For more details, refer to [VKE access](https://docs.byteplus.com/en/docs/vmp/cluster-monitoring).

7. After you integrate clusters into the workspace, you can view metrics such as **maximum active time series** and **rate of writing samples** on the details page of the workspace.

   1. On the left navigation bar, click **Workspace** to go to the workspace list page.

   2. Click the name of the target workspace to go to the details page of the workspace, and view the details of the workspace.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ff115b3ce2daab635e52cf016c9131f3.png) </span>

8. You can determine whether to modify the configurations of the workspace based on your trial use experience.


<span id=".5Lyw566X5YW25LuW6YWN6aKd55So6YeP77yI5Y-v6YCJ77yJ"></span>
## Estimate other quota usage (optional)

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Selecting workspace specifications based on data storage days and the maximum number of active time series can meet the requirements of most use cases. If your use cases have special requirements, you can continue to evaluate other metrics.</div>


<span id=".5Lyw566X5pyA5aSn5oyH5qCH5pGE5YWl6YCf546H"></span>
### Estimate the maximum metric ingest rate

You can use the following formula to estimate the maximum metric ingest rate:

```Plain Text
time_series / scrape_interval
```


In the formula:


* `time_series`: indicates the maximum active time series.

* `scrape_interval`: indicates the collection interval. In the prometheus\-agent add\-on, the default value is 15 seconds.


For example, if your maximum number of active time series is 10 million, and the collection interval is 15 seconds, your maximum metric ingest rate is calculated by using the following formula: 10,000,000/15 = 667,000 samples/s.

<span id=".5Lyw566X5p-l6K-iIFFQUyDkuI7mn6Xor6Llubblj5E="></span>
### Estimate query QPS and query concurrency

You can use the following formula to estimate the QPS:

```Plain Text
1.5 × panels × persons
```


In the formula:


* `panels`: indicates the maximum number of monitoring panels displayed on a screen at the same time.

* `persons`: indicates the maximum number of people that use the panels at the same time.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you have estimated the query QPS, the query concurrency can meet the requirements in most cases.</div>


<span id=".6K-E5Lyw57u85ZCI6LS555So5oiQ5pys"></span>
## Evaluate overall costs

After estimation and filtering, if multiple workspace specifications still meet your business requirements, you can make a choice based on the overall costs. 

<span id=".5ZCO57ut5L2_55So"></span>
## Subsequent usage

As your business grows, the original workspace specifications may no longer meet your business requirements. In this case, you can choose one of the following two methods to solve the capacity issue:


1. Divide the usage into different workspaces in appropriate dimensions such as development or production environment.

2. Modify the configurations of the workspace. For more details, refer to [Modifying workspace configurations](https://docs.byteplus.com/en/docs/vmp/Workspace_configuration_change).

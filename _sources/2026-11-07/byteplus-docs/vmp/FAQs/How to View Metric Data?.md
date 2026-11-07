---
title: "How to View Metric Data?"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/How-do-I-view-metric-data"
---

This article introduces how to view the data collected in the Vital Managed Service for Prometheus.

<span id=".5pa55rOV5LiAIOmAmui_hyBFeHBsb3JlIOafpeeciw=="></span>
## Method 1: View data on the Explore page


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus).

2. Click **Explore** on the left navigation bar to go to the Explore page.

3. In the upper right corner of the page, configure the **Workspace**, **Query Time Range**, and **Data Refresh Method** required for metric queries.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5491ffdb5bd56f37c73f7d6b84729cb4.png) </span>

   4. 4. Specify the metric to query. You can either manually enter a metric or select one from the search list.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_16cf0cbc603d9bbc48f0de748c11ce28.png) </span>

4. After the metric is configured, click **Query ** to retrieve the relevant metric and display it on the dashboard.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2ba6f2392b33fcb1eb72d2efd60bfebb.png) </span>


<span id=".5pa55rOV5LqMIOafpeeci-WOn-Wni-aMh-agh-aVsOaNrg=="></span>
## Method 2: View raw metric data

The collection targets of the Vital Managed Service for Prometheus may be deployed inside clusters or outside clusters (e.g., deployed on ECS hosts).


* When the collection target is deployed outside the cluster, you can directly view the original metric data of the collection target by using `curl http://target-ip:port/metrics`.

* When the collection target is deployed in the cluster, you can follow the following operation method to view the original metric data saved in the collection target:

   1. In the local environment, use kubectl to connect to the cluster where the collector is located.

   2. Execute the following command to map the port of the collection target (e.g., Exporter) to the local environment.

   ```bash
   kubectl port-forward pod/rabbitmq-exporter-5fxxxx 9419:9419 -n volcano-metrics
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><code>rabbitmq-exporter-5fxxxx</code> is the instance name of the collection target. In this example, RabbitMQ\-Exporter is used. You need to replace it with your collection target's instance name during actual operation.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><code>9419</code> is the port number for exposing metrics of this collection target. The port number differs for different collection targets. You need to replace it with the correct port number during actual operation.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><code>-n volcano-metrics</code> is the namespace where the collection target is located. You need to replace it with the namespace of the collection target during actual operation.   </div>
   

   3. Open a browser in the local environment (Linux/Mac), enter **localhost:9419** in the address bar to enter the collection target page and directly view the original metric data.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c890eaa065ac9e014c3f00a7c0feb889.png) </span>

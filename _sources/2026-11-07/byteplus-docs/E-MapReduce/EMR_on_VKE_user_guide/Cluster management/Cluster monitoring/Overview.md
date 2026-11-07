---
title: "Overview"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/vke_cluster_monitoring_overview"
---

Volcano Engine E\-MapReduce on VKE (EMR on VKE) cluster monitoring mainly consists of **node monitoring** and **service monitoring**.


* Node monitoring: Monitoring features for dedicated nodes in this cluster, including CPU monitoring, memory monitoring, and storage monitoring.

* Service monitoring: Provides detailed monitoring features for major services installed on the cluster, such as Ray, Celeborn, and Spark.


<span id="949951d3"></span>
# View monitoring


1. Log in to [EMR console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home).

2. Select **on VKE \> cluster name** to enter the cluster details page.

3. In the left navigation bar, click Cluster monitoring to enter the monitoring interface.

4. Select the node or service name you want to view monitoring for. Depending on the service, you can filter and view relevant monitoring metrics by node, time range, or RayCluster.


For detailed descriptions of each service metric, refer to:


* [Ray service metrics](https://docs.byteplus.com/docs/E-MapReduce/109067)

* [Celeborn service metrics](https://docs.byteplus.com/docs/E-MapReduce/109066)

* [Spark service metrics](https://docs.byteplus.com/docs/E-MapReduce/109068)

* [VolcanoScheduler service metrics](https://docs.byteplus.com/docs/E-MapReduce/109069)

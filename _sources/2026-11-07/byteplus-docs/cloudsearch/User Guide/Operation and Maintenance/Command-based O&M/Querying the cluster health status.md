---
title: "Querying the cluster health status"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/cluster-health-status"
---

You can run O&M commands in the console of the visualization tool to query the cluster status. This helps detect cluster exceptions promptly and mitigate potential risks.

<span id="2d770cde"></span>
## Background information

The cluster health status is expressed by three colors: red, yellow, and green. Each color has its unique meaning.


* Red: indicates that the cluster has unavailable primary shards. In this state, some data becomes unavailable, while other data remains available.

* Yellow: indicates that all primary shards of the cluster are available, but some replica shards are not assigned. Although all data is accessible, the cluster is not highly available due to the unassigned replicas.

* Green: indicates that all primary shards and replica shards in the cluster are available. In this state, the cluster is healthy and highly available.


<span id="63b4349d"></span>
## Querying the cluster status


1. Log on to the visualization tool. For more information, please see [Logging on to the visualization tool](https://docs.byteplus.com/en/docs/cloudsearch/logging-tool).

2. Click the menu icon on the upper\-left corner, and choose **Management \> Dev Tools**.

3. On the **Console** tab, run the `GET /_cluster/health` command in the left\-side area, and click the request icon.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/892cf7cb9be2430da267fe5655fa9c50~tplv-goo7wpa0wc-image.image) </span>

   After the command is successfully executed, the following result is returned. The result shows the cluster status is **yellow**, indicating that some replicas in the cluster are unavailable.

   ```JSON
   {
     "cluster_name" : "00g0***al97",
     "status" : "yellow",
     "timed_out" : false,
     "number_of_nodes" : 15,
     "number_of_data_nodes" : 6,
     "active_primary_shards" : 5,
     "active_shards" : 26,
     "relocating_shards" : 0,
     "initializing_shards" : 0,
     "unassigned_shards" : 3,
     "delayed_unassigned_shards" : 0,
     "number_of_pending_tasks" : 0,
     "number_of_in_flight_fetch" : 0,
     "task_max_waiting_in_queue_millis" : 0,
     "active_shards_percent_as_number" : 89.65517241379311
   }
   ```
   


<span id="5dbf4e72"></span>
## Restoring the cluster status

A **yellow** cluster status indicates that some replicas in the cluster are unavailable. In this case, performing operations like modifying passwords or upgrading cluster specifications require additional time. We recommend that you restore the cluster status to **green** before performing these operations.

The **yellow** cluster status occurs when one or more indices in the cluster experience replica loss. To resolve this issue, identify the affected indices and rectify the fault.


1. Log on to the visualization tool. For more information, refer to [Logging on to the visualization tool](https://docs.byteplus.com/en/docs/cloudsearch/logging-tool).

2. Click the menu icon on the upper\-left corner, and choose **Management \> Dev Tools**.

3. Identify abnormal indices.

   On the **Console** tab, run the `GET /_cat/indices?v` command in the left\-side area, and click the request icon.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c82e6a29dd944ed788775bbe6ec26b6d~tplv-goo7wpa0wc-image.image) </span>

   The following information is returned, indicating that the status of some indices is **yellow**.

   The **yellow** index status occurs when an index has more replicas than the total number of nodes minus one. To resolve this issue, adjust the number of replicas accordingly.

4. Restore the indices.

   On the **Console** tab, run the following command in the left\-side area, and click the request icon.

   ```Shell
   PUT //_settings 
   {
   "index":{"number_of_replicas":1}
   }
   ```
   

   The following information is returned:

   ```Shell
   {
      
     "acknowledged" : true
      
   }
      
   ```
   

5. Verify whether the index status changes to **green**.

   On the **Console** tab, run the `GET /_cat/indices?v` command in the left\-side area, and click the request icon. The output shows that the index status becomes **green**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6f88b64feb9a4711b967636fdcf10f9f~tplv-goo7wpa0wc-image.image) </span>

6. Verify whether the cluster status changes to **green**.

   On the **Console** tab, run the `GET /_cluster/health` command in the left\-side area, and click the request icon.

   The output shows that the cluster status becomes **green**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/768ef74b85db4032b7d4373e6f11651e~tplv-goo7wpa0wc-image.image) </span>

---
title: "Viewing monitoring data"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/view-monitoring-data"
---

MongoDB instances include replica set and sharding cluster instances. Different types of instances allow you to view different monitoring metrics. You can learn the running status and usage of instances based on monitoring metrics. This topic introduces how to view monitoring data of MongoDB instances.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, click the target instance name.

5. On the instance details page, click **Monitoring** tab.

6. On the **Monitoring** tab, you can select different tabs based on instance types or different components of instances to view details of monitoring metrics within the specified duration (such as the past 1 hour).

   * **Replica set instance**

      On the **Replica Set** tab of a replica set instance, you can select one or more nodes to view performance monitoring details.

   * **Sharding cluster instance**

      On the **Mongos**, **Config Servers**, and **Shards** tabs of a sharding cluster instance, you can select one or more nodes to view performance monitoring details.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can view the node roles (such as <strong>Primary</strong>, <strong>Secondary</strong>, <strong>Hidden</strong>, and <strong>ReadOnly</strong>) of replica set instances, and Config Server and Shard components in sharding cluster instances in the node information section on the <strong>Monitoring</strong> tab, enabling you to quickly identify monitoring data for different node types.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can view performance metric details for up to the past 15 days.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For more information about monitoring metrics, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/monitoring-metric">Monitoring metrics</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can click <strong>Create alarm strategy</strong> in the upper\-right corner of the <strong>Monitoring</strong> tab to set alerts. For more information, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/set-alert">Setting alerts</a>.   </div>
   


<span id=".55u45YWz5paH5qGj"></span>
## Relevant documents

[Troubleshooting manual for MongoDB high CPU utilization](https://docs.byteplus.com/en/docs/mongodb/troubleshooting-for-high-cpu-utilization)

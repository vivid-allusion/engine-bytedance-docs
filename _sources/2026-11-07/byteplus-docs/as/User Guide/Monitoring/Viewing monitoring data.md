---
title: "Viewing monitoring data"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Viewing-Monitoring-Data"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

Auto Scaling supports real\-time monitoring of dynamic changes in metrics such as the instance count, instance type, and distribution within the scaling group. For example, instances in the scaling group, the number of instances in service, and the distribution of instance numbers by availability zone, instance type, and billing method.

Visualized data allows you to quickly understand the current and historical usage and distribution of resources. This way, you can develop better Auto Scaling policies and fault response measures to improve system stability and reliability.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can also <a href="https://docs.byteplus.com/en/docs/as/Viewing-scaling-activities">view scaling logs</a> to obtain the above\-mentioned information.</div>


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Scaling Group console](https://console.byteplus.com/as/group). 

2. In the top menu bar, select the project and region of target resource.

3. Click the name of the scaling group, select the "Monitor" tab, and view resource information on the Resource Overview page.

4. In the data monitoring window, you can switch between the "Instance" and "Listener" tabs to view the corresponding monitoring metrics.

   * Data update frequency: Automatic refresh and manual refresh are supported. After you enable automatic refresh on the right side of the monitoring page, the page refreshes automatically once per minute.

   * Data retention period: By default, monitoring data from the last hour is displayed. Only the most recent month of monitoring data can be retained and viewed.

   * Chart data may not exactly match your current actual conditions. Possible causes include:

      * The data displayed in the charts is collected every minute. If the instance count in the scaling group changes multiple times within one minute, the changes can not be reflected in the charts. Suppose the number of instances was 1 at 12:00, changed to 3 after 30 seconds, and then changed to 2 after another 30 seconds. In this case, the chart shows the number of instances changing from 1 at 12:00 to 2 at 12:01, but the intermediate changes are not displayed.

      * For instances automatically created during scaling activities, the charts display the information about instance specification and billing method at the time of creation. If you change the instance specifications or billing methods for created instances, the chart data will not be updated to reflect the changes.


&nbsp;

&nbsp;

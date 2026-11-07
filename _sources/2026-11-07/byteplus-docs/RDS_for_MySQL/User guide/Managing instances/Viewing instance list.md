---
title: "Viewing instance list"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_instance_list"
---

This topic describes the information displayed in the RDS for MySQL Instances list and the steps to view it.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

The instance list displays information such as the instance name, instance ID, and running status in columns. By default, only some columns are displayed in the Instances list. You can customize the columns displayed as needed. The following table describes each column in the Instances list and indicates whether it is displayed.


|Columns of the instance list |Note |Whether to display by default |Whether to support customized display |Whether to support filtering |Whether to support sorting |
|---|---|---|---|---|---|
|Instance name/ID |Instance name and ID. Click the instance name to enter the **Summary** page. |Yes |No |No |No |
|Monitoring |Click the monitoring chart to quickly view the monitoring dashboard of the instance. |Yes |Yes |No |No |
|State |The running status of the instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the instance is not in the <strong>Running</strong> state, hover over the status text to view associated tasks or operation and maintenance events.</div><br> |Yes |Yes |Yes |No |
|Availability zone |The node that each node of the instance belongs to. |Yes |Yes |Yes |No |
|Private network address/Port |The private network address and port of the instance's default connection endpoint. |Yes |Yes |No |No |
|Public network address/Port |The public network address and private network port of the instance's default connection endpoint. |No |Yes |No |No |
|IPv4 address |The internet protocol address and port of the instance's default endpoint. |Yes |Yes |No |No |
|Virtual private cloud |The Virtual Private Cloud that the instance uses. Hover over the Virtual Private Cloud name to view its ID in the pop\-up window. |Yes |Yes |No |No |
|Instance type |Instance type. |Yes |Yes |Yes |No |
|Tag |Tag information associated with the instance. The Instances list displays the number of tags associated with the instance. Hover over the number to view the keys and values of the tags associated with the instance. |Yes |Yes |Yes |No |
|Primary node specifications |Primary node specifications. |Yes |Yes |No |No |
|Number of nodes |Number of nodes. Hover over the number to view the IDs and specifications of each node type in the pop\-up window. Click the **View topology** button in the pop\-up window to go to the **Instance topology** page. |Yes |Yes |No |No |
|CPU utilization (%) |The average CPU usage rate of the instance's primary node in the recent minute. |No |Yes |No |Yes |
|Memory utilization (%) |The average Memory Usage rate of the instance primary node in the last minute first. |No |Yes |No |Yes |
|Disk utilization (%) |The average disk usage rate of the instance's primary node in the last minute. |No |Yes |No |Yes |
|Database version |Instance version information. |Yes |Yes |Yes |No |
|Kernel version |Kernel minor version information of the instance. |Yes |Yes |Yes |No |
|Engine type |The engine type of the instance. |Yes |Yes |Yes |No |
|Billing method |The billing type for the instance. The current MySQL instance supports two billing types: pay\-as\-you\-go and monthly/annual subscription. For more information about billing methods, refer to [Product billing](https://docs.byteplus.com/en/docs/RDS_for_MySQL/price_overview). |Yes |Yes |Yes.<br><br>Filter by monthly/annual subscription or pay\-as\-you\-go. |Yes.<br><br>You can sort by subscription \- ascending and subscription \- descending. |
|Creation time |The creation time of the instance. |Yes |Yes |No |No |
|Affiliate project |The project to which the instance belongs. Click the project name to go to the project details page. |Yes |Yes |No |No |
|Actions |Operations supported by the instance.<br><br><br>* [Login DBW](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-rds-for-mysql)<br><br>* Modify configuration<br><br>   * [Modifying specifications](https://docs.byteplus.com/en/docs/RDS_for_MySQL/standard_instance_specification_modification)<br><br>   * [Adding nodes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/adding_nodes)<br><br>   * [Deleting nodes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/deleting_nodes)<br><br>* [Configure allowlist](https://docs.byteplus.com/en/docs/RDS_for_MySQL/associating_allowlists_to_instances)<br><br>* [Buy a same instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_the_same_instance_configuration)<br><br>* [Switch to subscription](https://docs.byteplus.com/en/docs/RDS_for_MySQL/switching_to_yearly_or_monthly_subscription) (For pay\-as\-you\-go instances only)<br><br>* [Switch to pay-as-you-go](https://docs.byteplus.com/en/docs/RDS_for_MySQL/switching_to_pay-as-you-go) (For subscription instances only)<br><br>* [Renewal](https://docs.byteplus.com/en/docs/RDS_for_MySQL/renewal_management) (For subscription instances only)<br><br>* [Observation diagnosis](https://docs.byteplus.com/en/docs/DBW/observation-diagnosis-for-mysql)<br><br>* [Restart an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/restarting_an_instance)<br><br>* [Delete instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/deleting_or_unsubscribing_an_instance#.5Yig6Zmk5a6e5L6L) (For pay\-as\-you\-go instances only)<br><br>* [Unsubscribe instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/deleting_or_unsubscribing_an_instance#.6YCA6K6i5a6e5L6L) (For monthly/annual subscription instances only) |Yes |No |No |No |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For instances in the <strong>Running</strong> state, CPU utilization (%), memory utilization (%), and disk utilization (%) have minute\-level accuracy.</div>


* <div data-tips="true" data-tips-type="tip">When using subscription \- ascending or subscription \- descending, the system first filters the list to show only monthly/annual subscription instances. It then sorts these instances by due time in ascending order (instances due earlier are listed first) or descending order (instances due later are listed first). In this case, pay\-as\-you\-go instances are not displayed.</div>


* <div data-tips="true" data-tips-type="tip">Under billing type, the subscription \- ascending and subscription \- descending options first filter for monthly/annual subscription instances and then sort them in ascending or descending order.</div>


* <div data-tips="true" data-tips-type="tip">The subscription \- ascending, subscription \- descending, CPU utilization (%), memory utilization (%), and disk utilization (%) sorting methods are mutually exclusive. Only one sorting method can be applied at a time.</div>


* <div data-tips="true" data-tips-type="tip">In the upper\-left corner of the Instances list, you can search for instances by Instance ID, Instance name, Private network domain, Private network IP, or VPC ID. For more details, refer to Searching instance.</div>


* <div data-tips="true" data-tips-type="tip">The columns of the Instances list are customizable. For more information about the operations available for instances in the list, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/customizing_instances_list">Customizing the columns of the Instances list</a>.</div>



<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project to which the instance belongs is not set, this operation should select the project as <strong>All resources</strong>.   </div>
   

3. In the left navigation bar, click **Instances** to view the list of RDS for MySQL instances.


<span id=".5ZCO57ut5q2l6aqk"></span>
## Subsequent steps

[Customizing instance list columns](https://docs.byteplus.com/en/docs/RDS_for_MySQL/customizing_instances_list)

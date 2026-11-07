---
title: "Intelligent patrol"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/cdw-intelligent-patrol"
---

Intelligent patrol is a preventive maintenance measure used to check the status of the system and promptly identify potential issues. Intelligent patrol generates reports according to patrol items, allowing you to detect and resolve issues in advance, reducing system failures and downtime, and ensuring system stability and reliability.

<span id="a1463b03"></span>
# Usage restrictions

This feature is in Beta. To enable it, please submit a ticket or contact the ByteHouse team to request allowlist access.

<span id="60a3307b"></span>
# Feature overview

The details of the intelligent patrol feature are as follows.


|Sub\-item |Description |
|---|---|
|Patrol item |Current intelligent patrols involve checking system loads, query loads, and dedicated servers, with specific details as follows:<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9b06472d62144566ac11181f62745c91~tplv-goo7wpa0wc-image.image) </span> |
|Patrol type |* Manual patrol: Manually triggered.<br><br>* Scheduled patrol: Automatically performed at scheduled times, with options to conduct the patrol daily, weekly, or monthly. |
|Patrol results |After the execution of the patrol tasks, the system will generate a patrol report, analyzing the system issues from the perspectives of patrol items and their severity levels, extent of abnormal impact, and providing handling suggestions. |
|Resource utilization |Intelligent patrol will utilize resources in the current environment and impact performance. It is recommended to operate during off\-peak hours to avoid affecting business operations. |


<span id="afb736f0"></span>
# Create patrol task


1. Log in to the ByteHouse console, switch to the target environment, navigate to the **Diagnostics Analysis** tab, enter the **Intelligent patrol** page, click on the **Patrol task** tab, click **New patrol task**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43c015457fae4add84d07a55df2a4071~tplv-goo7wpa0wc-image.image) </span>

2. On the patrol task creation page, fill in the basic task information, select the patrol type, and view the patrol content.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9d20b2d3cabd4befb1ee4e767941e377~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Intelligent patrol will utilize resources in the current environment. It is recommended to operate during off\-peak hours to avoid affecting business operations.   </div>
   

   * Patrol task configuration information

      
      |Parameter Item |Parameter Description |
      |---|---|
      |Patrol task name |Supports custom patrol task names. |
      |Patrol type |Supports manual patrol and scheduled patrol.<br><br><br>* Manual patrol: You can manually trigger the patrol in the patrol task list after creating a patrol task.<br><br>* Scheduled patrol: You can set the patrol cycle, and within the patrol cycle, the system will automatically execute the patrol tasks. |
      

   * Patrol content

      
      |Category |Patrol Item |Patrol item description and risk level assessment rules |
      |---|---|---|
      |Virtual Warehouse (VW) Resources |Prepay VW expiry |Days before the expiration of the annual/monthly computing group. The risk level assessment rules are as follows, in days:<br><br><br>* Normal: [365, 7]<br><br>* Medium Risk: [7, 3]<br><br>* High Risk: [3, 0] |
      ||Peak VW CPU usage over last day |Calculate the average CPU usage every 30 minutes in the past 1 day, and get the highest value. The unit is %. Risk level judgment rules are as follows:<br><br><br>* Normal: [0, 90]<br><br>* Medium Risk: [90, 95]<br><br>* High Risk: [95, 100] |
      ||Peak VW memory usage over last day |Calculate the maximum average memory usage every 30 minutes over the past 1 day. The unit is %. The risk level judgement rules are as follows:<br><br><br>* Normal: [0, 80]<br><br>* Moderate Risk: [80, 85]<br><br>* High Risk: [85, 100] |
      ||Peak VW iNode usage over last day |Calculate the maximum average iNode usage rate per minute over the past 1 day. The unit is %. The risk level judgement rules are as follows:<br><br><br>* Normal: [0, 90]<br><br>* Moderate Risk: [90, 95]<br><br>* High risk: [95, 100] |
      ||Peak VW disk cache usage over last day |Calculates the average cache usage rate per minute over the last 1 day and takes the maximum value. The unit is %. Risk level evaluation rules are as follows:<br><br><br>* Normal: [0, 90]<br><br>* Medium risk: [90, 93]<br><br>* High risk: [93, 100] |
      |VW Query |VW Insert success rate |Calculation formula: insert successful queries / total insert queries. The unit is %. The rules for determining risk levels are as follows:<br><br><br>* Normal: [100, 98]<br><br>* Medium Risk: [98, 95]<br><br>* High Risk: [95, 0] |
      ||VW Query success rate |Calculation formula: Successful queries/All queries. The unit is %. The rules for determining risk levels are as follows:<br><br><br>* Normal: [100%, 98%]<br><br>* Medium Risk: [98%, 95%]<br><br>* High Risk: [95%, 0] |
      |Private Server |Prepay private server expiry |Days before expiration date for annual and monthly exclusive Servers. Risk level determination rules are as follows, in days:<br><br><br>* Normal: [365, 7]<br><br>* Medium Risk: [7, 3]<br><br>* High Risk: [3, 0] |
      ||Peak private server CPU usage over last day |Calculate the average CPU usage of exclusive Servers every 10 minutes over the past day and take the maximum value. The unit is %. Risk level determination rules are as follows:<br><br><br>* Normal: [0, 90]<br><br>* Medium risk: [90, 95]<br><br>* High risk: [95, 100] |
      ||Peak private server memory usage over last day |Statistics for the past day: calculates the average memory usage of the dedicated server every 10 minutes, taking the maximum value among them. The unit is %. Risk level determination rules are as follows:<br><br><br>* Normal: [0, 80]<br><br>* Medium risk: [80, 85]<br><br>* High risk: [85, 100] |
      |Table |Unhealthy parts |Count how many tables in the current environment contain unhealthy partitions. Risk level judgment rules are as follows:<br><br><br>* Normal: [0, 0]<br><br>* Medium risk: [0, 100,000]<br><br>* High risk: [100,000, 100,000]<br><br><br>ByteHouse provides a dedicated partition health diagnosis function. For detailed partition health of data tables, see [Partition health diagnosis](https://docs.byteplus.com/docs/bytehouse/partition-health-diagnosis). |
      |Gateway Connection |Gateway connection ratio |Calculation formula: Current TCP connections / TCP connection limit (Unit: %).<br><br>Note: The number of connections varies across different environments. If you need to adjust the gateway connection limit, please refer to [Gateway Connections](https://docs.byteplus.com/docs/bytehouse/monitoring-and-alarm#08df7055).<br><br>Risk level assessment rules are as follows:<br><br><br>* Normal: [0, 90]<br><br>* Medium risk: [90, 95]<br><br>* High risk: [95, 100] |
      |API Key |API Key expiry |The days before the expiration of all user API keys. Risk level assessment rules are as follows, unit in days:<br><br><br>* Normal: [365, 7]<br><br>* Medium risk: [7, 3]<br><br>* High Risk: [Mar, 0] |
      

3. Click **Ok**. The system will create the patrol task.

4. You can view the created tasks in the patrol task list. You can also enter the task name in the patrol task list to view the patrol tasks.


<span id="bb4ab3da"></span>
# Manually execute patrol tasks

For tasks set as manual patrol, you can manually trigger the execution of tasks as needed.

In the patrol task list, click the **Run Immediately** button in the operation column, then click **OK** in the popup, and the system will perform the patrol.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ba0caa1d07bb401682d3b90eeece8cb9~tplv-goo7wpa0wc-image.image) </span>

After the system displays "**The task was successfully executed**", you can view the results on the patrol report page.

<span id="41e84d35"></span>
# Manage patrol reports

You can view the generated patrol report on the patrol report page, including patrol results, exceptional impacts, and handling suggestions.

<span id="eb205d27"></span>
## View patrol report

On the patrol report page, you can view the list of generated patrol reports. Click on **patrol Report ID** or the **View Report** button in the operation column to see the report details.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e220dd73083e4fd0ae7ad2908449c586~tplv-goo7wpa0wc-image.image) </span>

The patrol report displays detailed patrol information, including patrol items, values, severity levels, categories, exceptional impacts, and handling suggestions. You can decide whether to handle an anomaly based on information like patrol values, severity levels, and exceptional impacts.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/517fec5a94c343a58fa69a7fcf26e01d~tplv-goo7wpa0wc-image.image) </span>

<span id="fc249f98"></span>
## Download patrol report

On the patrol report page, click on the **Download Report** button in the operation column to download the current report.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/433034c3862a40bf9033fb5d587fbb90~tplv-goo7wpa0wc-image.image) </span>

You can also click on **Patrol Report ID**, enter the details page, and click **Download**.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c749f1f298394971b1f17ed2c4ffbc6c~tplv-goo7wpa0wc-image.image) </span>

<span id="2b7b140c"></span>
## (Optional) Delete patrol report

If you need to delete a patrol report, you can do so on the patrol report page by clicking the **Delete** button in the operation column.

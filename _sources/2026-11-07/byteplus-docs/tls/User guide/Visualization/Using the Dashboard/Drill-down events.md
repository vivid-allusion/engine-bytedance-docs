---
title: "Drill-down events"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Drill-down_events"
---

Torch Log Service (TLS) supports drill\-down events added to charts on your dashboard to enhance interactions among the charts. This topic describes the basic types of drill\-down events.

<span id="891ae924"></span>
## Background

TLS allows you to set drill\-down events on certain types of charts. After you create and save a drill\-down event on your dashboard, the corresponding action is triggered when you click the specified field on the dashboard. For example, on the UV field in a table, you create a drill\-down event to open the specified topic. After you save the configuration, click a cell in the UV column in the table, then click **Open topic** in the pop\-up window. You are then navigated to the **query and analysis** page of the topic.

The following types of charts support drill\-down events: tables, line charts, column charts, pie charts, histograms, single\-value charts, and statistics charts. The following types of drill\-down events are supported: **Open topic**, **Open dashboard**, and **Custom HTTP links**.

<span id="96bb7daa"></span>
## Configuration description

In the TLS console, after you execute an SQL query on the query and analysis page, select a chart type on the **Chart analysis** tab, then configure a drill\-down action. After the chart is added to the dashboard, you can trigger the drill\-down action on the dashboard.

<span id="7f112e0b"></span>
### **Open topic**

On the **Drill\-down event** tab of a chart, click **Add**, then select a field and configure a drill\-down action. To set an **Open topic** event, configure the following parameters in the pop\-up window:


|Parameter |Description |
|---|---|
|Custom name |Set a name for the drill\-down event. The default name is `Open topic`. |
|Select project |Select the project to which the target topic belongs. |
|Select Topic |Select the target topic. After the drill\-down event is triggered, you are navigated to the page of this topic. |
|Open a new window |Specify whether to open the topic page in a new window. |
|Time range |Specify the default query time range. After the drill\-down effect is triggered and the **query and analysis** page of the topic opens, the system queries data collected within the specified time range. Valid values:<br><br><br>* **Inherit the current query time**: the time range set for querying data for the chart when the drill\-down event is triggered.<br><br>* Relative time ranges such as **Last 1 minute**: a relative time period.<br><br>* Time frame such as **Today**: a time frame. |
|Whether to inherit filtering |Specify whether to inherit the filter conditions of the current dashboard for querying data on the **query and analysis** page of the target topic. When this feature is enabled, the filter conditions of the current dashboard are added to the query statement saved on the **query and analysis** page of the target topic. The filter conditions inherited and the query statements are evaluated by using the `AND` operator. |
|Filter statement |Configure a filter statement. When the **query and analysis** page of the target topic opens, the system uses this filter statement to query and analyze log data.<br><br>Click **Add Variable** to add variables to the filter clause. After a variable is added, the value of the variable is used as a filter condition. All fields in query results can be used as condition variables.<br><br>For example, `Area: ${{Province}} AND Method: ${{Method}}` indicates that the specified values of the Area and Method fields are used as filter conditions. |


<span id="68905bf3"></span>
### **Open dashboard**

On the **Drill\-down event** tab of a chart, click **Add**, then select a field and configure a drill\-down action. To set an **Open dashboard** event, configure the following parameters in the pop\-up window:


|Parameter |Description |
|---|---|
|Custom name |Set a name for the drill\-down event. The default name is `Open dashboard`. |
|Select project |Select the project to which the target dashboard belongs. |
|Select dashboard |Select the target dashboard. After the drill\-down event is triggered, you are navigated to the page of this dashboard. |
|Open a new window |Specify whether to open the dashboard in a new window. |
|Time range |Specify the default query time range. After the drill\-down effect is triggered and the **query and analysis** page of the topic opens, the system queries data collected within the specified time range. Valid values:<br><br><br>* **Inherit the current query time**: the time range set for querying data for the chart when the drill\-down event is triggered.<br><br>* Relative time ranges such as **Last 1 minute**: a relative time period.<br><br>* Time frame such as **Today**: a time frame. |
|Whether to inherit filtering |Specify whether to inherit the filter conditions of the current dashboard for querying data on the target dashboard. When this feature is enabled, the filter conditions of the current dashboard are added to the query statement saved on the **query and analysis** page of the target topic. The filter conditions inherited and the query statements are evaluated by using the `AND` operator. |
|Whether to inherit variables |Specify whether to inherit the variables of the current dashboard for querying data on the target dashboard. |
|Filter statement |Configure a filter statement. When the target dashboard opens, this filter statement is added to the target dashboard. The logic relationship among filter conditions is `AND`.<br><br>Click **Add Variable** to add variables to the filter clause. After a variable is added, the value of the variable is used as a filter condition. All fields in query results can be used as condition variables.<br><br>For example, `Area: ${{Province}} AND Method: ${{Method}}` indicates that the specified values of the Area and Method fields are used as filter conditions. |
|Dynamic variable |Specify the dynamic variables that you want to add to the target dashboard.<br><br>Click **Add Dynamic variable**, then set variable names and the columns in which the variable values reside. TLS dynamically synchronizes variable values from the specified columns to the target dashboard.<br><br>You can add up to five dynamic variables. |
|Static variable |Specify the static variables that you want to add to the target dashboard.<br><br>Click **Add Static variable**, then set variable names and the columns in which the variable values reside. TLS automatically synchronizes variable values from the specified columns to the dashboard.<br><br>You can add up to five static variables. |


<span id="1299b45e"></span>
### **Custom HTTP links**

On the **Drill\-down event** tab of a chart, click **Add**, then select a field and configure a drill\-down action. To add a **Custom HTTP links** event, configure the following parameters in the pop\-up window:


|Parameter |Description |
|---|---|
|Custom name |Set a name for the drill\-down event. The default name is `Custom HTTP links`. |
|agreement |Specify the protocol for accessing the destination URL. |
|Link address |Specify the destination URL.<br><br>You can specify a URL with variables. All fields in query results can be used as condition variables. |
|Whether to transcode |Specify whether to encode the query parameters in the URL. |
|Open a new window |Specify whether to open the topic page in a new window. |


<span id="9bb4788f"></span>
## **Configuration examples**

Assume that a topic named user\-log in the project named user\-log\-project is used to store access logs of a website. To monitor the access metrics of the website, you must create a dashboard. In this example, the dashboard is named `AccessMonitoringDashboard`. You can add various charts to the dashboard for displaying the website access metrics, such as the list of the cities where the visitors are located, the list of the top 5 most\-visited pages, and the proportion of each access method.

You can also add drill\-down events to the charts on the dashboard. For example, set an **Open dashboard** event on the table that displays the IP list to open the line chart that displays page view (PV) trends in the dashboard. The PV count is indicated by the PV field, and the line chart displays PV trends over time. After you complete and submit the configurations, click a IP address in the table. Then, you are navigated to the chart displaying the PV trend of the corresponding IP address.

Perform the following steps to set up the drill\-down event:


1. Create a dashboard and name it `AccessMonitoringDashboard`. Then, add a line chart and name it `PVTrend`.

   The `PVTrend` line chart displays PV trends over time. The query statement is as follows:

   ```SQL
   * | SELECT date_format(__time__, 'Y-M-d HH:mm') AS time , COUNT(*) as PV group by time order by time
   ```
   

   The configurations of the line chart are as follows:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c6fff76ccaed4de0a21c24772acdf046~tplv-goo7wpa0wc-image.image) </span>

2. Add a table to the `AccessMonitoringDashboard` dashboard and name it `IPList`.

   The `IPList` table is used for querying the PV count of each IP address. The query statement is as follows:

   ```SQL
   * | SELECT IP, COUNT(*) as PV group by IP
   ```
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6b9c55d704b64953ab4c3ca1b6e06489~tplv-goo7wpa0wc-image.image) </span>

3. Set up a drill\-down event on the `IPList` table and name the event `ViewCurrentIPData`.

   The event configurations are as follows.

   * Select `AccessMonitoringDashboard` from the **Select dashboard** drop\-down list.

   * Set the following filter statement: `IP:${{IP}}`.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/78abf34f517d4ad5a2b87278d9d34fef~tplv-goo7wpa0wc-image.image) </span>

4. Verify the action of the drill\-down event.

   * In the `IPList` table, click a IP address, then select **ViewCurrentIPData**. TLS opens the `AccessMonitoringDashboard` dashboard and adds a filter condition `IP:10.0.0.xx` to the dashboard.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b4d93fe81d36423f8f21a5a84ed188f1~tplv-goo7wpa0wc-image.image) </span>

   * The `PVTrend` chart displays the trend of PVs from the IP over time.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fa344a6340fb421c8bc6ff3a58193f80~tplv-goo7wpa0wc-image.image) </span>

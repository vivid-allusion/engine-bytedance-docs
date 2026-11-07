---
title: "Configure custom charts"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/Configure_custom_charts"
---

You can customize the range of charts displayed on the security overview page, configuring the corresponding preset charts according to different functional modules that need to be displayed. If you have configured a dashboard in the log service, you can also add the dashboard to the security overview page for real\-time viewing of dynamic analysis results.

<span id="7224a5f4"></span>
## Show or hide preset charts

The security overview page includes multiple functional modules, each equipped with corresponding preset charts. The system defaults to displaying all preset charts, and you can flexibly adjust the display status of each chart according to actual needs.


1. Log in to [Web Application Firewall Console](https://console.byteplus.com/waf/dashboard).

2. Select the region of your instance in the top menu bar.

3. Select **Security Overview** from the left navigation.

4. Click **Configure Charts**.

5. Select the functional module that needs to be configured, and check the charts that need to be displayed; unchecked charts will not be displayed on the overview page.

   For example, the attack overview module supports displaying the following charts. If you do not need to display the relevant charts, you can uncheck the box.

6. If you still need to set up a log dashboard, you can refer to [add the log dashboard to the security overview page](https://docs.byteplus.com/en/docs/waf/Configure_custom_charts#4a8a64aa).


<span id="4a8a64aa"></span>
## Add a custom log dashboard

The log service dashboard is one of the visualization features provided by the log service, a collection of monitoring charts for log data analysis. You can create the corresponding dashboard in the log service console and add charts, then add it to the web application firewall's security overview page to facilitate monitoring of the corresponding log metrics, meeting diverse business monitoring needs.

<span id="b2357a5f"></span>
### Scenario example

Under the attack overview module on the security overview page, add a chart to aggregate and display the number of intercepted requests by client IP and domain name. The following are the specific steps to achieve the display of this chart:

<span id="392557f8"></span>
### Step 1: Create a dashboard


1. Log in to [the log service console](https://console.byteplus.com/tls/).

2. Select the region where the log service is located from the top menu bar.

3. In the left navigation bar, select **Common Functions** \> **Dashboard**

4. Click **+** Create Dashboard.

5. Select **Create Blank Dashboard**, then click **Next: Configure Dashboard**.

6. Configure the dashboard parameters.



|Parameter |Description |
|---|---|
|Dashboard name |Set the dashboard name, here set as `Attack Overview`. |
|Description |Enter a brief description of the dashboard. |
|Log project |Select the log project to which the dashboard belongs, generally named `tls-waf-project-****`, which is a log resource dedicated to the Web application firewall. |



7. Click **Finish: Create Dashboard**.


<span id="9255e84a"></span>
### Step 2: Add a chart to the Dashboard

After creating the dashboard, you need to add the statistical charts under the same log item to the dashboard in order to view the dynamic log analysis results in real time through the dashboard.


1. Log in to the [Log Service Console](https://console.byteplus.com/tls/).

2. Select the region where the log service is located in the top menu bar.

3. In the left navigation bar, select **Common Functions** \> **Dashboard**.

4. Select the created dashboard from the dashboard list.

5. In the upper right corner of the dashboard page, click **Add ** **Chart**.

6. Enter the following retrieval analysis statement and click **Start Analysis**.

   ```SQL
   ActionType:"block" |
   SELECT MatchedHost, ClientIP, COUNT(*) AS count
   GROUP BY MatchedHost, ClientIP
   ORDER BY count DESC
   ```
   

   Where:

   * `ActionType:"block"`: Filter the logs where the action is blocked.

   * `SELECT MatchedHost, ClientIP, COUNT(*) AS count`: Count the number of logs in each group and name the log count as count.

   * `GROUP BY MatchedHost, ClientIP`: Group by domain name and client IP.

   * `ORDER BY count DESC`: Sort the logs in descending order by count.

7. Set chart parameters on the right side of the interface, such as chart type, title, style, and other parameters.

8. After confirming, click **Apply to Dashboard** in the upper right corner.

   The current log dashboard page will display the corresponding charts.

9. Save this dashboard.


<span id="b25006ed"></span>
### Step 3: Add the log dashboard to the Security Overview page

The Security Overview page supports adding log dashboards for various functional modules. Before adding the dashboard, please ensure you have selected the specific functional module you want to operate on.


1. Log in to [Web Application Firewall Console](https://console.byteplus.com/waf/dashboard).

2. In the top menu bar, select the region of your instance.

3. In the left navigation, select **Security Overview**.

4. Click **Configure Chart**.

5. Select the functional module to configure, and then choose [Step One: Create Dashboard](https://docs.byteplus.com/en/docs/waf/Configure_custom_charts#392557f8) to create the dashboard you have created.

6. Click **Confirm**.


<span id="12d1806b"></span>
### Configuration results

After adding the dashboard, you can return to the security overview page to view the configuration results. 

For example, based on the charts created in this document, click the **Attack Overview** tab, scroll to the bottom of the page, and you will see the chart query results added in [Step Two: Add Chart to Dashboard](https://docs.byteplus.com/en/docs/waf/Configure_custom_charts#9255e84a).

<span id="11ad274a"></span>
### Related operations


* **Adjust Domain Range and Time Interval**: You can set the query domain range and time interval at the top of the security overview page.

* **Adjust Dashboard Layout** or **Export Custom Dashboard**:

   1. Log in to the [Log Service Console](https://console.byteplus.com/tls/).

   2. Select the region where the log service is located from the top menu bar.

   3. In the left navigation bar, select **Common Functions** \> **Dashboard**.

   4. Select the dashboard created in Step One.

   5. Click the three dots in the upper right corner of the chart `···` to edit the dashboard style or download the dashboard.

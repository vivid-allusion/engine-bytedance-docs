---
title: "Configure data classification chart"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Configure_data_classification_chart"
---

The log service provides data transformation functions to convert query and analysis results, currently only supporting data classification. The data classification function supports categorizing data based on specified fields and counts the quantity for each category.

This section introduces how to configure data classification charts in existing dashboards.

<span id="0466c601"></span>
## Prerequisites

When configuring data classification charts, relevant conditions in the [notes](https://docs.byteplus.com/docs/tls/chart_overview#.5rOo5oSP5LqL6aG5) must be met.

<span id="6ddc8d75"></span>
## Configure data classification chart steps


1. Log in to the [Torch Log Service console](https://console.byteplus.com/tls).

2. On the top navigation bar, select the region where the log service is located.

3. In the left navigation bar, select **Common Features** \> **dashboard**.

4. Select the dashboard to add a chart, click **Add Chart**, then click **Create Chart**.

5. Select the retrieval time range.

6. Under the **query and analysis** tab, add data sources as needed, select the target log topic, and enter the query and analysis statement.

7. Under the **Data Transformation** tab, click **Add Transformation**, then click **Data Classification**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Data transformation also supports enabling data classification and data aggregation functions below the chart analysis on the query and analysis page.   </div>
   

8. Set the following configurations, then click **Start Analysis**.

   
   |Parameter |Description |
   |---|---|
   |Row field |Select the target field as the row field. |
   |Column field |Select the field used for classification as the column field. |
   |Value field |Select a numeric field. |
   |Null value |When null values appear in the data, they will be replaced with the value you specify here, defaulting to null. |
   

9. After completing the chart settings, click **Save dashboard**. Or click **Apply to dashboard**, preview the effect, then click **Save** again.


<span id="fc8e48d5"></span>
## Configuration example

Count the number of logs corresponding to different level values every 5 minutes. By default, the line chart does not support displaying the number of logs by level value categories. By configuring classification rules in data transformation, the system divides the query and analysis results into three categories based on level values (info, warning, error) and displays the numbers for each category in the line chart.


* Query and analysis configuration<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_eb479f534846ca36d0a796485699411f.png) </span>

   ```SQL
   *| SELECT DATE_FORMAT(__time__ - __time__ % 300000, 'Y-M-d HH:mm') AS time, COUNT(*) AS count, level GROUP BY time, level ORDER BY time
   ```
   

* Data transformation configuration

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0f7d358a1f5230ddc354c217c63120f9.png) </span>

* Query and analysis results (table)

   After adding data classification operations, Log Service extracts the level values (info, warning, error) as headers and categorizes the number of logs for each level value.

   * Before data transformation

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_90ae96a700b064ad293c22b5eff11149.png) </span>

   * After data transformation

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b54e43c3960c090bf440c0675746150c.png) </span>

* Query and analysis results (line chart)

   After adding data classification, the log service supports displaying the number of logs for each level value by category.

   * Before data transformation

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ddea2cec0270bd70b6fee13b05cb7504.png) </span>

   * After data transformation<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0bc8c5c63f47a2386a6149525c0f38ac.png) </span>


&nbsp;

&nbsp;

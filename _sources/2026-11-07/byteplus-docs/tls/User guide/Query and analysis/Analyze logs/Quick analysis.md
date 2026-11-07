---
title: "Quick analysis"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Quick-analysis-2"
---

When you query log data from Torch Log Service (TLS), you can use the quick analysis feature to instantly view information on the top five values of a field in a specific time period. This topic describes how to use the quick analysis feature.

<span id="Background"></span>
## Background

The quick analysis feature for fields is displayed in the sidebar of the query and analysis page. To view the top five values of a field in a recent time period, use the feature to perform query in one click without query statements. The quick analysis feature can be used when you want to preview the types and proportion of field values. For example, you can view the proportion of various requests and the top five API actions accessed.

<span id="97d25e4e"></span>
## Before you begin

Configure indexes and enable the statistics feature for fields on which you want to perform quick analysis. For more information, refer to [Configure indexes](https://docs.byteplus.com/docs/tls/Configure-indexes-2).

<span id="98cf9440"></span>
## Procedure


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the left\-side navigation pane, choose **Common functions** \> **Query and analysis**.

3. Select a project and a topic.

4. Specify a time range.

   The default time range is 5 minutes. You can change the time range as needed. If the specified time range exceeds the retention period of logs, the expired and deleted data cannot be queried.

5. In the left\-side sidebar, click the name of a field.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The <strong>Other fields</strong> area displays the fields in the index configuration that have not enabled the statistical function. For example, in the following figure, the statistics feature is not enabled for the <code>__tag____client_ip__</code> field. For information on how to enable the statistics feature, refer to <a href="https://docs.byteplus.com/docs/tls/Configure-indexes-2">Configure indexes</a>.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/db9e207a369c41e68d95918e414a656a~tplv-goo7wpa0wc-image.image) </span>

   * The pop\-up window displays the top five values of the field by proportion and the corresponding proportion in the specified time range.

   * Click the expand arrow of a value, then you can add the value to query conditions to find logs with this value from the query results. Alternatively, you can exclude this value from the query results.

   * Click **View the field distribution** in the chart to view the proportion of each field in a pie chart. Alternatively, you can modify chart configurations to display quick analysis results in another chart type.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a36cae15abea4bd6be8701e03b68b03f~tplv-goo7wpa0wc-image.image) </span>

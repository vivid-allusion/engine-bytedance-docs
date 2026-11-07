---
title: "Create a line chart with double Y-axes"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Create-a-line-chart-with-double-y-axis"
---

If you need to use a line chart to display different kinds or different scales of data, you can add multiple Y\-axes to the line chart to display different data. This topic describes how to create a line chart withdouble Y\-axis.

## Background Information

TLS Line Chart supports adding multiple Y\-axes to display data of different types or levels. For example, you can show the trend of PV and UV in a line chart. Since the orders of magnitude of PV and UV are usually quite different, when the two share a Y\-axis, the UV trend shown in the line chart is not clear. At this time, you can add a double Y\-axis, add a suitable Y\-axis for PV and UV respectively according to their orders of magnitude, so as to better display their changing trends.

## Prerequisites

* The project and topic have been created and the log data has been successfully collected.

* Indexes are created. For more information, see [Configure indexes](https://docs.byteplus.com/docs/tls/Configure-indexes-2).

## Steps

1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the left\-side navigation pane, choose **Common Functions** \> **Dashboard**.

3. Find the target dashboard, then click the name of the dashboard.

4. In the dashboard, click **Add chart**.

5. In the destination chart, click **Create chart**.

6. In the **Query analysis** area, select the target topic, enter the following query and analysis statement, and then click **Start analyzing**.

   ```SQL
   * | SELECT DATE_FORMAT(__time__ - __time__ % 300000, 'Y-M-d HH:mm') AS time, COUNT(*) AS PV, COUNT(DISTINCT(UID)) AS UV GROUP BY time ORDER BY time
   ```

7. In the **Chart settings** area, set the line chart.

   On **Query and analysis field** area, set the **X\-axis field source column** to `time`, and set the **Y\-axis field source column** to `PV`, `UV`. After the setting is completed, the change trend of PV and UV will be displayed on the page.

8. Add field configuration.

   In the **Field Configuration** tab, add a Y\-axis for the `UV` column. For specific parameter descriptions, see [Field configuration](https://docs.byteplus.com/docs/tls/Line_chart#.5a2X5q616YWN572u).

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/98db653a4928456ab4cb9e826958fbc0~tplv-goo7wpa0wc-image.image)

   After the setup is complete, the line chart will have two Y axes, and the two Y axes are of different orders of magnitude, the left Y axis for PV and the right Y axis for UV, as shown in the figure below.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9cc820db26e841cd9c5d63bb6f482db0~tplv-goo7wpa0wc-image.image)

9. Click **Apply to dashboard** to save the chart configuration.

10. Click **Save** to save the dashboard.

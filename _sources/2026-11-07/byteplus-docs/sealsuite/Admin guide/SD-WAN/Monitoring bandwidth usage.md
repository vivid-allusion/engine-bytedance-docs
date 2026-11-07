---
title: "Monitoring bandwidth usage"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/monitoring-bandwidth-usage"
---

The **Monitoring** page provides a real\-time dashboard for tracking bandwidth consumption across your **Branch Gateways**, **Cross\-Border Connections**, and **Cloud Access Gateways**. You can filter data by time granularity, date range, and other criteria to view detailed usage metrics and peak values, or export the results.

<span id="d0f1726c"></span>
## Prerequisites

To monitor cross\-border bandwidth, you must have an active subscription for the cross\-border bandwidth feature.

<span id="82850fea"></span>
## **Monitoring branch gateway bandwidth**

This section allows you to monitor real\-time data for your branch gateways, with options to filter by region and view upload/download usage over specific time periods.

> Note: Billing is based on the higher of the peak upload or download usage.


1. Log in to the Admin Console.

2. From the left navigation bar, go to **SD\-WAN** \> **Monitoring**.

3. Select the **Branch Gateway** tab and use filters to refine your view.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f7afccb9bd8d46c78b5b99931477e33f~tplv-goo7wpa0wc-image.image) </span>

4. After applying filters, the chart will display detailed bandwidth metrics based on your selected time granularity (e.g., peak usage for every 5\-minute interval).

   * Hover over any point on the chart to see the specific peak bandwidth value for that timestamp.

   * The table below the chart shows detailed metrics. You can sort the upload and download columns.

5. (Optional) Click **Refresh** to fetch the latest data.

6. (Optional) Click **Export List** to download the data. You can choose to export either the filtered results or the entire dataset.


<span id="fd351a29"></span>
## **Monitoring cross\-border bandwidth**

This section allows you to monitor real\-time data for your cross\-border connections.

> Note: Billing is based on the higher of the peak upload or download usage.


1. Log in to the Admin Console.

2. Go to **SD\-WAN** \> **Monitoring**.

3. Select the **Cross\-border Bandwidth** tab and use filters to refine your view.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0b8ce2b4327c4b4daa1b9a3d9530b63c~tplv-goo7wpa0wc-image.image) </span>

4. The chart and table will display detailed bandwidth usage for the selected connection.

   * The data points represent the peak usage within each interval of the chosen time granularity (e.g., the highest 5\-minute peak within a 1\-hour interval).

   * Hover over any point to see the specific peak value.

5. (Optional) Click **Refresh** to fetch the latest data.

6. (Optional) Click **Export List** to download the data.


<span id="cf048343"></span>
## **Monitoring cloud access gateway bandwidth**

This section allows you to monitor bandwidth consumption for individual users connected through the Cloud Access Gateway.


1. Log in to the Admin Console.

2. Go to **SD\-WAN** \> **Monitoring**.

3. Select the **Cloud Access Gateway** tab and use filters to refine your view.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b692ea6869104df3b01f18b14a78a55c~tplv-goo7wpa0wc-image.image) </span>

4. The chart and table will display the selected employee's detailed bandwidth usage.

   * Hover over any point to see the peak value for that timestamp.

5. (Optional) Click **Refresh** to fetch the latest data.

6. (Optional) Click **Export List** to download the data.

---
title: "Configure data analysis charts"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Configure_data_analysis_charts"
---

Log Service supports displaying query analysis results in charts, with various configuration options:


* Configure charts on the query and analysis page. For details, see [analyze logs](https://docs.byteplus.com/docs/tls/Analyze-logs-2).

* Add charts to an existing dashboard.


This section explains how to add data analysis charts to an existing dashboard.

<span id="aea37a3d"></span>
## Prerequisites

When adding charts to the dashboard, you must meet the relevant conditions in [precautions](https://docs.byteplus.com/docs/tls/chart_overview#.5rOo5oSP5LqL6aG5).

<span id="94e1b11d"></span>
## Steps to configure data analysis charts


1. Log in to the [Torch Log Service console](https://console.byteplus.com/tls).

2. On the top navigation bar, select the region where the log service is located.

3. In the left navigation pane, select **common functions** \> **dashboard**.

4. Select the dashboard where you want to add a chart, then click **add chart**.

   * Click **create chart** to proceed to the next step.

   * Click **import chart** to import charts created in other dashboards as prompted, then finish the operation.

5. Select the time range for the query.

6. Under the **query and analysis** tab, select the target log topic, enter the query and analysis statement, then click **start analysis**.

   * The system displays query and analysis results in a table at the top of the current page.

   * Support configuring other chart types to display query and analysis results in the **Chart Settings** on the right side of the page.

7. After setting up the chart, click **Save dashboard**. Or click **Apply to dashboard**, preview the effect, then click **Save** again.

   You can also add multiple query and analysis operations and use data aggregation to combine the results into a single statistical chart. For detailed information on data aggregation, see [Configure data aggregation charts](https://docs.byteplus.com/docs/tls/Statistical-chart-related-operations).


<span id="d66fdf7f"></span>
## Related actions


|Actions |Description |
|---|---|
|Rename |The system names query and analysis operations by default using uppercase letters in order, such as A, B, etc.<br><br>You can also click the edit button to rename. |
|View data source |Click **View data source** to see the query and analysis results. |
|Copy query and analysis |Click the copy button to duplicate a new query and analysis. |
|Delete query and analysis |Click the delete button to remove the current query and analysis. |
|Sort query and analysis |Hover over the sort button, hold the mouse button, and drag to reorder the current query and analysis. |


&nbsp;

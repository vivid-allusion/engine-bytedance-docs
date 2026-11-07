---
title: "Add charts to a dashboard"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Adding_charts_to_a_dashboard"
---

After you create a dashboard, you must add charts created in the same project to the dashboard. You can then view the dynamic analysis results.

You can use one of the following methods to add a chart to a dashboard:


* Saving a chart to the dashboard.

* Adding a chart to the dashboard.


<span id="注意事项"></span>
## Precautions


* Up to 50 charts can be added to a dashboard.

* After you add a chart to a dashboard and **The current query result** is empty is displayed in the chart, verify whether the chart can access log data or whether a correct query statement is configured for the chart.

* After a chart is added to a dashboard, you can modify or copy the chart as needed. For more information, refer to [Manage dashboards](https://docs.byteplus.com/docs/tls/Managing_dashboards).


<span id="保存图表到仪表盘"></span>
## Saving a chart to a dashboard


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the left\-side navigation pane, choose **Common functions** \> **Query and analysis**.

3. Select a project and a topic.

4. Type the query and analysis statement in the input box, then click **Search**.

   Torch Log Service (TLS) supports multiple types of charts. For more information on how to configure a chart, refer to [Chart overview](https://docs.byteplus.com/docs/tls/chart_overview).

5. On the right\-side of the page, click **Add to dashboard**.

6. Specify the dashboard to which you want to add the chart.

   
   |Parameter |Description |
   |---|---|
   |Chart name |The name of the chart. |
   |Target Dashboard |The dashboard to which you want to add the chart.<br><br><br>* **Existing Dashboard**: add the chart to an existing dashboard.<br><br>* **New Dashboard**: create a new dashboard and add the chart to the dashboard. |
   |Dashboard |The name of the dashboard. |
   |Description |If you set the value of **Target Dashboard** to **New Dashboard**, describe the new dashboard. |
   

7. Click **OK**.

   When you are navigated to the dashboard page, you can view all charts that are added to the dashboard. In each chart, the query time range and query statement specified for the chart is displayed.


<span id="在仪表盘中添加图表"></span>
## Adding a chart to a dashboard


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the left\-side navigation pane, choose **Common functions** \> **Dashboard**.

3. In the left list, find the target dashboard.

4. On the upper\-right corner of the dashboard page, click **Add chart**.

5. Click **Create chart**.

6. Enter a query statement, then configure a chart.

   Torch Log Service (TLS) supports multiple types of charts. For more information on how to configure a chart, refer to [Chart overview](https://docs.byteplus.com/docs/tls/chart_overview).

7. Set a name for the chart. On the upper\-right corner of the **Edit chart** page, click **Apply to dashboard**.

8. (Optional) Adjust the location and size of the chart.

   Drag the chart to adjust the chart location or drag the lower\-right corner of the chart to adjust the chart size.

9. On the upper\-right corner of the page, click **Save**.


<span id="相关操作"></span>
## Related operations

[Manage dashboards](https://docs.byteplus.com/docs/tls/Managing_dashboards)

---
title: "Data Monitoring"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ALB-Monitoring"
---

You can view monitoring data for ALB instances and listeners through the ALB console or the CloudMonitor console. For a detailed description of ALB monitoring metrics, see [ALB monitoring metrics.](https://console.byteplus.com/cloud_monitor/docs?namespace=VCM_ALB)

<div data-tips="true" data-tips-type="tip">Tip</div>



* <div data-tips="true" data-tips-type="tip">CloudMonitor collects monitoring metric data for an ALB every 30 seconds, and the data represents the average value over that 30‑second period. For example, the new connection count displayed by CloudMonitor is the average number of new connections per second over the 30\-second interval.</div>


* <div data-tips="true" data-tips-type="tip">IAM cannot view ALB monitoring data directly. To enable this, the root user that the IAM user belongs to must grant CloudMonitor permissions to the IAM user.</div>


* <div data-tips="true" data-tips-type="tip">You can also view ALB monitoring data in the <a href="https://console.byteplus.com/cloud-monitor/overview">CloudMonitor console</a> and configure automated alerts. For details, see <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy">Cloud Monitor guidance documentation</a>.</div>



<span id="ui2orX07"></span>
## Prerequisites


* An ALB instance has been created and configured with listeners.

* [BytePlus CloudMonitor](https://console.byteplus.com/cloud-monitor/overview) service has been activated.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures


1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. In the top menu bar, select the target project and region.

3. In the left navigation pane, select **Instance**.

4. Click the monitor icon to the right of the target ALB instance.

   * **View ALB instance**: On the **Monitoring information \> Instance** tab, you can select a specific time range for data statistics. The system will then aggregate and display monitoring data at the instance level based on the selected time range.

   * **View listener:**  On the **Monitoring information \> Listener** tab, select the listener you want to view from the left panel. You can select a specific time range for data statistics. The system will collect and display monitoring data at the instance level based on the selected time range.

   * **View** ** server group**: On the **Monitoring information \> server group** tab, select the server group you want to view from the left panel. You can select a specific time range for data statistics, and the system will aggregate and display the monitoring data by server group based on the selected time range.

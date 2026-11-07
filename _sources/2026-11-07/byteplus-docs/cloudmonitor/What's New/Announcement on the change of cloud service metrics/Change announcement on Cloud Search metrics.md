---
title: "Change announcement on Cloud Search metrics"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Change_announcement_on_Cloud_Search_metrics"
---

The Cloud Monitor team will soon adjust the monitoring metrics for Cloud Search, aiming to provide you with a more accurate and comprehensive monitoring experience.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For cloud product metrics and details, see <a href="https://console.byteplus.com/cloud_monitor/docs">Cloud product metrics query</a>.</div>


<span id="L7J3Nvj8"></span>
## May 2026


|MetricName |SubNamespace |Types |Descriptions |Impacts |
|---|---|---|---|---|
|IndexOps |operation |Unit change |The metric unit changes from "none" to `Count/s`. |* This change does not affect the normal operation of cloud product instances and your business.<br><br>* Monitoring dashboards will display data based on the updated metrics.<br><br>* Alert rules remain unchanged and active. Alert notifications will be sent according to the settings in alerting rules. |
|MergeOps |||||
|QueryOps |||||
|NodeIndexOPS |||||
|NodeMergeOPS |||||
|NodeQueryOPS |||||


<span id="eyX5EJlm"></span>
## March 2025


|MetricName |SubNamespace |Types |Descriptions |Impacts |
|---|---|---|---|---|
|ESCloudDiskIOUtil |resource |Usage deprecation |* Before the change, the usage purpose of the metric was alerting.<br><br>* After the change, the usage purpose of the metric is none. |* This change does not affect the normal operation of cloud service instances and your business.<br><br>* Monitoring dashboards can still display data based on metrics.<br><br>* If an exclamation mark (!) is added before an existing alert rule, it indicates that the alert rule contains an invalid metric, and the alert will no longer be triggered. You need to modify the metric in the alert rule.<br><br>* If you do not remove or update the metric for an existing alert template, you cannot save the template. |

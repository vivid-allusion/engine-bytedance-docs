---
title: "Change log of CloudWAN metrics"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Change_log_of_CloudWAN_metrics"
---

The Cloud Monitor team will soon adjust the monitoring metrics for CloudWAN, aiming to provide you with a more accurate and comprehensive monitoring experience.

> **tip**

> For cloud product metrics and details, see [Cloud product metrics query](https://console.byteplus.com/cloud_monitor/docs).

## October 2026

|MetricName |SubNamespace |Type |Description |Impact |
|---|---|---|---|---|
|cn_region_in_byte |core_network_region_metrics |Unit change |The metric unit has changed from `Bytes(SI)` to<br><br>`Bytes(IEC)`. |* This change does not affect the normal operation of cloud product instances and your business.<br><br>* Monitoring dashboards will display data based on the updated metrics.<br><br>* Alert rules remain unchanged and active. Alert notifications will be sent according to the settings in alert rules. |
|cn_region_out_byte |||||
|cn_region_blackhole_byte |||||
|cn_region_route_miss_byte |||||
|cn_az_in_byte |core_network_az_metrics ||||
|cn_az_out_byte |||||
|cn_az_blackhole_byte |||||
|cn_az_route_miss_byte |||||
|cn_attachment_in_byte |core_network_attachment_metrics ||||
|cn_attachment_out_byte |||||
|cn_attachment_blackhole_byte |||||
|cn_attachment_route_miss_byte |||||
|cn_attachment_in_rl_drop_byte |||||
|cn_attachment_out_rl_drop_byte |||||
|cn_attachment_az_in_byte |core_network_attachment_az_metrics ||||
|cn_attachment_az_out_byte |||||
|cn_attachment_az_blackhole_byte |||||
|cn_attachment_az_route_miss_byte |||||
|cn_attachment_az_in_rl_drop_byte |||||
|cn_attachment_az_out_rl_drop_byte |||||

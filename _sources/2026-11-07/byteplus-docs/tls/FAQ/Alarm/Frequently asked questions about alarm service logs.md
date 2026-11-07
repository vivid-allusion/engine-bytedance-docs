---
title: "Frequently asked questions about alarm service logs"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Alarm_service_log_FAQs"
---

<span id="c66e1570"></span>
## How to query and analyze alert service logs?

After you create an alarm policy, TLS automatically enables the alarm service log feature and records the entire lifecycle of alarms as log entries. All alarm service logs are stored in the `tls_service-project` project under the `tls_alarm-log` log topic. For detailed information about alarm service logs, please refer to [alarm policy execution log](https://docs.byteplus.com/docs/tls/service_log_fields#275238d1) and [alarm event log](https://docs.byteplus.com/docs/tls/service_log_fields#6487bd15).

You can view and analyze alarm service logs in the `tls_alarm-log` log topic. For example, you can execute the following statement to count the number of times each monitoring policy triggered an alarm in the past day.


* Query and analysis statement

   ```SQL
   ReachTrigger:true | SELECT ProjectName, AlarmName, count(*) AS num GROUP by ProjectName, AlarmName ORDER BY num DESC
   ```
   

* Query and analysis results

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d6eedb4a09aa616489c48afa07a1ac02.png) </span>


<span id="ef3290c4"></span>
## Alarm service logs are stored for only 30 days. How can the storage period be extended?

Alarm service logs include [alarm policy execution logs](https://docs.byteplus.com/docs/tls/service_log_fields#275238d1) and [alarm event logs](https://docs.byteplus.com/docs/tls/service_log_fields#6487bd15), which are all stored in the `tls_service-project` project under the `tls_alarm-log` log topic. This log topic does not incur basic fees such as storage, and its log storage period is fixed at 30 days and cannot be modified. If you want to store logs for a longer period, you can use data transformation to copy service logs to another log topic and set a longer log storage period.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Data transformation and storing data to other log topics will incur costs such as data transformation traffic and log storage space. </div>

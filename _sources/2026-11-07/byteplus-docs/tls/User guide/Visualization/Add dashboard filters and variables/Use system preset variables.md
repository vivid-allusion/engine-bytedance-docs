---
title: "Use system preset variables"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Using_system_preset_variables"
---

This chapter introduces how to use system preset variables in the Log Service dashboard with related examples.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Log data has been collected and indexes configured. For details, refer to [Quick Start](https://docs.byteplus.com/docs/tls/getting_started_collecte_logs).

* The dashboard has been created and statistical charts added to it. For details, refer to [Creating a dashboard](https://docs.byteplus.com/docs/tls/Creating_a_dashboard) and [Adding charts to the dashboard](https://docs.byteplus.com/docs/tls/Adding_charts_to_a_dashboard).


<span id="2557463e"></span>
## System preset variables

Log Service provides preset variables such as `__from` and `__to`, which can be used directly in the dashboard’s query and analysis statements, chart titles, and text boxes without creation.

<span id="762b4da0"></span>
### Time range variables

After adding the time range variable, the system will display the start time based on the selected time range.


|Variable |Description |
|---|---|
|`${{__from}}` |Start time of query and analysis.<br><br>When used with time_format, supports formatting timestamps. For details, refer to [Format usage](https://docs.byteplus.com/docs/tls/Adding_filters_to_a_dashboard#59c7a6b6). |
|`${{__to}}` |Query and analysis result time.<br><br>Supports formatting timestamps when combined with time_format. For details, see [Format usage](https://docs.byteplus.com/docs/tls/Adding_filters_to_a_dashboard#59c7a6b6). |


<span id="d35bd2c6"></span>
### Time length variable

After adding the time range variable, the system will calculate the time length based on the selected time range.


|Variable |Description |
|---|---|
|`${{__range}}` |Duration in milliseconds. Equivalent to `${{__range_ms}}`. |
|`${{__range_s}}` |Time length in seconds. |
|`${{__range_ms}}` |Time length, unit is milliseconds. |


<span id="f69b568c"></span>
### Time granularity variable

After adding the granularity variable, the system will automatically adjust the time granularity according to the selected time range.


|Variable |Description |
|---|---|
|`${{__interval}}` |Time granularity variable, the default unit is milliseconds.<br><br>Supports formatting time intervals and rounding up to the largest integer time unit when combined with duration_round_format. For detailed explanation, refer to [Format usage](https://docs.byteplus.com/docs/tls/Adding_filters_to_a_dashboard#59c7a6b6). |


For example, use the `${{__interval}}` variable in query and analysis statements.


* Query and analysis statement settings

   ```SQL
   * | SELECT $__timeGroup(__time__, ${{__interval}}) AS time, count(*) AS PV GROUP BY time ORDER BY time
   ```
   

* Query and analysis results

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6bd08cc5d686dc78736a9e060ea1123c.png) </span>


<span id="61d537f1"></span>
### Region variable

After adding the region variable, the system will display region information based on the current dashboard's location.


|Variable |Description |
|---|---|
|`${{__dashboard_region}}` |Region variable, displays the region of the current dashboard. |
|`${{__dashboard_host}}` |Domain variable, shows the domain of the current Log Service console. |


For example, in the **open HTTP link** interaction event, use the `${{__dashboard_region}}` and `${{__dashboard_host}}` variables to concatenate the log service dashboard page URL. The link address configuration example is as follows:

```Plain
https://${{__dashboard_host}}/tls/region:tls+${{__dashboard_region}}/v2/dashboard
```


<span id="9fead1e0"></span>
## Related actions

After adding filters and variables, you can easily use, modify, or delete them on the dashboard. For detailed instructions, refer to [Dashboard Common Operations](https://docs.byteplus.com/docs/tls/Managing_dashboards).

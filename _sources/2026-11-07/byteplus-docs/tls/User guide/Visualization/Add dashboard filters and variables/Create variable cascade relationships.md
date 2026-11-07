---
title: "Create variable cascade relationships"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Creating_variable_cascade_relationships"
---

After creating variables, Log Service supports configuring cascade relationships among variables to clarify dependencies between them. This section explains how to create variable cascade relationships and use Format.

## Prerequisites

* Log data has been collected, and indexes have been configured. For details, see [Getting Started](https://docs.byteplus.com/docs/tls/getting_started_collecte_logs).

* A dashboard has been created, with statistical charts added. For details, see [Creating a dashboard](https://docs.byteplus.com/docs/tls/Creating_a_dashboard) and [Adding charts to a dashboard](https://docs.byteplus.com/docs/tls/Adding_charts_to_a_dashboard).

* Dashboard variables have been created.

## Create variable cascade relationships

Take creating a cascade relationship between the name variable and the email variable as an example.

1. Create the name variable.

2. Create the email variable.

   When creating the email variable, reference the name variable in the variable value.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a67d145794ac46dde9209b016a2e8c92.png)

3. Use the variables.

   There is a cascade relationship between the name variable and the email variable. After selecting the name variable value, the email variable value filters automatically.

   You can also go to the **Filters and variables** tab and click **View variable cascade relationships** to check the cascade relationships between variables in the current dashboard.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6b33b09f254925f9e8682c4455dbca25.png)

## Use Format syntax

Log Service supports using Format in variables.

|Format |Description |
|---|---|
|time_format |Format millisecond\-level timestamps.<br><br>Supports use with `${{__from}}` and `${{__to}}` variables. For supported format configurations, refer to [format](https://day.js.org/docs/zh-CN/display/format).<br><br>For example:<br><br><br>* `${{__to:time_format("YYYY-MM-DD HH:mm:ss.SSS")}}`: formats the query end time as `YYYY-MM-DD HH:mm:ss.SSS`.<br><br>   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_323bef71a20daa680c406c004c76bf73.png)<br><br>* `${{__from:time_format("DD/MM/YYYY")}}`: formats the query start time as `DD/MM/YYYY`.<br><br>   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5a2659b31cbfc3bc17bc640f6a63f3f0.png) |
|duration_round_fomat |format the time interval and round to the largest integer time unit.<br><br>supports use with the `${{__interval}}` variable, such as `${{__interval:duration_round_format }}`.<br><br>for example:<br><br><br>* the system automatically adapts the time grain to 2000 ms based on the selected time range. After formatting, the largest integer time unit is seconds, so the final formatted result is 2s.<br><br>* The system automatically adapts the time granularity to 600000 milliseconds based on the selected time range. After formatting, the largest integer time unit is minutes, so the formatted result is 10m. |
|tls_search_filter |Convert variable values into query conditions.<br><br>The format is `tls_search_filter("key", "AND")` or `tls_search_filter("key", "NOT")`, where key is the field name, and AND and NOT are logical operators. **Must be used with custom variables or system preset variables**.<br><br>For example:<br><br><br>* `${{method:tls_search_filter("method", "AND")}}`: converts the variable value `${{method}}` into a query condition.<br><br>* `${{status:tls_search_filter("status", "AND")}}`: converts the variable value `${{status}}` into a query condition and uses it in the query and analysis statement.<br><br>   * Query and analysis statement<br><br>      ```SQL```<br>```      * ${{status:tls_search_filter("status", "AND")}}```<br>```      ```<br>      <br><br>   * Query and analysis results<br><br>      ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e4e493c83af6961f9ad6729ea015aad8.png)<br><br>      ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_71f23cb4eb42cbbb96e4d8d5ec88888f.png)<br><br><br> |
|encode_base64 |Encode the variable value in Base64.<br><br>For example: use `${{method:encode_base64}}` to encode the value of the `${{method}}` variable.<br><br>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_df75c6219698b20e541525a9fe0af8b8.png) |

## Related actions

After adding filters and variables, you can conveniently use and modify or delete filters and variables in the dashboard as needed. For details, refer to [dashboard common operations](https://docs.byteplus.com/docs/tls/Managing_dashboards).

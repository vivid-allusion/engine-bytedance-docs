---
title: "Customizing and exporting audit logs"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/customizing-audit-logs"
---

After data plane auditing is enabled for a Cloud Search instance, you can customize log reports on the Kibana page and export log files in CSV format.

<span id="f0cff0d4"></span>
## Before you begin

After data plane auditing is enabled, data access events are written into indices that start with `.security-auditlog-` and end with a date. Before you can customize log reports and export log files, configure the index pattern on the Kibana page.

For more information about how to create an access index, please see [Querying data plane audit logs](https://docs.byteplus.com/en/docs/cloudsearch/query-data-plane-audit-logs).

<span id="efc61a75"></span>
## Customizing a log report

On the **Visualize** page of Kibana, you can configure various visual charts to customize log reports.


1. Log on to the Kibana page using the public endpoint. For more information, please see [Logging on to the visualization tool](https://docs.byteplus.com/en/docs/cloudsearch/logging-tool).

2. In the Kibana menu bar, select **Visualize**, and then click **Create new visualization**.

3. Create a visual chart as needed.

   Assume that you want to perform statistics on changes in access requests of different accounts. For this purpose, create an `Area` chart, and select the `.security-auditlog-*` index pattern as the data source.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/11186bb19b4c499e9ca89ecf3150316b~tplv-goo7wpa0wc-image.image) </span>

4. Configure the X\-axis and Y\-axis of the `Area` chart, and then click **Update**.

   
   |**Parameter** |**Description** |
   |---|---|
   |Y\-axis |Configure the aggregation of the Y\-axis as `Count` and the custom label as `requests`.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eca7f44938c64337ad32c01963723b91~tplv-goo7wpa0wc-image.image) </span> |
   |X\-axis |Configure the field of the X\-axis as `@timestamp` and the aggregation as `Data Histogram`.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/88a408704fa24f91bd9049e779090756~tplv-goo7wpa0wc-image.image) </span> |
   |Split series |Configure the split field for the X\-axis as `audit_request_effective_user_is_admin` and the sub aggregation as `Terms`.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4fa6612c261c4bfdb455790a073d7f51~tplv-goo7wpa0wc-image.image) </span> |
   

5. View the custom `Area` chart, and then click **Save** in the upper\-right corner.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e374f2f033a240c5970539a00167916a~tplv-goo7wpa0wc-image.image) </span>


<span id="173416c0"></span>
## Exporting audit logs

On the **Discover** page of Kibana, you can filter logs by configuring filter conditions and time ranges, then export the logs to the local device in CSV format. You can also create a custom report to repeatedly get audit logs that are filtered by using the same filter conditions.

<span id="695c7148"></span>
### Exporting CSV logs


1. Configure filter conditions and specify a time range.

   * Click  **+Add filter** to configure filter conditions. In this example, the filter condition is `audit_request_effective_user_is_admin: false`, which indicates querying event logs of non\-admin users.

   * Specify the time range as needed.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/33f4242006a04e27875ab1a6df29701b~tplv-goo7wpa0wc-image.image) </span>

2. Click **Save** in the upper\-right corner to save the log report.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/017d611071224568b0a72aa9437394d6~tplv-goo7wpa0wc-image.image) </span>

3. Click **Reporting** in the upper\-right corner, and then select **Generate CSV** to export the log report in CSV format.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/20cc118dbbb24b17bfe4cc52eeb5ba55~tplv-goo7wpa0wc-image.image) </span>


<span id="4bb977be"></span>
### Repeatedly getting logs filtered by using the same filter conditions


1. On the **Discover** page, after you configure and save filter conditions, you can click **Reporting** in the upper\-right corner, and then select **Create report definition**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/77b8e4f57f074593b6aa2b8d11528879~tplv-goo7wpa0wc-image.image) </span>

2. Configure the information such as the report name, report source, time range, and trigger type as needed, and then click **Create** in the lower\-right corner.

   * Report source: configure the report source as **Saved search**, and select the filter conditions you saved.

   * Time range: specify a time range as needed, for example, `Last 1 day`.

   * Trigger type: configure the trigger type as needed. In this example, the trigger type is configured as `On demand`, which means that reports are triggered through requests.

      For recurring reports, select Schedule and configure the recurring trigger mechanism as `Recurring` or `Cron based`.

3. View the custom report ID (primary key).

   After the custom report is created, the system generates an index named `.opendistro-reports-definitions`. You can create an index pattern for the index, and view the report ID (primary key) on the **Discover** page.

   1. Navigate to **Stack Management \> Index patterns**, and create an index pattern named `.opendistro-reports-definitions`.

   2. On the **Discover** page, view the report ID (primary key).

      You can select key fields as **Selected fields** to intuitively view the information you are following.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/affe5424be244693bfe0c65e944f1426~tplv-goo7wpa0wc-image.image) </span>

4. Get a log file.

   You can run the following command to get a log file. You must correctly enter the public endpoint of Kibana, report ID, username, and password.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Log files that are downloaded manually contain audit log information that was generated 24 hours before the download request is sent.   </div>
   

   ```Bash
   curl -k -XPOST 'https://'${kibana_public_endpoint}'/api/reporting/generateReport/'${report_id}'?timezone=Asia%2FShanghai' -H 'kbn-xsrf: true' -u ${user}:${password}
   ```

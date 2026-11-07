---
title: "Monitoring and Alerting"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Monitoring_and_Alerting"
---

<span id="_1-概述"></span>
# 1. Overview

The monitoring and alerting feature can be used to monitor metrics in charts, providing real\-time monitoring at the hour, day, and month granularity. Users can configure monitoring rules and monitoring frequency to set up monitoring.

The alerting methods currently supported by the system include email, Lark, WeCom, Webex, DingTalk, and Webhook. To use this module, the enterprise domain administrator must complete the office platform integration configuration. For detailed steps, see [Office platform integration](https://docs.byteplus.com/docs/undefined/69c349c050cba904c1f628f7).

To view and manage the monitoring configurations already set up in the current project, see [Monitoring Management](https://docs.byteplus.com/docs/DataWind/Monitoring_Management).

**Common application scenarios**


* Detecting changes in dimension items: For example, when a company develops offline stores in multiple locations, and needs to monitor changes in city coverage based on the city\-store list, dimension value change monitoring can be selected, with the monitoring dimension set to "city". When a new city appears in the list or a city disappears, the corresponding alert notification will be received.

* Monitoring abnormal metric fluctuations: For example, monitoring fluctuations in the company's sales revenue. When the fluctuation amount rises or falls beyond the expected value, an alert notification is sent so that relevant analysts can promptly investigate the cause.

* Intelligent fluctuation detection (supported only for line charts): For example, monitoring daily profit changes and using a time series anomaly detection algorithm to determine whether there are abnormal fluctuations in the data. If abnormal fluctuations are detected, an alert will be sent.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b68c3366583b430480a981fe97c44398~tplv-goo7wpa0wc-image.image) </span>


<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-离线数据监控"></span>
## 2.1 Offline data monitoring

**Step 1** Before configuring monitoring, the following prerequisites must be met:


* The base table must be updated regularly.

* The date filter must be set to 'recent' or 'recent with data'.

* Save the chart.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/62a878ff8f0e4c74b11d0bf9558906a4~tplv-goo7wpa0wc-image.image) </span>

**Step 2** Click 'Create Monitoring' to open the settings dialog.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5869a9c19af744f4bb000d9d989f1946~tplv-goo7wpa0wc-image.image) </span>

**Step 3** Enter the monitoring name, select the monitoring time range and trigger factors, and configure the alerting rules, monitoring time, and notification methods, and more.


* Note the selection of the time range. For example, in the screenshot below, if the time range is set to the selected payment date range, the monitored data will include all rows currently displayed in the chart. If the time range is set to the most recent time point, only the row with the payment date of 2022\-05\-30 will be monitored.


**Step 4** Click Send Test to view the test information in the configured monitoring receiving application and adjust parameters.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Here, using Lark as an example, complete the integration steps described in <a href="https://docs.byteplus.com/docs/DataWind/Basic_Configuration_for_Lark_Integration">Basic Configuration for Lark Integration</a> in advance</div>


**Step 5** Click Confirm to successfully create a new monitoring task. To view more historical monitoring records, click [Monitoring List] to access 'Monitoring Management' in the project center.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9549140252d04e65aaca58cdd8ee3f10~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-实时数据监控"></span>
## 2.2 Real\-time data monitoring

**The following prerequisites must be met:** 


* The base table must be real\-time data from Kafka.

* The time partition field must be aggregated.

* The date filter must be set to recent or recent with data.

* Save the chart.


Other operational steps are consistent with those above.

<span id="_3-功能介绍"></span>
# 3. Feature introduction

<span id="_3-1-时间范围"></span>
## 3.1 Time range

<span id="c11b9ef5"></span>
### **3.1.1 Date dimension**

The selectable dates for the time range are related to the date dimensions in the dimension bar of the monitoring chart. For example, if the chart dimensions in the screenshot select p_date and payment date, you can choose the range of these two date dimensions in the monitoring time range options.


* **Range of date dimensions**


Taking the payment date in the screenshot below as an example:

(1) Selecting the most recent time point means only monitoring the data for the latest payment date, that is, the row with 2022\-01\-15 as the payment date.

(2) Selecting the most recent N time points and setting N to 5 means monitoring the data for the five rows from 2022\-01\-11 to 2022\-01\-15.

(3) Selecting the chosen time range means monitoring all data retrieved under the current payment date filter conditions.

<span id="03cfcbaa"></span>
### 3.1.2 Most recent time point

The range for the most recent one or n time points depends on the **date type** of the time field, and supports **1/5/15 minutes, year\-month\-day\-hour, year\-month\-day, year\-week, and year\-month.** 

For example, if the date type of the time field is set to "year\-month\-day\-hour\-minute" with a granularity of "15 minutes" and the condition is set to "most recent 1 time point", then at the next monitoring trigger, the current data will be compared with the data from 15 minutes earlier.

> If the date type is another type, such as seconds, biweekly, bimonth, and more, the following rules apply:

> * If the date type is datetime, such as seconds, 10 minutes, 20 minutes, and more, then the range for the most recent 1 time point is **1 second**

> * If the date type is date, such as biweekly, bimonth, quarter, and more, then the range for the most recent 1 time point is **1 day**


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/128b8c96dcbd4be5a1ac40fea2fa8930~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-触发因素"></span>
## 3.2 Trigger factors

<span id="_3-2-1-指标值变化"></span>
### 3.2.1 Metric value changes

Metric value change monitoring supports configuring multiple alert rules. You can choose to trigger an alert when any rule or all rules are met. Metric conditions are required, while dimension conditions are optional.


* **All rules / Any rule: Multiple alert rules can be added to the monitoring configuration at the same time.** 

   When all rules are selected, an alert is triggered only when all rule conditions are met simultaneously. For example, as shown in the figure below, an alert is triggered when the profit for the most recent day fluctuates by more than 5% compared to the previous day and the cost fluctuates by more than 10% compared to the previous day.


When any rule is selected, an alert is triggered when any single rule is met. For example, as shown in the figure below, an alert is triggered as soon as either the profit for the most recent day fluctuates by more than 5% compared to the previous day or the cost fluctuates by more than 10% compared to the previous day.


* **Dimension filtering**

   Each rule supports configuration of dimension filtering, allowing you to monitor specified dimension items in the chart.

   For example, see the screenshot below:

   When the OR condition is selected: Data that meets any of the city or province filters will be monitored.

   When the AND condition is selected: Only data that meets both the city and province filters will be monitored.

* **Metric monitoring criteria**

   Configuration for metric filtering is supported under each rule. You can choose to monitor a single metric or multiple metrics, or set multiple conditions for the same metric.

   For example, see the screenshot below:

   When any condition is selected: If the profit for the most recent day meets **any one** of the following conditions—fluctuates by more than 5% compared to the previous day or the original value is greater than 4,000,000—an alert will be triggered.

   When all conditions are selected: An alert will be triggered only when the profit for the most recent day **simultaneously meets** both conditions—fluctuates by more than 5% compared to the previous day and the original value is greater than 4,000,000.

* **Metric monitoring condition settings**

   **All data / Any data:** 

   The default is any data, which means an alert is triggered immediately when any data meets the condition. When all data is set, an alert will only be triggered when all data under the specified dimension conditions meet the criteria.

   **Metric selection:** 

   The metrics placed in the metric bar on the chart page can be selected, and comparison and period\-over\-period derived fields are supported.

   **Comparison range:** 

   Supports comparison with 1 day ago, 7 days ago, 30 days ago, absolute value, original value, and the previous time point; comparison with the average of the previous 7 days or the average of the previous 30 days (these two options are only available when the first dimension in the chart's dimension bar is a partition field).

   **Comparison method:** 

   Ratio type: fluctuation greater than, increase greater than, decrease greater than

   Absolute value / original value: \>, \>=, <, <=, =

   **Comparison criteria:** 

   Value: a fixed value can be entered

   %: a percentage value can be entered

   Metric: supports comparison between the currently monitored metric and other metrics (including comparison and period\-over\-period derived fields). For example, as shown in the screenshot, an alert is triggered when the original value of profit is less than the original value of cost.


<span id="_3-2-2-维度值变化"></span>
### 3.2.2 Dimension value changes

Dimension value change monitoring can monitor a specific dimension value in the current chart. When the enumeration value of the dimension for the current day changes compared to 1 day ago, 7 days ago, or 30 days ago, an alert is triggered.


* **Monitored dimensions**

   The dimensions that can be monitored are the dimension items of the current chart (monitoring of hidden dimensions is supported).

* **Comparison conditions**

   Supports comparison with 1 day ago, 7 days ago, and 30 days ago.


<span id="_3-2-3-智能波动检测"></span>
### 3.2.3 Intelligent fluctuation detection

Intelligent fluctuation detection monitors indicator fluctuations over a period of time using the S\-H\-ESD algorithm for time series anomaly detection. If an abnormal fluctuation is detected, an alert is triggered.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Intelligent fluctuation detection only supports line charts; other chart types cannot be selected, and the monitoring period must contain at least 15 time points</div>



* Monitoring indicators


The selectable monitoring indicators are those in the current chart indicator bar. Monitoring of hidden fields and derived fields from analysis features (such as year\-over\-year and month\-over\-month fields) is supported.

<span id="_3-3-监控时间"></span>
## 3.3 Monitoring schedule

<span id="_3-3-1-定时"></span>
### 3.3.1 Scheduled monitoring


* Daily: Monitoring is triggered at the specified time point each day.

   * The default is a time picker for quick selection of a 24\-hour time point. After selecting a custom time, minute\-level precision is supported, with a minimum monitoring interval of 10 minutes.

   * UTC time zone selection is supported.

* Hourly: Within the selected time range, monitoring is triggered every N hours.

   * Monitoring can be triggered every 1, 2, 3, 4, 6, 8, or 12 hours.

   * UTC time zone selection is supported.

* Minute\-level: Within the selected time range, monitoring is triggered every N minutes.

   * Monitoring can be triggered every 10, 15, 20, or 30 minutes.

   * UTC time zone selection is supported.

* Weekly: Monitoring can be triggered at a fixed time point on a specified day of the week.

   * The weekly range supports selection from Monday to Sunday.

   * Monitoring can be triggered at N hours and N minutes on the selected day. The default is a time picker for quick selection of a 24\-hour time point. After selecting a custom time, minute\-level precision is supported, with a minimum monitoring interval of 10 minutes.

   * UTC time zone selection is supported.

* Monthly: Monitoring can be triggered at a specified time point on the Nth day of each month.

   * The monthly range supports triggering monitoring on the 1st to 31st day of each month. (If the 31st is selected and a month does not have 31 days, no alert will be sent.)

   * Monitoring can be triggered at N hours and N minutes on the selected day. The default is a time picker for quick selection of a 24\-hour time point. After selecting a custom time, minute\-level precision is supported, with a minimum monitoring interval of 10 minutes.

   * UTC time zone selection is supported.


Custom time: Monitoring can be triggered on working days, trading days, or every day.

<span id="_3-3-2-数据完成同步时触发"></span>
### 3.3.2 Trigger on data synchronization completion

When the chart dataset is synchronized daily, monitoring can be configured to trigger upon completion of data synchronization.


* Triggered when data synchronization is complete; supports UTC time zone selection

   * This option is only visible for charts with a daily update frequency (that is, datasets with a daily synchronization cycle or automatic synchronization). After configuration, the following conditions are required to trigger monitoring:

      * The T\-N time partition data has completed synchronization

      * The earliest trigger time has been reached

* Example: The subscription trigger date is 2020\-01\-02. The trigger date is set to T\-1, and the earliest trigger time is 10:00.

   * If the dataset completes synchronization at 9:00 on 2020\-01\-01, the monitoring notification will wait until 10:00 to be sent.

   * If the dataset completes synchronization at 11:00 on 2020\-01\-01, the monitoring notification will be delayed until 11:00 to be sent.


<span id="_3-4-推送方式"></span>
## 3.4 Notification methods

The product currently supports the following alert methods: email, Lark, WeCom, Webex, DingTalk, and Webhook. The specific alert method depends on the office platform integration configured by your company's system administrator. If no notification methods are available here, please refer to [office platform integration](https://www.volcengine.com/docs/4726/67928) for configuration. For IM group notifications, multiple group IDs can be added, separated by English commas, and each group must have a bot. To send monitoring results to Lark via Webhook, you need to parse and construct requests using a standardized output script.

For Webhook output, when the data meets a user\-configured condition, an HTTP request will be sent to the specified recipient (Webhook address). The following provides the output script specifications for your reference.

<span id="f2cbcb0a"></span>
### **Alert message**

```JSON

{
  "secret": "xxx",//Key, used by the business party for authentication
  "event": {//Message content
    "channel": "aeolus_monitor",//Used to distinguish monitoring messages from other types of messages
    "timestamp": 1610941345327,//Timestamp of this message
    "title": "monitor_alarm",//monitor_alarm: alert message for monitoring
    "payload": {
      "status": 1,//0: alert triggered, 1: alert not triggered

      "alarm_rule": [//Specific alert content and alert conditions; this field is empty when no alert is triggered
        {
          "metric_monitor_condition": [//Metric constraints
            "指标筛选条件满足任一条件:",
            "「sum(is_active_tea) 规则：>0.0」",
            "「sum(is_active_aeolus) 规则：>0.0」"
          ],
          "dimension_monitor_condition": [//Dimension constraints
            "维度筛选条件满足所有条件",
            "tea_app_name in [Lantern]"
          ],
          "data_link": "https://...."//Link to the file containing the complete alert content
        },
        ......
      ],
      "report_link": "'https://data.bytedance.net/aeolus/#/dataQuery?appId=555371&rid=39452'",//Chart link
      "date_range": {//Time range for chart query
        "p_date_start": "2021-10-07",//Business start date
        "p_date_end": "2021-10-07"//Business end date
      },
      "suggestion": "通知管理员",//Handling suggestions
      "monitor_name": "监控_1008_5"//Monitoring name
    }
  }
}
```


<span id="89f15557"></span>
### **Edit monitoring notification**

```JSON

{
  "secret": "xxx", //Key, used by the business party for authentication
  "event": {//Message content
    "channel": "aeolus_monitor", //Used to distinguish monitoring messages from other types of messages
    "timestamp": 1610941345327, //Timestamp of this message
    "title": "monitor_creation", //Create monitoring: monitor_creation, update monitoring: monitor_update, delete monitoring: monitor_delete,
    "payload": {
      "monitor_status": 1,//Monitoring status. 0: enabled, 1: paused'
      "name": "监控_1008_3", //Monitoring name
      "hour": "10:00",//Time point when monitoring is activated
      "trigger_type": 0,//Trigger type. 0: scheduled, 1: base table update
      "notified": "{\"lark\":\"duxingwang.001\"}",//Lark users to be notified
      "compute_type": 0,//Trigger factors, 0: "dimension + metric change", 1: "dimension value change", 2: "fluctuation anomaly detection"
      "extra": {//Additional information, currently stores alert suggestions and whether the base table is kafka. json format'
        "external_header": "",//Can be ignored
        "need_confirm": false,//Whether alert confirmation is required
        "show_condition": true,//Whether to display monitoring conditions in the alert
        "suggestion": "通知管理员",//Handling suggestions
        "timezone": "UTC+08:00",//Time zone
        "urgent_alarm": {
          "emails": "",
          "times": ""
        }
      },
      "shield_duration": 0,//Mute time span, in hours
      "lark_group_id": "{}",//Lark group IDs to notify, comma-separated string
      "notice_type": -1,//Push method
      "frequency": 0,//Scheduled frequency. 0: daily, 1: hourly
      "date_filter_conf": {},
      "rule_conf": {//Rule configuration, json format
        "rule_list": [//Rule list
          {
            "metric": {//Metric alert conditions
              "rule_list": [//List of metrics to be satisfied
                {
                  "dim_id": "sum_1586869275872",
                  "op_unit": 0,
                  "op_type": ">",
                  "compare_type": 3,
                  "op_value": 0
                }
              ],
              "op": 1//1: logical AND, 0: logical OR
            },
            "dimension": {//Dimension alert conditions
              "where_list": [
                {
                  "option": {
                    "is_report_filter": false,
                    "filter_pattern": "Accurate",
                    "custom_list": []
                  },
                  "val": [
                    "EasyShoot,galaxy"
                  ],
                  "pre_relation": "and",
                  "val_option": {
                    "true_all_selected": false,
                    "preview_val": [],
                    "excluded_val": []
                  },
                  "id": "1586869275867",
                  "unique_id": 211008185453007,
                  "op": "in"
                }
              ],
              "op": 1//1: logical AND, 0: logical OR
            }
          }
        ],
        "op": 1//1: logical AND, 0: logical OR
      },
      "data_ready": {},
      "owner_email_prefix": "duxingwang.001",//Creator
      "webhooks": [//Configured webhook id
        14
      ],
      "shield_start_time": "",//Mute alert start time
      "domain_id": 1,
      "report_id": 39452//Chart id
    }
  }
}
```


<span id="1d6c8922"></span>
### **data_link format**

```JSON
["tea_app_name", "is_active_tea"]//Column names of the chart
["1", "2"]//The first chart record that triggered the alert
["3", "5"] //The second chart record that triggered the alert
......
```


<span id="_3-5-处理建议"></span>
## 3.5 Handling suggestions

You can add text and URLs.

<span id="_3-6-警报结果"></span>
## 3.6 Alert results


* Display monitoring conditions in the alert

   * When selected, the alert card will include the configured monitoring conditions.


<span id="_3-7-发送测试"></span>
## 3.7 Send test

Immediately send a notification message for this configuration condition to preview the monitoring effect (test messages will not be sent to groups)

<span id="_3-8-监控列表管理"></span>
## 3.8 Monitoring list management

Access the monitoring list:

You can access the monitoring list through the dropdown menu in the visual monitoring page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f83b9510ca8466cac81febc590e1cdb~tplv-goo7wpa0wc-image.image) </span>

Alternatively, click Project Center \- Scheduled Tasks \- Monitoring Management to access


* The roles with permission to view and edit monitoring tasks


The people who can view and edit monitoring tasks are: the monitoring creator, the project administrator, the owner of the chart corresponding to the monitoring, and the administrator of the dashboard where the chart corresponding to the monitoring is located

By granting others dashboard management permissions, you can add collaborators for the monitoring of charts within that dashboard. This operation is not supported for personal dashboards.


| |Viewing scope |Operational scope |
|---|---|---|
|Project administrator |Can view all monitoring items in the project |Has full permissions |
|Project member |All monitoring items created by me |Has full permissions |
|Project member |All monitoring items created based on the charts I manage |Has full permissions |
|Project member |All monitoring items where I am the recipient |No permissions |



* Monitoring and subscriptions support batch transfer of ownership

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fed3643749524f5e90c606f65bbdaeaf~tplv-goo7wpa0wc-image.image) </span>

   Note: If the monitoring recipient is empty, the monitoring will not take effect


<span id="_4-使用示例"></span>
# 4. Usage examples

<span id="_4-1-dau-增速波动监控"></span>
## 4.1 DAU growth rate fluctuation monitoring

Data: DAU data for each app on both Android and iOS platforms

Monitoring scenario: monitor products with over 10 million DAU where the year\-over\-year growth exceeds 10 percent

Configuration parameters:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8feac896166a4d11ad36ad6c1a0aa2d0~tplv-goo7wpa0wc-image.image) </span>

If an app meets the criteria, an alert will be triggered:

<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_81b91653033c24c6e7720dc0e63456ad) </span>

<span id="_4-2-应用商店排行榜排名变化监控"></span>
## 4.2 Monitoring changes in app store ranking

Data: China Apple App Store overall ranking

Monitoring scenario: monitor changes in the daily top 10 apps

Configuration parameters:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9f5fa69a44864e7e8126ef4c26230071~tplv-goo7wpa0wc-image.image) </span>

If an app meets the criteria, an alert will be triggered:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1bd64e918e0f8ea632b3f30ebf87bb4a.png) </span>

<span id="_4-3-城市利润监控，小于1天前全国利润均值报警"></span>
## 4.3 City profit monitoring: alert if profit is less than the national average profit from one day ago


* Chart data: date, city, profit

* Monitoring requirement: compare each city's profit for the day with the national average profit from one day ago. If it is lower than the national average, trigger an alert.

* Implementation method:

   * Create a national average profit field ({filter=true:fixed [date]:avg([profit])})

   * Place the national average profit field in the metrics bar

   * Use the day\-over\-day analysis function to calculate the original value of the national average profit from one day ago

   * Configure monitoring with the condition: original profit value < original day\-over\-day value of the national average profit from one day ago

* Send a test to check whether the monitoring configuration meets the requirements

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_467e0bb3674b2ffc76b752af65cd598c) </span>


<span id="_4-4-防止数据毛刺导致的报警"></span>
## 4.4 Preventing alerts caused by data spikes


* Applicable scenarios:

* Monitor network latency in real time; trigger an alert if it exceeds 50 ms. Due to instability caused by special circumstances, there was a sudden spike to 120 ms at a certain moment, which triggered an alert. However, during troubleshooting, the data had already immediately returned to the normal range. To avoid false alarms caused by transient spikes, configure it so that an alert is triggered only if all data in the last 3 minutes exceed 50 ms.

* Implementation method

   * In the dimension conditions, select the time range as the last 3 minutes.

   * For the metric condition, select "All data" and set the condition to network latency \> 50.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4d0f283354a645be996eb003510328eb~tplv-goo7wpa0wc-image.image) </span>


<span id="_4-5-常见问题（配置-比n天前波动-发现满足报警条件未报警）"></span>
## 4.5 Common issues

<span id="5f764c36"></span>
### 4.5.1 Configure fluctuation compared to N days ago: Alert condition met but no alert triggered


* Using the profit field in the chart below as an example, if the configuration for profit fluctuating by more than 5% compared to 1 day ago does not take effect,

   * You can first configure the period\-over\-period growth rate for the profit field in the chart.

   * Create monitoring, select the period\-over\-period growth rate as the monitoring metric, and set the condition to absolute value \> 5%.

* This can also achieve monitoring for fluctuations exceeding 5% compared to the previous day.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_5af4fffb7135a094c1709d5de218f619) </span>

   This method allows monitoring compared to any previous N days.


<span id="b30a0a0e"></span>
### 4.5.2 **Configure monitoring to compare with X days ago: Alert condition met but no alert triggered**

When performing monitoring to compare with X days ago, note the following two points:


* If non\-p_date fields are involved, the date field among the non\-p_date fields must be placed as the first dimension. For example, if payment date is used as a non\-p_date field, ensure that payment date is the first dimension.

* After selecting a non\-p_date date field, the system will automatically shift both the p_date and non\-p_date date fields as a whole. For example, if the reference date is [payment date], and the last 1 day is [03 \- 06]. In practice, the data for p_date March 5 and payment date March 5 is compared with the data for p_date March 6 and payment date March 6. It does not compare the data for p_date March 6, payment date March 5, and payment date March 6 together.


To more conveniently and accurately complete the monitoring setup for comparison with X days ago, it is recommended to first configure the comparison rules for X days ago through analysis \- year\-over\-year and period\-over\-period comparison. After completing the comparison rule configuration, use the original value or absolute value of the period\-over\-period or year\-over\-year fields in the monitoring rule settings to ensure that monitoring operates accurately according to the configured comparison rules.

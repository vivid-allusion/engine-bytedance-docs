---
title: "Set log parameters"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/Set_log_parameters"
---

After purchasing the log service, you can set log capacity alarm thresholds and alarm intervals based on business needs, and modify the log storage duration to make efficient use of log capacity. You can also view the log capacity usage in real\-time, upgrade the capacity at any time, and avoid the inability to collect log data.

<span id="f8acbb62"></span>
## Requirements

The WAF log service functionality module has been purchased.

<span id="7250b90a"></span>
## Steps


1. Log in to [Web Application Firewall Console](https://console.byteplus.com/waf/region:waf+cn-gaofang-nt3/purchase-guide).

2. Select the region of the instance from the top bar.

3. Select **Log Management** from the left navigation to enter the log management page.

4. Click on **Log Settings** at the upper right corner of the page to enter the log parameters settings page.

5. Set different parameters as needed and confirm.

   * General Settings

      
      |Configuration |Description |
      |---|---|
      |Log capacity |The WAF allocates log capacity based on the purchased log service specifications, and the log capacity module shows the currently used log capacity and the total log capacity purchased. Click **upgrade capacity** to upgrade instance log specifications. |
      |Capacity alarm |When the used log storage level reaches the set alarm threshold, the platform will push alarm notifications.<br><br><br>* Alarm threshold: Alarm notifications are pushed when the log capacity usage rate reaches the alarm threshold, which defaults to 80%. Support an adjustment range of 50%\-100%.<br><br>* Alarm interval: The interval between two consecutive capacity alarms, with the default log capacity alarm interval being at least 3 days. Supports adjusting the range to 1\-90 days.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Please upgrade the log capacity in a timely manner to avoid log data being unable to continue writing due to exceeding the log capacity.</div><br> |
      |Storage duration |The retention period for log data is 180 days by default, with adjustable ranges from 30 to 3650 days, where 3650 days represents permanent storage.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The Cloud Firewall allocates log capacity based on the purchased Log Service specifications. If the amount of logs corresponding to the set log storage duration exceeds the purchased log capacity, logs will only be collected within the purchased log capacity. If some log data cannot be stored for the expected duration due to exceeding the log capacity or expiration, you can upgrade or renew as needed to ensure the log data is stored for the expected duration.</div><br> |
      |Log alarm strategy |The WAF supports configuring alarm strategies for the collected log data. Based on specified retrieval analysis conditions, it regularly queries the log data and reports alarms to the designated alarm group when triggering conditions are met. |
      |Log alarm history |After the log alarm policy takes effect, it will periodically perform monitoring tasks and record the execution status of each monitoring task. |
      

   * Log Collection: WAF supports customizing the range of log collection, with an “AND” logic between different collection range conditions, meaning that the collected logs must meet all the set conditions. After modifying the collection range, it only takes effect for newly ingested logs.

      
      |Configuration |Description |
      |---|---|
      |Domain Collection Range |The range of domains from which logs need to be collected. Changes will only apply to newly connected logs. |
      |Field collection range |The range of fields that need to collect logs; by default, only required fields are collected, and modifications will only take effect for newly ingested logs. For detailed explanations of log fields, please refer to [Log Field Description](https://docs.byteplus.com/en/docs/waf/Log_field_description). |
      |Disposal action collection range |Choose the log collection range based on the request type and the actions taken by WAF. By default, all action categories are collected, and modifications will only take effect for newly ingested logs.<br><br><br>* Access Requests: Record log information of requests that did not trigger WAF protection rules and requests allowed by WAF.<br><br>* Attack Requests: Record log information of requests that triggered WAF protection rules and executed different actions, among which:<br><br>   * Observation: Includes requests triggered with an action of "observe";<br><br>   * Interception: Includes requests with the trigger action “interception”<br><br>   * Human verification: Includes requests with the trigger actions “human verification” and “human verification \- interception.” |

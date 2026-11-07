---
title: "Time format"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/time_format"
---

Logs usually contain time\-related content by themselves. When collecting log data via LogCollector, you can configure the time conversion format so that LogCollector can parse the time\-related content in the logs into log timestamps. This topic introduces common time conversion formats and corresponding examples.

<span id="日志时间"></span>
## Log time

When you use LogCollector to collect log data, you can specify the log time using either of the following ways:


* Use log collection time:

   Take the system time when LogCollector collects logs as the log time. If LogCollector is running in a Linux server, then the time zone of the system time (time.Local) is the machine's time zone. If LogCollector is running in a Kubernetes cluster, after version v2.0.0 of LogCollector, the time zone of the system time (time.Local) is UTC+08:00.

* Customize log time:

   Extract the time included in the original logs as the log time. At this time, you need to fill in the **Time key name**, **Time regular** (optional), **Time conversion format** and **Time zone attribute**. Among them, when LogCollector collects log data, it will parse the time\-related content in the original logs according to the time conversion format you set and unify it into a Unix timestamp.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the <strong>Time conversion format</strong> is filled in incorrectly, LogCollector will be unable to correctly parse the time\-related content in the original logs, and thus the time of log collection will be used.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">By default, the log time can be accurate to milliseconds. If it is necessary to be accurate to nanoseconds, you can check the box to enable the nanosecond time precision. If the conversion format for milliseconds or nanoseconds is not specified in the <strong>Time conversion format</strong>, the milliseconds or nanoseconds part will be automatically filled with 0.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When the time\-related content in the original logs has a time zone, you can fill in the time zone parsing expression in the <strong>Time conversion format</strong> or specify the time zone attribute in the collection rules. The priorities of the two are as follows:   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the time zone expression (%z or %Z) is filled in the <strong>Time conversion format</strong> and the time zone attribute is specified in the collection rules, the time zone (%z or %Z) in the time conversion format shall prevail.   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the time zone expression (%z or %Z) is filled in the <strong>Time conversion format</strong> and the time zone attribute is not specified in the collection rules, the time zone (%z or %Z) in the time conversion format shall prevail.   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the time zone expression (%z or %Z) is not filled in the <strong>Time conversion format</strong> and the time zone attribute is specified in the collection rules, the time zone in the collection rules shall prevail.   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the time zone expression (%z or %Z) is not filled in the <strong>Time conversion format</strong> and the time zone attribute is not specified in the collection rules, the time zone of the system time (time.Local) shall prevail.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the time\-related content in the logs is longer than the time conversion format, the remaining part of the time\-related content in the logs will be ignored. For example, if the time\-related content in the logs is <code>2024-04-30T16:33:31.399+0800</code> and the time conversion format is <code>%Y-%m-%dT%H:%M:%S</code>, the remaining part <code>.399+0800</code> will be ignored, and the final time parsing result will be <code>2024-04-30 16:33:31</code>.   </div>
   


<span id="常见的时间转换格式"></span>
## Common time conversion formats


|Category |Time Conversion Format |Description |Example |
|---|---|---|---|
|Century |%C |Century number. It is obtained by dividing the year number by 100. Valid values: 00 to 99. |01 |
|Year |%Y |Year number that includes the century number. Valid values: 0000~9999. For example, 2022 represents the year 2022. |2022 |
||%y |Year number that does not include a century number. Valid values: 00~99. For example, 22 represents the year 2022. |22 |
||%G |Year number that includes the century number. Valid values: 0000~9999. For example, 2022 represents the year 2022. |2022 |
||%g |Year number that does not include a century number. Valid values: 00~99. For example, 22 represents the year 2022. |22 |
|Month |%m |Month. Valid values: 01 to 12. The value 01 indicates January. |08 |
||%B |Full spelling of a month name in English. |June |
||%b |Abbreviation of a month name in English. |Jan |
||%h |Abbreviation of a month name in English. It is equivalent to %b. |Jan |
|Day |%d |The Day of the month. Valid values: 01 to 31. For example, 21 represents the 21st day. |21 |
||%e |The Day of the month. Valid values: 01 to 31. For example, 21 represents the 21st day.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If it is a single\-digit number, a space needs to be added in front of it.</div><br> |21 |
|Hour |%H |Hour in 24\-hour format. Valid values: 00 to 23. For example, 21 represents 21 o'clock. |21 |
||%I |Hours in 12\-hour format. Valid values: 01 to 12. For example, 09 represents 9 o'clock.<br><br>Among them, `I` is in uppercase. |09 |
||%P |AM or PM. |AM |
||%p |AM or PM. |AM |
|Minute |%M |Minute. Valid values: 00 to 59. For example, 01 represents the first minute of an hour. |01 |
|Second |%S |Second. Valid values: 00 to 59. |01 |
|Millisecond, Microsecond, Nanosecond |%f |Millisecond, microsecond, and nanosecond time. Valid values: 000000000 to 999999999. For example, 1 represents 100000000 nanoseconds.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If it is less than 9 digits, add zeros at the back.</div><br> |100000000 |
|Second\-level Timestamp |%s |Second\-level Unix timestamp. It is a 10\-digit number. |1651648193 |
|Millisecond\-level Timestamp |%F |Millisecond\-level Unix timestamp. It is a 13\-digit number. |1651648192000 |
|Time Zone |%Z |Time zone names, such as UTC, EST, CST. |UTC |
||%z |Time zone offset in the format of `±HHMM` or `±HH:MM`. For example, `+08:00` represents the East Eight Zone, and `-0500` represents the West Five Zone. |\-0500 |
|Others |%A |Full spelling of a weekday name in English. |Thursday |
||%a |Abbreviation of a weekday name in English. |Thur |
||%j |The day of the year. Valid values: 001 to 366. |340 |
||%% |The `%` character. |% |


<span id="时间转换格式示例"></span>
## Examples of time conversion formats


|Time Field Content |Time Conversion Format |
|---|---|
|[2022\-05\-04 15:12:12.012] |[%Y\-%m\-%d %H:%M:%S.%f] |
|22019\-10\-12T07:20:50.52Z07:00 |%Y\-%m\-%dT%H:%M:%S |
|1651648409 |%s |
|1651648416882 |%F |

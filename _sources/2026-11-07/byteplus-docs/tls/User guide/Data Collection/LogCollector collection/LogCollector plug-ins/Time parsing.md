---
title: "Time parsing"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Time-parsing"
---

When you collect logs through LogCollector, you can use the time parsing plug\-in to parse the time content in the raw log and record the parsed time as a log timestamp on the server.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">LogCollector version 1.0.48 and later versions support this plug\-in. For more information on how to view the LogCollector version, refer to <a href="https://docs.byteplus.com/docs/tls/install_logCollector_on_a_host#%E6%9F%A5%E7%9C%8B%E8%BD%AF%E4%BB%B6%E7%89%88%E6%9C%AC">View software version</a>.</div>


<span id="a7cf7f97"></span>
## Parameter description


|Parameter |Type |Required |Description |
|---|---|---|---|
|field |String |Yes |Specify the name of the field you want to parse. |
|format |String |Yes |Specify the time format used to parse the time content. For more information, refer to [Log time](https://docs.byteplus.com/docs/tls/time_format#%E6%97%A5%E5%BF%97%E6%97%B6%E9%97%B4).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">By default, configuration to milliseconds is supported when configuring the time conversion format. If no millisecond\-level resolution is specified in the time conversion format, the millisecond portion is automatically filled with 0.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the high\-precision timestamp function is enabled, configuration to nanoseconds is supported when configuring the time conversion format. If no nanosecond resolution is specified in the time conversion format, the nanosecond portion is automatically filled with 0.</div><br> |
|time_zone |String |No |Configure the time zone. Defaults to the time zone of the server where the LogCollector is located, and supports GMT and UTC. For example `GMT + 08:00, Asia/Shanghai`. |
|extract_regex |String |No |Specify the regular expression used for extracting time. If you only parse part of the time content in a field, you can extract it with a regular expression. |
|enable_nanosecond |Boolean |No |Whether to enable the high\-precision time function. After enabling it, the precision of the parsed log time is at the nanosecond level.<br><br>By default, the precision of the log time is at the millisecond level. |
|set_year |String |No |When the year information is missing from the log time, you can use this parameter to supplement the year information for the log time.<br><br><br>* When you expect to manually set a fixed year, it can be set to a specific year, for example, `"set_year": "2024"`.<br><br>* When you expect to use the year of the current time of the system, it can be set as `"set_year": "auto"`.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When <code>"set_year": "auto"</code> is set and the <code>time_zone</code> is configured, the system time will be converted to the time zone you configured according to the <code>time_zone</code>, and then the year will be obtained.</div><br><br><br>   <div data-tips="true" data-tips-type="tip">For example, if the current system time is <code>2023-12-31 20:00:00</code> in London time, and the <code>time_zone</code> is <code>GMT+08:00</code>, the time will be converted to <code>2024-01-01 04:00:00</code> in the Beijing time zone, and then 2024 will be used as the year.   </div><br>   <br><br>* <div data-tips="true" data-tips-type="tip">When <code>"set_year": "auto"</code> is set, the year may be incorrect due to extremely short collection delays during the New Year's transition. It is recommended to print the year information in the log time.</div><br> |


<span id="f15e08ff"></span>
## Example

<span id="88333b1f"></span>
### Example 1: The high\-precision timestamp function is not enabled


* Key\-value pair logs processed through collection modes or other plugins.

   ```Plain
   "message": "[2023-12-19T19:00:00,000] [INFO] java.lang.Exception: exception happened"
   ```
   

* LogCollector plugin configuration

   ```JSON
   {
       "processors": [
           {
               "strp_time": {
                   "field": "message",
                   "format": "%Y-%m-%dT%H:%M:%S,%f",
                   "time_zone": "GMT+08:00",
                   "extract_regex": "\\[(\\d{4}\\-\\d{2}\\-\\d{2}T\\d{2}:\\d{2}:\\d{2},\\d{3})\\]"
               }
           }
       ]
   }
   ```
   

* processing result

   The parsed log timestamp is 1702983600000, which is 2023\-12\-19 19:00:00,000.

   ```Plain
   "message": "[2023-12-19T19:00:00,000] [INFO] java.lang.Exception: exception happened"
   Log.Time=1702983600000
   ```
   


<span id="de8d7aa1"></span>
### Example 2: Enabling the high\-precision time function


* Key\-value pair logs processed through collection modes or other plugins.

   ```Plain
   "message": "[2024-05-15T12:30:19,123456789] [INFO] java.lang.Exception: exception happened"
   ```
   

* LogCollector plugin configuration

   ```JSON
   {
       "processors": [
           {
               "strp_time": {
                   "field": "message",
                   "format": "%Y-%m-%dT%H:%M:%S,%f",
                   "time_zone": "GMT+08:00",
                   "extract_regex": "\\[(\\d{4}\\-\\d{2}\\-\\d{2}T\\d{2}:\\d{2}:\\d{2},\\d{3})\\]",
                   "enable_nanosecond": true
               }
           }
       ]
   }
   ```
   

* processing result

   The parsed log timestamp is 1715747419123, which is 2024\-05\-15 12:30:19, 123456789.

   ```Plain
   "message": "[2024-05-15T12:30:19,123456789] [INFO] java.lang.Exception: exception happened"
   Log.Time=1715747419123
   ```
   


<span id="ba2562a7"></span>
### Example 3: Automatically supplement the year information in the log time


* Key\-value pair logs processed through collection modes or other plugins.

   ```Plain
   "message": "[01-01T04:00:00,123456] [INFO] java.lang.Exception: exception happened"
   ```
   

* LogCollector plugin configuration

   ```JSON
   {
       "processors": [
           {
               "strp_time": {
                   "field": "message",
                   "format": "%m-%dT%H:%M:%S,%f",
                   "time_zone": "GMT+08:00",
                   "extract_regex": "\[(\d{2}\-\d{2}T\d{2}:\d{2}:\d{2},\d{3})\]",
                   "set_year": "auto"
               }
           }
       ]
   }
   ```
   

* Suppose the system time when starting to process this log entry is 2023\-12\-31 20:00:00 (GMT+00:00).

   The query time of the log is `2024-01-01 04:00:00,123`.

   ```Plain
   "message": "[01-01T04:00:00,123456] [INFO] java.lang.Exception: exception happened"
   Log.Time=1704052800123
   ```

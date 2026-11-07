---
title: "Log format update"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-offline-log-format-updated"
---

To enhance our service and improve the accuracy of data logging, we will be optimizing and upgrading the offline log format for BytePlus MediaLive on March 14, 2024. Previously, we used the same format for various log types and differentiated them using the `log_type` field. With the forthcoming update, we will be providing a distinct log format for each log type.

<span id="34952981"></span>
## New log

Please refer to [Querying logs](https://docs.byteplus.com/docs/byteplus-media-live/docs-managing-logs) for an introduction to the log formats.

<span id="c71e13d0"></span>
## Old log

If you still need to use the old format, please contact [technical support](https://www.byteplus.com/en/support).

Below is an example of the old log:

```plaintext
{"request_time":1649982298644,"account_id":"21XXX957","is_source":"true","is_relay":"","node_ip":"101.75.2X1.133","domain":"q2.Xpush.lurenxin.com","app":"livetob","stream":"regression_2022X0415082401BNIL","total_in_byte":"1752959","total_out_byte":"0","in_bitrate":"2749741","out_bitrate":"0","protc_type":"rtmp","client_ip":"110.XX9.198.186","log_type":"push"}
```


Below is a detailed description of log fields:


|**Parameter** |**Description** |**Example** |
|---|---|---|
|request_time |The UNIX timestamp for when the request is sent. |1644474350524 |
|account_id |Your account ID. |0000000000 |
|is_source |Whether the traffic is input traffic. |true |
|is_relay |Whether the traffic is server\-initiated. |true |
|node_ip |The IP address of the edge server. |10.225.84.221 |
|domain |Domain name. |example_live_pull.doc.com |
|app |Application name. |example_app |
|stream |Stream name. |stream_example_obs_0211_01_hls |
|total_in_byte |The size of the request in bytes. |1752959 |
|total_out_byte |The size of the response in bytes. |0 |
|in_bitrate |Push\-stream bitrate in bps. |2749741 |
|out_bitrate |Pull\-stream bitrate in bps. |*  |
|protc_type |Protocol. |http |
|client_ip |The IP address of the client. |10.10.10.1 |
|log_type |The type of the log, including "pull" and "push". |pull |

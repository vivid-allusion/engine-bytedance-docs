---
title: "Querying logs"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-managing-logs"
---

Logs include Access logs, Push\-stream logs, and relay logs. You can download logs for a specific period of time.

<span id="235cc0a6"></span>
## Rules and limitations


* **Query scope:**  You can query logs for the last 30 days.

* **File splitting**: Log files are split per hour, with a maximum of 1.5 million log entries per file.

   * No log file will be created if no logs are generated for a specific hour.

   * Multiple log files will be generated if more than 1.5 million logs of the current event are generated within an hour. The sequence number at the end of the file name indicates the log file order. For example, 2023_08_11_000000_010000_0.gz, 2023_08_11_000000_010000_1.gz.

* **Naming Convention**:

   * When related to a domain name: domain name_year_month_day_start time_end time_file index. For example, www.example.com_2023_08_11_000000_010000_0.gz.

   * When unrelated to a domain name: year_month_day_start time_end time_file index. For example, 2023_08_11_000000_010000_0.gz.


<span id="a29afae1"></span>
## Procedure


1. Go to [BytePlus MediaLive console > Logs](https://console.byteplus.com/live/main/log-management).

2. Select the log type and domain name and set the time range.

3. Click **Download** or click **Download all** after selecting multiple log files to save the logs locally.


<span id="930a9665"></span>
## Log format

<span id="65a6e356"></span>
### Access logs

The following is an example of an access log:

```Plain
[05/Sep/2023:15:44:08 +0000] 10.10.10.10 GET HTTP/2.0 200 "sub.example.net" "https://sub.example.net/exaple_app/example_stream.m3u8" 345 5432 "agr1=111" "domain" "Go-http-client/1.1" 172.16.10.10 httpq,rtmpq,http3,rtmq
```


Below is a detailed description of fields in the log:


|**Field** |**Data type** |**Example** |
|---|---|---|
|Log record time<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For requests that do not require periodic logging, the log record time is the start time of the request.</div><br> |Time |[05/Sep/2023:15:44:08 +0000] |
|User IP |String |10.10.10.10 |
|HTTP request method |String |GET |
|HTTP protocol version |String |HTTP/2.0 |
|Status code |String |200 |
|Domain name for stream pulling |String |"sub.example.net" |
|Request URI |String |"https://sub.example.net/example_app/example_stream.m3u8" |
|Playback duration (ms)<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The Playback duration is the duration from the time of request to the time of log record.</div><br> |Long |345 |
|Downstream traffic (byte) |Long |5432 |
|Request parameters |String |"agr1=111" |
|Request referrer |String |"domain" |
|User\-Agent |String |"Go\-http\-client/1.1" |
|Edge server IP |String |172.16.10.10 |
|QUIC protocols |String |httpq,rtmpq,http3,rtmq |


<span id="2f02e84f"></span>
### Push\-stream logs

The following is an example of a push\-stream log:

```plaintext
[05/Sep/2023:15:59:59 +0000] 10.10.10.10 PUSH "push.example.com" "rtmp://sub.example.net/exaple_app/example_stream" 345 "agr1=111" 172.16.10.10 httpq,rtmpq,http3,rtmq
```


Below is a detailed description of fields in the log:


|**Field** |**Data type** |**Example** |
|---|---|---|
|Request time |Time |[05/Sep/2023:15:59:59 +0000] |
|User IP |String |10.10.10.10 |
|Request method |String |PUSH |
|Domain name for stream pushing |String |"push.example.com" |
|Request URI |String |"rtmp://sub.example.net/exaple_app/example_stream" |
|Upstream traffic (byte) |Long |345 |
|Request parameters |String |"agr1=111" |
|Edge server IP |String |172.16.10.10 |
|QUIC protocols |String |httpq,rtmpq,http3,rtmq |


<span id="80fac79d"></span>
### Origin\-pull\-stream logs

The following is an example of an origin\-pull\-stream log:

```plaintext
[05/Sep/2023:15:59:59 +0000] 10.10.10.10 GET HTTP/2.0 200 "example.com" "/live0714/dcjtest2.m3u8" "agr1=111" 3939 9204
```


Below is a detailed description of fields in the log:


|**Field** |**Data type** |**Example** |
|---|---|---|
|Origin\-pull\-stream request time |time |[05/Sep/2023:15:59:59 +0000] |
|Origin\-pull\-stream IP |string |10.10.10.10 |
|HTTP request method |string |GET |
|HTTP protocol version |string |HTTP/2.0 |
|Status code |string |200 |
|Domain name |string |"example.com" |
|Request URI |string |"/live0714/dcjtest2.m3u8" |
|Request parameters |string |"agr1=111" |
|Origin\-pull\-stream duration (ms) |long |3939 |
|Origin\-pull\-stream file size (byte) |long |9204 |


<span id="8e970a8f"></span>
### Relay logs

The following is an example of a relay log:

```JSON
[05/Sep/2023:13:21:44 +0000] f1fd49****cc2db2 live 1670 447769 "rtmp://172.16.10.10/example_app/example_stream?domain=pull.example.com" "rtmp://172.16.10.11/example_app/example_stream?domain=push.example.com" MediaLive
```


Below is a detailed description of fields in the log:


|**Field** |**Data type** |**Example** |
|---|---|---|
|Task creation time |Time |[05/Sep/2023:13:21:44 +0000] |
|Task ID |String |f1fd49\*\*\*\*cc2db2 |
|Relay duration (ms) |Long |1670 |
|Relayed traffic (byte) |Long |447769 |
|Source address |String |"rtmp://172.16.10.10/example_app/example_stream?domain=pull.example.com" |
|Target address |String |"rtmp://172.16.10.11/example_app/example_stream?domain=push.example.com" |
|Type of target address. `volc` means relaying to MediaLive, while `other` means relaying to third\-party. |String |MediaLive |

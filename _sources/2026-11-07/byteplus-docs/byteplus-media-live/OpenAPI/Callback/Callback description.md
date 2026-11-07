---
title: "Callback description"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-callback-description"
---

After you configure the corresponding callback URL, when related events occur, BytePlus MediaLive sends JSON packets carrying event information to your business server by using a **POST request**.

## Network protocol

* **Request method**: HTTP POST.

* **Request header**: The default value of Content\-Type is `application/json`.

* **Request body**: Structured JSON. For specific parameters, see [Callback message description](https://docs.byteplus.com/en/docs/24/7810#callback-message-description).

* **Response**: Your business server must return the `200 OK` status code. BytePlus MediaLive determines whether the business server successfully receives the callback message based only on the HTTP status code, and does not check the response body.

## Reliability

To ensure stable callback delivery, BytePlus MediaLive retries callback requests when a callback request fails.

* After the first request fails, BytePlus MediaLive immediately retries up to **3 times**, with a **3\-second interval** between retries.

* If the request still fails, BytePlus MediaLive enters the retry queue. The maximum retry duration is **10 minutes**, starting from the time when the first request is sent. After the retry duration expires, BytePlus MediaLive stops retrying.

* The following cases are considered request failures:

   * Request timeout: no response is received within 4 seconds.

   * The HTTP status code is not 200.

## Common security signature parameters

The callback messages for stream pushing starts, stream pushing ends, recording events, and screenshot events include the `sign` and `t` signature parameters. After you specify a callback key in [callback configurations](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-a-callback-task), your business server can use these parameters to verify that the callback request comes from BytePlus MediaLive.

|Parameter |Data Type |Description |
|---|---|---|
|sign |String |The signature string. After you specify a callback key, your business server can calculate the signature and compare it with the `sign` value in the callback request as follows:<br><br><br>1. Concatenate `AuthKeyPrimary` (callback key) and `t` (signature expiration time) in order. For example, if the callback key is `abc` and the signature expiration time is `1787800827`, the concatenated string is `abc1787800827`.<br><br>2. Calculate the MD5 hash of the concatenated string and generate a 32\-character lowercase string.<br><br><br>If the calculated result is the same as the `sign` value in the callback request, the signature verification succeeds.<br><br>> **Note**<br><br><br>> If no callback key is specified, the value is an empty string.<br> |
|t |Long |The signature expiration time. By default, this value is 10 minutes after the callback request is sent. Unix timestamp, in seconds.<br><br>> **Note**<br><br><br><br>* > After you specify a callback key, if your business server receives a callback request after the time specified by `t`, the callback request can be considered invalid to prevent network replay attacks.<br><br><br>* > If no callback key is specified, the value is fixed to `0`.<br> |

## Callback message description

### Common message structure

The callback messages for stream pushing starts, stream pushing ends, and recording events use the following common structure. Business parameters for each callback are contained in `data`. For the structure of other callback messages, see the corresponding sections.

|Parameter |Data Type |Description |
|---|---|---|
|code |Integer |The callback message status code. The value is fixed to `0`. |
|message |String |The callback message status information. The value is fixed to `ok`. |
|data |Object |The callback data. For specific parameters, see the parameter description of each callback message. |

### Stream pushing starts

When stream pushing starts, BytePlus MediaLive sends a callback message to your configured callback URL. For details about configuring callback URLs, see [Configuring a callback task](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-a-callback-task).

|**Parameter** |**Data Type** |**Description** |
|---|---|---|
|vhost |String |The domain name space. |
|domain |String |The domain name for stream pushing. |
|app |String |The `AppName`. |
|stream |String |The `StreamName`. |
|event_type |String |The event type, which is `push_start` for this callback. |
|sign |String |The common security signature parameter used to verify that the callback request comes from BytePlus MediaLive. For more information, see [Common security signature parameters](https://docs.byteplus.com/en/docs/24/7810#common-security-signature-parameters). |
|t |Long |The common security signature parameter that indicates the request expiration time. For more information, see [Common security signature parameters](https://docs.byteplus.com/en/docs/24/7810#common-security-signature-parameters). |
|uniq_id |String |The event ID, used for event deduplication. |
|detail |Object of [detail](https://docs.byteplus.com/en/docs/24/7810#detail) |Detailed information. |

#### detail

|**Parameter** |**Data Type** |**Description** |
|---|---|---|
|priority |Integer |The stream pushing priority. A larger value indicates a higher priority. |
|time |Integer |The stream pushing start time. Unix timestamp, in seconds. |
|time_ms |Integer |The stream pushing start time. Unix timestamp, in milliseconds. |
|transcoded |Boolean |Whether the stream in this callback is a transcoded stream. Valid values:<br><br><br>* `true`: Transcoded stream.<br><br>* `false`: Non\-transcoded stream.<br><br><br>> **Note**<br><br><br>> To trigger callbacks for transcoded streams, you must enable **Applies to transcoded stream** in the callback configuration. For details, see [Callback configurations](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-a-callback-task).<br> |
|fp_node_ip |String |The IP address of the stream pushing node. |
|fp_client_ip |String |The IP address of the stream pushing client. |
|fp_user_url |String |The URL parameters carried in the stream push request. |
|location_ip |String |Deprecated. |
|location_port |Integer |Deprecated. |
|push_protocol |String |The stream pushing protocol. Valid values:<br><br><br>* `rtmp`: RTMP.<br><br>* `rtmps`: RTMPS.<br><br>* `srt`: SRT.<br><br>* `rts`: RTM.<br><br>* `rtsp`: RTSP.<br><br>* `unknown`: Unrecognized. |
|session_id |String |The session ID of the current stream push. |
|sequence_id |String |The sequence ID that uniquely identifies the current stream push. |
|stream_params |String |Platform\-reserved parameter. Ignore it if you have no special requirements. |

Below is a sample callback message:

```JSON
{
    "code":0,
    "message":"ok",
    "data":{
        "vhost":"push.example.com",
        "domain":"push.example.com",
        "app":"live",
        "stream":"test",
        "event_type":"push_start",
        "sign":"xxxxx",
        "t":1787747992,
        "uniq_id":"push.example.com:live:test_on_publish_start_1045216675",
        "detail":{
            "priority":0,
            "time":1787665054,
            "time_ms":1787665054820,
            "transcoded":false,
            "fp_node_ip":"111.**.***.154",
            "fp_client_ip":"117.***.**.85",
            "fp_user_url":"",
            "location_ip":"10.***.***.45",
            "location_port":1935,
            "push_protocol":"rtmp",
            "session_id":"1045216675",
            "sequence_id":"1824004938.n.cn-cn3130g1.54012_3287659",
            "stream_params":""
        }
    }
}
```

### Stream pushing ends

When stream pushing ends, BytePlus MediaLive sends a callback message to your configured callback URL. For details about configuring callback URLs, see [Configuring a callback task](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-a-callback-task).

|**Parameter** |**Data Type** |**Description** |
|---|---|---|
|vhost |String |The domain name space. |
|domain |String |The domain name for stream pushing. |
|app |String |The `AppName`. |
|stream |String |The `StreamName`. |
|event_type |String |The event type, which is `push_end` for this callback. |
|sign |String |The common security signature parameter used to verify that the callback request comes from BytePlus MediaLive. For more information, see [Common security signature parameters](https://docs.byteplus.com/en/docs/24/7810#common-security-signature-parameters). |
|t |Long |The common security signature parameter that indicates the request expiration time. For more information, see [Common security signature parameters](https://docs.byteplus.com/en/docs/24/7810#common-security-signature-parameters). |
|uniq_id |String |The event ID, used for event deduplication. |
|detail |Object of [detail](https://docs.byteplus.com/en/docs/24/7810#detail-1) |Detailed information. |

#### detail

|**Parameter** |**Data Type** |**Description** |
|---|---|---|
|time |Integer |The stream pushing end time. Unix timestamp, in seconds. |
|time_ms |Integer |The stream pushing end time. Unix timestamp, in milliseconds. |
|priority |Integer |The stream pushing priority. A larger value indicates a higher priority. |
|errmsg |String |The reason the stream push ends. For more information, see [Stream interruption reasons](https://docs.byteplus.com/en/docs/24/7810#stream-interruption-reasons). |
|err_msg_v2 |String |The reason the stream push ends. |
|errcode |Integer |The code indicating why the stream push ends. |
|fp_node_ip |String |The IP address of the stream pushing node. |
|fp_client_ip |String |The IP address of the stream pushing client. |
|fp_user_url |String |The URL parameters carried in the stream push request. |
|location_ip |String |Deprecated. |
|location_port |Integer |Deprecated. |
|push_duration |Integer |The stream pushing duration, in milliseconds. This parameter adds an extra 10 minutes to the actual stream pushing duration. For example, if the actual stream pushing duration is 2 minutes, this parameter value is 720000, which is 720 seconds or 12 minutes.<br><br>> **Note**<br><br><br>> BytePlus MediaLive charges only based on the actual stream pushing duration.<br> |
|push_protocol |String |The stream pushing protocol. Valid values:<br><br><br>* `rtmp`: RTMP.<br><br>* `rtmps`: RTMPS.<br><br>* `srt`: SRT.<br><br>* `rts`: RTM.<br><br>* `rtsp`: RTSP.<br><br>* `unknown`: Unrecognized. |
|session_id |String |The session ID of the current stream push. |
|sequence_id |String |The sequence ID that uniquely identifies the current stream push. |
|stream_params |String |Platform\-reserved parameter. Ignore it if you have no special requirements. |
|transcoded |Boolean |Whether the stream in this callback is a transcoded stream. Valid values:<br><br><br>* `true`: Transcoded stream.<br><br>* `false`: Non\-transcoded stream.<br><br><br>> **Note**<br><br><br>> To trigger callbacks for transcoded streams, you must enable **Applies to transcoded stream** in the callback configuration. For details, see [Callback configurations](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-a-callback-task).<br> |

Below is a sample callback message:

```JSON
{
    "code":0,
    "message":"ok",
    "data":{
        "vhost":"push.example.com",
        "domain":"push.example.com",
        "app":"live",
        "stream":"test",
        "event_type":"push_end",
        "sign":"xxxxxx",
        "t":1787747992,
        "uniq_id":"push.example.com:live:test_on_publish_stop_1234567890",
        "detail":{
            "time":1640849502,
            "time_ms":1640849502762,
            "priority":0,
            "transcoded":false,
            "errmsg":"func:OnStop:eof",
            "fp_node_ip":"10.**.**.1",
            "fp_client_ip":"10.**.**.2",
            "fp_user_url":"",
            "location_ip":"10.**.**.1",
            "location_port":1935,
            "push_duration":720000,
            "push_protocol":"rtmp",
            "session_id":"3693930911_150.139.***.***",
            "sequence_id":"027-20241313130E.1231423483",
            "stream_params":"",
            "errcode":0,
            "err_msg_v2":"The reason for the streaming disconnection is unknown"
        }
    }
}
```

### A recording event

When a recorded file from a live stream is stored, BytePlus MediaLive sends a callback message to your configured callback URL. For details about configuring callback URLs, see [Configuring a callback task](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-a-callback-task).

|Parameter |Data Type |Description |
|---|---|---|
|account_id |String |Your account ID. |
|vhost |String |The domain name space. |
|domain |String |The domain name for stream pushing. |
|app |String |The `AppName`. |
|stream |String |The `StreamName`. |
|event_type |String |The event type, which is `record_event` for this callback. |
|sign |String |The common security signature parameter used to verify that the callback request comes from BytePlus MediaLive. For more information, see [Common security signature parameters](https://docs.byteplus.com/en/docs/24/7810#common-security-signature-parameters). |
|t |Long |The common security signature parameter that indicates the request expiration time. For more information, see [Common security signature parameters](https://docs.byteplus.com/en/docs/24/7810#common-security-signature-parameters). |
|detail |Object of [detail](https://docs.byteplus.com/docs/byteplus-media-live/docs-callback-description#263467b3) |Detailed information. |

#### detail

|Parameter |Data Type |Description |
|---|---|---|
|tos_bucket |String |The name of the TOS bucket where the recorded file is stored.<br><br>> **Note**<br><br><br>> This parameter has a value only when the recorded file is stored in TOS.<br> |
|uri |String |The `vid` of the recorded file in BytePlus VOD.<br><br>> **Note**<br><br><br>> This parameter has a value only when the recorded file is stored in VOD.<br> |
|tos_object |String |The recorded file path. When the recorded file is stored in TOS, the value is the full path of the recorded file in TOS. When the recorded file is stored in VOD, the value is the same as `vod_filename`. |
|duration |Integer |The length of the recording, in milliseconds. |
|duration_ms |Integer |Deprecated. |
|start_time |Integer |The start time of the recording. Unix timestamp, in seconds. |
|start_time_ms |Integer |Deprecated |
|stop_time |Integer |The end time of the recording. Unix timestamp, in seconds. |
|format |String |The recording format. Valid values:<br><br><br>* `mp4`<br><br>* `m3u8`<br><br>* `flv` |
|url |String |The address of the recorded file stored in TOS.<br><br>> **Note**<br><br><br>> This parameter has a value only when the recorded file is stored in TOS. You can obtain the playback address from BytePlus VOD by using `uri` or `vod_filename`.<br> |
|data_source |String |Deprecated. |
|account_id |String |Your account ID. |
|task_id |String |The task ID. |
|size |Long |The size of the recorded file, in bytes. |
|width |Integer |The width of the recorded file, in pixels. |
|height |Integer |The height of the recorded file, in pixels. |
|extra |String |Deprecated. |
|s3_endpoint |String |Deprecated. |
|codec |String |Deprecated. |
|vod_filename |String |The file path of the recorded file in BytePlus VOD.<br><br>> **Note**<br><br><br>> This parameter has a value only when the recorded file is stored in VOD.<br> |

Below is a sample callback message when a recorded file is stored in a VOD space.

```json
{
    "code":0,
    "message":"ok",
    "data":{
        "account_id":"10000**",
        "vhost":"push.example.com",
        "domain":"push.example.com",
        "app":"live",
        "stream":"test",
        "event_type":"record_event",
        "sign":"xxxx",
        "t":1787747992,
        "detail":{
            "tos_bucket":"",
            "tos_object":"record/push.example.com/live/test_1640847072_1640849947_record.m3u8",
            "uri":"v0df17g10000ca6ut9pka0prk****pig",
            "duration":2868674,
            "duration_ms":2868674,
            "start_time":1640847072,
            "start_time_ms":0,
            "stop_time":1640849947,
            "format":"m3u8",
            "url":"",
            "data_source":"",
            "account_id":"10000**",
            "task_id":"1234",
            "size":28361,
            "width":1280,
            "height":720,
            "extra":"{}",
            "s3_endpoint":"",
            "codec":"",
            "vod_filename":"record/push.example.com/live/test_1640847072_1640849947_record.m3u8"
        }
    }
}
```

Below is a sample callback message when a recorded file is stored in a TOS bucket.

```json
{
    "code": 0,
    "message": "ok",
    "data": {
        "account_id":"10000**",
        "vhost": "push.example.com",
        "domain": "push.example.com",
        "app": "live",
        "stream": "test",
        "event_type": "record_event",
        "sign":"xxxx",
        "t":1787747992,
        "detail": {
            "tos_bucket": "livetest",
            "tos_object": "record/record/push.example.com/live/test/1653469134_1653469220.m3u8",
            "uri": "",
            "duration": 84430,
            "duration_ms":84430,
            "start_time": 1653469134,
            "start_time_ms":0,
            "stop_time": 1653469220,
            "format": "m3u8",
            "url": "http://livetest.tos.volces.com/record/record/push.example.com/live/test/1653469134_1653469220.m3u8",
            "data_source":"",
            "account_id": "10000**",
            "task_id":"1234",
            "size": 689,
            "width":1280,
            "height":720,
            "extra":"{}",
            "s3_endpoint":"",
            "codec":"",
            "vod_filename":""
        }
    }
}
```

### A screenshot event

When a live screenshot is stored, BytePlus MediaLive sends a callback message to your configured callback URL. For details about configuring callback URLs, see [Configuring a callback task](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-a-callback-task).

|Parameter |Data Type |Description |
|---|---|---|
|Vhost |String |The domain name space. |
|Domain |String |The domain name for stream pushing. |
|App |String |The `AppName`. |
|Stream |String |The `StreamName`. |
|StreamURL |String |Deprecated. |
|Bucket |String |The name of the TOS bucket where the screenshot is stored. |
|ObjectKey |String |The storage path to the screenshot. |
|Height |Integer |The height of the screenshot, in pixels. |
|Width |Integer |The width of the screenshot, in pixels. |
|Format |String |The image format. Valid values:<br><br><br>* `jpg`<br><br>* `jpeg` |
|TimeStamp |Integer |The time the screenshot was taken. Unix timestamp, in seconds. |
|AccountId |String |Your account ID. |
|event_type |String |The event type, which is `snapshot_event` for this callback. |
|sign |String |The common security signature parameter used to verify that the callback request comes from BytePlus MediaLive. For more information, see [Common security signature parameters](https://docs.byteplus.com/en/docs/24/7810#common-security-signature-parameters). |
|t |Long |The common security signature parameter that indicates the request expiration time. For more information, see [Common security signature parameters](https://docs.byteplus.com/en/docs/24/7810#common-security-signature-parameters). |

Below is a sample callback message:

```json
{
    "Vhost":"push.example.com",
    "Domain":"push.example.com",
    "App":"live",
    "Stream":"test",
    "StreamURL":"",
    "Bucket":"bucket1",
    "ObjectKey":"push.example.com/live/test/20211****.jpeg",
    "Height":864,
    "Width":480,
    "Format":"jpeg",
    "TimeStamp":1640849845,
    "AccountId": "2000****74",
    "event_type":"snapshot_event",
    "sign":"xxxx",
    "t":1787747992
}
```

### A relay event

When a relay task starts, ends, starts relaying a live stream or VOD file, triggers an alarm, or is interrupted, BytePlus MediaLive sends a callback message to your configured callback URL. For details about configuring callback URLs, see [Configuring a relay task](https://docs.byteplus.com/docs/byteplus-media-live/docs-relay).

|Parameter |Data Type |Description |
|---|---|---|
|action |String |The event type that triggers this callback. Valid values:<br><br><br>* `init`: The task starts.<br><br>* `done`: The task ends.<br><br>* `live_start`: Starts relaying a live stream.<br><br>* `vod_start`: Starts relaying a VOD file.<br><br>* `alarm`: A task alarm is triggered.<br><br>* `stop`: The stream is interrupted. |
|description |String |A brief description of the reason for the stream interruption or alarm.<br><br>> **Note**<br><br><br>> This parameter is returned only when `action` is `alarm` or `stop`.<br> |
|event_time |Integer |The time when this callback is triggered. Unix timestamp, in nanoseconds. |
|task_id |String |The ID of the relay task you create. |
|dst |String |The push stream address. |
|type |Integer |The video source type. Valid values:<br><br><br>* `0`: Live stream.<br><br>* `1`: VOD. |
|cycle_mode |Integer |The loop mode of the VOD file. Valid values:<br><br><br>* `-1`: The VOD file loops indefinitely.<br><br>* `0`: The VOD file loops a specified number of times.<br><br><br>> **Note**<br><br><br>> This parameter takes effect only when the video source is VOD (`type` is `1`).<br> |
|event_type |String |The event type, which is `live_pull_to_push` for this callback. |
|src |String |The video source address.<br><br><br>* When the video source is a live stream (`type` is `0`), this parameter indicates the pull stream address of the live stream.<br><br>* When the video source is VOD (`type` is `1`), this parameter indicates the playback address of the current VOD file. |
|play_progress |Float |The playback duration of the current VOD file, in seconds, with two decimal places.<br><br>> **Note**<br><br><br>> This parameter is returned only when the video source is VOD (`type` is `1`) and the playback duration is greater than `0`.<br> |
|msg |Object of [CallbackMsg](https://docs.byteplus.com/docs/byteplus-media-live/docs-callback-description#cd95ef28) |Detailed information. |

#### CallbackMsg

|Parameter |Data Type |Description |
|---|---|---|
|type |String |Type of callback message. The following values are supported:<br><br><br>* `PullFileUnstable`: When the callback `action` is `alarm`, it indicates that pulling the source stream in the relay task is unstable.<br><br>* `PushStreamUnstable`: When the callback `action` is `alarm`, it indicates that pushing the stream in the relay task is unstable.<br><br>* `PullFileFailed`: When the callback `action` is `stop`, it indicates that the relay task ended because pulling the source stream failed.<br><br>* `PushStreamFailed`: When the callback `action` is `stop`, it indicates that the relay task ended because pushing the stream failed.<br><br>* `FileEndEarly`: When the callback `action` is `stop`, it indicates that the task ended earlier than the scheduled end time, possibly due to the VOD file reaching the maximum number of playback times. |
|error |String |Error type when the callback indicates an exception. |
|message |String |Error description when the callback indicates an exception. |

Below is a sample callback message:

```json
{
    "action":"stop",
    "description": "src_addr_invalid",
    "event_time":1650263223542095385,
    "task_id":"5f4c37605b7d711b51e28d73fa60****",
    "dst":"rtmp://push.example.com/live/teststream",
    "type":1,
    "cycle_mode":-1,
    "event_type": "live_pull_to_push",
    "src":"http://pull.example.com/live/test.m3u8",
    "play_progress":10.00,
    "msg": {
      "type": "PullFileFailed",
      "error": "HTTP_NOT_FOUND",
      "message": "Server returned 404 Not Found"
    }
}
```

### AI Dubbing

When an AI Dubbing task starts or ends, stream relay succeeds or fails, an alarm is triggered, or subtitles are generated, BytePlus MediaLive sends a callback message to your configured callback URL. This callback applies to AI Dubbing tasks and subtitle configurations. For details about configuring callback URLs, see [AI Dubbing](https://docs.byteplus.com/docs/byteplus-media-live/ai-liveinterpret-simultaneous-audio-and-video-interpretation) or [Subtitle configuration](https://docs.byteplus.com/docs/byteplus-media-live/docs-manage-subtitle-configuration).

|Parameter |Data Type |Description |
|---|---|---|
|action |String |The event type that triggers this callback. Valid values:<br><br><br>* `speech_init`: The task starts. This callback is triggered when the AI Dubbing task reaches the relay start time.<br><br>* `speech_done`: The task ends. This callback is usually triggered when the AI Dubbing task reaches the relay end time. If `msg.type` is `speech_done`, the AI Dubbing task exited unexpectedly.<br><br>* `speech_opt_start`: Stream relay succeeds.<br><br>* `speech_opt_stop`: Stream relay fails.<br><br>* `speech_subtitle`: Subtitle content is generated.<br><br>* `speech_alarm`: A task alarm is triggered. The live stream is not interrupted, but an exception occurs during translation processing. |
|event_type |String |The event name. The value is fixed to `speech_event`, indicating an AI Dubbing event. |
|event_time |Long |The time when this callback is triggered. Unix timestamp, in nanoseconds. |
|task_id |String |The AI Dubbing task ID.<br><br>> **Note**<br><br><br>> This parameter is returned only for callbacks triggered by an AI Dubbing task.<br> |
|opt_url |Array of String |The relay push stream addresses. The AI Dubbing task pushes the processed live stream to these addresses.<br><br>> **Note**<br><br><br>> This parameter is returned only for callbacks triggered by an AI Dubbing task.<br> |
|src_url |String |The address from which the AI Dubbing task pulls the source stream.<br><br>> **Note**<br><br><br>> This parameter is returned only for callbacks triggered by an AI Dubbing task.<br> |
|vhost |String |The domain name space.<br><br>> **Note**<br><br><br>> This parameter is returned only for callbacks triggered by a subtitle configuration.<br> |
|app |String |The `AppName`.<br><br>> **Note**<br><br><br>> This parameter is returned only for callbacks triggered by a subtitle configuration.<br> |
|stream |String |The `StreamName`.<br><br>> **Note**<br><br><br>> This parameter is returned only for callbacks triggered by a subtitle configuration.<br> |
|suffix |String |The subtitle suffix.<br><br>> **Note**<br><br><br>> This parameter is returned only for callbacks triggered by a subtitle configuration.<br> |
|pipe |String |The task type. Valid values:<br><br><br>* `si`: AI Dubbing mode. This mode is suitable for conference live streams and other scenarios that require strong synchronization and immersion.<br><br>* `mix`: Subtitle Only mode.<br><br>* `realtime`: Real\-time interpretation mode. This mode is suitable for latency\-sensitive scenarios such as sports live streams. |
|lip_sync |Boolean |Whether lip sync is enabled. Valid values:<br><br><br>* `true`: Enabled. After this feature is enabled, the speaker's lip movements are synchronized with the dubbed audio, making the live stream more immersive.<br><br>* `false`: Disabled.<br><br><br>> **Note**<br><br><br>> This parameter is returned only when `pipe` is `si`.<br> |
|voice_show |Boolean |In real\-time interpretation mode (`pipe` is `realtime`), specifies whether dubbed audio is enabled. Valid values:<br><br><br>* `true`: Enabled. After this feature is enabled, translated speech with voice cloning is provided.<br><br>* `false`: Disabled.<br><br><br>> **Note**<br><br><br><br>* > This parameter is returned only when `pipe` is `realtime`.<br><br><br>* > When `pipe` is `si`, dubbed audio is enabled by default.<br> |
|delay |Long |The playback delay, in seconds. |
|src_language |String |The source language. |
|opt_language |Array of String |The target languages. |
|msg |Object of [msg](https://docs.byteplus.com/en/docs/24/7810#hXzRw3taf) |The callback details.<br><br>> **Note**<br><br><br>> This parameter has a value only when an exception occurs or subtitles are generated.<br> |

#### msg

|Parameter |Data Type |Description |
|---|---|---|
|type |String |Additional information about why this callback is triggered. Valid values:<br><br><br>* `speech_opt_stop`: Stream relay fails due to pull or push stream failures or other unknown reasons.<br><br>* `speech_alarm`: A task alarm is triggered due to translation processing exceptions, disconnections, or other issues.<br><br>* `speech_done`: The AI Dubbing task exited unexpectedly.<br><br>* `speech_subtitle`: Subtitle content is generated. |
|message |String |The callback message.<br><br><br>* For exception callbacks, this parameter indicates the error details.<br><br>* When `type` is `speech_subtitle`, the value is a JSON string. For details, see [message](https://docs.byteplus.com/en/docs/24/7810#huB1bcftm). |

#### message

|Parameter |Data Type |Description |
|---|---|---|
|text |String |The subtitle text. |
|time |Long |The system time when the subtitles are generated. Unix timestamp, in milliseconds.<br><br>This time is calculated based on the first\-frame system time and the subtitle PTS (presentation timestamp) offset. |
|language |String |The subtitle language. |
|definite |Boolean |Whether the subtitle text is a complete sentence. Currently, the value is fixed to `true`. |
|start_time |Long |The subtitle start time, corresponding to the PTS of the source stream, in milliseconds. |
|end_time |Long |The subtitle end time, corresponding to the PTS of the source stream, in milliseconds. |
|sequence |Long |The subtitle sequence ID. The value keeps increasing. |
|term |Long |Used to determine whether a stream interruption occurred between two consecutive callbacks. If this callback and the previous callback have different `term` values, a stream interruption occurred between the two callbacks. You can check `errmsg` in the [Stream pushing ends](https://docs.byteplus.com/en/docs/24/7810#stream-pushing-ends) callback to identify the cause of the interruption. |
|words |Array of [words](https://docs.byteplus.com/en/docs/24/7810#hXv1hAbI1) |The segmented word information. For details, see [words](https://docs.byteplus.com/en/docs/24/7810#hXv1hAbI1).<br><br>> **Note**<br><br><br>> This parameter is returned only in Original (ASR) subtitles mode.<br> |

#### words

|Parameter |Data Type |Description |
|---|---|---|
|text |String |The segmented word. |
|start_time |Long |The word start time, corresponding to the PTS of the source stream, in milliseconds. |
|end_time |Long |The word end time, corresponding to the PTS of the source stream, in milliseconds. |

Below is a sample callback message for an AI Dubbing task:

```JSON
{
    "action": "speech_done",
    "event_type": "speech_event",
    "event_time": 1786087231912211287,
    "task_id": "11***11",
    "opt_url": [
        "rtmp://push.example.com/live/test"
    ],
    "src_url": "https://pull.example.com/live/test.flv",
    "pipe": "si",
    "lip_sync": true,
    "delay": 3,
    "src_language": "zh",
    "opt_language": [
        "en"
    ],
    "msg": {
        "type": "",
        "message": ""
    }
}
```

Below is a sample callback message for a subtitle configuration:

```JSON
{
    "action": "speech_subtitle",
    "event_type": "speech_event",
    "event_time": 1786087231912211287,
    "vhost": "push.example.com",
    "app": "live",
    "stream": "test",
    "suffix": "_uhd",
    "pipe": "mix",
    "delay": 8,
    "src_language": "zh",
    "opt_language": [
        "en"
    ],
    "msg": {
        "type": "speech_subtitle",
        "message": "[{\"text\":\"This is a test.\",\"time\":1723433155645,\"language\":\"en\",\"definite\":true,\"start_time\":3000,\"end_time\":6000,\"sequence\":0,\"term\":0}]"
    }
}
```

## Stream interruption reasons

The following table describes common stream interruption reasons. If the reason you receive is not listed or you cannot determine how to handle it, [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) to contact technical support.

|errmsg |Description |
|---|---|
|func:HandleInputPacket:net:func:Input:rtmp:FLV Signature don't match |Stream pushing is disconnected because FLV protocol parsing failed. |
|func:HandleInputPacket:net:func:Input:rtmp:close stream id 0 don't match 1 |Stream pushing is disconnected because of RTMP protocol incompatibility. |
|func:conn.Read:net:local error: tls: bad record MAC |Stream pushing is disconnected because of a TLS protocol failure. |
|func:timeout:idle_too_long |Stream pushing times out and is disconnected because the stream pushing client has not sent data for a long time. |
|io:conn_reset_by_peer |Stream pushing is disconnected because the stream pushing client did not stop the live stream normally, such as due to network interruption or directly closing the stream pushing software. |
|func:conn.Read:net:read_i/o_timeout |Stream pushing is disconnected because of a data I/O error in BytePlus MediaLive. |
|param:Priority:priority |A low\-priority stream is disconnected because it is replaced by a high\-priority stream. |
|auth:JudgePublishAuth:timeout:invalid_sign |Stream pushing is disconnected because URL authentication parameters are invalid or authentication times out. |
|stream:invalid_sign |Stream pushing is disconnected because authentication failed. |
|func:JudgePublishAuth:timeout:invalid_sign |Stream pushing is disconnected because authentication failed. |
|func:OnStatus:func:RtmpStatusCode2NssError:not_allowed |Stream pushing is disconnected because the live stream is disabled. |
|func:OnStatus:func:RtmpStatusCode2NssError:api_close |The live stream is disconnected by calling the `KillStream` API. |
|func:sendEvent:param:receiver:not_running |An internal error occurs in BytePlus MediaLive. Contact [technical support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980). |
|auth:remote_auth:not_allowed |Stream pushing is disconnected because remote authentication failed. |
|auth:JudgePublishAuth:param:MissParam:invalid_sign |Stream pushing is disconnected because authentication parameters are missing. |
|func:conn.Read:eof |Stream pushing is disconnected due to complex reasons. Contact [technical support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980). |
|func:JudgePublishAuth:param:MissParam:invalid_sign |Stream pushing is disconnected because authentication parameters are not found. |
|func:handleOnTime:func:timeout:idle_too_long |Stream pushing is disconnected because no data is received before timeout. |
|func:OnStop:eof |The stream pushing client ends stream pushing normally by stopping the live stream. |
|func:conn.Read:net:The socket was properly connected, but the connection has been broken |Stream pushing is disconnected because of a network anomaly. |
|func:OnStatus:func:RtmpStatusCode2NssError:duplicate |Stream pushing is disconnected because another stream is pushed with the same stream name. |
|auth:BypassAuthPub:invalid_sign |Stream pushing is disconnected because remote authentication failed. |

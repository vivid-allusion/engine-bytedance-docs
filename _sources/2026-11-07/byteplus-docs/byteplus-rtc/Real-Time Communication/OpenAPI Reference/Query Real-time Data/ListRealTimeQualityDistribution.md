---
title: "ListRealTimeQualityDistribution"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-163729"
---

<span id="description"></span>
## Description

Call `ListRealTimeQualityDistribution` to track the performance of your App in real time across a range of dimensions, including first\-level administrative divisions, countries, operation systems, and network types.

<span id="restriction"></span>
## Restriction


|Category |Frequency capping |
|---|---|
|Maximum number of queries |* **10** times per minute<br><br>* **1440** times per day |
|The furthest queryable time |Last **60** minutes |
|Maximum time span of single query |**60** minutes |
|Data Delay |**1** minute |


<span id="make-a-call"></span>
## Make a call

For the service address, communication protocol, character encoding, and signature mechanism of the interface, see [Call OpenAPI](https://docs.byteplus.com/en/docs/12/docs-69828).

<span id="request-method"></span>
### Request method

POST

<span id="request-parameter"></span>
### Request parameter

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters ](https://docs.byteplus.com/en/docs/12/docs-69828#request-parameters).

<span id="query"></span>
#### Query


|**Parameter** |**Data Type** |**Required** |**Description** |
|---|---|---|---|
|Action |String |Yes |The action to perform. Example: `ListRealTimeQualityDistribution` |
|Version |String |Yes |The API version to use. Example: `2020-12-01` |


<span id="body"></span>
## Body


|**Parameter** |**Data Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|AppId |String |Yes |`Your_AppId` |The only identifier for your audio & video app |
|StartTime |String |Yes |`2022-05-22T12:00:00+08:00` |Start timestamp for querying in the format of RFC3339 in second |
|EndTime |String |Yes |`2022-05-22T12:59:00+08:00` |End timestamp for querying in the format of RFC3339 in second |
|**Indicator** |String |Yes |`join_room_success_rate` |The performance indicators. **Choose only one indicator per query.**  For more information about the performance indicators, see [Performance Indicators](https://docs.byteplus.com/en/docs/12/14236#performanceindicators). |
|**Dimension** |String |Yes |`Province` |The query dimensions. **Choose only one dimension per query.** <br><br>You can choose from the following dimensions:<br><br><br>* **Province.** <br><br>   First\-level administrative divisions such as China's 23 provinces, 5 autonomous regions (Inner Mongolia, Guangxi, Tibet, Ningxia, Xinjiang), 4 municipalities (Beijing, Tianjin, Shanghai, Chongqing), 2 Special Administrative Regions(Hong Kong and Macao), and Taiwan.<br><br>* **Country**<br><br>* \*\*OS.\*\*The Operation System.<br><br><br>Include: `Android`, `iOS`, `macOS`, `Windows`, `Linux`<br><br><br>* **Access.**  The network type, including `2G`,`3G`,`4G`,`5G`,`Wi-Fi` |


**Performance Indicators**  


|**Indicator** |**Description** |
|---|---|
|`join_room_success_rate` |The success rate of joining a room within a period of time(%).<br><br>For example, `5s_join_room_success_rate` means the success rate of joining a room within 5s.<br><br>The default value for the time used to join a room is **5s**. |
|`stall_rate` |The percentage of time during an audio and video call when the stuttering(ms) is within a period of time(%).<br><br>For example, `80ms_audio_stall_rate` means the percentage of time during a call when audio stuttering(ms) is within 80ms.<br><br><br>* The default value for audio stuttering is **80ms**.<br><br>* The default value for video stuttering is **500ms**. |
|`first_frame_send_success_rate` |The success rate of sending the first frame(%). |
|`first_frame_recv_success_rate` |The success rate of decoding the first frame (%). |
|`network_trans_delay` |The percentage of time during an audio and video call when the transmission delay (ms) between users is within a period of time(%).<br><br>For example, `400ms_video_network_trans_delay` means the percentage of time during a call when the delay in video transmission is within 400ms.<br><br>The default value for transmission delay is **400 ms**. |


<span id="request-example"></span>
### Request example

<span id="query"></span>
## Query

```postscript
https://open.byteplusapi.com?Action=ListRealTimeQualityDistribution&Version=2020-12-01
```


<span id="body"></span>
## Body

```json
{
    "AppId": "Your_AppId",
    "StartTime": "2022-12-12T14:00:00+08:00",
    "EndTime": "2022-12-12T14:01:00+08:00",
    "Indicator": [
        "join_room_success_rate"
    ],
    "Dimension":"OS"
}
```


<span id="return-parameter"></span>
### Return Parameter

\*\*Result: \*\*


|**Parameter** |**Data Type** |**Description** |
|---|---|---|
|**Indicators** |Array of [Indicator](https://docs.byteplus.com/en/docs/12/14236#indicator) |The indicator name. |


**Indicator**  


|**Parameter** |**Data Type** |**Example** |**Description** |
|---|---|---|---|
|**Name** |string |`5s_join_room_success_rate` |The indicator name. |
|Data |Array of [DataItem](https://docs.byteplus.com/en/docs/12/14236#dataitem) | | |


**DataItem**  


|**Parameter** |**Data Type** |**Description** |
|---|---|---|
|**Timestamp** |String |The start time of your query. Use the RFC 3339 format. |
|**Dimension** |String |The query dimension. |
|**Value** |float |The indicator data. Display only two digits after the decimal point. |


<span id="response"></span>
## Response

<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata":{
        "RequestId":"Your_RequestId",
        "Action":"ListRealTimeQualityDistribution",
        "Version":"2020-12-01",
        "Service":"rtc",
        "Region":"ap-singapore-1"
    },
    "Result":{
        "Indicators": [
            {
                "Name": "5s_join_room_success_rate",
                "Data": [
                    {
                        "TimeStamp": "2022-12-12T14:00:00+08:00",
                        "Value": 99.05,
                        "Dimension": "windows"
                    },
                    {
                        "TimeStamp": "2022-12-12T14:00:00+08:00",
                        "Value": 99.24,
                        "Dimension": "ios"
                    },
                    {
                        "TimeStamp": "2022-12-12T14:00:00+08:00",
                        "Value": 99.12,
                        "Dimension": "android"
                    },
                    {
                        "TimeStamp": "2022-12-12T14:00:00+08:00",
                        "Value": 99.83,
                        "Dimension": "mac"
                    },
                    {
                        "TimeStamp": "2022-12-12T14:00:00+08:00",
                        "Value": 100,
                        "Dimension": "linux"
                    },
                    {
                        "TimeStamp": "2022-12-12T14:00:30+08:00",
                        "Value": 99.82,
                        "Dimension": "mac"
                    },
                    {
                        "TimeStamp": "2022-12-12T14:00:30+08:00",
                        "Value": 99.49,
                        "Dimension": "linux"
                    },
                    {
                        "TimeStamp": "2022-12-12T14:00:30+08:00",
                        "Value": 98.98,
                        "Dimension": "android"
                    },
                    {
                        "TimeStamp": "2022-12-12T14:00:30+08:00",
                        "Value": 99.15,
                        "Dimension": "ios"
                    },
                    {
                        "TimeStamp": "2022-12-12T14:00:30+08:00",
                        "Value": 99.06,
                        "Dimension": "windows"
                    }
                ]
            }
        ]
    }
}
```

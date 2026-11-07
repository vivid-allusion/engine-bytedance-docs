---
title: "UpdateRecord"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/updaterecord-wtn"
---

After you enable Cloud Recording and make a custom layout in mixing\-stream recording mode, you can update configuration parameters relevant to recording. You can use the `UpdateRecord` OpenAPI to do this.

For information on how to enable cloud recording, see [StartRecord](https://docs.byteplus.com/en/docs/12/startrecord-wtn).

<span id="description"></span>
## Description

You can call the `UpdateRecord` to override the following parameters previously set in `StartRecord` or `UpdateRecord`:


* `TargetWTNStreams`

* `Layout.CustomLayout.Canvas.Background` and `Layout.CustomLayout.Canvas.BackgroundImage`

* `Layout.CustomLayout.Regions`


<span id="prerequisites"></span>
## Prerequisites

You must have enabled cloud recording and use mixing\-stream mode.

Only `RecordMode =0` and `Layout.LayoutMode=2` when you call `StartRecord`, this API can only be called, that is, task parameters can only be updated in the custom layout mode of mixing\-stream recording.

<span id="make-a-call"></span>
## Make a call

For the service address, communication protocol, character encoding, and signature mechanism of the API, see [Call OpenAPI](https://docs.byteplus.com/en/docs/12/docs-69828).

<span id="request-method"></span>
### Request method

POST

<span id="request-parameters"></span>
### Request parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters](https://docs.byteplus.com/en/docs/12/docs-69828#request-parameters).

<span id="query"></span>
#### Query


|Parameter |Type |Required |Example |Description |
|---|---|---|---|---|
|Action |String |Yes |`UpdateRecord` |API name. The value of this API: `UpdateRecord`. |
|Version |String |Yes |`2022-06-01` |OpenAPI version. The value of this API: `2022-06-01`. |


<span id="body"></span>
#### Body


|Parameter |Type |Required |Example |Description |
|---|---|---|---|---|
|AppId |String |Yes |`Your_AppId` |The only identifier for your audio & video app |
|BusinessId |String |No |`Your_BusinessId` |The Business identifier for your audio & video app |
|TargetType |Uint32 |Yes |`1` |`1` for WTN streams. |
|TaskId |String |Yes |`Your_TaskId` |Task ID of cloud recording. |
|TargetWTNStreams |[WTNStreamList](https://docs.byteplus.com/en/docs/12/docs-115995#wtnstreamlist) |No |\- |You can use this parameter to set streams to be recorded. The maximum number of streams recorded is 5 in mixing\-stream or single\-stream recording. When you use an empty list, you are not recording any WTN stream. |
|Layout |[Layout](https://docs.byteplus.com/en/docs/12/docs-115995#wtnlayout) |No |\- |Layout parameters. |


<span id="request-sample-code"></span>
### Request sample code

<span id="query"></span>
#### Query

```json
https://open.byteplusapi.com?Action=UpdateRecord&Version=2022-06-01
```


<span id="body"></span>
#### Body

```json
{
    "AppId": "663e22",
    "BusinessId": "Your_BusinessId",
    "TaskId": "Task1",
    "TargetWTNStreams": {
        "WTNStreamList": [
            { 
                "Index": 0,
                "StreamId": "streamId1" 
            },
        ]
    },
    "Layout": {
        "LayoutMode": 2,
        "CustomLayout": {
            "Canvas": { 
                "Width": 1280,
                "Height": 720,
                "Background": "#cca085" 
            },
            "Regions": [
                { 
                    "StreamIndex": 0,
                    "LocationX": 0,
                    "LocationY": 0,
                    "WidthProportion": 0.75,
                    "HeightProportion": 0.75,
                    "ZOrder": 0,
                    "Alpha": 1,
                    "RenderMode": 1 
                }
            ]
        }
    },
    "TargetType": 1
}
```


<span id="response"></span>
## Response

`Result` returns "ok" only when the request succeeds and null when it fails.

<span id="sample-response"></span>
### Sample response

```json
{
    "Result": "ok",
    "ResponseMetadata": {
        "RequestId": "Your_RequestId",
        "Action": "UpdateRecord",
        "Version": "2022-06-01",
        "Service": "rtc",
        "Region": "ap-singapore-1"
    }
}
```

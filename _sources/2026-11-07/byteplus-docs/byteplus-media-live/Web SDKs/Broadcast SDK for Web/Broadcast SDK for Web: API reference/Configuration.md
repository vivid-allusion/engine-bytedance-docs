---
title: "Configuration"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-configuration"
---

<span id="configoptions"></span>
## ConfigOptions

The initialization configuration options for BytePlus MediaLive Broadcast SDK specify the timeout, retry attempts, interval duration, and streaming mode.

<span id="property"></span>
### Property


|Property |Type |Description |
|---|---|---|
|timeout |number |The timeout for requesting the push stream address, in milliseconds. |
|retryCount |number |The number of retry attempts after failing to request the push stream address. |
|retryDelay |number |Interval time for retrying the request for the push stream address, in milliseconds (ms). |
|mode |[PushMode](https://docs.byteplus.com/en/docs/24/ref#pushmode) |Default streaming method.<br><br><br>* `rtm`: Streaming with RTM protocol. |


**Type**

```ts
{
  timeout?: number;
  retryCount?: number;
  retryDelay?: number;
  mode?: PushMode;
}
```


<span id="pushmode"></span>
## PushMode  

The streaming mode used in the SDK.


* `rtm`: Use RTM for streaming.


**Type**

```ts
'rtm'
```


<span id="imixingviewconfig"></span>
## IMixingViewConfig

Type：`interface`

Basic information of the merge canvas, such as dimensions, frame rate, background color, etc.

<span id="property"></span>
### Property


|Property |Type |Description |
|---|---|---|
|width |number |The width of the merge canvas. |
|height |number |The height of the merge canvas. |
|frameRate |number |The frame rate of the merge canvas, measured in fps. It is recommended to set `frameRate` to 15 fps or higher to ensure smoothness. |
|backgroundColor |string |The background color of the merge canvas, which defaults to black. |


<span id="ivideostreamlayoutparams"></span>
## IVideoStreamLayoutParams

Type：`interface`

Configuration Information for Merged Video Sources

<span id="property"></span>
### Property


|Property |Type |Description |
|---|---|---|
|x |number |The x coordinate of the layout, measured in px. |
|y |number |The y\-coordinate of the layout, in px. |
|width |number |The width of the layout, measured in px. |
|height |number |The height of the layout, in px. |
|zOrder |number |The higher the layout level, the more it will be on top. |
|keepRatio |boolean |Whether to maintain the aspect ratio. |
|streamId |string |The ID of the video stream. |
|volume |number |When the video stream contains audio content, the corresponding audio volume ranges from `[0,100]`. |


<span id="iaudiostreamlayoutparams"></span>
## IAudioStreamLayoutParams

Type：`interface`

Configuration information of the audio stream during mixing.

<span id="property"></span>
### Property


|Property |Type |Description |
|---|---|---|
|streamId |string |The ID of the audio stream. |
|volume |number |The volume of the audio stream ranges from `[0,100]`. |

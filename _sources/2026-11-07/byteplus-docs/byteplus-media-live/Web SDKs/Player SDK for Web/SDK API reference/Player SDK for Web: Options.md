---
title: "Player SDK for Web: Options"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1155423"
---

## LiveVePlayerOptions

|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|rtm |[Rtm](https://docs.byteplus.com/en/docs/24/7605#rtm) |No |\- |Configurations for playing an RTM stream. |
|flv |[Flv](https://docs.byteplus.com/en/docs/24/7605#flv) |No |\- |Configurations for playing an FLV stream.<br><br>> **Note**<br><br><br>> FLV pull stream format stream configurations are applicable to PC browsers, Android browsers that support MSE playback, and iOS browsers that support MMS API.<br> |
|hls |[Hls](https://docs.byteplus.com/en/docs/24/7605#hls) |No |\- |Configurations for playing an HLS stream.<br><br>> **Note**<br><br><br><br>* > The HLS format stream configuration is only applicable to PC browsers and Android browsers that support the MSE API.<br><br><br>* > This configuration takes effect by default on PC;<br><br><br>* > For mobile devices, the configuration takes effect only when `enableMSE` is set to `true` for the browser.<br> |
|infoPanel |[InfoPanelConfig](https://docs.byteplus.com/en/docs/24/7605#infopanel) |No |\- |Configures the information panel for the player, including options to show/hide the panel and the time interval between each information update. The panel supports displaying information for HLS and FLV addresses. If you opt for software decoding, additional information related to software decoding will be displayed. |
|timeShift |[TimeShiftConfig](https://docs.byteplus.com/en/docs/24/7605#timeshiftconfig) |No |\- |Configurations for time shifting. |
|logger |[LoggerConfig](https://docs.byteplus.com/en/docs/24/7605#loggerconfig) |No |\- |Configurations for log upload. Supports enabling/disabling log upload and setting log parameters. |
|ignores |string[] |No |\- |A list of built\-in plug\-ins to be disabled. For the access method, please refer to [Plugin descriptions](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-d8idjfeza4#disabling-plugins). |
|icons |any |Yes |\- |The plug\-in icon. For the access method, please refer to [Plugin descriptions](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-d8idjfeza4#replacing-plugin-icons). |
|drm |[Drm](https://docs.byteplus.com/en/docs/24/7605#drm) |No |\- |Digital Rights Management (DRM) configurations. |
|fallback |[Fallback](https://docs.byteplus.com/en/docs/24/7605#fallback) |No |\- |Configure protocol downgrade parameters. When playback fails or stutters, other protocols can be downgraded according to the strategy. |
|id |string |No |`'veplayer'` |The container ID of the player. You should specify either `id` or `el`, or both. If both are specified, the `VePlayer` object will be inserted in the container specified by `id`. |
|el |HTMLElement |No |\- |The container element of the player. You should specify either `id` or `el`, or both. If both are specified, the `VePlayer` object will be inserted in the container specified by `id`. |
|width |string \| number |No |`'100%'` |The width of the player. If you set it to a number, the player will attach the unit "pixel" to it. If you set it to a string, the parameter value will be directly assigned to the `width` property of the player container. |
|height |string \| number |No |`'100%'` |The height of the player. If you set it to a number, the player will attach the unit "pixel" to it. If you set it to a string, the parameter value will be directly assigned to the `height` property of the player container. |
|url |string |No |\- |The pull stream address. You can manually construct the address or use the address generator to generate one. To see how to generate an address, refer to [Generate live-stream addresses](https://docs.byteplus.com/en/byteplus-media-live/docs/generating-live-stream-addresses). You should specify either `url` or `playList`, or both. |
|playlist |[Source](https://docs.byteplus.com/en/docs/24/7605#source)[] |No |\- |A list of live stream sources for the player. You should specify either `url` or `playList`, or both. |
|defaultSource |string |No |\- |The default pull stream address for the player when there are multiple addresses available. If this parameter is not specified, the first address in the playlist will become the default address. |
|defaultDefinition |string |No |\- |The default resolution for the player when there are multiple resolutions available. If this parameter is not specified, the first resolution in the list will become the default resolution. |
|decodeType |[DecodeType](https://docs.byteplus.com/en/docs/24/7605#decodetype) |No |`'hardware'` |The decoding method for the player.<br><br>> **Note**<br><br><br>> When software decoding is enabled, the player uses the software decoder of the browser to decode the stream. Software decoding offers high compatibility and is suitable for various devices and browsers, but it relies on the device's CPU capacity and may have freezes or latencies when playing high\-resolution or high\-bitrate videos. We recommend enabling software decoding in the following scenarios:<br><br><br><br>1. > In certain Android browsers, the player can sometimes be hijacked, causing certain features to be unavailable. Enabling software decoding can address this issue.<br><br><br>2. > Browsers on mobile devices do not support the FLV format. To play videos in this format, you can enable software decoding.<br><br><br>3. > Some browsers do not support the H.265 codec. To play videos encoded with H.265, you can enable software decoding.<br> |
|codec |[Codec](https://docs.byteplus.com/en/docs/24/7605#codec) |No |`'h264'` |The actual codec of the live stream. If you specify `degradation` to `soft-first`, that is, the player should fall back to software decoding when hardware decoding is not supported, we recommend specifying the parameter so that the player does not need to detect the codec information. |
|degradation |boolean \| [Degradation](https://docs.byteplus.com/en/docs/24/7605#degradation) |No |`'soft-first'` |Whether to enable H.265 compatibility mode for the player. In the H.265 compatibility mode, the player will prioritize hardware decoding for decoding H.265 streams. If the device or browser does not support hardware decoding for H.265, it will automatically fall back to software decoding. |
|poster |string \| [Poster](https://docs.byteplus.com/en/docs/24/7605#poster) |No |\- |The URL of the player's cover image. |
|lang |string |No |\- |The initial display language of the player. If the language pack does not exist, the 'en'language pack will be displayed by default. The default value is `document.documentElement.getAttribute('lang') \|\| navigator.language \|\| 'zh-cn'`. |
|i18n | |No |\- |Configures a custom multilingual dictionary for the player. You can set the dictionary for each language in the format { texts: { [key: string]: Object; } }. For example, { texts: { 'zh\-cn': { PIP: '画中画' }, en: { PIP: 'pip' } }}.<br><br>You can use the [default dictionary](https://docs.byteplus.com/byteplus-media-live/docs/default-dictionary_1) as a reference. |
|autoplay |boolean \| |No |`{ muted: true }` |Whether to enable autoplay for the player. If `muted` is set to `true`, the autoplay is muted. |
|volume |number |No |`0.6` |The default volume for the player. Valid range: [0,1]. |
|pip |boolean |No |`false` |Whether to display the Picture\-in\-Picture (PiP) button.<br><br><br>* `true`: Display;<br><br>* `false`: Do not display. |
|fullscreen |boolean \| [Fullscreen](https://docs.byteplus.com/en/docs/24/7605#fullscreen) |No |\- |Whether to display the full\-screen button.<br><br><br>* `true`: Display;<br><br>* `false`: Do not display. |
|error |[ErrorConfig](https://docs.byteplus.com/en/docs/24/7605#errorconfig) |No |\- |The error message of the player. When a playback error occurs, you can configure the error message and image displayed and whether to display the refresh button. |
|controls |boolean \| |No |`true` |Whether to display the control bar for the player.<br><br><br>* `true`: Display;<br><br>* `false`: Do not display. |
|listType |[ListType](https://docs.byteplus.com/en/docs/24/7605#listtype) |No |`'bottom'` |Select the panel style for resolution and line selection. This parameter takes effect on mobile devices only. |
|playsinline |boolean |No |`true` |Whether to enable inline playback for the player. The `playsinline` property is a property of the `video` element in HTML5. It specifies whether the video should be played inline.<br><br><br>* `true`: Enable inline playback.<br><br>* `false`: Disable. The default browser playback behavior will be used.<br><br>   This option only takes effect on mobile devices. When it is set to `true`, the `playsinline`, `webkit-playsinline`, and `x5-playsinline` properties are set to `true` when the video or audio objects are initialized. You can refer to [New Policies for iOS](https://webkit.org/blog/6784/new-video-policies-for-ios/) for more information about the inline playback.<br><br><br>> **Note**<br><br><br><br>* > Safari on iOS 10 and above supports inline playback.<br><br><br>* > Safari on iOS versions lower than 10 does not support inline playback. The player will automatically enter fullscreen mode when playback begins.<br> |
|videoAttributes | |No |\- |Additional properties for the `video` element that will be applied when the `videoElement` or `audioElement` objects are initialized. Refer to [HTMLMediaElement](https://developer.mozilla.org/en-US/docs/Web/API/HTMLMediaElement#properties) for supported properties. |
|fluid |boolean |No |`false` |Whether to enable responsive layout for the player. If responsive layout is enabled, the player size will be auto\-adjusted according to the width of the screen to ensure a proper display on different screen sizes.<br><br><br>* `true`: Enable<br><br>* `false`: Disable<br><br><br>> **Note**<br><br><br>> When responsive layout is enabled:<br><br><br>> If `width` and `height` are of type number, the player's aspect ratio will be determined based on their values.<br><br><br>> If `width` and `height` are not of type number, the player uses a 16:9 aspect ratio.<br> |
|fitVideoSize |"fixWidth" \| "fixHeight" \| "fixed" |No |`'fixed'` |The adaptation mode for the player size. After the video resource is initialized, the player container's aspect ratio is adjusted based on the obtained values of `videoWidth` and `videoHeight`. The available options include:<br><br><br>* `fixed`: Keep the container's width and height without adaptation;<br><br>* `fixWidth`: Keep the container's width and adjust the height;<br><br>* `fixHeight`: Keep the container's height and adjust the width. |
|videoFillMode |"cover" \| "auto" \| "fillHeight" \| "fillWidth" \| "fill" |No |`'auto'` |The fill mode of the video. The available options include:<br><br><br>* `fillwidth`: Fill the width of the container and crop the height if necessary.<br><br>* `fillHeight`: Fill the height of the container and crop the width if necessary.<br><br>* `fill`: Stretch the video to fill the container;<br><br>* `cover`: Fill the entire container while keeping the original aspect ratio;<br><br>* `auto`: Use the default fill mode of the browser. |
|marginControls |boolean |No |`false` |Whether to enable the separation of the video and the control bar. When enabled, the control bar will remain visible without overlapping the video content.<br><br><br>* `true`: Enable<br><br>* `false`: Disable |
|'x5\-video\-player\-type' |string |No |\- |Enable playing the video on the same player as WeChat. |
|'x5\-video\-player\-fullscreen' |boolean |No |\- |Whether to enable full\-screen playback in WeChat.<br><br><br>* `true`: Enable<br><br>* `false`: Disable |
|'x5\-video\-orientation' |"landscape" \| "portrait" \| "landscape\|portrait" |No |\- |The orientation of the video when played on WeChat. The following values are supported:<br><br><br>* `landscape`: Horizontal screen;<br><br>* `portrait`: Vertical screen;<br><br>* `landscape \| portrait`: Rotate with the mobile. |
|plugins |any[] |No |\- |A list of custom plugins. |
|closeVideoClick |boolean |No |`false` |Whether to disable the click\-to\-play feature.<br><br><br>* `true`: Disable.<br><br>* `false`: Enable. Play/pause the video on mounse click for the PCs. |
|closeVideoDblclick |boolean |No |`false` |Whether to disable the double\-click/tap action.<br><br><br>* `true`: Disable.<br><br>* `false`: Enable.<br><br>   * For the PCs, double click on the video to enter or exit the full screen mode.<br><br>   * For the mobiles, play/pause the video with double tap. |
|mediaElement |HTMLVideoElement \| null |No |\- |Supports passing in a `video` DOM element, suitable for scenarios where multiple players share the same video. |

## Rtm

|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|loadTimeout |number |No |`5000` |The maximum wait time for pulling an RTM stream, in milliseconds. If no response is received from the server within this duration, the network request is considered as failed. |
|retryCount |number |No |`3` |The maximum number of retries when an RTM pull\-stream request fails. When set to `0`, it means to disable retry. |
|retryDelay |number |No |`1000` |The interval between each retry to pull the stream, in milliseconds. |
|enableRTMAutoTranscode |boolean |No |`false` |Whether to enable automatic transcoding when the player requests to pull an RTM stream.<br><br><br>* `true`: Enable;<br><br>* `false`: Disable.<br><br><br>> **Note**<br><br><br>> If you want to use the automatic transcoding feature when playing an RTM stream, please [contact support](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate).<br> |
|networkEvaluateInterval |number |No |\- |Specify the recent time length for network evaluation in milliseconds. The default is 1000, which means evaluating the network conditions over the last 1000 milliseconds. |
|seamlesslyReload |boolean |No |`false` |Whether the processing method for re\-pulling the stream after pausing is seamless replacement.<br><br><br>* `true`: Yes, there will be no black screen phenomenon during re\-pulling the stream.<br><br>* `false`: No, there will be a black screen phenomenon during re\-pulling the stream.<br><br><br>> **Note**<br><br><br>> Safari browsers do not support using this configuration when performing RTM stream pulling.<br> |
|disconnectTime |number |No |\- |The disconnection time after pausing playback is in seconds. By default, there is no disconnection.<br><br>> **Note**<br><br><br>> When Safari browser performs RTM streaming, if there is a disconnection, there will be a short black screen or loading situation when re\-streaming.<br> |
|delayHint |number |No |\- |buffer delay to handle network jitter, in seconds. |
|checkStatsErrorDelay |number |No |`5000` |After the RTM streaming connection is successfully established, the player delays for a specified period (in milliseconds) before checking if data is successfully received. If no data is received within this period, a playback error will be triggered. |
|enableSei |boolean |No |`true` |Whether to enable RTM SEI data receiving. Valid values:<br><br><br>* `true`: Enable RTM SEI data receiving.<br><br>* `false`: Disable RTM SEI data receiving. |

## Flv

|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|retryCount |number |No |`3` |The maximum number of retries when an FLV pull\-stream request fails. When set to `0`, it means to disable retry. |
|retryDelay |number |No |`1000` |The interval between each retry to pull the stream, in milliseconds. |
|loadTimeout |number |No |`10000` |The maximum wait time for pulling an FLV stream, in milliseconds. If no response is received from the server within this duration, the network request is considered as failed. |
|enableLowLatency |boolean |No |`false` |Whether to enable low latency when playing an FLV address. For example, if you have enabled low latency, and set GOP to 2 seconds, the average latency will be around 2 seconds.<br><br><br>* `true`: Enable;<br><br>* `false`: Disable.<br><br><br>> **Note**<br><br><br>> Low\-latency FLV pull\-streaming is only effective in PC browsers.<br> |
|lowLatency |[LowLatency](https://docs.byteplus.com/en/docs/24/7605#lowlatency) |No |\- |Detailed configuration for low latency. |
|abr |[Abr](https://docs.byteplus.com/en/docs/24/7605#abr) |No |\- |Set the Adaptive Bitrate (ABR) configuration for FLV streaming in the player. |
|maxReaderInterval |number |No |\- |Set the maximum duration for no data return in milliseconds. The default value is 5. If this duration is exceeded, it will be considered a stream interruption and trigger an ended event. |
|disconnectTime |number |No |`0` |The disconnection time after pausing playback is in seconds. The default value is 0, indicating immediate disconnection after pausing playback. |
|seamlesslyReload |boolean |No |`false` |Whether the processing method for re\-pulling the stream after pausing is seamless replacement.<br><br><br>* `true`: Yes, there will be no black screen phenomenon during re\-pulling the stream.<br><br>* `false`: No, there will be a black screen phenomenon during re\-pulling the stream. |

## LowLatency

|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|enableFrameChasing |boolean |No |`true` |Whether to enable speed\-up frame chasing in FLV low latency mode.<br><br><br>* `true`: enabled;<br><br>* `false`: disabled. |

## Abr

|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|enable |boolean |No |\- |Enable or disable the Adaptive Bitrate (ABR) feature. The default setting is enabled.<br><br><br>* `true`: Enable;<br><br>* `false`: Disable. |
|debug |boolean |No |`false` |Whether to start debug mode, default is false.<br><br><br>* `true`: Enable,<br><br>* `false`: Disable. |
|bitrate |number |No |\- |The bitrate corresponding to the current pull\-stream address URL. |
|urls | |No |\- |Adaptive bitrate (ABR) stream information. |

## Hls

|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|loadTimeout |number |No |`10000` |The maximum wait time for pulling an HLS stream, in milliseconds. If no response is received from the server within this duration, the network request is considered as failed. |
|retryCount |number |No |`3` |The maximum number of retries when an HLS pull\-stream request fails. When set to `0`, it means to disable retry. |
|retryDelay |number |No |`1000` |The interval between each retry to pull the stream, in milliseconds. |
|enableMSE |boolean |No |`false` |Whether to prioritize the use of Media Source Extensions API for playing an HLS stream on mobile devices.<br><br><br>* `false`: Do not prioritize<br><br>* `true`: Prioritize |

## InfoPanel

|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|visible |boolean |No |`false` |Whether to display the information panel. |
|interval |number |No |`500` |The time interval between each information update, in milliseconds. |

## TimeShiftConfig

|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|liveStartTime |number |No |`Date.now() / 1000` |The time the live stream session started. Unix timestamp in seconds. The time must be specified according to the time zone of the browser. |
|maxShiftOffset |number |No |`604800` |The maximum amount of time shifting available during playback, in seconds. For example, if you set `maxShiftOffset` to `60`, it means that anything streamed more than 60 seconds ago will no longer be available to playback. Valid range: [6,604800]. |

## LoggerConfig

|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|enable |boolean |No |`true` |Whether to enable log upload. |
|appId |string |No |\- |The SDK application ID. You can access it by logging in to the BytePlus MediaLive console and navigating to [SDK Management](https://console.byteplus.com/live/main/sdk). |
|appName |string |No |\- |The application name. |
|userId |string |No |\- |The ID used to identify a single user. If not set, a random user ID will be generated and stored in the browser cache.<br><br>> **Note**<br><br><br>> We recommend using a business\-related user ID to quickly locate and troubleshoot problems in the event of playback errors.<br> |
|deviceId |string |No |\- |The ID used to identify a user's device. If not set, a random device ID will be generated and stored in the browser cache.<br><br>> **Note**<br><br><br>> We recommend using a business\-related device ID to quickly locate and troubleshoot problems in the event of playback errors.<br> |
|showUserIdInErrorPanel |boolean |No |`true` |Whether to display the current user ID in the error panel when an error occurs. |

## Drm

|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|fairplay |[FairplayDrm](https://docs.byteplus.com/en/docs/24/7605#fairplaydrm) |No |\- |FairPlay DRM configuration, used for encrypted content playback on Apple devices. |
|widevine |[WidevineDrm](https://docs.byteplus.com/en/docs/24/7605#widevinedrm) |No |\- |Widevine DRM configurations. |
|playready |[PlayreadyDrm](https://docs.byteplus.com/en/docs/24/7605#playreadydrm) |No |\- |PlayReady DRM configuration, used for encrypted content playback on Windows/Edge. |

## FairplayDrm

|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|serverCertificatePath |string |No |\- |URL used to acquire the FairPlay certificate. |
|serverProcessSPCPath |string |No |\- |URL used to acquire the DRM license. |

## WidevineDrm

|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|serverProcessSPCPath |string |No |\- |URL used to acquire the DRM license. |

## PlayreadyDrm

|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|serverProcessSPCPath |string |No |\- |URL used to acquire the DRM license. |

## Fallback

|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|fallbackOrder |("rtm" \| "flv" \| "hls")[] |No |\- |Protocol priority list. When multiple protocols are configured, the player selects the first supported protocol in this order. On playback failure, the next protocol is selected based on `fallbackStrategy`. |
|fallbackStrategy |Record<"rtm" \| "flv" \| "hls" \| "all", [FallbackStrategy](https://docs.byteplus.com/en/docs/24/7605#fallbackstrategy)\> |No |\- |Strategy for protocol fallback.<br><br>> **Note**<br><br><br><br>* > By default, fallback is triggered when RTM playback fails.<br><br><br>* > Use `all` to apply the same strategy across all protocols.<br><br><br>* > If both `all` and a specific protocol (e.g., `rtm`) are set, the specific protocol strategy takes precedence.<br> |

## FallbackStrategy

|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|Error |[ErrorFallbackStrategy](https://docs.byteplus.com/en/docs/24/7605#errorfallbackstrategy) |No |\- |The protocol downgrade strategy when a pull stream encounters an error. |

## ErrorFallbackStrategy

|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|excludeList |[ErrorCode](https://docs.byteplus.com/en/docs/24/docs-1158675#errorcode)[] |No |\- |List of error codes to ignore for fallback. If the error code is in this list, fallback will not be triggered. |
|shouldFallback |`(type: string, params: { error: VeError;}) => boolean` |No |\- |Custom fallback logic. Returns:<br><br><br>* `true`: fallback will occur<br><br>* `false`: no fallback |

## Source

|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|name |string |No |\- |The playback source ID. This value must be unique. |
|text |string \| Record<string, string\> |No |\- |The display name of the live stream source. Multiple languages are supported. For example, you set it to `{text: {'zh-cn': '线路一', 'en': 'LineOne'}}`. |
|definitions |(string \| [Definition](https://docs.byteplus.com/en/docs/24/7605#definition))[] |Yes |\- |A list of resolutions of the current source. |

## Definition

|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|url |string |Yes |\- |The playback address. |
|definition |string |No |\- |The resolution ID. This value must be unique. |
|text |string \| Record<string, string\> |No |\- |The display name of the resolution. Multiple languages are supported, such as `{text: {'zh-cn': '高清', 'en': 'HD'}}`. |

## Poster

|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|poster |string |Yes |\- |The URL of the player's cover image. |
|isEndedShow |boolean |No |`true` |Whether to display the cover image after playback ends.<br><br><br>* `true`：display the cover image after playback ends.<br><br>* `false`：not display the cover image after playback ends. |
|hideCanplay |boolean |No |`false` |Whether to hide the poster image after playback starts.<br><br><br>* `true`：The poster image remains visible until video playback actually starts (i.e., video frames are rendered), preventing a black screen before playback.<br><br>* `false`：The poster image is hidden immediately when the `play` event is triggered, which may cause a brief black screen before video appears. |
|fillMode |"fixWidth" \| "fixHeight" \| "cover" \| "contain" |No |\- |Fill mode of the poster image. The available options are as follows:<br><br><br>* `fixWidth`：Scales the image to fit the container's width while maintaining aspect ratio. Height is scaled proportionally, which may leave vertical blank space.<br><br>* `fixHeight`：Scales the image to fit the container's height while maintaining aspect ratio. Width is scaled proportionally, which may leave horizontal blank space.<br><br>* `cover`：Scales the image proportionally and crops overflow to fully cover the container without black borders.<br><br>* `contain`：Scales the image to fully fit the container. May stretch non\-proportionally to avoid black borders, potentially causing distortion. |

## Fullscreen

|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|rotateFullscreen |boolean |No |`false` |Whether to play the video in landscape mode when the video enters full\-screen mode. This feature is usually used on mobile devices. Once enabled, when the video enters fullscreen mode, the player will be rotated from portrait mode by 90 degrees to landscape mode. This property has a lower priority than `useCssFullscreen`.<br><br><br>* `true`: Enable.<br><br>* `false`: Disable. |
|useCssFullscreen |boolean |No |`false` |Whether to use full\-window.<br><br><br>* `true`: Use full\-window mode, in which the player covers the browser window.<br><br>* `false`: Use full\-screen mode, in which the player covers the entire desktop. |
|needBackIcon |boolean |No |`false` |Whether to display a return button at the top\-right corner when the player is in full\-screen mode. This feature is usually turned on on mobile devices.<br><br><br>* `true`: Display;<br><br>* `false`: Do not display. |

## ErrorConfig

|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|showErrorImg |boolean |No |`true` |Whether to display the error image. |
|showErrorTip |boolean |No |`true` |Whether to display the error message. |
|showRefresh |boolean |No |`true` |Whether to display the refresh button. |
|errorTipsText |string \| Record<string, string\> |No |None |Custom error message. |
|extraTips |{ label: string \| Record<Lang, string\>; value: string \| Record<Lang, string\>; }[] |No |None |More tips. |

## RTMNetWorkInfo

Network conditions obtained in the RTM pull stream scenario.

|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|speed |number |No |\- |The download speed within the latest network evaluation period, in units of bps. |
|avgSpeed |number |No |\- |The average download speed within the recent 5 network evaluation cycles, with the unit of bps. |
|lostRate |number |No |\- |The packet loss rate of the network within the latest network evaluation cycle. |
|avgLostRate |number |No |\- |The average network packet loss rate within the recent 5 network evaluation cycles. |

## SEIDelayStats

Delay statistics derived from server SEI data.

|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|delay_s2s |number |No |\- |Server\-to\-server delay, in milliseconds. Indicates the time taken for the stream to travel from the MediaLive push\-side edge node to the MediaLive pull\-side edge node. Empty when valid server SEI data is unavailable. |
|delay_s2e |number |No |\- |Server\-to\-end delay, in milliseconds. Indicates the time taken from when the stream reaches the MediaLive push\-side edge node to when the Player SDK for Web plays the corresponding frame. Because the Player SDK parses the SEI message before playing the corresponding frame, the local player buffer duration is included in the calculation. Empty when valid server SEI data is unavailable. |

## StatsSnapShoot

RTM live stream information.

|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|video | |No |\- |Video information. |
|audio | |No |\- |Audio information. |

## Stats

Basic information for HLS and FLV protocol playback.

|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|avgSpeed |number |Yes |\- |Average download speed. |
|bitrate |number |Yes |\- |bitrate. |
|bufferEnd |number |Yes |\- |Remaining buffer time. |
|currentTime |number |Yes |\- |The current playing time. |
|downloadSpeed |number |Yes |\- |Current download speed. |
|encodeType |string |Yes |\- |Encoding method. |
|fps |number |Yes |\- |Frame rate. |
|height |number |Yes |\- |Video height. |
|width |number |Yes |\- |Video wight. |

## FlvStats

FLV live stream information.

|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|totalReceivedByte |number |Yes |\- |The total number of bytes received. |
|totalReceivedCost |number |Yes |\- |The time consumed for receiving all bytes. |

## PrepareOptions

Player strategy configuration settings.

|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|appId |string |Yes |\- |The SDK application ID. You can access it by logging in to the BytePlus MediaLive console and navigating to [SDK Management](https://console.byteplus.com/live/main/sdk). |
|userId |string |No |\- |The ID used to identify a single user. If not set, a random user ID will be generated and stored in the browser cache.<br><br>> **Note**<br><br><br>> We recommend using a business\-related user ID to quickly locate and troubleshoot problems in the event of playback errors.<br> |
|strategies | |Yes |\- |Playback Strategy Configuration. |

## DecodeType

Type：`enum`

Decoding method.

|Property |Value |Description |
|---|---|---|
|Software |`'software'` |Software decoding. |
|Hardware |`'hardware'` |Hardware decoding. |

## Codec

Type：`enum`

The actual codec of the video. If you set the SoftFirst property in degradation (that is, hard solutions do not support downgrading soft solutions), it is recommended that you pass this parameter to save the operation of probing the actual encoding format.

|Property |Value |Description |
|---|---|---|
|H265 |`'h265'` |H.265. |
|H264 |`'h264'` |H.264. |

## Degradation

Type：`enum`

Whether to use H.265 compatibility mode. In H.265 compatibility mode, the player will prioritize hardware decoding to decode H.265 video. If the device or browser does not support H.265 hardware decoding, it will automatically fall back to H.265 software decoding.

|Property |Value |Description |
|---|---|---|
|SoftFirst |`'soft-first'` |When hardware decoding is not supported, prioritize downgrading to software decoding. |

## ListType

Type：`enum`

The panel style for resolution and live stream source selection. This setting is effective on mobile devices only.

|Property |Value |Description |
|---|---|---|
|Bottom |`'bottom'` |Bottom navigation drawer. |
|Fullscreen |`'fullscreen'` |Right navigation drawer. This is often used for fullscreen display. |
|Inner |`'inner'` |Overlay. |

## LicenseConfig

Type: `interface`

SDK license configuration.

### license

Type: string | [IlicenseContent](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1155423?lang=en#ilicensecontent)

License configuration. Supports either a license URL or the content of a license file.

## IlicenseContent

Type: `interface`

Content of a license file.

### content

Type: `string`

Corresponds to the `Content` field in the license file, which includes permission levels and version information.

### sign

Type: `string`

Corresponds to the `Signature` field in the license file, used for authentication.

### mainUrl

Type: `string | undefined`

Corresponds to the `MainURL` field in the license file, which is the license URL.

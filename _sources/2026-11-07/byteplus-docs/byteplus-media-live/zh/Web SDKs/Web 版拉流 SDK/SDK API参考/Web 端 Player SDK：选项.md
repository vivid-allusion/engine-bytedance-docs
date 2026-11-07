---
title: "Web 端 Player SDK：选项"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1155423-zh-CN"
---

## LiveVePlayerOptions

|配置 |类型 |是否必填 |默认值 |描述 |
|---|---|---|---|---|
|rtm |[Rtm](https://docs.byteplus.com/en/docs/24/106641#rtm) |否 |\- |播放 RTM 流的配置。 |
|flv |[Flv](https://docs.byteplus.com/en/docs/24/106641#flv) |否 |\- |播放 FLV 流的配置。<br><br>> **说明**<br><br><br>> FLV 拉流格式的流配置适用于 PC 浏览器、支持 MSE 播放的 Android 浏览器，以及支持 MMS API 的 iOS 浏览器。<br> |
|hls |[Hls](https://docs.byteplus.com/en/docs/24/106641#hls) |否 |\- |播放 HLS 流的配置。<br><br>> **说明**<br><br><br><br>* > HLS 格式流配置仅适用于 PC 浏览器和支持 MSE API 的 Android 浏览器。<br><br><br>* > 此配置在 PC 端默认生效；<br><br><br>* > 在移动设备上，仅当浏览器的 `enableMSE` 设置为 `true` 时，此配置才会生效。<br> |
|infoPanel |[InfoPanelConfig](https://docs.byteplus.com/en/docs/24/106641#infopanel) |否 |\- |配置播放器的信息面板，包括显示或隐藏面板，以及每次信息更新的时间间隔。该面板支持显示 HLS 和 FLV 地址的信息。如果选择软解码，将显示与软解码相关的附加信息。 |
|timeShift |[TimeShiftConfig](https://docs.byteplus.com/en/docs/24/106641#timeshiftconfig) |否 |\- |时移配置。 |
|logger |[LoggerConfig](https://docs.byteplus.com/en/docs/24/106641#loggerconfig) |否 |\- |日志上传配置。支持启用或禁用日志上传，以及设置日志参数。 |
|ignores |string[] |否 |\- |要禁用的内置插件列表。接入方法请参见[插件说明](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-d8idjfeza4#disabling-plugins)。 |
|icons |any |是 |\- |插件图标。接入方法请参见[插件说明](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-d8idjfeza4#replacing-plugin-icons)。 |
|drm |[Drm](https://docs.byteplus.com/en/docs/24/106641#drm) |否 |\- |数字版权管理（DRM）配置。 |
|fallback |[Fallback](https://docs.byteplus.com/en/docs/24/106641#fallback) |否 |\- |配置协议降级参数。当播放失败或卡顿时，可根据策略降级到其他协议。 |
|id |string |否 |`'veplayer'` |播放器的容器 ID。您应指定 `id` 或 `el`，也可以同时指定两者。如果同时指定，`VePlayer` 对象将插入到 `id` 指定的容器中。 |
|el |HTMLElement |否 |\- |播放器的容器元素。您应指定 `id` 或 `el`，也可以同时指定两者。如果同时指定，`VePlayer` 对象将插入到 `id` 指定的容器中。 |
|width |string \| number |否 |`'100%'` |播放器的宽度。如果设置为数字，播放器会为其附加“像素”单位。如果设置为字符串，参数值会直接赋给播放器容器的 `width` 属性。 |
|height |string \| number |否 |`'100%'` |播放器的高度。如果设置为数字，播放器会为其附加“像素”单位。如果设置为字符串，参数值会直接赋给播放器容器的 `height` 属性。 |
|url |string |否 |\- |拉流地址。您可以手动构造地址，或使用地址生成器生成地址。要了解如何生成地址，请参见[生成直播流地址](https://docs.byteplus.com/en/byteplus-media-live/docs/generating-live-stream-addresses)。您应指定 `url` 或 `playList`，也可以同时指定两者。 |
|playlist |[Source](https://docs.byteplus.com/en/docs/24/106641#source)[] |否 |\- |播放器的直播流源列表。您应指定 `url` 或 `playList`，也可以同时指定两者。 |
|defaultSource |string |否 |\- |当有多个地址可用时，播放器的默认拉流地址。如果未指定此参数，播放列表中的第一个地址将成为默认地址。 |
|defaultDefinition |string |否 |\- |当有多个分辨率可用时，播放器的默认分辨率。如果未指定此参数，列表中的第一个分辨率将成为默认分辨率。 |
|decodeType |[DecodeType](https://docs.byteplus.com/en/docs/24/106641#decodetype) |否 |`'hardware'` |播放器的解码方式。<br><br>> **说明**<br><br><br>> 启用软解码后，播放器使用浏览器的软件解码器解码流。软解码兼容性高，适用于多种设备和浏览器，但依赖设备的 CPU 能力。播放高分辨率或高码率视频时，可能出现卡顿或延迟。建议在以下场景启用软解码：<br><br><br><br>1. > 在某些 Android 浏览器中，播放器有时会被劫持，导致部分功能不可用。启用软解码可以解决此问题。<br><br><br>2. > 移动设备上的浏览器不支持 FLV 格式。要播放此格式的视频，可以启用软解码。<br><br><br>3. > 某些浏览器不支持 H.265 编解码器。要播放使用 H.265 编码的视频，可以启用软解码。<br> |
|codec |[Codec](https://docs.byteplus.com/en/docs/24/106641#codec) |否 |`'h264'` |直播流的实际编解码器。如果将 `degradation` 指定为 `soft-first`，即播放器在不支持硬解码时应回退到软解码，建议指定此参数，以便播放器无需检测编解码器信息。 |
|degradation |boolean \| [Degradation](https://docs.byteplus.com/en/docs/24/106641#degradation) |否 |`'soft-first'` |是否为播放器启用 H.265 兼容模式。在 H.265 兼容模式下，播放器会优先使用硬解码来解码 H.265 流。如果设备或浏览器不支持 H.265 硬解码，将自动回退到软解码。 |
|poster |string \| [Poster](https://docs.byteplus.com/en/docs/24/106641#poster) |否 |\- |播放器封面图的 URL。 |
|lang |string |否 |\- |播放器的初始显示语言。如果语言包不存在，默认显示 'en' 语言包。默认值为 `document.documentElement.getAttribute('lang') \|\| navigator.language \|\| 'zh-cn'`。 |
|i18n | |否 |\- |为播放器配置自定义多语言字典。您可以按 { texts: { [key: string]: Object; } } 格式为每种语言设置字典。例如，{ texts: { 'zh\-cn': { PIP: '画中画' }, en: { PIP: 'pip' } }}。<br><br>您可以参考[默认字典](https://docs.byteplus.com/byteplus-media-live/docs/default-dictionary_1)。 |
|autoplay |boolean \| |否 |`{ muted: true }` |是否为播放器启用自动播放。如果 `muted` 设置为 `true`，自动播放将静音。 |
|volume |number |否 |`0.6` |播放器的默认音量。有效范围：[0,1]。 |
|pip |boolean |否 |`false` |是否显示画中画（PiP）按钮。<br><br><br>* `true`：显示；<br><br>* `false`：不显示。 |
|fullscreen |boolean \| [Fullscreen](https://docs.byteplus.com/en/docs/24/106641#fullscreen) |否 |\- |是否显示全屏按钮。<br><br><br>* `true`：显示；<br><br>* `false`：不显示。 |
|error |[ErrorConfig](https://docs.byteplus.com/en/docs/24/106641#errorconfig) |否 |\- |播放器的错误消息。发生播放错误时，您可以配置显示的错误消息和图片，以及是否显示刷新按钮。 |
|controls |boolean \| |否 |`true` |是否显示播放器的控制栏。<br><br><br>* `true`：显示；<br><br>* `false`：不显示。 |
|listType |[ListType](https://docs.byteplus.com/en/docs/24/106641#listtype) |否 |`'bottom'` |选择分辨率和线路选择的面板样式。此参数仅在移动设备上生效。 |
|playsinline |boolean |否 |`true` |是否为播放器启用内联播放。`playsinline` 属性是 HTML5 中 `video` 元素的属性。它指定视频是否应内联播放。<br><br><br>* `true`：启用内联播放。<br><br>* `false`：禁用。将使用默认的浏览器播放行为。<br><br>   此选项仅在移动设备上生效。当设置为 `true` 时，初始化视频或音频对象时，`playsinline`、`webkit-playsinline` 和 `x5-playsinline` 属性会设置为 `true`。有关内联播放的更多信息，请参阅 [iOS 新策略](https://webkit.org/blog/6784/new-video-policies-for-ios/)。<br><br><br>> **说明**<br><br><br><br>* > iOS 10 及以上版本的 Safari 支持内联播放。<br><br><br>* > iOS 10 以下版本的 Safari 不支持内联播放。播放器将在播放开始时自动进入全屏模式。<br> |
|videoAttributes | |否 |\- |`video` 元素的附加属性，将在初始化 `videoElement` 或 `audioElement` 对象时应用。支持的属性请参见 [HTMLMediaElement](https://developer.mozilla.org/en-US/docs/Web/API/HTMLMediaElement#properties)。 |
|fluid |boolean |否 |`false` |是否为播放器启用响应式布局。启用响应式布局后，播放器大小会根据屏幕宽度自动调整，以确保在不同屏幕尺寸下正确显示。<br><br><br>* `true`：启用<br><br>* `false`：禁用<br><br><br>> **说明**<br><br><br>> 启用响应式布局时：<br><br><br>> 如果 `width` 和 `height` 为 number 类型，播放器的宽高比将根据其值确定。<br><br><br>> 如果 `width` 和 `height` 不是 number 类型，播放器使用 16:9 的宽高比。<br> |
|fitVideoSize |"fixWidth" \| "fixHeight" \| "fixed" |否 |`'fixed'` |播放器大小的适配模式。视频资源初始化后，会根据获取到的 `videoWidth` 和 `videoHeight` 值调整播放器容器的宽高比。可用选项包括：<br><br><br>* `fixed`：保持容器的宽度和高度，不进行适配；<br><br>* `fixWidth`：保持容器宽度并调整高度；<br><br>* `fixHeight`：保持容器高度并调整宽度。 |
|videoFillMode |"cover" \| "auto" \| "fillHeight" \| "fillWidth" \| "fill" |否 |`'auto'` |视频的填充模式。可用选项包括：<br><br><br>* `fillwidth`：填充容器宽度，并在必要时裁剪高度。<br><br>* `fillHeight`：填充容器高度，并在必要时裁剪宽度。<br><br>* `fill`：拉伸视频以填充容器；<br><br>* `cover`：保持原始宽高比并填满整个容器；<br><br>* `auto`：使用浏览器的默认填充模式。 |
|marginControls |boolean |否 |`false` |是否启用视频与控制栏分离。启用后，控制栏将保持可见，且不会覆盖视频内容。<br><br><br>* `true`：启用<br><br>* `false`：禁用 |
|'x5\-video\-player\-type' |string |否 |\- |启用与微信相同播放器的视频播放。 |
|'x5\-video\-player\-fullscreen' |boolean |否 |\- |是否在微信中启用全屏播放。<br><br><br>* `true`：启用<br><br>* `false`：禁用 |
|'x5\-video\-orientation' |"landscape" \| "portrait" \| "landscape\|portrait" |否 |\- |在微信中播放视频时的视频方向。支持以下值：<br><br><br>* `landscape`：横屏；<br><br>* `portrait`：竖屏；<br><br>* `landscape \| portrait`：随手机旋转。 |
|plugins |any[] |否 |\- |自定义插件列表。 |
|closeVideoClick |boolean |否 |`false` |是否禁用点击播放功能。<br><br><br>* `true`：禁用。<br><br>* `false`：启用。PC 端通过鼠标点击播放或暂停视频。 |
|closeVideoDblclick |boolean |否 |`false` |是否禁用双击或双击屏幕操作。<br><br><br>* `true`：禁用。<br><br>* `false`：启用。<br><br>   * 在 PC 端，双击视频进入或退出全屏模式。<br><br>   * 在移动端，双击屏幕播放或暂停视频。 |
|mediaElement |HTMLVideoElement \| null |否 |\- |支持传入 `video` DOM 元素，适用于多个播放器共享同一视频的场景。 |

## Rtm

|配置 |类型 |是否必填 |默认值 |描述 |
|---|---|---|---|---|
|loadTimeout |number |否 |`5000` |拉取 RTM 流的最长等待时间，单位为毫秒。如果在此时长内未收到服务器响应，则认为网络请求失败。 |
|retryCount |number |否 |`3` |RTM 拉流请求失败时的最大重试次数。设置为 `0` 时，表示禁用重试。 |
|retryDelay |number |否 |`1000` |每次重试拉流的间隔，单位为毫秒。 |
|enableRTMAutoTranscode |boolean |否 |`false` |当播放器请求拉取 RTM 流时，是否启用自动转码。<br><br><br>* `true`：启用；<br><br>* `false`：禁用。<br><br><br>> **说明**<br><br><br>> 如果您希望在播放 RTM 流时使用自动转码功能，请[联系支持](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。<br> |
|networkEvaluateInterval |number |否 |\- |指定网络评估的最近时间长度，单位为毫秒。默认值为 1000，表示评估最近 1000 毫秒内的网络状况。 |
|seamlesslyReload |boolean |否 |`false` |暂停后重新拉流的处理方式是否为无缝替换。<br><br><br>* `true`：是，重新拉流期间不会出现黑屏现象。<br><br>* `false`：否，重新拉流期间会出现黑屏现象。<br><br><br>> **说明**<br><br><br>> Safari 浏览器在执行 RTM 拉流时不支持使用此配置。<br> |
|disconnectTime |number |否 |\- |暂停播放后的断开时间，单位为秒。默认不进行断开。<br><br>> **说明**<br><br><br>> 当 Safari 浏览器执行 RTM 流式传输时，如果发生断开，重新拉流时会出现短暂黑屏或加载情况。<br> |
|delayHint |number |否 |\- |用于处理网络抖动的缓冲延迟，单位为秒。 |
|checkStatsErrorDelay |number |否 |`5000` |RTM 流式传输连接成功建立后，播放器延迟指定时间（单位为毫秒）后检查是否成功接收数据。如果在此时间内未收到数据，将触发播放错误。 |
|enableSei |boolean |否 |`true` |是否启用 RTM SEI 数据接收。有效值：<br><br><br>* `true`：启用 RTM SEI 数据接收。<br><br>* `false`：禁用 RTM SEI 数据接收。 |

## Flv

|配置 |类型 |是否必填 |默认值 |描述 |
|---|---|---|---|---|
|retryCount |number |否 |`3` |FLV 拉流请求失败时的最大重试次数。设置为 `0` 时，表示禁用重试。 |
|retryDelay |number |否 |`1000` |每次重试拉流的间隔，单位为毫秒。 |
|loadTimeout |number |否 |`10000` |拉取 FLV 流的最长等待时间，单位为毫秒。如果在此时长内未收到服务器响应，则认为网络请求失败。 |
|enableLowLatency |boolean |否 |`false` |播放 FLV 地址时是否启用低延迟。例如，如果您启用了低延迟，并将 GOP 设置为 2 秒，则平均延迟约为 2 秒。<br><br><br>* `true`：启用；<br><br>* `false`：禁用。<br><br><br>> **说明**<br><br><br>> 低延迟 FLV 拉流仅在 PC 浏览器中生效。<br> |
|lowLatency |[LowLatency](https://docs.byteplus.com/en/docs/24/106641#lowlatency) |否 |\- |低延迟的详细配置。 |
|abr |[Abr](https://docs.byteplus.com/en/docs/24/106641#abr) |否 |\- |为播放器中的 FLV 流式传输设置自适应码率（ABR）配置。 |
|maxReaderInterval |number |否 |\- |设置无数据返回的最大时长，单位为毫秒。默认值为 5。如果超过此时长，将被视为流中断，并触发 ended 事件。 |
|disconnectTime |number |否 |`0` |暂停播放后的断开时间，单位为秒。默认值为 0，表示暂停播放后立即断开。 |
|seamlesslyReload |boolean |否 |`false` |暂停后重新拉流的处理方式是否为无缝替换。<br><br><br>* `true`：是，重新拉流期间不会出现黑屏现象。<br><br>* `false`：否，重新拉流期间会出现黑屏现象。 |

## LowLatency

|配置 |类型 |是否必填 |默认值 |描述 |
|---|---|---|---|---|
|enableFrameChasing |boolean |否 |`true` |是否在 FLV 低延迟模式下启用加速追帧。<br><br><br>* `true`：启用；<br><br>* `false`：禁用。 |

## Abr

|配置 |类型 |是否必填 |默认值 |描述 |
|---|---|---|---|---|
|enable |boolean |否 |\- |启用或禁用自适应码率（ABR）功能。默认设置为启用。<br><br><br>* `true`：启用；<br><br>* `false`：禁用。 |
|debug |boolean |否 |`false` |是否启动调试模式，默认为 false。<br><br><br>* `true`：启用，<br><br>* `false`：禁用。 |
|bitrate |number |否 |\- |当前拉流地址 URL 对应的码率。 |
|urls | |否 |\- |自适应码率（ABR）流信息。 |

## Hls

|配置 |类型 |是否必填 |默认值 |描述 |
|---|---|---|---|---|
|loadTimeout |number |否 |`10000` |拉取 HLS 流的最长等待时间，单位为毫秒。如果在此时长内未收到服务器响应，则认为网络请求失败。 |
|retryCount |number |否 |`3` |HLS 拉流请求失败时的最大重试次数。设置为 `0` 时，表示禁用重试。 |
|retryDelay |number |否 |`1000` |每次重试拉流的间隔，单位为毫秒。 |
|enableMSE |boolean |否 |`false` |在移动设备上播放 HLS 流时，是否优先使用 Media Source Extensions API。<br><br><br>* `false`：不优先使用<br><br>* `true`：优先使用 |

## InfoPanel

|配置 |类型 |是否必填 |默认值 |描述 |
|---|---|---|---|---|
|visible |boolean |否 |`false` |是否显示信息面板。 |
|interval |number |否 |`500` |每次信息更新之间的时间间隔，单位为毫秒。 |

## TimeShiftConfig

|配置 |类型 |是否必填 |默认值 |描述 |
|---|---|---|---|---|
|liveStartTime |number |否 |`Date.now() / 1000` |直播流会话开始的时间。Unix 时间戳，单位为秒。必须根据浏览器所在时区指定时间。 |
|maxShiftOffset |number |否 |`604800` |播放期间可用的最大时移时长，单位为秒。例如，如果将 `maxShiftOffset` 设置为 `60`，表示 60 秒之前推送的任何内容都将无法再播放。有效范围：[6,604800]。 |

## LoggerConfig

|配置 |类型 |是否必填 |默认值 |描述 |
|---|---|---|---|---|
|enable |boolean |否 |`true` |是否启用日志上传。 |
|appId |string |否 |\- |SDK 应用 ID。您可以登录 BytePlus MediaLive 控制台并前往 [SDK 管理](https://console.byteplus.com/live/main/sdk)获取。 |
|appName |string |否 |\- |应用名称。 |
|userId |string |否 |\- |用于标识单个用户的 ID。如果未设置，将生成随机用户 ID 并存储在浏览器缓存中。<br><br>> **说明**<br><br><br>> 建议使用与业务相关的用户 ID，以便在发生播放错误时快速定位和排查问题。<br> |
|deviceId |string |否 |\- |用于标识用户设备的 ID。如果未设置，将生成随机设备 ID 并存储在浏览器缓存中。<br><br>> **说明**<br><br><br>> 建议使用与业务相关的设备 ID，以便在发生播放错误时快速定位和排查问题。<br> |
|showUserIdInErrorPanel |boolean |否 |`true` |发生错误时，是否在错误面板中显示当前用户 ID。 |

## Drm

|配置 |类型 |是否必填 |默认值 |描述 |
|---|---|---|---|---|
|fairplay |[FairplayDrm](https://docs.byteplus.com/en/docs/24/106641#fairplaydrm) |否 |\- |FairPlay DRM 配置，用于在 Apple 设备上播放加密内容。 |
|widevine |[WidevineDrm](https://docs.byteplus.com/en/docs/24/106641#widevinedrm) |否 |\- |Widevine DRM 配置。 |
|playready |[PlayreadyDrm](https://docs.byteplus.com/en/docs/24/106641#playreadydrm) |否 |\- |PlayReady DRM 配置，用于在 Windows/Edge 上播放加密内容。 |

## FairplayDrm

|配置 |类型 |是否必填 |默认值 |描述 |
|---|---|---|---|---|
|serverCertificatePath |string |否 |\- |用于获取 FairPlay 证书的 URL。 |
|serverProcessSPCPath |string |否 |\- |用于获取 DRM 许可证的 URL。 |

## WidevineDrm

|配置 |类型 |是否必填 |默认值 |描述 |
|---|---|---|---|---|
|serverProcessSPCPath |string |否 |\- |用于获取 DRM 许可证的 URL。 |

## PlayreadyDrm

|配置 |类型 |是否必填 |默认值 |描述 |
|---|---|---|---|---|
|serverProcessSPCPath |string |否 |\- |用于获取 DRM 许可证的 URL。 |

## Fallback

|配置 |类型 |是否必填 |默认值 |描述 |
|---|---|---|---|---|
|fallbackOrder |("rtm" \| "flv" \| "hls")[] |否 |\- |协议优先级列表。配置多个协议时，播放器按此顺序选择第一个受支持的协议。播放失败时，根据 `fallbackStrategy` 选择下一个协议。 |
|fallbackStrategy |Record<"rtm" \| "flv" \| "hls" \| "all", [FallbackStrategy](https://docs.byteplus.com/en/docs/24/106641#fallbackstrategy)\> |否 |\- |协议回退策略。<br><br>> **说明**<br><br><br><br>* > 默认情况下，RTM 播放失败时会触发回退。<br><br><br>* > 使用 `all` 将同一策略应用于所有协议。<br><br><br>* > 如果同时设置了 `all` 和特定协议（例如 `rtm`），特定协议策略优先。<br> |

## FallbackStrategy

|配置 |类型 |是否必填 |默认值 |描述 |
|---|---|---|---|---|
|Error |[ErrorFallbackStrategy](https://docs.byteplus.com/en/docs/24/106641#errorfallbackstrategy) |否 |\- |拉流遇到错误时的协议降级策略。 |

## ErrorFallbackStrategy

|配置 |类型 |是否必填 |默认值 |描述 |
|---|---|---|---|---|
|excludeList |[ErrorCode](https://docs.byteplus.com/en/docs/24/docs-1158675#errorcode)[] |否 |\- |要忽略回退的错误码列表。如果错误码在此列表中，将不会触发回退。 |
|shouldFallback |`(type: string, params: { error: VeError;}) => boolean` |否 |\- |自定义回退逻辑。返回：<br><br><br>* `true`：将发生回退<br><br>* `false`：不回退 |

## Source

|配置 |类型 |是否必填 |默认值 |描述 |
|---|---|---|---|---|
|name |string |否 |\- |播放源 ID。此值必须唯一。 |
|text |string \| Record<string, string\> |否 |\- |直播流源的显示名称。支持多语言。例如，您将其设置为 `{text: {'zh-cn': '线路一', 'en': 'LineOne'}}`。 |
|definitions |(string \| [Definition](https://docs.byteplus.com/en/docs/24/106641#definition))[] |是 |\- |当前源的分辨率列表。 |

## Definition

|配置 |类型 |是否必填 |默认值 |描述 |
|---|---|---|---|---|
|url |string |是 |\- |播放地址。 |
|definition |string |否 |\- |分辨率 ID。此值必须唯一。 |
|text |string \| Record<string, string\> |否 |\- |分辨率的显示名称。支持多语言，例如 `{text: {'zh-cn': '高清', 'en': 'HD'}}`。 |

## Poster

|配置 |类型 |是否必填 |默认值 |描述 |
|---|---|---|---|---|
|poster |string |是 |\- |播放器封面图的 URL。 |
|isEndedShow |boolean |否 |`true` |播放结束后是否显示封面图。<br><br><br>* `true`：播放结束后显示封面图。<br><br>* `false`：播放结束后不显示封面图。 |
|hideCanplay |boolean |否 |`false` |播放开始后是否隐藏封面图。<br><br><br>* `true`：封面图会保持可见，直到视频实际开始播放（即渲染出视频帧），防止播放前出现黑屏。<br><br>* `false`：触发 `play` 事件时立即隐藏封面图，这可能导致视频出现前出现短暂黑屏。 |
|fillMode |"fixWidth" \| "fixHeight" \| "cover" \| "contain" |否 |\- |封面图的填充模式。可用选项如下：<br><br><br>* `fixWidth`：按容器宽度缩放图像并保持宽高比。高度按比例缩放，可能留下垂直空白。<br><br>* `fixHeight`：按容器高度缩放图像并保持宽高比。宽度按比例缩放，可能留下水平空白。<br><br>* `cover`：按比例缩放图像并裁剪溢出部分，以完全覆盖容器且无黑边。<br><br>* `contain`：缩放图像以完全适配容器。可能为避免黑边而非等比例拉伸，从而导致变形。 |

## Fullscreen

|配置 |类型 |是否必填 |默认值 |描述 |
|---|---|---|---|---|
|rotateFullscreen |boolean |否 |`false` |视频进入全屏模式时，是否以横屏模式播放视频。此功能通常用于移动设备。启用后，当视频进入全屏模式时，播放器将从竖屏模式旋转 90 度到横屏模式。此属性的优先级低于 `useCssFullscreen`。<br><br><br>* `true`：启用。<br><br>* `false`：禁用。 |
|useCssFullscreen |boolean |否 |`false` |是否使用全窗口。<br><br><br>* `true`：使用全窗口模式，播放器覆盖浏览器窗口。<br><br>* `false`：使用全屏模式，播放器覆盖整个桌面。 |
|needBackIcon |boolean |否 |`false` |播放器处于全屏模式时，是否在右上角显示返回按钮。此功能通常在移动设备上开启。<br><br><br>* `true`：显示；<br><br>* `false`：不显示。 |

## ErrorConfig

|配置 |类型 |是否必填 |默认值 |描述 |
|---|---|---|---|---|
|showErrorImg |boolean |否 |`true` |是否显示错误图片。 |
|showErrorTip |boolean |否 |`true` |是否显示错误消息。 |
|showRefresh |boolean |否 |`true` |是否显示刷新按钮。 |
|errorTipsText |string \| Record<string, string\> |否 |无 |自定义错误消息。 |
|extraTips |{ label: string \| Record<Lang, string\>; value: string \| Record<Lang, string\>; }[] |否 |无 |更多提示。 |

## RTMNetWorkInfo

在 RTM 拉流场景中获取的网络状况。

|配置 |类型 |是否必填 |默认值 |描述 |
|---|---|---|---|---|
|speed |number |否 |\- |最新网络评估周期内的下载速度，单位为 bps。 |
|avgSpeed |number |否 |\- |最近 5 个网络评估周期内的平均下载速度，单位为 bps。 |
|lostRate |number |否 |\- |最新网络评估周期内的网络丢包率。 |
|avgLostRate |number |否 |\- |最近 5 个网络评估周期内的平均网络丢包率。 |

## SEIDelayStats

从服务端 SEI 数据派生的延迟统计。

|配置 |类型 |是否必填 |默认值 |描述 |
|---|---|---|---|---|
|delay_s2s |number |否 |\- |服务端到服务端延迟，单位为毫秒。表示流从 MediaLive 推流侧边缘节点传输到 MediaLive 拉流侧边缘节点所需的时间。当有效的服务端 SEI 数据不可用时为空。 |
|delay_s2e |number |否 |\- |服务端到终端延迟，单位为毫秒。表示从流到达 MediaLive 推流侧边缘节点，到 Web 端 Player SDK 播放对应帧所需的时间。由于 Player SDK 会在播放对应帧之前解析 SEI 消息，因此计算中包含本地播放器缓冲时长。当有效的服务端 SEI 数据不可用时为空。 |

## StatsSnapShoot

RTM 直播流信息。

|配置 |类型 |是否必填 |默认值 |描述 |
|---|---|---|---|---|
|video | |否 |\- |视频信息。 |
|audio | |否 |\- |音频信息。 |

## Stats

HLS 和 FLV 协议播放的基本信息。

|配置 |类型 |是否必填 |默认值 |描述 |
|---|---|---|---|---|
|avgSpeed |number |是 |\- |平均下载速度。 |
|bitrate |number |是 |\- |码率。 |
|bufferEnd |number |是 |\- |剩余缓冲时间。 |
|currentTime |number |是 |\- |当前播放时间。 |
|downloadSpeed |number |是 |\- |当前下载速度。 |
|encodeType |string |是 |\- |编码方式。 |
|fps |number |是 |\- |帧率。 |
|height |number |是 |\- |视频高度。 |
|width |number |是 |\- |视频宽度。 |

## FlvStats

FLV 直播流信息。

|配置 |类型 |是否必填 |默认值 |描述 |
|---|---|---|---|---|
|totalReceivedByte |number |是 |\- |已接收的总字节数。 |
|totalReceivedCost |number |是 |\- |接收所有字节所消耗的时间。 |

## PrepareOptions

播放器策略配置设置。

|配置 |类型 |是否必填 |默认值 |描述 |
|---|---|---|---|---|
|appId |string |是 |\- |SDK 应用 ID。您可以登录 BytePlus MediaLive 控制台并前往 [SDK 管理](https://console.byteplus.com/live/main/sdk)获取。 |
|userId |string |否 |\- |用于标识单个用户的 ID。如果未设置，将生成随机用户 ID 并存储在浏览器缓存中。<br><br>> **说明**<br><br><br>> 建议使用与业务相关的用户 ID，以便在发生播放错误时快速定位和排查问题。<br> |
|strategies | |是 |\- |播放策略配置。 |

## DecodeType

类型：`enum`

解码方式。

|属性 |值 |描述 |
|---|---|---|
|Software |`'software'` |软解码。 |
|Hardware |`'hardware'` |硬解码。 |

## Codec

类型：`enum`

视频的实际编解码器。如果在 degradation 中设置 SoftFirst 属性（即硬解方案不支持降级到软解方案），建议您传入此参数，以节省探测实际编码格式的操作。

|属性 |值 |描述 |
|---|---|---|
|H265 |`'h265'` |H.265。 |
|H264 |`'h264'` |H.264。 |

## Degradation

类型：`enum`

是否使用 H.265 兼容模式。在 H.265 兼容模式下，播放器会优先使用硬解码来解码 H.265 视频。如果设备或浏览器不支持 H.265 硬解码，将自动回退到 H.265 软解码。

|属性 |值 |描述 |
|---|---|---|
|SoftFirst |`'soft-first'` |当不支持硬解码时，优先降级到软解码。 |

## ListType

类型：`enum`

分辨率和直播流源选择的面板样式。此设置仅在移动设备上生效。

|属性 |值 |描述 |
|---|---|---|
|Bottom |`'bottom'` |底部导航抽屉。 |
|Fullscreen |`'fullscreen'` |右侧导航抽屉。通常用于全屏显示。 |
|Inner |`'inner'` |覆盖层。 |

## LicenseConfig

类型：`interface`

SDK 许可证配置。

### license

类型：string | [IlicenseContent](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1155423?lang=en#ilicensecontent)

许可证配置。支持许可证 URL 或许可证文件内容。

## IlicenseContent

类型：`interface`

许可证文件内容。

### content

类型：`string`

对应许可证文件中的 `Content` 字段，其中包含权限级别和版本信息。

### sign

类型：`string`

对应许可证文件中的 `Signature` 字段，用于身份验证。

### mainUrl

类型：`string | undefined`

对应许可证文件中的 `MainURL` 字段，即许可证 URL。

---
title: "拉流 SDK for Web：错误码"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1158675-zh-CN"
---

<span id="errorcode"></span>
## VeError

类型：`class`

错误对象。

<span id="a2b2fa8d"></span>
### 属性


|属性 |类型 |接口行为 |
|---|---|---|
|errorCode |[ErrorCode](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1158675#errorcode) |`Readonly` 错误码。 |
|level |[Level](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1158675#level) |`Readonly` 错误级别。 |
|message |string |错误信息。 |
|ext |any |`Readonly` 其他错误信息。 |


<span id="7aba7b47"></span>
## Level

类型：`enum`

错误级别。


|属性 |值 |接口行为 |
|---|---|---|
|Fatal |`'Fatal'` |发生严重错误，通常由于 CDN 拉取失败或 DRM 权限校验失败，导致无法回放。 |
|Error |`'Error'` |流异常或离线状态导致回放失败。 |
|Warn |`'Warn'` |发出警告，通常由于日志配置错误或缺少 RTM 备用地址。 |


<span id="51f604a5"></span>
## ErrorCode


|值 |属性 |接口行为 |解决方案 |
|---|---|---|---|
|`210` |INVALID_PARAMETER |参数错误。 |请检查是否已指定必需的参数 `url` 和 `playlist`。 |
|`220` |INVALID_LOGGER |日志错误。 |日志选项配置不正确。详情请参见 [Playback Logging and Reporting](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-playback-logging-and-reporting)。 |
|`1100` |MANIFEST_HLS_ERROR |视频解析错误。 |请 [contact support](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。 |
|`1200` |MANIFEST_DASH_ERROR |视频解析错误。 |请 [contact support](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。 |
|`2100` |NETWORK |网络错误。 |请检查当前网络环境，并确保拉流地址有效。 |
|`2101` |NETWORK_TIMEOUT |网络请求超时。 |请检查拉流地址是否有效。 |
|`2103` |NETWORK_FORBIDDEN |播放器收到 403 返回调用结果（响应码）。 |请检查拉流地址中的鉴权信息。 |
|`2104` |NETWORK_NOTFOUND |播放器收到 404 返回调用结果（响应码）。 |请检查拉流地址是否有效。 |
|`2116` |NETWORK_RANGE_NOT_SATISFIABLE |播放器收到 206 返回调用结果（响应码）。 |请检查拉流地址是否有效。 |
|`3100` |DEMUX_FLV_ERROR |视频解析错误。 |请检查拉流地址是否有效，或 [contact support](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。 |
|`3200` |DEMUX_HLS_ERROR |视频解析错误。 |请检查拉流地址是否有效，或 [contact support](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。 |
|`3300` |DEMUX_MP4_ERROR |视频解析错误。 |请检查拉流地址是否有效，或 [contact support](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。 |
|`3400` |DEMUX_FMP4_ERROR |视频解析错误。 |请检查拉流地址是否有效，或 [contact support](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。 |
|`3410` |DEMUX_SIDX_ERROR |视频解析错误。 |请检查拉流地址是否有效，或 [contact support](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。 |
|`4100` |REMUX_FMP4_ERROR |视频解析错误。 |请检查拉流地址是否有效，或 [contact support](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。 |
|`4200` |REMUX_MP4_ERROR |视频解析错误。 |请检查拉流地址是否有效，或 [contact support](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。 |
|`5101` |MEDIA_ERR_ABORTED |获取数据过程被中止。 |请检查请求是否正确，然后重新尝试拉流。 |
|`5102` |MEDIA_ERR_NETWORK |发生网络错误，无法成功获取媒体文件。 |请检查请求是否正确，然后重新尝试拉流。 |
|`5103` |MEDIA_ERR_DECODE |浏览器在解码媒体资源时发生错误。 |1. 检查原始视频是否存在问题。<br><br>2. 重新转码视频并再次播放。<br><br>3. 若错误仍然存在，请 [contact support](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。 |
|`5104` |MEDIA_ERR_SRC_NOT_SUPPORTED |由于视频格式不支持或服务器或网络问题，无法加载视频。 |1. 检查浏览器请求是否存在问题。<br><br>2. 检查浏览器及当前页面是否支持该视频格式。<br><br>3. 若错误仍然存在，请 [contact support](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。 |
|`5105` |MEDIA_ERR_CODEC_NOT_SUPPORTED |当前浏览器不支持视频解码。 |1. 检查浏览器请求是否存在问题。<br><br>2. 检查浏览器及当前页面是否支持该视频格式。<br><br>3. 若错误仍然存在，请[联系支持](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。 |
|`5106` |MEDIA_ERR_URL_EMPTY |当前拉流地址为空。 |请检查是否已指定 'url' 或 'playlist'。 |
|`5200` |MEDIA_MSE_ADD_SB |发生回放问题。 |请检查直播流源或[联系支持](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。 |
|`5201` |MEDIA_MSE_APPEND_BUFFER |发生回放问题。 |请检查直播流源或[联系支持](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。 |
|`5202` |MEDIA_MSE_OTHER |发生回放问题。 |请检查直播流源或[联系支持](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。 |
|`5203` |MEDIA_MSE_FULL |发生回放问题。 |请检查直播流源或[联系支持](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。 |
|`5204` |MEDIA_MSE_HIJACK |发生回放问题。 |请检查直播流源或[联系支持](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。 |
|`5301` |MEDIA_EME_HIJACK |发生回放问题。 |请检查直播流源或[联系支持](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。 |
|`7101` |DRM_UNSUPPORTED |不支持DRM加密回放 |请确认当前浏览器是否支持指定的DRM类型，例如Widevine或FairPlay。 |
|`7103` |DRM_NO_MEDIA_KEY |未能获取解密所需的MediaKey。 |* 请确保DRM类型与当前环境兼容。<br><br>* 请确认操作在HTTPS或localhost环境下进行。 |
|`7104` |DRM_NO_KEY_SESSION |无法建立DRM解密所需的KeySession。 |* 请确保DRM类型与当前环境兼容。<br><br>* 请确认操作在HTTPS或localhost环境下进行。 |
|`7105` |DRM_GENERATE_QUEST_FAIL |解密回放错误 |请检查直播流源或[联系支持](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。 |
|`7106` |DRM_LACK_SERVER_CERTIFICATE_PATH |缺少DRM证书请求链接 |缺少必需的serverProcessSPCPath配置。 |
|`7107` |DRM_LACK_SERVER_PROCESS_SPC_PATH |缺少DRM License请求链接 |缺少必需的`serverProcessSPCPath`配置。 |
|`7108` |DRM_LICENSE_FAIL |License请求或更新失败 |请检查直播流源或[联系支持](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。 |
|`7109` |DRM_KEY_ERROR |解密错误 |请检查直播流源或[联系支持](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。 |
|`7110` |DRM_CERT_FAIL |DRM证书请求失败 |请检查网络及证书地址的有效性。 |
|`8000` |OTHER |发生回放问题。 |请检查直播流源或[联系支持](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。 |
|`9001` |RUNTIME_NO_CANPLAY_ERROR |发生回放问题。 |请检查直播流源或[联系支持](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。 |
|`9002` |RUNTIME_BUFFERBREAK_ERROR |发生回放问题。 |请检查直播流源或[联系支持](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。 |
|`9003` |RUNTIME_WAITING_TIMEOUT_ERROR |发生回放问题。 |请检查直播流源或[联系支持](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。 |
|`110` |MODULE_LOAD_ERROR |CDN异步拉取失败。 |请刷新页面或检查网络环境。 |

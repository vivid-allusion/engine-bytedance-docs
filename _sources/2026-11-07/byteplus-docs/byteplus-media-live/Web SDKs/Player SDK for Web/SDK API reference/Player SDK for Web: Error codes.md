---
title: "Player SDK for Web: Error codes"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1158675"
---

<span id="veerror"></span>
## VeError

Type：`class`

The error object.

<span id="property"></span>
### Property


|Property |Type |Description |
|---|---|---|
|errorCode |[ErrorCode](https://docs.byteplus.com/en/docs/24/7608#errorcode) |`Readonly` Error code. |
|level |[Level](https://docs.byteplus.com/en/docs/24/7608#level) |`Readonly` The error level. |
|message |string |The error message. |
|ext |any |`Readonly` Other error messages. |


<span id="level"></span>
## Level  

Type：`enum`

Error level.


|Property |Value |Description |
|---|---|---|
|Fatal |`'Fatal'` |A critical error occurs, typically due to CDN fetching failure or DRM permission verification failure, resulting in playback inability. |
|Error |`'Error'` |A stream anomaly or offline state causes playback to fail. |
|Warn |`'Warn'` |A warning is issued, usually due to incorrect log configuration or a missing RTM fallback address. |


<span id="errorcode"></span>
## ErrorCode  


|Value |Property |Description |Solution |
|---|---|---|---|
|`210` |INVALID_PARAMETER |Parameter errors. |Please check whether the required parameters `url` and `playlist` are specified. |
|`220` |INVALID_LOGGER |Log errors. |Log options are not configured correctly. For details, see [Playback Logging and Reporting](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-playback-logging-and-reporting). |
|`1100` |MANIFEST_HLS_ERROR |Video parsing error. |Please [contact support](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate). |
|`1200` |MANIFEST_DASH_ERROR |Video parsing error. |Please [contact support](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate). |
|`2100` |NETWORK |Network error. |Please check the current network environment and ensure the pull stream address is valid. |
|`2101` |NETWORK_TIMEOUT |Network request timed out |Please check whether the pull stream address is valid. |
|`2103` |NETWORK_FORBIDDEN |The player received a 403 response code. |Check the authentication information in the pull stream address. |
|`2104` |NETWORK_NOTFOUND |The player received a 404 response code. |Check whether the pull stream address is valid. |
|`2116` |NETWORK_RANGE_NOT_SATISFIABLE |The player received a 206 response code. |Check whether the pull stream address is valid. |
|`3100` |DEMUX_FLV_ERROR |Video parsing error. |Check whether the pull stream address is valid, or [contact support](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate). |
|`3200` |DEMUX_HLS_ERROR |Video parsing error. |Check whether the pull stream address is valid, or [contact support](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate). |
|`3300` |DEMUX_MP4_ERROR |Video parsing error. |Check whether the pull stream address is valid, or [contact support](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate). |
|`3400` |DEMUX_FMP4_ERROR |Video parsing error. |Check whether the pull stream address is valid, or [contact support](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate). |
|`3410` |DEMUX_SIDX_ERROR |Video parsing error. |Check whether the pull stream address is valid, or [contact support](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate). |
|`4100` |REMUX_FMP4_ERROR |Video parsing error. |Check whether the pull stream address is valid, or [contact support](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate). |
|`4200` |REMUX_MP4_ERROR |Video parsing error. |Check whether the pull stream address is valid, or [contact support](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate). |
|`5101` |MEDIA_ERR_ABORTED |The process of obtaining data was aborted. |Check whether the request is correct and then try to pull the stream again. |
|`5102` |MEDIA_ERR_NETWORK |A network error occurred and the media file could not be successfully obtained. |Check whether the request is correct and then try to pull the stream again. |
|`5103` |MEDIA_ERR_DECODE |An error occurred to the browser while decoding the media resources. |1. Check whether there is any issue with the original video.<br><br>2. Re\-transcode the video and play it again.<br><br>3. If the error persists, please [contact support](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate). |
|`5104` |MEDIA_ERR_SRC_NOT_SUPPORTED |The video cannot be loaded due to unsupported video format or server or network issues. |1. Check whether there is any issue with the browser's request.<br><br>2. Check whether the browser and the current page support the video format.<br><br>3. If the error persists, please [contact support](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate). |
|`5105` |MEDIA_ERR_CODEC_NOT_SUPPORTED |The current browser does not support video decoding. |1. Check whether there is any issue with the browser's request.<br><br>2. Check whether the browser and the current page support the video format.<br><br>3. If the error persists, please [contact support](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate). |
|`5106` |MEDIA_ERR_URL_EMPTY |The current pull stream address is empty. |Check whether 'url' or 'playlist' is specified. |
|`5200` |MEDIA_MSE_ADD_SB |A playback issue occurred. |Check the live stream source or [contact support](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate). |
|`5201` |MEDIA_MSE_APPEND_BUFFER |A playback issue occurred. |Check the live stream source or [contact support](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate). |
|`5202` |MEDIA_MSE_OTHER |A playback issue occurred. |Check the live stream source or [contact support](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate). |
|`5203` |MEDIA_MSE_FULL |A playback issue occurred. |Check the live stream source or [contact support](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate). |
|`5204` |MEDIA_MSE_HIJACK |A playback issue occurred. |Check the live stream source or [contact support](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate). |
|`5301` |MEDIA_EME_HIJACK |A playback issue occurred. |Check the live stream source or [contact support](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate). |
|`7101` |DRM_UNSUPPORTED |DRM encrypted playback is not supported |Please verify whether the current browser supports the specified DRM type, such as Widevine or FairPlay. |
|`7103` |DRM_NO_MEDIA_KEY |Failed to acquire the MediaKey needed for decryption. |* Ensure DRM type compatibility with current environment.<br><br>* Confirm operation is within HTTPS or localhost context. |
|`7104` |DRM_NO_KEY_SESSION |Unable to establish the KeySession required for DRM decryption |* Ensure DRM type compatibility with current environment.<br><br>* Confirm operation is within HTTPS or localhost context. |
|`7105` |DRM_GENERATE_QUEST_FAIL |Decryption playback error |Check the live stream source or [contact support](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate). |
|`7106` |DRM_LACK_SERVER_CERTIFICATE_PATH |Missing DRM certificate request link |Missing required serverProcessSPCPath configuration. |
|`7107` |DRM_LACK_SERVER_PROCESS_SPC_PATH |Missing DRM License request link |Missing required `serverProcessSPCPath` configuration. |
|`7108` |DRM_LICENSE_FAIL |Request or update License failed |Check the live stream source or [contact support](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate). |
|`7109` |DRM_KEY_ERROR |Decryption error |Check the live stream source or [contact support](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate). |
|`7110` |DRM_CERT_FAIL |Request for DRM certificate failed |Please check the network and the validity of the certificate address. |
|`8000` |OTHER |A playback issue occurred. |Check the live stream source or [contact support](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate). |
|`9001` |RUNTIME_NO_CANPLAY_ERROR |A playback issue occurred. |Check the live stream source or [contact support](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate). |
|`9002` |RUNTIME_BUFFERBREAK_ERROR |A playback issue occurred. |Check the live stream source or [contact support](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate). |
|`9003` |RUNTIME_WAITING_TIMEOUT_ERROR |A playback issue occurred. |Check the live stream source or [contact support](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate). |
|`110` |MODULE_LOAD_ERROR |CDN asynchronous fetch failed. |Refresh the page or check the network environment. |

---
title: "Web 版 Player SDK：錯誤碼"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1158675-zh-TW"
---

<span id="errorcode"></span>
## VeError

類型：`class`

錯誤物件。

<span id="a2b2fa8d"></span>
### 屬性


|屬性 |類型 |說明 |
|---|---|---|
|errorCode |[ErrorCode](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1158675#errorcode) |`Readonly` 錯誤碼。 |
|level |[Level](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1158675#level) |`Readonly` 錯誤等級。 |
|message |string |錯誤訊息。 |
|ext |any |`Readonly` 其他錯誤訊息。 |


<span id="7aba7b47"></span>
## Level

類型：`enum`

錯誤等級。


|屬性 |值 |說明 |
|---|---|---|
|Fatal |`'Fatal'` |發生嚴重錯誤，通常因 CDN 抓取失敗或 DRM 權限驗證失敗，導致無法播放。 |
|Error |`'Error'` |串流異常或離線狀態導致播放失敗。 |
|Warn |`'Warn'` |發出警告，通常因日誌配置錯誤或缺少 RTM 備援地址。 |


<span id="51f604a5"></span>
## ErrorCode


|值 |屬性 |說明 |解決方案 |
|---|---|---|---|
|`210` |INVALID_PARAMETER |參數錯誤。 |請檢查是否已指定必要參數 `url` 和 `playlist`。 |
|`220` |INVALID_LOGGER |日誌錯誤。 |日誌選項配置不正確。詳情請參閱 [Playback Logging and Reporting](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-playback-logging-and-reporting)。 |
|`1100` |MANIFEST_HLS_ERROR |影片解析錯誤。 |請 [聯絡客服](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。 |
|`1200` |MANIFEST_DASH_ERROR |影片解析錯誤。 |請 [聯絡客服](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。 |
|`2100` |NETWORK |網路錯誤。 |請檢查目前網路環境，並確認拉流地址有效。 |
|`2101` |NETWORK_TIMEOUT |網路請求逾時 |請檢查拉流地址是否有效。 |
|`2103` |NETWORK_FORBIDDEN |播放器收到 403 回應碼。 |請檢查拉流地址中的驗證資訊。 |
|`2104` |NETWORK_NOTFOUND |播放器收到 404 回應碼。 |請檢查拉流地址是否有效。 |
|`2116` |NETWORK_RANGE_NOT_SATISFIABLE |播放器收到 206 回應碼。 |請檢查拉流地址是否有效。 |
|`3100` |DEMUX_FLV_ERROR |影片解析錯誤。 |請檢查拉流地址是否有效，或 [聯絡客服](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。 |
|`3200` |DEMUX_HLS_ERROR |影片解析錯誤。 |請檢查拉流地址是否有效，或 [聯絡客服](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。 |
|`3300` |DEMUX_MP4_ERROR |影片解析錯誤。 |請檢查拉流地址是否有效，或 [聯絡客服](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。 |
|`3400` |DEMUX_FMP4_ERROR |影片解析錯誤。 |請檢查拉流地址是否有效，或 [聯絡客服](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。 |
|`3410` |DEMUX_SIDX_ERROR |影片解析錯誤。 |請檢查拉流地址是否有效，或 [聯絡客服](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。 |
|`4100` |REMUX_FMP4_ERROR |影片解析錯誤。 |請檢查拉流地址是否有效，或 [聯絡客服](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。 |
|`4200` |REMUX_MP4_ERROR |影片解析錯誤。 |請檢查拉流地址是否有效，或 [聯絡客服](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。 |
|`5101` |MEDIA_ERR_ABORTED |取得資料的過程已中止。 |請檢查請求是否正確，然後重新嘗試拉流。 |
|`5102` |MEDIA_ERR_NETWORK |發生網路錯誤，無法成功取得媒體檔案。 |請檢查請求是否正確，然後重新嘗試拉流。 |
|`5103` |MEDIA_ERR_DECODE |瀏覽器在解碼媒體資源時發生錯誤。 |1. 請檢查原始影片是否有問題。<br><br>2. 重新轉碼影片並再次播放。<br><br>3. 若錯誤仍然存在，請 [聯絡客服](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。 |
|`5104` |MEDIA_ERR_SRC_NOT_SUPPORTED |因影片格式不支援或伺服器／網路問題，無法載入影片。 |1. 請檢查瀏覽器請求是否有問題。<br><br>2. 請檢查瀏覽器及目前頁面是否支援該影片格式。<br><br>3. 若錯誤仍然存在，請 [聯絡客服](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。 |
|`5105` |MEDIA_ERR_CODEC_NOT_SUPPORTED |目前瀏覽器不支援影片解碼。 |1. 檢查瀏覽器的請求是否存在問題。<br><br>2. 檢查瀏覽器及當前頁面是否支援該影片格式。<br><br>3. 若錯誤仍然存在，請[聯絡客服](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。 |
|`5106` |MEDIA_ERR_URL_EMPTY |目前拉流地址為空。 |請檢查是否已指定 'url' 或 'playlist'。 |
|`5200` |MEDIA_MSE_ADD_SB |發生播放問題。 |請檢查直播流來源或[聯絡客服](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。 |
|`5201` |MEDIA_MSE_APPEND_BUFFER |發生播放問題。 |請檢查直播流來源或[聯絡客服](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。 |
|`5202` |MEDIA_MSE_OTHER |發生播放問題。 |請檢查直播流來源或[聯絡客服](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。 |
|`5203` |MEDIA_MSE_FULL |發生播放問題。 |請檢查直播流來源或[聯絡客服](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。 |
|`5204` |MEDIA_MSE_HIJACK |發生播放問題。 |請檢查直播流來源或[聯絡客服](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。 |
|`5301` |MEDIA_EME_HIJACK |發生播放問題。 |請檢查直播流來源或[聯絡客服](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。 |
|`7101` |DRM_UNSUPPORTED |不支援 DRM 加密播放 |請確認目前瀏覽器是否支援指定的 DRM 類型，例如 Widevine 或 FairPlay。 |
|`7103` |DRM_NO_MEDIA_KEY |無法取得解密所需的 MediaKey。 |* 請確保 DRM 類型與目前環境相容。<br><br>* 請確認操作是在 HTTPS 或 localhost 環境下進行。 |
|`7104` |DRM_NO_KEY_SESSION |無法建立 DRM 解密所需的 KeySession。 |* 請確保 DRM 類型與目前環境相容。<br><br>* 請確認操作是在 HTTPS 或 localhost 環境下進行。 |
|`7105` |DRM_GENERATE_QUEST_FAIL |解密播放錯誤 |請檢查直播流來源或[聯絡客服](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。 |
|`7106` |DRM_LACK_SERVER_CERTIFICATE_PATH |缺少 DRM 證書請求連結 |缺少必要的 serverProcessSPCPath 設定。 |
|`7107` |DRM_LACK_SERVER_PROCESS_SPC_PATH |缺少 DRM 授權請求連結 |缺少必要的`serverProcessSPCPath`設定。 |
|`7108` |DRM_LICENSE_FAIL |授權請求或更新失敗 |請檢查直播流來源或[聯絡客服](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。 |
|`7109` |DRM_KEY_ERROR |解密錯誤 |請檢查直播流來源或[聯絡客服](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。 |
|`7110` |DRM_CERT_FAIL |DRM 證書請求失敗 |請檢查網路及證書地址的有效性。 |
|`8000` |OTHER |發生播放問題。 |請檢查直播流來源或[聯絡客服](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。 |
|`9001` |RUNTIME_NO_CANPLAY_ERROR |發生播放問題。 |請檢查直播流來源或[聯絡客服](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。 |
|`9002` |RUNTIME_BUFFERBREAK_ERROR |發生播放問題。 |請檢查直播流來源或[聯絡客服](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。 |
|`9003` |RUNTIME_WAITING_TIMEOUT_ERROR |發生播放問題。 |請檢查直播流來源或[聯絡客服](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。 |
|`110` |MODULE_LOAD_ERROR |CDN 非同步抓取失敗。 |請重新整理頁面或檢查網路環境。 |

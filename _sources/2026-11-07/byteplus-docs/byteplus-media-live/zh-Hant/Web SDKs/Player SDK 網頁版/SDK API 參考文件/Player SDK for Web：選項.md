---
title: "Player SDK for Web：選項"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1155423-zh-TW"
---

## LiveVePlayerOptions

|設定 |類型 |必填 |預設值 |說明 |
|---|---|---|---|---|
|rtm |[Rtm](https://docs.byteplus.com/en/docs/24/107484#rtm) |否 |\- |播放 RTM 串流的設定。 |
|flv |[Flv](https://docs.byteplus.com/en/docs/24/107484#flv) |否 |\- |播放 FLV 串流的設定。<br><br>> **備註**<br><br><br>> FLV 拉流格式串流設定適用於 PC 瀏覽器、支援 MSE 播放的 Android 瀏覽器，以及支援 MMS API 的 iOS 瀏覽器。<br> |
|hls |[Hls](https://docs.byteplus.com/en/docs/24/107484#hls) |否 |\- |播放 HLS 串流的設定。<br><br>> **備註**<br><br><br><br>* > HLS 格式串流設定僅適用於 PC 瀏覽器和支援 MSE API 的 Android 瀏覽器。<br><br><br>* > 此設定預設在 PC 上生效；<br><br><br>* > 對於行動裝置，僅當瀏覽器的 `enableMSE` 設為 `true` 時，此設定才會生效。<br> |
|infoPanel |[InfoPanelConfig](https://docs.byteplus.com/en/docs/24/107484#infopanel) |否 |\- |設定播放器資訊面板，包括顯示/隱藏面板的選項，以及每次資訊更新之間的時間間隔。面板支援顯示 HLS 和 FLV 位址的資訊。如果選擇軟體解碼，將顯示與軟體解碼相關的其他資訊。 |
|timeShift |[TimeShiftConfig](https://docs.byteplus.com/en/docs/24/107484#timeshiftconfig) |否 |\- |時移設定。 |
|logger |[LoggerConfig](https://docs.byteplus.com/en/docs/24/107484#loggerconfig) |否 |\- |日誌上傳設定。支援啟用/停用日誌上傳，以及設定日誌參數。 |
|ignores |string[] |否 |\- |要停用的內建外掛程式清單。如需接入方法，請參閱[外掛程式說明](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-d8idjfeza4#disabling-plugins)。 |
|icons |any |是 |\- |外掛程式圖示。如需接入方法，請參閱[外掛程式說明](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-d8idjfeza4#replacing-plugin-icons)。 |
|drm |[Drm](https://docs.byteplus.com/en/docs/24/107484#drm) |否 |\- |數位版權管理 (DRM) 設定。 |
|fallback |[Fallback](https://docs.byteplus.com/en/docs/24/107484#fallback) |否 |\- |設定通訊協定降級參數。播放失敗或卡頓時，可根據策略降級到其他通訊協定。 |
|id |string |否 |`'veplayer'` |播放器的容器 ID。您應指定 `id` 或 `el`，或同時指定兩者。如果同時指定兩者，`VePlayer` 物件將插入由 `id` 指定的容器。 |
|el |HTMLElement |否 |\- |播放器的容器元素。您應指定 `id` 或 `el`，或同時指定兩者。如果同時指定兩者，`VePlayer` 物件將插入由 `id` 指定的容器。 |
|width |string \| number |否 |`'100%'` |播放器的寬度。如果設為數字，播放器會為其加上「pixel」單位。如果設為字串，參數值會直接指派給播放器容器的 `width` 屬性。 |
|height |string \| number |否 |`'100%'` |播放器的高度。如果設為數字，播放器會為其加上「pixel」單位。如果設為字串，參數值會直接指派給播放器容器的 `height` 屬性。 |
|url |string |否 |\- |拉流位址。您可以手動建構位址，或使用位址產生器產生位址。如需了解如何產生位址，請參閱[產生直播串流位址](https://docs.byteplus.com/en/byteplus-media-live/docs/generating-live-stream-addresses)。您應指定 `url` 或 `playList`，或同時指定兩者。 |
|playlist |[Source](https://docs.byteplus.com/en/docs/24/107484#source)[] |否 |\- |播放器的直播串流來源清單。您應指定 `url` 或 `playList`，或同時指定兩者。 |
|defaultSource |string |否 |\- |有多個位址可用時，播放器的預設拉流位址。如果未指定此參數，播放清單中的第一個位址將成為預設位址。 |
|defaultDefinition |string |否 |\- |有多個解析度可用時，播放器的預設解析度。如果未指定此參數，清單中的第一個解析度將成為預設解析度。 |
|decodeType |[DecodeType](https://docs.byteplus.com/en/docs/24/107484#decodetype) |否 |`'hardware'` |播放器的解碼方法。<br><br>> **備註**<br><br><br>> 啟用軟體解碼時，播放器使用瀏覽器的軟體解碼器解碼串流。軟體解碼具有高度相容性，適用於各種裝置和瀏覽器，但依賴裝置的 CPU 能力。播放高解析度或高位元率影片時，可能會發生凍結或延遲。建議在下列情境啟用軟體解碼：<br><br><br><br>1. > 在某些 Android 瀏覽器中，播放器有時可能被劫持，導致某些功能無法使用。啟用軟體解碼可解決此問題。<br><br><br>2. > 行動裝置上的瀏覽器不支援 FLV 格式。若要播放此格式的影片，可以啟用軟體解碼。<br><br><br>3. > 某些瀏覽器不支援 H.265 編解碼器。若要播放以 H.265 編碼的影片，可以啟用軟體解碼。<br> |
|codec |[Codec](https://docs.byteplus.com/en/docs/24/107484#codec) |否 |`'h264'` |直播串流的實際編解碼器。如果您將 `degradation` 指定為 `soft-first`，也就是當不支援硬體解碼時播放器應回退到軟體解碼，建議指定此參數，讓播放器無需偵測編解碼器資訊。 |
|degradation |boolean \| [Degradation](https://docs.byteplus.com/en/docs/24/107484#degradation) |否 |`'soft-first'` |是否為播放器啟用 H.265 相容模式。在 H.265 相容模式下，播放器會優先使用硬體解碼來解碼 H.265 串流。如果裝置或瀏覽器不支援 H.265 硬體解碼，將自動回退到軟體解碼。 |
|poster |string \| [Poster](https://docs.byteplus.com/en/docs/24/107484#poster) |否 |\- |播放器封面圖片的 URL。 |
|lang |string |否 |\- |播放器的初始顯示語言。如果語言包不存在，預設會顯示 'en' 語言包。預設值為 `document.documentElement.getAttribute('lang') \|\| navigator.language \|\| 'zh-cn'`。 |
|i18n | |否 |\- |設定播放器的自訂多語言字典。您可以用 { texts: { [key: string]: Object; } } 格式為每種語言設定字典。例如，{ texts: { 'zh\-cn': { PIP: '画中画' }, en: { PIP: 'pip' } }}。<br><br>您可以參考[預設字典](https://docs.byteplus.com/byteplus-media-live/docs/default-dictionary_1)。 |
|autoplay |boolean \| |否 |`{ muted: true }` |是否為播放器啟用自動播放。如果 `muted` 設為 `true`，自動播放將為靜音。 |
|volume |number |否 |`0.6` |播放器的預設音量。有效範圍：[0,1]。 |
|pip |boolean |否 |`false` |是否顯示子母畫面 (PiP) 按鈕。<br><br><br>* `true`：顯示；<br><br>* `false`：不顯示。 |
|fullscreen |boolean \| [Fullscreen](https://docs.byteplus.com/en/docs/24/107484#fullscreen) |否 |\- |是否顯示全螢幕按鈕。<br><br><br>* `true`：顯示；<br><br>* `false`：不顯示。 |
|error |[ErrorConfig](https://docs.byteplus.com/en/docs/24/107484#errorconfig) |否 |\- |播放器的錯誤訊息。發生播放錯誤時，您可以設定顯示的錯誤訊息和圖片，以及是否顯示重新整理按鈕。 |
|controls |boolean \| |否 |`true` |是否顯示播放器控制列。<br><br><br>* `true`：顯示；<br><br>* `false`：不顯示。 |
|listType |[ListType](https://docs.byteplus.com/en/docs/24/107484#listtype) |否 |`'bottom'` |選擇解析度和線路選擇的面板樣式。此參數僅在行動裝置上生效。 |
|playsinline |boolean |否 |`true` |是否為播放器啟用行內播放。`playsinline` 屬性是 HTML5 中 `video` 元素的屬性。它指定影片是否應以行內方式播放。<br><br><br>* `true`：啟用行內播放。<br><br>* `false`：停用。將使用預設瀏覽器播放行為。<br><br>   此選項僅在行動裝置上生效。設為 `true` 時，初始化影片或音訊物件時，`playsinline`、`webkit-playsinline` 和 `x5-playsinline` 屬性會設為 `true`。如需更多關於行內播放的資訊，您可以參閱 [New Policies for iOS](https://webkit.org/blog/6784/new-video-policies-for-ios/)。<br><br><br>> **備註**<br><br><br><br>* > iOS 10 及以上版本的 Safari 支援行內播放。<br><br><br>* > 低於 iOS 10 版本的 Safari 不支援行內播放。開始播放時，播放器將自動進入全螢幕模式。<br> |
|videoAttributes | |否 |\- |初始化 `videoElement` 或 `audioElement` 物件時，將套用到 `video` 元素的其他屬性。如需支援的屬性，請參閱 [HTMLMediaElement](https://developer.mozilla.org/en-US/docs/Web/API/HTMLMediaElement#properties)。 |
|fluid |boolean |否 |`false` |是否為播放器啟用回應式版面配置。如果啟用回應式版面配置，播放器大小會根據螢幕寬度自動調整，以確保在不同螢幕尺寸上正確顯示。<br><br><br>* `true`：啟用<br><br>* `false`：停用<br><br><br>> **備註**<br><br><br>> 啟用回應式版面配置時：<br><br><br>> 如果 `width` 和 `height` 為 number 類型，播放器的長寬比將根據其值決定。<br><br><br>> 如果 `width` 和 `height` 不是 number 類型，播放器會使用 16:9 長寬比。<br> |
|fitVideoSize |"fixWidth" \| "fixHeight" \| "fixed" |否 |`'fixed'` |播放器大小的適配模式。影片資源初始化後，播放器容器的長寬比會根據取得的 `videoWidth` 和 `videoHeight` 值調整。可用選項包括：<br><br><br>* `fixed`：保持容器的寬度和高度，不進行適配；<br><br>* `fixWidth`：保持容器寬度並調整高度；<br><br>* `fixHeight`：保持容器高度並調整寬度。 |
|videoFillMode |"cover" \| "auto" \| "fillHeight" \| "fillWidth" \| "fill" |否 |`'auto'` |影片的填充模式。可用選項包括：<br><br><br>* `fillwidth`：填滿容器寬度，必要時裁切高度。<br><br>* `fillHeight`：填滿容器高度，必要時裁切寬度。<br><br>* `fill`：拉伸影片以填滿容器；<br><br>* `cover`：保持原始長寬比並填滿整個容器；<br><br>* `auto`：使用瀏覽器的預設填充模式。 |
|marginControls |boolean |否 |`false` |是否啟用影片與控制列分離。啟用後，控制列會保持可見，且不會覆蓋影片內容。<br><br><br>* `true`：啟用<br><br>* `false`：停用 |
|'x5\-video\-player\-type' |string |否 |\- |啟用在與 WeChat 相同的播放器上播放影片。 |
|'x5\-video\-player\-fullscreen' |boolean |否 |\- |是否在 WeChat 中啟用全螢幕播放。<br><br><br>* `true`：啟用<br><br>* `false`：停用 |
|'x5\-video\-orientation' |"landscape" \| "portrait" \| "landscape\|portrait" |否 |\- |在 WeChat 上播放時影片的方向。支援下列值：<br><br><br>* `landscape`：橫向螢幕；<br><br>* `portrait`：直向螢幕；<br><br>* `landscape \| portrait`：隨行動裝置旋轉。 |
|plugins |any[] |否 |\- |自訂外掛程式清單。 |
|closeVideoClick |boolean |否 |`false` |是否停用點擊播放功能。<br><br><br>* `true`：停用。<br><br>* `false`：啟用。在 PC 上透過滑鼠點擊播放/暫停影片。 |
|closeVideoDblclick |boolean |否 |`false` |是否停用雙擊/雙點動作。<br><br><br>* `true`：停用。<br><br>* `false`：啟用。<br><br>   * 對於 PC，雙擊影片可進入或結束全螢幕模式。<br><br>   * 對於行動裝置，透過雙點播放/暫停影片。 |
|mediaElement |HTMLVideoElement \| null |否 |\- |支援傳入 `video` DOM 元素，適用於多個播放器共用同一個影片的情境。 |

## Rtm

|設定 |類型 |必填 |預設值 |說明 |
|---|---|---|---|---|
|loadTimeout |number |否 |`5000` |拉取 RTM 串流的最長等待時間，單位為毫秒。如果在此期間內未收到伺服器回應，網路請求將視為失敗。 |
|retryCount |number |否 |`3` |RTM 拉流請求失敗時的最大重試次數。設為 `0` 時，表示停用重試。 |
|retryDelay |number |否 |`1000` |每次重試拉流之間的間隔，單位為毫秒。 |
|enableRTMAutoTranscode |boolean |否 |`false` |播放器請求拉取 RTM 串流時，是否啟用自動轉碼。<br><br><br>* `true`：啟用；<br><br>* `false`：停用。<br><br><br>> **備註**<br><br><br>> 如果您想在播放 RTM 串流時使用自動轉碼功能，請[聯絡支援](https://console.byteplus.com/auth/login?redirectURI=%2Fworkorder%2Fcreate)。<br> |
|networkEvaluateInterval |number |否 |\- |指定網路評估的近期時間長度，單位為毫秒。預設值為 1000，表示評估最近 1000 毫秒內的網路狀況。 |
|seamlesslyReload |boolean |否 |`false` |暫停後重新拉流的處理方式是否為無縫替換。<br><br><br>* `true`：是，重新拉流期間不會出現黑畫面現象。<br><br>* `false`：否，重新拉流期間會出現黑畫面現象。<br><br><br>> **備註**<br><br><br>> Safari 瀏覽器在執行 RTM 拉流時不支援使用此設定。<br> |
|disconnectTime |number |否 |\- |暫停播放後的斷線時間，單位為秒。預設不斷線。<br><br>> **備註**<br><br><br>> Safari 瀏覽器執行 RTM 串流時，如果發生斷線，重新串流時會出現短暫黑畫面或載入情況。<br> |
|delayHint |number |否 |\- |用於處理網路抖動的緩衝延遲，單位為秒。 |
|checkStatsErrorDelay |number |否 |`5000` |RTM 串流連線成功建立後，播放器會延遲指定期間（毫秒）再檢查是否成功收到資料。如果在此期間內未收到資料，將觸發播放錯誤。 |
|enableSei |boolean |否 |`true` |是否啟用 RTM SEI 資料接收。有效值：<br><br><br>* `true`：啟用 RTM SEI 資料接收。<br><br>* `false`：停用 RTM SEI 資料接收。 |

## Flv

|設定 |類型 |必填 |預設值 |說明 |
|---|---|---|---|---|
|retryCount |number |否 |`3` |FLV 拉流請求失敗時的最大重試次數。設為 `0` 時，表示停用重試。 |
|retryDelay |number |否 |`1000` |每次重試拉流之間的間隔，單位為毫秒。 |
|loadTimeout |number |否 |`10000` |拉取 FLV 串流的最長等待時間，單位為毫秒。如果在此期間內未收到伺服器回應，網路請求將視為失敗。 |
|enableLowLatency |boolean |否 |`false` |播放 FLV 位址時，是否啟用低延遲。例如，如果您已啟用低延遲，並將 GOP 設為 2 秒，平均延遲約為 2 秒。<br><br><br>* `true`：啟用；<br><br>* `false`：停用。<br><br><br>> **備註**<br><br><br>> 低延遲 FLV 拉流僅在 PC 瀏覽器中有效。<br> |
|lowLatency |[LowLatency](https://docs.byteplus.com/en/docs/24/107484#lowlatency) |否 |\- |低延遲的詳細設定。 |
|abr |[Abr](https://docs.byteplus.com/en/docs/24/107484#abr) |否 |\- |設定播放器中 FLV 串流的自適應位元率 (ABR) 設定。 |
|maxReaderInterval |number |否 |\- |設定無資料返回的最大持續時間，單位為毫秒。預設值為 5。如果超過此持續時間，將視為串流中斷並觸發 ended 事件。 |
|disconnectTime |number |否 |`0` |暫停播放後的斷線時間，單位為秒。預設值為 0，表示暫停播放後立即斷線。 |
|seamlesslyReload |boolean |否 |`false` |暫停後重新拉流的處理方式是否為無縫替換。<br><br><br>* `true`：是，重新拉流期間不會出現黑畫面現象。<br><br>* `false`：否，重新拉流期間會出現黑畫面現象。 |

## LowLatency

|設定 |類型 |必填 |預設值 |說明 |
|---|---|---|---|---|
|enableFrameChasing |boolean |否 |`true` |是否在 FLV 低延遲模式中啟用加速追幀。<br><br><br>* `true`：啟用；<br><br>* `false`：停用。 |

## Abr

|設定 |類型 |必填 |預設值 |說明 |
|---|---|---|---|---|
|enable |boolean |否 |\- |啟用或停用自適應位元率 (ABR) 功能。預設設定為啟用。<br><br><br>* `true`：啟用；<br><br>* `false`：停用。 |
|debug |boolean |否 |`false` |是否啟動偵錯模式，預設為 false。<br><br><br>* `true`：啟用，<br><br>* `false`：停用。 |
|bitrate |number |否 |\- |目前拉流位址 URL 對應的位元率。 |
|urls | |否 |\- |自適應位元率 (ABR) 串流資訊。 |

## Hls

|設定 |類型 |必填 |預設值 |說明 |
|---|---|---|---|---|
|loadTimeout |number |否 |`10000` |拉取 HLS 串流的最長等待時間，單位為毫秒。如果在此期間內未收到伺服器回應，網路請求將視為失敗。 |
|retryCount |number |否 |`3` |HLS 拉流請求失敗時的最大重試次數。設為 `0` 時，表示停用重試。 |
|retryDelay |number |否 |`1000` |每次重試拉流之間的間隔，單位為毫秒。 |
|enableMSE |boolean |否 |`false` |在行動裝置上播放 HLS 串流時，是否優先使用 Media Source Extensions API。<br><br><br>* `false`：不優先使用<br><br>* `true`：優先使用 |

## InfoPanel

|設定 |類型 |必填 |預設值 |說明 |
|---|---|---|---|---|
|visible |boolean |否 |`false` |是否顯示資訊面板。 |
|interval |number |否 |`500` |每次資訊更新之間的時間間隔，單位為毫秒。 |

## TimeShiftConfig

|設定 |類型 |必填 |預設值 |說明 |
|---|---|---|---|---|
|liveStartTime |number |否 |`Date.now() / 1000` |直播串流工作階段開始的時間。Unix 時間戳記，單位為秒。必須根據瀏覽器的時區指定時間。 |
|maxShiftOffset |number |否 |`604800` |播放期間可用的最大時移時間量，單位為秒。例如，如果您將 `maxShiftOffset` 設為 `60`，表示超過 60 秒前串流的任何內容將無法再播放。有效範圍：[6,604800]。 |

## LoggerConfig

|設定 |類型 |必填 |預設值 |說明 |
|---|---|---|---|---|
|enable |boolean |否 |`true` |是否啟用日誌上傳。 |
|appId |string |否 |\- |SDK 應用程式 ID。您可以登入 BytePlus MediaLive 控制台，並前往 [SDK Management](https://console.byteplus.com/live/main/sdk) 取得。 |
|appName |string |否 |\- |應用程式名稱。 |
|userId |string |否 |\- |用於識別單一使用者的 ID。如果未設定，將產生隨機使用者 ID，並儲存在瀏覽器快取中。<br><br>> **備註**<br><br><br>> 建議使用與業務相關的使用者 ID，以便在發生播放錯誤時快速定位並排解問題。<br> |
|deviceId |string |否 |\- |用於識別使用者裝置的 ID。如果未設定，將產生隨機裝置 ID，並儲存在瀏覽器快取中。<br><br>> **備註**<br><br><br>> 建議使用與業務相關的裝置 ID，以便在發生播放錯誤時快速定位並排解問題。<br> |
|showUserIdInErrorPanel |boolean |否 |`true` |發生錯誤時，是否在錯誤面板中顯示目前使用者 ID。 |

## Drm

|設定 |類型 |必填 |預設值 |說明 |
|---|---|---|---|---|
|fairplay |[FairplayDrm](https://docs.byteplus.com/en/docs/24/107484#fairplaydrm) |否 |\- |FairPlay DRM 設定，用於 Apple 裝置上的加密內容播放。 |
|widevine |[WidevineDrm](https://docs.byteplus.com/en/docs/24/107484#widevinedrm) |否 |\- |Widevine DRM 設定。 |
|playready |[PlayreadyDrm](https://docs.byteplus.com/en/docs/24/107484#playreadydrm) |否 |\- |PlayReady DRM 設定，用於 Windows/Edge 上的加密內容播放。 |

## FairplayDrm

|設定 |類型 |必填 |預設值 |說明 |
|---|---|---|---|---|
|serverCertificatePath |string |否 |\- |用於取得 FairPlay 憑證的 URL。 |
|serverProcessSPCPath |string |否 |\- |用於取得 DRM 授權的 URL。 |

## WidevineDrm

|設定 |類型 |必填 |預設值 |說明 |
|---|---|---|---|---|
|serverProcessSPCPath |string |否 |\- |用於取得 DRM 授權的 URL。 |

## PlayreadyDrm

|設定 |類型 |必填 |預設值 |說明 |
|---|---|---|---|---|
|serverProcessSPCPath |string |否 |\- |用於取得 DRM 授權的 URL。 |

## Fallback

|設定 |類型 |必填 |預設值 |說明 |
|---|---|---|---|---|
|fallbackOrder |("rtm" \| "flv" \| "hls")[] |否 |\- |通訊協定優先順序清單。設定多個通訊協定時，播放器會依此順序選擇第一個支援的通訊協定。播放失敗時，會根據 `fallbackStrategy` 選擇下一個通訊協定。 |
|fallbackStrategy |Record<"rtm" \| "flv" \| "hls" \| "all", [FallbackStrategy](https://docs.byteplus.com/en/docs/24/107484#fallbackstrategy)\> |否 |\- |通訊協定回退策略。<br><br>> **備註**<br><br><br><br>* > 預設情況下，RTM 播放失敗時會觸發回退。<br><br><br>* > 使用 `all` 對所有通訊協定套用相同策略。<br><br><br>* > 如果同時設定 `all` 和特定通訊協定（例如 `rtm`），特定通訊協定策略優先。<br> |

## FallbackStrategy

|設定 |類型 |必填 |預設值 |說明 |
|---|---|---|---|---|
|Error |[ErrorFallbackStrategy](https://docs.byteplus.com/en/docs/24/107484#errorfallbackstrategy) |否 |\- |拉流發生錯誤時的通訊協定降級策略。 |

## ErrorFallbackStrategy

|設定 |類型 |必填 |預設值 |說明 |
|---|---|---|---|---|
|excludeList |[ErrorCode](https://docs.byteplus.com/en/docs/24/docs-1158675#errorcode)[] |否 |\- |回退時要忽略的錯誤碼清單。如果錯誤碼在此清單中，將不會觸發回退。 |
|shouldFallback |`(type: string, params: { error: VeError;}) => boolean` |否 |\- |自訂回退邏輯。返回：<br><br><br>* `true`：將發生回退<br><br>* `false`：不回退 |

## Source

|設定 |類型 |必填 |預設值 |說明 |
|---|---|---|---|---|
|name |string |否 |\- |播放來源 ID。此值必須唯一。 |
|text |string \| Record<string, string\> |否 |\- |直播串流來源的顯示名稱。支援多種語言。例如，您將其設為 `{text: {'zh-cn': '线路一', 'en': 'LineOne'}}`。 |
|definitions |(string \| [Definition](https://docs.byteplus.com/en/docs/24/107484#definition))[] |是 |\- |目前來源的解析度清單。 |

## Definition

|設定 |類型 |必填 |預設值 |說明 |
|---|---|---|---|---|
|url |string |是 |\- |播放位址。 |
|definition |string |否 |\- |解析度 ID。此值必須唯一。 |
|text |string \| Record<string, string\> |否 |\- |解析度的顯示名稱。支援多種語言，例如 `{text: {'zh-cn': '高清', 'en': 'HD'}}`。 |

## Poster

|設定 |類型 |必填 |預設值 |說明 |
|---|---|---|---|---|
|poster |string |是 |\- |播放器封面圖片的 URL。 |
|isEndedShow |boolean |否 |`true` |播放結束後是否顯示封面圖片。<br><br><br>* `true`：播放結束後顯示封面圖片。<br><br>* `false`：播放結束後不顯示封面圖片。 |
|hideCanplay |boolean |否 |`false` |播放開始後是否隱藏海報圖片。<br><br><br>* `true`：海報圖片會保持可見，直到影片實際開始播放（即影片影格已轉譯），以防止播放前出現黑畫面。<br><br>* `false`：觸發 `play` 事件時立即隱藏海報圖片，這可能導致影片出現前短暫黑畫面。 |
|fillMode |"fixWidth" \| "fixHeight" \| "cover" \| "contain" |否 |\- |海報圖片的填充模式。可用選項如下：<br><br><br>* `fixWidth`：縮放圖片以符合容器寬度，同時保持長寬比。高度會按比例縮放，可能留下垂直空白。<br><br>* `fixHeight`：縮放圖片以符合容器高度，同時保持長寬比。寬度會按比例縮放，可能留下水平空白。<br><br>* `cover`：按比例縮放圖片並裁切溢出部分，以完整覆蓋容器且不產生黑邊。<br><br>* `contain`：縮放圖片以完整符合容器。可能會非等比例拉伸以避免黑邊，進而造成變形。 |

## Fullscreen

|設定 |類型 |必填 |預設值 |說明 |
|---|---|---|---|---|
|rotateFullscreen |boolean |否 |`false` |影片進入全螢幕模式時，是否以橫向模式播放影片。此功能通常用於行動裝置。啟用後，影片進入全螢幕模式時，播放器會從直向模式旋轉 90 度到橫向模式。此屬性的優先順序低於 `useCssFullscreen`。<br><br><br>* `true`：啟用。<br><br>* `false`：停用。 |
|useCssFullscreen |boolean |否 |`false` |是否使用全視窗。<br><br><br>* `true`：使用全視窗模式，播放器會覆蓋瀏覽器視窗。<br><br>* `false`：使用全螢幕模式，播放器會覆蓋整個桌面。 |
|needBackIcon |boolean |否 |`false` |播放器處於全螢幕模式時，是否在右上角顯示返回按鈕。此功能通常在行動裝置上開啟。<br><br><br>* `true`：顯示；<br><br>* `false`：不顯示。 |

## ErrorConfig

|設定 |類型 |必填 |預設值 |說明 |
|---|---|---|---|---|
|showErrorImg |boolean |否 |`true` |是否顯示錯誤圖片。 |
|showErrorTip |boolean |否 |`true` |是否顯示錯誤訊息。 |
|showRefresh |boolean |否 |`true` |是否顯示重新整理按鈕。 |
|errorTipsText |string \| Record<string, string\> |否 |無 |自訂錯誤訊息。 |
|extraTips |{ label: string \| Record<Lang, string\>; value: string \| Record<Lang, string\>; }[] |否 |無 |更多提示。 |

## RTMNetWorkInfo

在 RTM 拉流情境中取得的網路狀況。

|設定 |類型 |必填 |預設值 |說明 |
|---|---|---|---|---|
|speed |number |否 |\- |最新網路評估期間內的下載速度，單位為 bps。 |
|avgSpeed |number |否 |\- |最近 5 個網路評估週期內的平均下載速度，單位為 bps。 |
|lostRate |number |否 |\- |最新網路評估週期內的網路封包遺失率。 |
|avgLostRate |number |否 |\- |最近 5 個網路評估週期內的平均網路封包遺失率。 |

## SEIDelayStats

衍生自伺服器 SEI 資料的延遲統計。

|設定 |類型 |必填 |預設值 |說明 |
|---|---|---|---|---|
|delay_s2s |number |否 |\- |伺服器到伺服器延遲，單位為毫秒。表示串流從 MediaLive 推流側邊緣節點傳輸到 MediaLive 拉流側邊緣節點所需時間。當有效的伺服器 SEI 資料不可用時為空。 |
|delay_s2e |number |否 |\- |伺服器到端延遲，單位為毫秒。表示從串流到達 MediaLive 推流側邊緣節點，到 Player SDK for Web 播放對應影格所需時間。因為 Player SDK 會在播放對應影格前解析 SEI 訊息，所以本機播放器緩衝時長包含在計算中。當有效的伺服器 SEI 資料不可用時為空。 |

## StatsSnapShoot

RTM 直播串流資訊。

|設定 |類型 |必填 |預設值 |說明 |
|---|---|---|---|---|
|video | |否 |\- |影片資訊。 |
|audio | |否 |\- |音訊資訊。 |

## Stats

HLS 和 FLV 通訊協定播放的基本資訊。

|設定 |類型 |必填 |預設值 |說明 |
|---|---|---|---|---|
|avgSpeed |number |是 |\- |平均下載速度。 |
|bitrate |number |是 |\- |位元率。 |
|bufferEnd |number |是 |\- |剩餘緩衝時間。 |
|currentTime |number |是 |\- |目前播放時間。 |
|downloadSpeed |number |是 |\- |目前下載速度。 |
|encodeType |string |是 |\- |編碼方式。 |
|fps |number |是 |\- |影格率。 |
|height |number |是 |\- |影片高度。 |
|width |number |是 |\- |影片寬度。 |

## FlvStats

FLV 直播串流資訊。

|設定 |類型 |必填 |預設值 |說明 |
|---|---|---|---|---|
|totalReceivedByte |number |是 |\- |已接收的位元組總數。 |
|totalReceivedCost |number |是 |\- |接收所有位元組所耗費的時間。 |

## PrepareOptions

播放器策略設定。

|設定 |類型 |必填 |預設值 |說明 |
|---|---|---|---|---|
|appId |string |是 |\- |SDK 應用程式 ID。您可以登入 BytePlus MediaLive 控制台，並前往 [SDK Management](https://console.byteplus.com/live/main/sdk) 取得。 |
|userId |string |否 |\- |用於識別單一使用者的 ID。如果未設定，將產生隨機使用者 ID，並儲存在瀏覽器快取中。<br><br>> **備註**<br><br><br>> 建議使用與業務相關的使用者 ID，以便在發生播放錯誤時快速定位並排解問題。<br> |
|strategies | |是 |\- |播放策略設定。 |

## DecodeType

類型：`enum`

解碼方法。

|屬性 |值 |說明 |
|---|---|---|
|Software |`'software'` |軟體解碼。 |
|Hardware |`'hardware'` |硬體解碼。 |

## Codec

類型：`enum`

影片的實際編解碼器。如果您在 degradation 中設定 SoftFirst 屬性（也就是硬體解決方案不支援降級到軟體解決方案），建議您傳入此參數，以節省探測實際編碼格式的作業。

|屬性 |值 |說明 |
|---|---|---|
|H265 |`'h265'` |H.265。 |
|H264 |`'h264'` |H.264。 |

## Degradation

類型：`enum`

是否使用 H.265 相容模式。在 H.265 相容模式下，播放器會優先使用硬體解碼來解碼 H.265 影片。如果裝置或瀏覽器不支援 H.265 硬體解碼，將自動回退到 H.265 軟體解碼。

|屬性 |值 |說明 |
|---|---|---|
|SoftFirst |`'soft-first'` |不支援硬體解碼時，優先降級到軟體解碼。 |

## ListType

類型：`enum`

解析度和直播串流來源選擇的面板樣式。此設定僅在行動裝置上有效。

|屬性 |值 |說明 |
|---|---|---|
|Bottom |`'bottom'` |底部導覽抽屜。 |
|Fullscreen |`'fullscreen'` |右側導覽抽屜。這通常用於全螢幕顯示。 |
|Inner |`'inner'` |覆蓋層。 |

## LicenseConfig

類型：`interface`

SDK 授權設定。

### license

類型：string | [IlicenseContent](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1155423?lang=en#ilicensecontent)

授權設定。支援授權 URL 或授權檔案內容。

## IlicenseContent

類型：`interface`

授權檔案的內容。

### content

類型：`string`

對應於授權檔案中的 `Content` 欄位，其中包含權限等級和版本資訊。

### sign

類型：`string`

對應於授權檔案中的 `Signature` 欄位，用於驗證。

### mainUrl

類型：`string | undefined`

對應於授權檔案中的 `MainURL` 欄位，也就是授權 URL。

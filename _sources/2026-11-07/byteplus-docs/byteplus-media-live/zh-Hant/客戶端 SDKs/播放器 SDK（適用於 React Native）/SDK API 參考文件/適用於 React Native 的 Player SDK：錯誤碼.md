---
title: "適用於 React Native 的 Player SDK：錯誤碼"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api-error-code-zh-TW"
---

<span id="veliveplayererror"></span>
## VeLivePlayerError

類型：`class`

播放錯誤。

<span id="d8ff1226"></span>
### errorCode

類型：`number`

`Readonly`，錯誤碼。

<span id="b154dc48"></span>
### errorMsg

類型：`string`

`Readonly`，錯誤訊息。

<span id="9b9c7921"></span>
## VeLivePlayerErrorCode

類型：`enum`

播放錯誤碼。


|屬性 |值 |說明 |
|---|---|---|
|VeLivePlayerNoError |`0` |無錯誤。 |
|VeLivePlayerInvalidLicense |`-1` |SDK 授權無效。此錯誤可能因授權整合不正確或授權已過期而發生。請檢查授權整合方式並確保授權仍有效。 |
|VeLivePlayerInvalidParameter |`-2` |參數無效。請檢查輸入參數並重新呼叫方法。 |
|VeLivePlayerErrorRefused |`-3` |方法呼叫已被拒絕。此錯誤於方法在錯誤時間點被呼叫時發生。 |
|VeLivePlayerErrorLibraryLoadFailed |`-4` |載入函式庫檔案失敗。此錯誤可能因 SDK 整合不正確而發生。 |
|VeLivePlayerErrorPlayUrl |`-100` |拉流地址不存在或無效。此錯誤可能因拉流地址為空，或地址格式或長度無效而發生。 |
|VeLivePlayerErrorNoStreamData |`-101` |無法取得串流資料。此錯誤可能因直播串流不存在、中斷或已結束而發生。請檢查直播串流狀態。 |
|VeLivePlayerErrorInternalRetryStart |`-102` |內部重試播放直播串流，可能因播放器內部錯誤而發生。 |
|VeLivePlayerErrorInternalRetryFailed |`-103` |內部重試失敗且已達到最大重試次數。播放器已停止重試。可嘗試手動重試。 |
|VeLivePlayerErrorDnsParseFailed |`-200` |DNS 解析失敗。此錯誤可能因拉流地址錯誤或用戶端網路狀況造成。若驗證拉流地址及網路狀況後錯誤仍然存在，請聯絡 BytePlus 技術支援協助。 |
|VeLivePlayerErrorNetworkRequestFailed |`-201` |網路請求失敗。請檢查網路狀況。若錯誤持續，請聯絡 BytePlus 技術支援協助。 |
|VeLivePlayerErrorDemuxFailed |`-300` |視訊解封裝失敗。此錯誤可能因直播串流使用不支援的格式或協議，或音訊或視訊錯誤而發生。若錯誤持續，請聯絡 BytePlus 技術支援協助。 |
|VeLivePlayerErrorDecodeFailed |`-301` |解碼失敗。此錯誤可能因直播串流使用不支援的音訊或視訊格式而發生。若錯誤持續，請聯絡 BytePlus 技術支援協助。 |
|VeLivePlayerErrorAVOutputFailed |`-302` |渲染失敗。此錯誤可能因音訊或視訊輸出裝置出現問題而發生。若錯誤持續，請聯絡 BytePlus 技術支援協助。 |
|VeLivePlayerErrorSRDeviceUnsupported |`-303` |裝置型號不支援超解析度。如需協助，請聯絡 BytePlus 技術支援。 |
|VeLivePlayerErrorSRResolutionUnsupported |`-304` |目前解析度超過超解析度允許的上限。如需協助，請聯絡 BytePlus 技術支援。 |
|VeLivePlayerErrorSRFpsUnsupported |`-305` |目前幀率超過超解析度允許的上限。如需協助，請聯絡 BytePlus 技術支援。 |
|VeLivePlayerErrorSRInitFail |`-306` |初始化超解析度失敗。若錯誤持續，請聯絡 BytePlus 技術支援。 |
|VeLivePlayerErrorSRExecuteFail |`-307` |套用超解析度至視訊失敗。若錯誤持續，請聯絡 BytePlus 技術支援。 |
|VeLivePlayerLicenseUnsupportedH265 |`-308` |當前的 SDK 授權不支援 H.265 功能。 |
|VeLivePlayerDRMFetchCKCFailed |`-400` |DRM 驗證失敗。 |
|VeLivePlayerDRMFetchSPCFailed |`-401` |無法產生 Server Playback Context (SPC)。 |
|VeLivePlayerErrorInternal |`-999` |內部錯誤。請聯繫 BytePlus 技術支援以獲得協助。 |

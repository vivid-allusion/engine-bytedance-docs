---
title: "iOS 版 Player SDK：錯誤碼"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api-error-code-zh-TW"
---

# VeLivePlayerError

```objectivec
@interface VeLivePlayerError : NSError
```

Player SDK 錯誤。

## 成員屬性

|類型 |名稱 |
|---|---|
|NSInteger |[errorCode](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api-error-code#VeLivePlayerError-errorcode) |
|NSInteger |[subErrorCode](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api-error-code#VeLivePlayerError-suberrorcode) |
|NSString\* |[errorMsg](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api-error-code#VeLivePlayerError-errormsg) |

## 說明

### errorCode

```objectivec
@property (nonatomic, readonly) NSInteger errorCode;
```

Player SDK 錯誤碼。

### subErrorCode

```objectivec
@property (nonatomic, readonly) NSInteger subErrorCode;
```

Player SDK 子錯誤碼。

### errorMsg

```objectivec
@property (nonatomic, readonly, nullable) NSString* errorMsg;
```

Player SDK 錯誤訊息。

# VeLivePlayerErrorCode

```objectivec
typedef NS_ENUM(
    NSInteger,
    VeLivePlayerErrorCode
)
```

Player SDK 錯誤碼。

## 列舉值

|類型 |值 |說明 |
|---|---|---|
|VeLivePlayerNoError |0 |無錯誤。 |
|VeLivePlayerInvalidLicense |\-1 |授權無效。可能是授權整合錯誤或授權已過期。<br><br>**請檢查授權整合與有效期限。如果問題仍然存在，請聯絡** [BytePlus 技術支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **瞭解詳情。**  |
|VeLivePlayerInvalidParameter |\-2 |參數無效。<br><br>**請檢查後重試。**  |
|VeLivePlayerErrorRefused |\-3 |因呼叫時機不正確，呼叫遭拒。<br><br>**請檢查呼叫時機後重試。建議在開發階段處理此錯誤。**  |
|VeLivePlayerErrorLibraryLoadFailed |\-4 |載入程式庫檔案失敗。可能是 SDK 整合錯誤所致。<br><br>**請檢查 SDK 整合後重試。建議在開發階段處理此錯誤。**  |
|VeLivePlayerErrorPlayUrl |\-100 |拉流位址不存在或無效。可能是拉流位址為空、格式無效，或超過長度限制。<br><br>**開發期間，您可以監控此錯誤以排查使用問題。如果此錯誤發生在生產環境，建議以醒目提示通知觀眾播放器無法使用，並要求他們重新啟動播放器。**  |
|VeLivePlayerErrorNoStreamData |\-101 |串流資料不存在或網路請求失敗。可能是直播串流不存在、中斷或已結束。<br><br>**建議更換拉流位址、切換至低位元率串流，或提示觀眾網路問題。**  |
|VeLivePlayerErrorInternalRetryStart |\-102 |播放器內部重試。可能是播放器內部錯誤所致。<br><br>**建議更換拉流位址、切換至低位元率串流，或提示觀眾網路問題。**  |
|VeLivePlayerErrorInternalRetryFailed |\-103 |播放器內部重試失敗。播放器已達最大重試次數並停止重試。<br><br>**建議更換拉流位址、切換至低位元率串流，或提示觀眾網路問題。**  |
|VeLivePlayerErrorDnsParseFailed |\-200 |DNS 解析失敗。可能是拉流位址異常或用戶端網路狀態異常所致。<br><br>**建議更換拉流位址、切換至低位元率串流，或提示觀眾網路問題。**  |
|VeLivePlayerErrorNetworkRequestFailed |\-201 |網路請求失敗。<br><br>**建議更換拉流位址、切換至低位元率串流，或提示觀眾網路問題。**  |
|VeLivePlayerErrorDemuxFailed |\-300 |解多工失敗。可能是串流格式或通訊協定不受支援，或音訊/視訊串流錯誤所致。<br><br>**建議更換拉流位址、切換至低位元率串流，或提示觀眾網路問題。**  |
|VeLivePlayerErrorDecodeFailed |\-301 |視訊解碼失敗。可能是直播串流音訊/視訊格式不受支援，或解碼器錯誤所致。<br><br>**建議更換拉流位址、切換至低位元率串流，或提示觀眾網路問題。如果問題仍然存在，請聯絡** [BytePlus 技術支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **瞭解詳情。**  |
|VeLivePlayerErrorAVOutputFailed |\-302 |算繪失敗。可能是音訊或視訊輸出裝置異常所致。<br><br>**如果此錯誤發生在生產環境，建議以醒目提示通知觀眾播放器無法使用，並要求他們重新啟動播放器。**  |
|VeLivePlayerErrorSRDeviceUnsupported |\-303 |目前裝置不在超解析度模型允許清單中，且不支援超解析度功能。<br><br>**開發期間，您可以監控此錯誤以排查使用問題。請聯絡** [BytePlus 技術支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **瞭解詳情。**  |
|VeLivePlayerErrorSRResolutionUnsupported |\-304 |解析度超過超解析度限制。<br><br>**開發期間，您可以監控此錯誤以排查使用問題。請聯絡** [BytePlus 技術支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **瞭解詳情。**  |
|VeLivePlayerErrorSRFpsUnsupported |\-305 |影格率超過超解析度限制。<br><br>**開發期間，您可以監控此錯誤以排查使用問題。請聯絡** [BytePlus 技術支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **瞭解詳情。**  |
|VeLivePlayerErrorSRInitFail |\-306 |初始化超解析度失敗。<br><br>**開發期間，您可以監控此錯誤以排查使用問題。請聯絡** [BytePlus 技術支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **瞭解詳情。**  |
|VeLivePlayerErrorSRExecuteFail |\-307 |執行超解析度失敗。<br><br>**開發期間，您可以監控此錯誤以排查使用問題。請聯絡** [BytePlus 技術支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **瞭解詳情。**  |
|VeLivePlayerLicenseUnsupportedH265 |\-308 |您使用的基本授權不支援 H.265 硬體與軟體解碼功能。<br><br>**請購買並使用進階授權。如需瞭解如何取得進階授權，請參閱** [取得 SDK 授權](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **。**  |
|VeLivePlayerErrorSharpenDeviceUnsupported |\-309 |裝置不支援視訊銳化功能。<br><br>**開發期間，您可以監控此錯誤以排查使用問題。請聯絡** [BytePlus 技術支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **瞭解詳情。**  |
|VeLivePlayerErrorSharpenResolutionUnsupported |\-310 |解析度超過視訊銳化限制。<br><br>**開發期間，您可以監控此錯誤以排查使用問題。請聯絡** [BytePlus 技術支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **瞭解詳情。**  |
|VeLivePlayerErrorSharpenFpsUnsupported |\-312 |影格率超過視訊銳化限制。<br><br>**開發期間，您可以監控此錯誤以排查使用問題。請聯絡** [BytePlus 技術支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **瞭解詳情。**  |
|VeLivePlayerErrorSharpenInitFail |\-313 |初始化視訊銳化失敗。<br><br>**開發期間，您可以監控此錯誤以排查使用問題。請聯絡** [BytePlus 技術支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **瞭解詳情。**  |
|VeLivePlayerErrorLicenseUnsupportedABR |\-315 |您使用的基本授權不支援自適應位元率（ABR）串流功能。<br><br>**請購買並使用進階授權。如需瞭解如何取得進階授權，請參閱** [取得 SDK 授權](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **。**  |
|VeLivePlayerErrorLicenseUnsupportedDRM |\-316 |您使用的基本授權不支援播放 DRM（Digital Rights Management）加密串流。<br><br>**請購買並使用進階授權。如需瞭解如何取得進階授權，請參閱** [取得 SDK 授權](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **。**  |
|VeLivePlayerErrorLicenseUnsupportedSEI |\-317 |您使用的基本授權不支援 Supplemental Enhancement Information（SEI）訊息接收功能。<br><br>**請購買並使用進階授權。如需瞭解如何取得進階授權，請參閱** [取得 SDK 授權](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **。**  |
|VeLivePlayerErrorLicenseUnsupportedSuperResolution |\-318 |您使用的基本授權不支援超解析度功能。<br><br>**請購買並使用進階授權。如需瞭解如何取得進階授權，請參閱** [取得 SDK 授權](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **。**  |
|VeLivePlayerErrorLicenseUnsupportedSharpen |\-319 |您使用的基本授權不支援視訊銳化功能。<br><br>**請購買並使用進階授權。如需瞭解如何取得進階授權，請參閱** [取得 SDK 授權](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **。**  |
|VeLivePlayerErrorLicenseUnsupportedQUIC |\-320 |您使用的基本授權不支援 QUIC 通訊協定。<br><br>**請購買並使用進階授權。如需瞭解如何取得進階授權，請參閱** [取得 SDK 授權](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **。**  |
|VeLivePlayerErrorLicenseUnsupportedRTM |\-323 |您使用的基本授權不支援播放 RTM 串流。<br><br>**請購買並使用進階授權。如需瞭解如何取得進階授權，請參閱** [取得 SDK 授權](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **。**  |
|VeLivePlayerErrorLicenseUnsupportedMainBackup |\-324 |您使用的基本授權不支援主備串流切換功能。<br><br>**請購買並使用進階授權。如需瞭解如何取得進階授權，請參閱** [取得 SDK 授權](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **。**  |
|VeLivePlayerErrorLicenseUnsupportedFLVLowLatency |\-325 |您使用的基本授權不支援播放低延遲 FLV 串流（延遲為 2 到 3 秒）。<br><br>**請購買並使用進階授權。如需瞭解如何取得進階授權，請參閱** [取得 SDK 授權](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **。**  |
|VeLivePlayerDRMFetchCKCFailed |\-400 |DRM 驗證失敗。<br><br>**如果此錯誤發生在生產環境，建議以醒目提示通知觀眾播放器無法使用，並要求他們重新啟動播放器。**  |
|VeLivePlayerDRMFetchSPCFailed |\-401 |產生 Server Playback Context（SPC）失敗。<br><br>**如果此錯誤發生在生產環境，建議以醒目提示通知觀眾播放器無法使用，並要求他們重新啟動播放器。**  |
|VeLivePlayerErrorNotSupportResolutionSwitch |\-510 |播放器不支援畫質等級切換。<br><br>**開發期間，您可以監控此錯誤以排查使用問題。請聯絡** [BytePlus 技術支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **瞭解詳情。**  |
|VeLivePlayerErrorInternal |\-999 |內部錯誤。<br><br>**請聯絡** [BytePlus 技術支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **瞭解詳情。**  |

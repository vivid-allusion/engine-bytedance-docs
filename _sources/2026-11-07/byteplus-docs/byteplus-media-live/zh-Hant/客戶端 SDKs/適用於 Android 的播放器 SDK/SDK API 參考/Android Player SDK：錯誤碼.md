---
title: "Android Player SDK：錯誤碼"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-errorcode-zh-TW"
---

# VeLivePlayerError

```java
public class com.ss.videoarch.liveplayer.VeLivePlayerError
```

Player SDK 錯誤。

## 成員屬性

|類型 |預設值 |名稱 |
|---|---|---|
|int |`-` |[mErrorCode](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerError-merrorcode) |
|String |`-` |[mErrorMsg](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerError-merrormsg) |
|int |\-1 |[mSubCode](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerError-msubcode) |

## 成員函式

|傳回 |名稱 |
|---|---|
|VeLivePlayerError |[VeLivePlayerError](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerError-veliveplayererror-4) |

## 說明

### mErrorCode

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerError.mErrorCode
```

Player SDK 錯誤碼。

### mErrorMsg

```java
public String com.ss.videoarch.liveplayer.VeLivePlayerError.mErrorMsg
```

Player SDK 錯誤訊息。

### mSubCode

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerError.mSubCode = -1
```

Player SDK 子錯誤碼。

## 說明

### VeLivePlayerError

```java
public com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerError(
    int errorCode,
    int subCode,
    String errorMsg
)
```

建立包含錯誤碼、子錯誤碼和錯誤訊息的 `VeLivePlayerError` 執行個體。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|errorCode |int |錯誤碼。 |
|subCode |int |子錯誤碼。 |
|errorMsg |String |錯誤訊息。 |

**傳回值**

`VeLivePlayerError` 執行個體。

# VeLivePlayerErrorCode

```java
public static class com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode
```

Player SDK 錯誤碼。

## 成員屬性

|類型 |預設值 |名稱 |
|---|---|---|
|int |0 |[VeLivePlayerNoError](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayernoerror) |
|int |\-1 |[VeLivePlayerInvalidLicense](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayerinvalidlicense) |
|int |\-2 |[VeLivePlayerInvalidParameter](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayerinvalidparameter) |
|int |\-3 |[VeLivePlayerErrorRefused](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorrefused) |
|int |\-4 |[VeLivePlayerErrorLibraryLoadFailed](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorlibraryloadfailed) |
|int |\-100 |[VeLivePlayerErrorPlayUrl](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorplayurl) |
|int |\-101 |[VeLivePlayerErrorNoStreamData](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrornostreamdata) |
|int |\-102 |[VeLivePlayerErrorInternalRetryStart](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorinternalretrystart) |
|int |\-103 |[VeLivePlayerErrorInternalRetryFailed](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorinternalretryfailed) |
|int |\-200 |[VeLivePlayerErrorDnsParseFailed](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrordnsparsefailed) |
|int |\-201 |[VeLivePlayerErrorNetworkRequestFailed](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrornetworkrequestfailed) |
|int |\-300 |[VeLivePlayerErrorDemuxFailed](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrordemuxfailed) |
|int |\-301 |[VeLivePlayerErrorDecodeFailed](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrordecodefailed) |
|int |\-302 |[VeLivePlayerErrorAVOutputFailed](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererroravoutputfailed) |
|int |\-303 |[VeLivePlayerErrorSRDeviceUnsupported](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorsrdeviceunsupported) |
|int |\-304 |[VeLivePlayerErrorSRResolutionUnsupported](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorsrresolutionunsupported) |
|int |\-305 |[VeLivePlayerErrorSRFpsUnsupported](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorsrfpsunsupported) |
|int |\-306 |[VeLivePlayerErrorSRInitFail](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorsrinitfail) |
|int |\-307 |[VeLivePlayerErrorSRExecuteFail](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorsrexecutefail) |
|int |\-308 |[VeLivePlayerLicenseUnsupportedH265](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayerlicenseunsupportedh265) |
|int |\-309 |[VeLivePlayerErrorSharpenDeviceUnsupported](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorsharpendeviceunsupported) |
|int |\-310 |[VeLivePlayerErrorSharpenResolutionUnsupported](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorsharpenresolutionunsupported) |
|int |\-312 |[VeLivePlayerErrorSharpenFpsUnsupported](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorsharpenfpsunsupported) |
|int |\-313 |[VeLivePlayerErrorSharpenInitFail](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorsharpeninitfail) |
|int |\-314 |[VeLivePlayerErrorLicenseUnsupportedH266](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorlicenseunsupportedh266) |
|int |\-315 |[VeLivePlayerErrorLicenseUnsupportedABR](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorlicenseunsupportedabr) |
|int |\-316 |[VeLivePlayerErrorLicenseUnsupportedDRM](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorlicenseunsupporteddrm) |
|int |\-317 |[VeLivePlayerErrorLicenseUnsupportedSEI](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorlicenseunsupportedsei) |
|int |\-318 |[VeLivePlayerErrorLicenseUnsupportedSuperResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorlicenseunsupportedsuperresolution) |
|int |\-319 |[VeLivePlayerErrorLicenseUnsupportedSharpen](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorlicenseunsupportedsharpen) |
|int |\-320 |[VeLivePlayerErrorLicenseUnsupportedQUIC](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorlicenseunsupportedquic) |
|int |\-321 |[VeLivePlayerErrorLicenseUnsupportedCMAF](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorlicenseunsupportedcmaf) |
|int |\-323 |[VeLivePlayerErrorLicenseUnsupportedRTM](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorlicenseunsupportedrtm) |
|int |\-324 |[VeLivePlayerErrorLicenseUnsupportedMainBackup](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorlicenseunsupportedmainbackup) |
|int |\-325 |[VeLivePlayerErrorLicenseUnsupportedFLVLowLatency](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorlicenseunsupportedflvlowlatency) |
|int |\-400 |[VeLivePlayerDRMFetchCKCFailed](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayerdrmfetchckcfailed) |
|int |\-401 |[VeLivePlayerDRMFetchSPCFailed](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayerdrmfetchspcfailed) |
|int |\-510 |[VeLivePlayerErrorNotSupportResolutionSwitch](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrornotsupportresolutionswitch) |
|int |\-999 |[VeLivePlayerErrorInternal](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorinternal) |

## 說明

### VeLivePlayerNoError

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerNoError = 0
```

無錯誤。

### VeLivePlayerInvalidLicense

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerInvalidLicense = -1
```

授權無效。這可能是授權整合錯誤或授權到期所致。

**請檢查授權整合與有效期間。如果問題仍然存在，請聯絡** [BytePlus 技術支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **了解詳情。**

### VeLivePlayerInvalidParameter

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerInvalidParameter = -2
```

參數無效。

**請檢查後重試。**

### VeLivePlayerErrorRefused

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorRefused = -3
```

因呼叫時機不正確而遭拒。

**請檢查時機後重試。建議在開發階段處理此錯誤。**

### VeLivePlayerErrorLibraryLoadFailed

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorLibraryLoadFailed = -4
```

載入程式庫檔案失敗。這可能是 SDK 整合錯誤所致。

**請檢查 SDK 整合後重試。建議在開發階段處理此錯誤。**

### VeLivePlayerErrorPlayUrl

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorPlayUrl = -100
```

拉流位址不存在或無效。這可能是拉流位址為空、格式無效或超過長度限制所致。

**開發期間，您可以監控此錯誤以排查使用問題。如果此錯誤發生於生產環境，建議以醒目提示通知觀眾播放器無法使用，並要求觀眾重新啟動播放器。**

### VeLivePlayerErrorNoStreamData

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorNoStreamData = -101
```

串流資料不存在或網路請求失敗。這可能是直播串流不存在、中斷或已結束所致。

**建議更換拉流位址、切換到低位元率串流，或提示觀眾網路問題。**

### VeLivePlayerErrorInternalRetryStart

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorInternalRetryStart = -102
```

播放器內部重試。這可能是播放器內部錯誤所致。

**建議更換拉流位址、切換到低位元率串流，或提示觀眾網路問題。**

### VeLivePlayerErrorInternalRetryFailed

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorInternalRetryFailed = -103
```

播放器內部重試失敗。播放器在達到最大重試次數後已停止重試。

**建議更換拉流位址、切換到低位元率串流，或提示觀眾網路問題。**

### VeLivePlayerErrorDnsParseFailed

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorDnsParseFailed = -200
```

DNS 解析失敗。這可能是拉流位址異常或用戶端網路狀況異常所致。

**建議更換拉流位址、切換到低位元率串流，或提示觀眾網路問題。**

### VeLivePlayerErrorNetworkRequestFailed

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorNetworkRequestFailed = -201
```

網路請求失敗。

**建議更換拉流位址、切換到低位元率串流，或提示觀眾網路問題。**

### VeLivePlayerErrorDemuxFailed

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorDemuxFailed = -300
```

解多工失敗。這可能是串流格式或協定不支援，或音訊/視訊串流錯誤所致。

**建議更換拉流位址、切換到低位元率串流，或提示觀眾網路問題。**

### VeLivePlayerErrorDecodeFailed

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorDecodeFailed = -301
```

視訊解碼失敗。這可能是不支援的直播串流音訊/視訊格式或解碼器錯誤所致。

**建議更換拉流位址、切換到低位元率串流，或提示觀眾網路問題。如果問題仍然存在，請聯絡** [BytePlus 技術支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **了解詳情。**

### VeLivePlayerErrorAVOutputFailed

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorAVOutputFailed = -302
```

算繪失敗。這可能是音訊或視訊輸出裝置異常所致。

**如果此錯誤發生於生產環境，建議以醒目提示通知觀眾播放器無法使用，並要求觀眾重新啟動播放器。**

### VeLivePlayerErrorSRDeviceUnsupported

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorSRDeviceUnsupported = -303
```

目前裝置不在超解析度模型的允許清單中，且不支援超解析度功能。

**開發期間，您可以監控此錯誤以排查使用問題。請聯絡** [BytePlus 技術支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **了解詳情。**

### VeLivePlayerErrorSRResolutionUnsupported

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorSRResolutionUnsupported = -304
```

解析度超出超解析度限制。

**開發期間，您可以監控此錯誤以排查使用問題。請聯絡** [BytePlus 技術支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **了解詳情。**

### VeLivePlayerErrorSRFpsUnsupported

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorSRFpsUnsupported = -305
```

畫面更新率超出超解析度限制。

**開發期間，您可以監控此錯誤以排查使用問題。請聯絡** [BytePlus 技術支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **了解詳情。**

### VeLivePlayerErrorSRInitFail

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorSRInitFail = -306
```

初始化超解析度失敗。

**開發期間，您可以監控此錯誤以排查使用問題。請聯絡** [BytePlus 技術支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **了解詳情。**

### VeLivePlayerErrorSRExecuteFail

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorSRExecuteFail = -307
```

執行超解析度失敗。

**開發期間，您可以監控此錯誤以排查使用問題。請聯絡** [BytePlus 技術支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **了解詳情。**

### VeLivePlayerLicenseUnsupportedH265

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerLicenseUnsupportedH265 = -308
```

您使用的基本授權不支援 H.265 硬體與軟體解碼功能。

**請購買並使用進階授權。如需取得進階授權的詳細資訊，請參閱** [取得 SDK 授權](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **。**

### VeLivePlayerErrorSharpenDeviceUnsupported

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorSharpenDeviceUnsupported = -309
```

裝置不支援視訊銳化功能。

**開發期間，您可以監控此錯誤以排查使用問題。請聯絡** [BytePlus 技術支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **了解詳情。**

### VeLivePlayerErrorSharpenResolutionUnsupported

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorSharpenResolutionUnsupported = -310
```

解析度超出視訊銳化限制。

**開發期間，您可以監控此錯誤以排查使用問題。請聯絡** [BytePlus 技術支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **了解詳情。**

### VeLivePlayerErrorSharpenFpsUnsupported

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorSharpenFpsUnsupported = -312
```

畫面更新率超出視訊銳化限制。

**開發期間，您可以監控此錯誤以排查使用問題。請聯絡** [BytePlus 技術支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **了解詳情。**

### VeLivePlayerErrorSharpenInitFail

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorSharpenInitFail = -313
```

初始化視訊銳化失敗。

**開發期間，您可以監控此錯誤以排查使用問題。請聯絡** [BytePlus 技術支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **了解詳情。**

### VeLivePlayerErrorLicenseUnsupportedH266

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorLicenseUnsupportedH266 = -314
```

您使用的基本授權不支援 H.266 軟體解碼功能。

**請購買並使用進階授權。如需取得進階授權的詳細資訊，請參閱** [取得 SDK 授權](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **。**

### VeLivePlayerErrorLicenseUnsupportedABR

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorLicenseUnsupportedABR = -315
```

您使用的基本授權不支援自適應位元率 (ABR) 串流功能。

**請購買並使用進階授權。如需取得進階授權的詳細資訊，請參閱** [取得 SDK 授權](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **。**

### VeLivePlayerErrorLicenseUnsupportedDRM

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorLicenseUnsupportedDRM = -316
```

您使用的基本授權不支援播放 DRM（數位版權管理）加密串流。

**請購買並使用進階授權。如需取得進階授權的詳細資訊，請參閱** [取得 SDK 授權](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **。**

### VeLivePlayerErrorLicenseUnsupportedSEI

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorLicenseUnsupportedSEI = -317
```

您使用的基本授權不支援補充增強資訊 (SEI) 訊息接收功能。

**請購買並使用進階授權。如需取得進階授權的詳細資訊，請參閱** [取得 SDK 授權](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **。**

### VeLivePlayerErrorLicenseUnsupportedSuperResolution

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorLicenseUnsupportedSuperResolution = -318
```

您使用的基本授權不支援超解析度功能。

**請購買並使用進階授權。如需取得進階授權的詳細資訊，請參閱** [取得 SDK 授權](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **。**

### VeLivePlayerErrorLicenseUnsupportedSharpen

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorLicenseUnsupportedSharpen = -319
```

您使用的基本授權不支援視訊銳化功能。

**請購買並使用進階授權。如需取得進階授權的詳細資訊，請參閱** [取得 SDK 授權](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **。**

### VeLivePlayerErrorLicenseUnsupportedQUIC

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorLicenseUnsupportedQUIC = -320
```

您使用的基本授權不支援 QUIC 協定。

**請購買並使用進階授權。如需取得進階授權的詳細資訊，請參閱** [取得 SDK 授權](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **。**

### VeLivePlayerErrorLicenseUnsupportedCMAF

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorLicenseUnsupportedCMAF = -321
```

您使用的基本授權不支援播放 CMAF 串流。

**請購買並使用進階授權。如需取得進階授權的詳細資訊，請參閱** [取得 SDK 授權](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **。**

### VeLivePlayerErrorLicenseUnsupportedRTM

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorLicenseUnsupportedRTM = -323
```

您使用的基本授權不支援播放 RTM 串流。

**請購買並使用進階授權。如需取得進階授權的詳細資訊，請參閱** [取得 SDK 授權](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **。**

### VeLivePlayerErrorLicenseUnsupportedMainBackup

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorLicenseUnsupportedMainBackup = -324
```

您使用的基本授權不支援主備串流切換功能。

**請購買並使用進階授權。如需取得進階授權的詳細資訊，請參閱** [取得 SDK 授權](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **。**

### VeLivePlayerErrorLicenseUnsupportedFLVLowLatency

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorLicenseUnsupportedFLVLowLatency = -325
```

您使用的基本授權不支援播放低延遲 FLV 串流（延遲為 2 到 3 秒）。

**請購買並使用進階授權。如需取得進階授權的詳細資訊，請參閱** [取得 SDK 授權](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **。**

### VeLivePlayerDRMFetchCKCFailed

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerDRMFetchCKCFailed = -400
```

DRM 驗證失敗。

**如果此錯誤發生於生產環境，建議以醒目提示通知觀眾播放器無法使用，並要求觀眾重新啟動播放器。**

### VeLivePlayerDRMFetchSPCFailed

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerDRMFetchSPCFailed = -401
```

產生伺服器播放內容 (SPC) 失敗。

**如果此錯誤發生於生產環境，建議以醒目提示通知觀眾播放器無法使用，並要求觀眾重新啟動播放器。**

### VeLivePlayerErrorNotSupportResolutionSwitch

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorNotSupportResolutionSwitch = -510
```

播放器不支援畫質層級切換。

**開發期間，您可以監控此錯誤以排查使用問題。請聯絡** [BytePlus 技術支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **了解詳情。**

### VeLivePlayerErrorInternal

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorInternal = -999
```

內部錯誤。

**請聯絡** [BytePlus 技術支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **了解詳情。**

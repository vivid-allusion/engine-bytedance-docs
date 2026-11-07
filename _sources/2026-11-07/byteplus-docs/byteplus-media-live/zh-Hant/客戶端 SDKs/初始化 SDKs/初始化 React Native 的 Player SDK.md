---
title: "初始化 React Native 的 Player SDK"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-initializing-for-rn-zh-TW"
---

本主題介紹如何初始化 React Native 的 Player SDK。SDK 只需初始化一次。

<span id="de94af35"></span>
## 先決條件


* 你已依照 [整合 Player SDK 至 React Native](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-rn-zh-TW) 提供的指引將 SDK 集成至你的專案。

* 你已取得 app ID 及其他基本資訊。如需更多資訊，請參閱 [取得您的 SDK 授權](https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses-zh-TW)。


<span id="270ca9ed"></span>
## 初始化 SDK

打開 `src/store/pull/player.ts` 檔案，並進行以下修改。

```JavaScript
import {initEnv} from '@byteplus/react-native-live-pull';

initEnv({
  AppID: 'appId', // App ID，可在 MediaLive 控制台的 SDK 管理頁取得。
  // App 名稱。
  AppName: Platform.select({
      android: 'xxx', 
      ios: 'xxx'
  })

  // The channel through which to download the app.你也可以使用此參數來區分不同環境的 App 建置，例如生產、測試及除錯。
  AppChannel: Platform.select({
      android: 'GoogleStore',
      ios: 'AppStore',
      default: ''
  }),

  // The version number of your Android app.有效的版本號應包含兩個或以上分隔符，例如「1.3.2」。
  AppVersion: '1.0.0',
  
  // 授權檔案名稱。若更換授權檔案，需在此修改檔案名稱。為快速驗證 SDK，你可以替換原始授權檔案（ttsdk.lic）的內容。
  LicenseUri: {
    android: 'assets:///ttsdk.lic', 
    ios: 'ttsdk.lic'
  },
  UserUniqueID: 'VeLiveQuickStartDemo',
});
```


下表說明初始化參數：


|**參數** |**必填** |**資料型別** |**說明** |**範例** |
|---|---|---|---|---|
|AppID |是 |字串 |App ID，即你的 SDK 應用的唯一識別碼。詳情請參閱 [建立 SDK 應用](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management#creating-an-sdk-application)。 |`123456` |
|AppName |是 |字串 |應用名稱，即你的 SDK 應用的名稱。詳情請參閱 [建立 SDK 應用](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management#creating-an-sdk-application)。 |`video_demo` |
|AppVersion |是 |字串 |你的 App 的版本號。有效的版本號應包含兩個或以上分隔符，例如「1.3.2」。 |`1.3.2` |
|AppChannel |是 |字串 |用於下載 App 的渠道。你也可以使用此參數來區分不同環境的 App 建置，例如生產、測試及除錯。 |`google_play` |
|LicenseUri.android |是 |字串 |Android 授權檔案的本地路徑。 |`assets:///license1/license1_test.lic` |
|LicenseUri.ios |是 |字串 |iOS 授權檔案的本地路徑。 |`assets:///license2/license2_test.lic` |


<span id="f3d9c23d"></span>
## 上傳日誌

預設情況下，SDK 會自動上傳日誌，以協助排查生產問題並在質量平台上展示數據。為保護機密資料，你可以在 [初始化 SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-initializing-for-rn-zh-TW#270ca9ed) 之前呼叫 `openLog: false` 來停用日誌上傳。

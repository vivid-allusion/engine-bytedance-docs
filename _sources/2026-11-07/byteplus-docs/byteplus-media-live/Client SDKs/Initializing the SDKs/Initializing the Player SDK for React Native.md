---
title: "Initializing the Player SDK for React Native"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-initializing-for-rn"
---

This topic introduces how to initialize the Player SDK for React Native. You only need to initialize the SDK once.

<span id="de94af35"></span>
## Prerequisites


* You have integrated the SDK into your project by following the instructions provided in [Integrating the Player SDK for React Native](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-rn).

* You have obtained the app ID and other basic information. For more information, see [Getting your SDK license](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management).


<span id="270ca9ed"></span>
## Initializing the SDK

Open the `src/store/pull/player.ts` file and make the following modifications.

```JavaScript
import {initEnv} from '@byteplus/react-native-live-pull';

initEnv({
  AppID: 'appId', // App ID, get it on the SDK management page of the MediaLive console.
  // App name.
  AppName: Platform.select({
      android: 'xxx', 
      ios: 'xxx'
  })

  // The channel through which to download the app. You can also use this parameter to distinguish between app builds for different environments, such as production, testing, and debugging.
  AppChannel: Platform.select({
      android: 'GoogleStore',
      ios: 'AppStore',
      default: ''
  }),

  // The version number of your Android app. A valid version number should contain two or more separators, such as "1.3.2".
  AppVersion: '1.0.0',
  
  // License file name. If you replace the license file, you need to modify the file name here. To quickly verify the SDK, you can replace the content of the original license file (ttsdk.lic).
  LicenseUri: {
    android: 'assets:///ttsdk.lic', 
    ios: 'ttsdk.lic'
  },
  UserUniqueID: 'VeLiveQuickStartDemo',
});
```


The following table describes the initialization parameters:


|**Parameter** |**Required** |**Data Type** |**Description** |**Example** |
|---|---|---|---|---|
|AppID |Yes |String |App ID, which is the unique identifier of your SDK application. For details, see [Creating an SDK application](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management#creating-an-sdk-application). |`123456` |
|AppName |Yes |String |Application name, which is the name of your SDK application. For details, see [Creating an SDK application](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management#creating-an-sdk-application). |`video_demo` |
|AppVersion |Yes |String |The version number of your app. A valid version number should contain two or more separators, such as "1.3.2". |`1.3.2` |
|AppChannel |Yes |String |The channel through which to download the app. You can also use this parameter to distinguish between app builds for different environments, such as production, testing, and debugging. |`google_play` |
|LicenseUri.android |Yes |String |The local path to the Android license file. |`assets:///license1/license1_test.lic` |
|LicenseUri.ios |Yes |String |The local path to the iOS license file. |`assets:///license2/license2_test.lic` |


<span id="f3d9c23d"></span>
## Uploading logs

By default, automatic SDK log uploading is enabled for troubleshooting production issues and displaying data on the quality platform. To protect confidential data, you can call `openLog: false` to disable log uploading before [Initializing the SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-initializing-for-rn#270ca9ed).

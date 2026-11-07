---
title: "在 React Native 上構建您的第一個應用"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/docs-running-the-demo-react-native-zh-TW"
---

要快速構建一個跨平臺影片應用，您可以參考本指南執行 VideoOne Demo 專案。本文件為您提供在 React Native 框架內搭建專案並利用 React Native SDK 的分步操作說明。完成後，您將擁有一套程式碼庫，可同時生成具備強大影片播放功能的 Android 和 iOS 應用。

## 前置條件

請在開始前完成以下任務。建議您集中記錄每項任務獲得的資訊，便於專案搭建過程中隨時查閱。

|**任務** |**任務依賴功能** |**任務說明** |**完成後獲得的資訊** |
|---|---|---|---|
|1. 註冊 BytePlus 賬號。<br><br>2. 為賬號建立訪問金鑰。 |全部功能 |* [註冊 BytePlus 賬號](https://docs.byteplus.com/byteplus-platform/docs/signing-up-your-account)<br><br>* [建立訪問金鑰](https://docs.byteplus.com/byteplus-platform/docs/creating-an-accesskey) |* 訪問金鑰 ID（AK）<br><br>* 訪問金鑰（SK） |
|1. 啟用 BytePlus VOD 服務。<br><br>2. 建立 VOD 應用並獲取許可證。<br><br>> 如已建立 BytePlus MediaLive 應用，請繫結已有應用，無需新建。 |影片播放 |* [步驟 1：啟用 BytePlus VOD 服務](https://docs.byteplus.com/docs/byteplus-vod/docs-getting-started#step-1-enable-the-byteplus-vod-service)<br><br>* [應用管理](https://docs.byteplus.com/byteplus-vod/docs/sdk-management)<br><br>* [許可證管理](https://docs.byteplus.com/docs/byteplus-vod/docs-license-management) |* 應用 ID<br><br>* BytePlus VOD SDK 許可證檔案 |

## 開發環境

* **Watchman、Xcode 和 CocoaPods：** Xcode 需為 14.1 或更高版本。

* **Android JDK 和 Android Studio**

* **Node.js：** 建議使用 18.0 或更高版本。

* **實體移動裝置：**

   * Android 6.0 或更高版本。

   * iOS 13.0 或更高版本。

## 操作流程

### 克隆專案

請按照以下步驟克隆 Demo 專案：

1. 訪問 GitHub 並克隆 [VideoOneSolutions](https://github.com/byteplus-sdk/VideoOneSolutions) 倉庫。

2. 開啟終端，將當前目錄切換到 `Client/ReactNative`，即專案根目錄，並使用整合開發環境（IDE）開啟該目錄。

### 安裝依賴項

1. 全域性安裝 Expo CLI。

   ```Shell
   npm install -g @expo/cli
   ```

2. 安裝專案依賴項。

   ```Shell
   npm install
   ```

3. 進入 ios 目錄並安裝 iOS 依賴項。

   ```Shell
   cd ios && pod install
   ```

### 配置應用服務

開啟 `services/api.ts` 檔案，將 `SERVER_HOST` 修改為您的應用伺服器地址。

如需使用 BytePlus 提供的 Demo 應用伺服器，請將 `SERVER_HOST` 欄位設定為 `videocloud.byteplusapi.com`。

> **说明**

> 該地址僅供測試使用，不能用於生產環境。

### 配置 VOD 許可證

將您在前置準備環節獲得的許可證檔案重新命名為 `ttsdk.lic`，並移動到 `assets` 目錄下。

> **说明**

> 本專案透過 [Expo 外掛](https://docs.expo.dev/config-plugins/plugins/) 將許可證檔案複製到原生資源目錄。您也可以參考 [React Native Player SDK: Integrating the SDK](https://docs.byteplus.com/en/docs/byteplus-vod/docs-rn-player-quickstart) 中的指引，將許可證檔案分別放置在對應的 `ios` 和 `android` 目錄下。

### 專案配置

請按照以下步驟確保 App ID 與證書一致。

1. 在 `android/app/build.gradle` 檔案中，將 `applicationId` 修改為與證書對應的 Android 包名。

2. 使用 Xcode 開啟 `ios` 目錄。在 **Signing & Capabilities** 部分，將 **Bundle Identifier** 修改為與證書對應的 Bundle ID，並完成其他配置檔案的設定。

### 編譯並執行專案

請按照以下步驟編譯並執行專案。

1. 執行下方命令以啟動 Metro Server。啟動完成後，終端會顯示除錯用二維碼。

   ```Shell
   npm run start
   ```

2. 構建除錯應用：

   * Android

      1. 將電腦與 Android 手機連線。

      2. 執行下方命令，並在彈出的裝置列表中選擇已連線的手機裝置。

         ```Shell
         npm run android
         ```

      3. 在手機上允許應用安裝請求以完成安裝。

   * iOS

      4. 將電腦與 iPhone 連線。

      5. 執行下方命令，並在彈出的裝置列表中選擇已連線的 iPhone 裝置。專案會自動在您的手機上安裝應用。

      `Shell npm run ios`

### 體驗應用

開啟應用後，您可以探索並體驗短劇解決方案。

|![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/159babc54d5d42c1af358e6f9105572a~tplv-goo7wpa0wc-image.image) |![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/03abd5dd80ce4af2b5234c251de3f8f7~tplv-goo7wpa0wc-image.image) |![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2adc5303e4f14a47be08b7f7b923b36f~tplv-goo7wpa0wc-image.image) |
|---|---|---|

## 程式碼解析

### 專案結構

Demo 專案的目錄樹如下：

```Plain
Client/ReactNative/
├── app/                    # App screens (Expo Router)
│   ├── _layout.tsx         # Root layout
│   ├── index.tsx           # Home screen
│   ├── drama_channel.tsx   # Drama channel screen
│   ├── drama_player.tsx    # Video player screen
│   └── +not-found.tsx      # 404 screen
├── components/             # Reusable components
│   ├── player/             # Video player components
│   │   ├── VideoPlayer.tsx      # Main video player
│   │   ├── EpisodePlayer.tsx    # Episode player wrapper
│   │   ├── PlaybackControls.tsx # Playback control component
│   │   └── index.ts
│   ├── modals/             # Modal components
│   ├── feed/               # Content feed components
│   ├── ui/                 # UI components
│   ├── shared/             # Shared components
│   ├── drama/              # Drama-related components
│   │   ├── DramaCarousel.tsx  # Drama carousel
│   │   ├── DramaCover.tsx     # Drama cover
│   │   ├── DramaList.tsx      # Drama list
│   │   └── index.ts
│   └── index.ts            # Component exports
├── services/               # API services
│   ├── api.ts              # Base API client
│   ├── dramaService.ts     # Drama data service
│   ├── unlockService.ts    # Content unlock service
│   └── userService.ts      # User management service
├── hooks/                  # Custom React hooks
├── utils/                  # Utility functions
├── types/                  # TypeScript type definitions
├── constants/              # App constants
├── assets/                 # Static assets
│   ├── images/             # Images and icons
│   ├── minidrama/          # Drama-specific assets
│   └── ttsdk.lic           # SDK license file
├── android/                # Android-specific files
│   ├── app/                # Android app module
│   │   ├── build.gradle    # App build configuration
│   │   └── src/            # Android source code
│   ├── build.gradle        # Project build configuration
│.  ├── ...
├── ios/                    # iOS-specific files
│   ├── videoonern/         # iOS app target
│   │   ├── AppDelegate.swift
│   │   ├── ...
│   ├── videoonern.xcodeproj/     # Xcode project
│   ├── videoonern.xcworkspace/   # Xcode workspace
│   ├── Podfile             # CocoaPods dependencies
│   ├── Podfile.lock        # CocoaPods lock file
│   └── Pods/               # CocoaPods dependencies
├── plugins/                # Expo config plugins
│   ├── withATSConfig.js    # ATS configuration plugin
│   ├── withLicense.js      # License file plugin
│   ├── withPodfileSources.js # Podfile sources plugin
│   └── xcodeUtils.js       # Xcode utilities
├── app.json                # Expo app configuration
├── tsconfig.json           # TypeScript configuration
├── package.json            # npm package configuration
├── expo-env.d.ts           # Expo TypeScript definitions
├── eslint.config.js        # ESLint configuration
├── detection_tool.py       # Detection utility
├── LICENSE                 # License file
├── README.md               # English documentation
└── README-zh_CN.md         # Chinese documentation
```

### 技術架構

#### 核心技術

* **React Native**：跨平臺移動開發框架

* **Expo**：擁有豐富 API 和元件的開發平臺及工具鏈

* **TypeScript**：型別安全的 JavaScript 超集

* **Expo Router**：基於檔案的路由系統，簡化導航管理

#### 架構設計

以下主要介紹 VOD 短劇場景功能的設計：

1. **元件化架構**：按功能模組組織元件，提高程式碼複用性

   * `player/`：影片播放相關元件

   * `modals/`：彈窗元件

   * `feed/`：內容流元件

   * `ui/`：通用 UI 元件

   * `shared/`：共享元件

   * `drama/`：短劇相關元件

2. **服務層分離**：按業務領域分離 API 服務

   * `dramaService.ts`：短劇資料管理

   * `unlockService.ts`：內容解鎖服務

   * `userService.ts`：使用者管理服務

3. **自定義 hooks**：封裝可複用的業務邏輯

   * `useDramaChannel.ts`：短劇頻道資料管理

   * `useColorScheme.ts`：主題色管理

4. **型別安全**：全面的 TypeScript 型別定義

   * 完整的介面定義

   * 嚴格的型別檢查

   * 優異的開發體驗

### 功能介紹

以下介紹短劇解決方案的功能。有關播放器各功能的具體用法，請參考文件 [React Native Player SDK](https://docs.byteplus.com/en/docs/byteplus-vod/docs-rn-player-quickstart)。

#### 短劇功能

##### 播放功能

* **預載入影片**：支援自動策略的影片預載入

* **預渲染影片**：支援影片播放器的預渲染策略。

* **高質量影片流**：支援多種清晰度選項（720p、480p 等）

* **播放控制**：播放/暫停、進度條、音量控制

* **多倍速播放**：支援 0.5x 至 2.0x 的播放速度

* **橫豎屏切換**：自動適配螢幕方向，提供不同控制介面

* **進度管理**：支援拖動快進與播放位置記憶

##### 使用者互動功能

* **點贊系統**：支援點贊/取消點贊，實時計數更新

* **評論功能**：使用者評論與互動

* **觸覺反饋**：提供觸覺反饋，提升使用者體驗

##### 變現功能

* **廣告解鎖**：觀看廣告解鎖付費內容

* **VIP 訂閱**：付費解鎖全部內容

* **批次解鎖**：一次解鎖多集內容

##### 投屏功能

video\-one\-rn Demo 在應用層實現投屏。TTVideoEngine 負責本地播放，Demo 協調裝置選擇、原生投屏會話和播放交接。

* **AirPlay（iOS）** ：使用系統 AVRoutePickerView 和原生 AVPlayer 中轉播放器。在路由選擇和中轉啟動期間，本地播放器靜音；確認跳轉完成、媒體就緒和外部播放啟用後，暫停本地播放。

* **Google Cast（Android）** ：使用 react\-native\-google\-cast 選擇接收端，透過 RemoteMediaClient 載入解析後的媒體 URL、中繼資料和起始進度。連線期間即暫停本地播放，此時尚未確認遠端正在顯示影片。

* **停止投屏並返回本地播放**：iOS 上，停止投屏會開啟系統選擇器，使用者需選擇本地輸出；未改變外部路由而僅關閉選擇器，不會結束投屏。Android 會主動請求終止 Cast 會話，並抑制延遲到達的自動恢復回呼。僅停止投屏會保留當前播放頁；待執行的 iOS 返回操作會在路由回到本地且中轉狀態為 idle 後繼續執行。

* **頁面行為**：已連線或投屏狀態會顯示全屏覆蓋層、禁用劇集翻頁、關閉選集和解鎖對話框，並防止本地播放完成後自動切換下一集。頁面焦點和前景檢查會防止隱藏的本地播放器與當前活動播放器同時恢復播放。

兩個平臺都使用報告的遠端進度、儲存的遠端進度和本地進度中的最大值，恢復現有播放器。遠端向後拖動後，該位置可能與接收端的精確最終位置不同。iOS 的播放交接分支在恢復前檢查投屏前的播放狀態；Android 會自動恢復本地播放。獨立的頁面焦點和前景處理邏輯也會影響恢復。

投屏需要接收端能夠訪問和解碼的已解析 URL。當前請求不會轉發本地播放器的自定義請求頭、cookies 或 DRM 許可證配置。請在實體裝置和目標接收端上驗證簽名 URL、加密媒體、播放交接和音訊行為。

原生配置、控制器整合、各平臺流程和驗證場景，請參見[短劇影片 - React Native 整合：開發投屏功能](https://docs.byteplus.com/docs/byteplus-vos/short-drama-integration-by-reactnative-zh-tw#developing-the-casting-feature)。

##### 內容管理

* **短劇輪播**：首頁短劇推薦輪播

* **內容列表**：分類展示短劇內容

* **推薦系統**：基於使用者行為的智慧推薦

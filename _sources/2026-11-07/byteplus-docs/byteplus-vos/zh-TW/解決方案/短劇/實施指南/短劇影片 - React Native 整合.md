---
title: "短劇影片 - React Native 整合"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/short-drama-integration-by-reactnative-zh-tw"
---

本文面向希望基於 VideoOne React Native Demo 整合短劇能力的開發者，介紹從獲取原始碼、準備環境、配置專案和執行 Demo，到替換業務 API、理解程式碼結構的完整流程。

## 解決方案概述

React Native 短劇方案基於 BytePlus React Native VOD SDK 和 Expo 技術棧構建，提供移動端短劇場景的核心能力，包括短劇列表瀏覽、頻道頁導航、豎屏連續播放、劇集解鎖、使用者互動和推薦展示。對於已完成基礎環境搭建的團隊，建議複用 Demo 中的頁面、元件和服務層，再逐步替換面向業務的實現。

|維度 |說明 |建議 |
|---|---|---|
|目標場景 |移動端短劇播放與分集消費 |適合希望快速驗證短劇產品的團隊 |
|核心能力 |選集、續播、倍速、清晰度切換、解鎖、點贊、評論和推薦 |儘量複用 Demo 中現有的頁面和服務邊界 |
|整合工作量 |主要集中在 API 替換、資料對映和 UI 定製 |先跑通 Demo，再逐步替換業務模組 |

## 整合思路

與 Web 端的整合路徑類似，React Native 短劇整合建議分兩個階段進行。第一階段，完整執行官方 Demo，確認播放能力、許可證配置、原生專案和裝置除錯均正常。第二階段，逐步將 Demo 資料來源、解鎖邏輯和視覺樣式替換為自己的業務實現。分階段推進有助於區分環境問題、SDK 配置問題和業務整合問題，更容易定位故障。

第一階段，準備環境，配置服務地址和許可證，並在 iOS 和 Android 裝置上執行 Demo。

第二階段，替換短劇和頻道 API、使用者和解鎖邏輯，對映業務資料結構，並定製樣式與互動。

## 前置條件

開始整合 React Native 短劇前，請確保已滿足執行 Demo 所需的基礎條件。如果尚未完成基礎專案搭建，建議先閱讀同系列文件**在 React Native 上構建您的第一個應用**，再回到本文進行業務整合。

|項目 |用途 |獲得的資訊或資源 |
|---|---|---|
|BytePlus 賬號和 AK/SK |訪問雲服務並進行業務服務鑑權 |Access Key 和 Secret Key |
|VOD 服務和應用 |提供影片播放能力 |App ID 和許可證檔案 |
|React Native 開發環境 |執行 iOS 和 Android 專案 |Node、Expo CLI、Xcode、CocoaPods 和 Android Studio |
|實體測試裝置 |驗證移動端短劇互動 |Android 6.0+ 或 iOS 13.0+ 裝置 |

## 執行 Demo

### 操作步驟

1. **獲取原始碼**

   React Native Demo 位於 `VideoOneSolutions` 倉庫的 `Client/ReactNative` 目錄。建議直接基於該專案整合，以複用現有的短劇頁面、服務層和元件結構。

   ```Shell
   git clone https://github.com/byteplus-sdk/VideoOneSolutions
   cd VideoOneSolutions/Client/ReactNative
   ```

> 如果目標是快速整合短劇場景，建議從 Demo 開始，替換其中面向業務的部分，避免從空專案搭建。

2. **安裝依賴項**

   下載原始碼後，安裝 JavaScript 依賴和 iOS 原生依賴。專案基於 Expo 和 React Native，JavaScript 依賴用於頁面、路由和業務邏輯，`ios` 目錄中的 Pods 用於原生整合。

   1. 安裝 Expo CLI。

   2. 在專案根目錄安裝 npm 依賴。

   3. 進入 `ios` 目錄，執行 `pod install`，安裝 iOS 原生依賴。

   ```Shell
   npm install -g @expo/cli
   npm install
   cd ios && pod install
   ```

3. **配置應用服務**

   Demo 透過服務層封裝業務資料。將 Demo 整合到自己的短劇業務時，通常先替換應用服務地址。可以先使用 Demo 服務驗證完整頁面流程，再切換到自己的生產服務。

   開啟 `services/api.ts` 檔案，更新 `SERVER_HOST` 等服務地址配置。如果僅驗證 Demo，可以暫時保留 Demo 伺服器地址；正式整合時，將其替換為自己的業務服務域名。

   > **说明**

   > Demo 服務地址僅適用於測試和驗證，不能直接用於生產環境。

4. **配置許可證和原生專案**

   核心播放能力依賴 VOD SDK 許可證。將獲取的許可證檔案重新命名為 `ttssdk.lic`，放入 `assets` 目錄。當前 Demo 已透過 Expo Config Plugins 將許可證複製到原生資源目錄。

   除許可證外，還需確保 Android 包名、iOS Bundle Identifier 和簽名配置與證書一致，否則應用可能無法正常安裝或執行。

   * Android：更新 `android/app/build.gradle` 中的 `applicationId`。

   * iOS：在 Xcode 的 `Signing & Capabilities` 中更新 `Bundle Identifier`，並完成簽名相關配置。

5. **執行短劇 Demo**

   完成基礎配置後，在實體裝置上執行專案。短劇場景依賴滑動切換、沉浸式全屏播放、橫豎屏適配和觸覺反饋，模擬器無法充分驗證這些體驗，因此強烈建議使用實體裝置測試。

   ```Shell
   npm run start
   npm run android
   npm run ios
   ```

   |命令 |用途 |說明 |
   |---|---|---|
   |`npm run start` |啟動 Metro Server |提供資源打包和除錯入口 |
   |`npm run android` |安裝並啟動 Android 除錯應用 |建議在實體裝置上驗證滑動和解鎖體驗 |
   |`npm run ios` |安裝並啟動 iOS 除錯應用 |建議在 iPhone 上驗證播放、選集和互動 |

## 將 Demo 適配到自己的業務

Demo 穩定執行後，逐層替換業務邏輯。建議順序為**資料層 → 頁面入口 → 播放體驗 → 變現邏輯 → 互動功能**，以兼顧實現效率和除錯穩定性。

### 操作步驟

1. **替換 API**

   `services/` 目錄是業務適配的主要入口，通常可按以下職責進行對映：

   * `dramaService.ts`：短劇列表、頻道資料、推薦內容流和短劇詳情獲取。

   * `unlockService.ts`：解鎖狀態、廣告解鎖、批次解鎖和 VIP 解鎖邏輯。

   * `userService.ts`：使用者資訊、登入狀態和使用者相關行為。

   * `api.ts`：共享請求客戶端、主機配置和通用請求處理。

   整合時，建議保留現有服務函式邊界，僅替換內部請求實現和欄位對映，儘量減少頁面層的改造。

2. **適配資料結構**

   Web 短劇整合指南強調替換 API 和轉換資料結構，React Native 版本同樣適用。UI 元件通常需要穩定的前端資料模型，因此建議在服務層將後端響應欄位統一轉換為前端模型，避免在多個頁面元件中分別適配不同的後端資料結構。

   > **说明**

   > 建議先將後端欄位轉換為統一的短劇、劇集、使用者和解鎖狀態前端模型，再將這些模型傳遞給頁面和元件。

3. **替換頁面入口和路由**

   專案使用 Expo Router 組織頁面，短劇相關入口主要位於以下檔案：

   |**頁面檔案** |**職責** |**建議定製內容** |
   |---|---|---|
   |`app/index.tsx` |首頁入口 |可替換為自己的首頁或流量入口頁 |
   |`app/drama_channel.tsx` |短劇頻道頁 |適配頻道推薦、專題或分類邏輯 |
   |`app/drama_player.tsx` |短劇播放頁 |重點替換短劇載入、續播、解鎖和導航邏輯 |

4. **調整播放體驗**

   播放器邏輯主要位於 `components/player/` 和播放器配置工具中。短劇業務通常需要關注以下方面：

   * 預載入和預渲染策略，減少切換劇集時的等待。

   * 豎屏播放體驗和橫屏控制佈局。

   * 進度持久化和續播行為。

   * 倍速、清晰度和選集控制元件的顯示策略。

   * 自動播放下一集，以及播放結束後的推薦銜接。

   如果業務目標是提升連續觀看的流暢度，優先調整預載入策略、下一集銜接和解鎖成功後的無縫續播。

5. **替換變現和解鎖邏輯**

   Demo 已提供廣告解鎖、VIP 解鎖和批次解鎖等短劇變現示例。相關 UI 和彈窗邏輯主要位於：

   * `components/modals/VipUnlockModal.tsx`

   * `components/modals/UnlockMultipleModal.tsx`

   * `services/unlockService.ts`

   * `components/ui/AdComponent.tsx`

   可以將其替換為自己的變現模式，例如金幣解鎖、訂閱會員、激勵廣告或混合解鎖策略。建議在服務層和狀態層集中處理解鎖策略，避免將判斷邏輯分散到多個頁面。

6. **替換互動和推薦邏輯**

   短劇產品通常還包含社交互動和內容分發能力。Demo 已包含點贊、評論和推薦等基礎功能，整合時重點處理以下內容：

   * 替換點贊和取消點贊 API。

   * 替換評論列表和評論提交 API。

   * 替換推薦召回和推薦展示邏輯。

   * 調整頻道頁、播放頁和短劇結束頁的推薦銜接策略。

## 開發投屏功能

VideoOne React Native Demo 在應用層實現投屏。iOS 透過系統 AirPlay 路由選擇器和原生 AVPlayer 中轉播放器處理播放；Android 透過 react\-native\-google\-cast 在 Google Cast 接收端載入媒體。TTVideoEngine 負責本地播放，Demo 協調投屏 UI、會話和頁面互動。整合時需要同時接入 React Native 元件及對應的原生配置。

以下說明當前 `video-one-rn` 的實現。兩個平臺都透過 `useCast()` 暴露控制器，但啟動、本地暫停和停止流程有所不同。

### 投屏方式和媒體要求

|項目 |iOS |Android |
|---|---|---|
|協議 |AirPlay |Google Cast |
|裝置選擇 |`AVRoutePickerView` |`showCastDialog()` |
|遠端播放 |原生 `AirPlayRelay` 管理 AVPlayer |接收端透過 `RemoteMediaClient.loadMedia()` 載入 URL |
|本地播放暫停時機 |選擇裝置和啟動期間靜音；確認 `casting` 後暫停 |`isConnecting`、`isConnected` 或 `isCasting` 為 true 時暫停 |
|停止操作 |在系統選擇器中選擇 iPhone 或其他本地輸出 |呼叫 `endCurrentSession(true)` |

媒體 URL 來自 `VideoPlayer.tsx` 當前播放資訊中的 `MainPlayUrl`，透過 `onPlayUrlChange` 傳遞給 `EpisodePlayer`，播放回呼持續更新進度。投屏需要接收端能夠訪問和解碼的實際 URL。所有投屏介面的時間值均以秒為單位。是否支援投屏取決於解析後的 URL 和接收端能力，而非應用播放模式的名稱。

當前中轉請求不會轉發本地播放器的自定義請求頭、cookies 或 DRM 許可證配置。對於簽名 URL、加密媒體或受限網路，請先驗證接收端的訪問和解密能力。手機播放成功並不代表接收端相容。

### 原生專案配置

* **iOS**

   將 `ios/videoonern/AirPlayRelay.m` 和 `AirPlayRoutePickerViewManager.m` 加入應用 target，以匯出橋接模組和原生檢視。原生模組使用 `Playback`、`Default` 和 `LongFormVideo` 配置並啟用 Audio Session。請檢查本地網路使用說明，以及應用實際使用的 Bonjour 服務。Demo 還在 `UIBackgroundModes` 中包含 `audio`。

   本文介紹的 iOS 播放路徑使用 AirPlay，無需在應用程式碼中初始化 `GCKCastContext`。當前 Pod 鎖定檔案仍包含 react\-native\-google\-cast 自動連結引入的 Google Cast 依賴；存在依賴並不意味著當前投屏路徑使用該依賴。

* **Android**

   當前 `package.json` 宣告 `react-native-google-cast: ^4.9.1`，應用 Gradle 檔案顯式依賴 `com.google.android.gms:play-services-cast-framework:21.5.0`。`CastOptionsProvider.kt` 配置接收端和媒體通知。Manifest 註冊 `OPTIONS_PROVIDER_CLASS_NAME`，並宣告網際網路、網路狀態和 Wi\-Fi 狀態許可權。`MainActivity.onCreate` 初始化 `RNGCCastContext.getSharedInstance(this)`。

   Demo 使用 Google 預設媒體接收端 ID `CC1AD845`。如果應用需要自定義接收端，請替換為已註冊的 ID，並更新相關配置。Expo 專案應在 `app.json` 中保留 `./plugins/withGoogleCast`；該外掛生成 Android 配置，並補充 iOS 本地網路設定。如果手動維護原生專案，請檢查生成的檔案。

### 控制器和頁面整合

`app/drama_player.tsx` 建立一個 `castController`，透過 `EpisodePlayer` 傳遞給按鈕和播放器。頁面也使用該控制器渲染投屏覆蓋層。整合已有頁面時，請保留這一資料流，確保按鈕和頁面共享會話狀態。

```tsx
const castController = useCast();

<CastButton
  castController={castController}
  videoUrl={currentPlayUrl}
  currentTime={currentPlayTime}
  title={dramaTitle}
  coverUrl={dramaCoverUrl}
/>
```

示例中的媒體和進度變數由頁面維護。iOS 上，`CastButton` 渲染原生選擇器，`VideoPlayer` 透過 `AirPlayRelay.configureMedia()` 提供媒體。Android 上，建立會話後，按鈕使用傳入的 URL、進度和中繼資料呼叫 `startCasting()`。

|介面或狀態 |當前行為 |
|---|---|
|`isConnecting` |iOS 上對映為 `routeSelecting / routeSelected / starting`；Android 上跟隨會話連線事件。 |
|`isConnected / isCasting` |iOS 上均使用原生快照中的 `isCasting`。Android 上分別表示已建立會話，以及由媒體載入或狀態回呼設定的投屏標誌。 |
|`remotePosition` |兩個平臺均以秒為單位更新。iOS 裝置標籤為 AirPlay；Android 讀取接收端的友好名稱。 |
|`showCastPicker / startCasting / updateCastMedia / seekRemote` |Android 上執行對應操作。iOS hook 中這些介面不執行操作，投屏由原生選擇器和中轉模組驅動。 |
|`stopCasting` |主動結束 Android 會話。iOS 上僅在路由已回到本地時恢復 Audio Session，不能替代系統選擇器中的路由選擇。 |
|`isAvailable` |iOS 上檢查原生橋接模組是否存在。Android 上當前始終為 false，因此不表示裝置發現結果，也不能作為隱藏按鈕的可靠條件。 |

### iOS：AirPlay 中轉流程

僅當劇集可播放、播放器處於活動狀態且頁面擁有導航焦點時，才配置 AirPlay 媒體。`configureMedia()` 提供 URL、`startTime`、標題、封面和 `localWasPlaying`。選擇器顯示前呼叫 `beginRouteSelection()`，關閉後呼叫 `endRouteSelection()`。原生層還監聽路由通知，以確定實際輸出。

```text
idle → routeSelecting → routeSelected → starting → casting
casting → stopping → idle
starting → failed
```

在 `routeSelecting`、`routeSelected` 和 `starting` 期間，React Native 播放器靜音，並記錄此前是否正在播放。原生 AVPlayer 同樣以靜音狀態啟動，跳轉到傳入進度後開始播放。只有跳轉完成、`readyToPlay` 和 `externalPlaybackActive` 均滿足時，中轉播放器才取消靜音並報告 `casting`，隨後 React Native 暫停本地播放器。

原生模組透過 `AirPlayRelayStateChanged` 傳送快照，透過 `AirPlayRelayProgress` 大約每秒傳送一次進度更新。快照包含 `generation`、狀態、路由和外部播放標誌、進度以及本地恢復標誌。原生非同步操作和 React Native 進度監聽器會檢查 generation，丟棄過期回呼。啟動超時為 12 秒；失敗時報告錯誤，並清理中轉播放器、觀察者和定時器。

覆蓋層的停止投屏操作使用另一個 `AVRoutePickerView`。顯示前呼叫 `beginStopRouteSelection()`，使用者在系統面板中選擇本地輸出。保留外部路由而僅關閉面板，不算停止投屏。路由回到本地後，原生層釋放中轉播放器、恢復 Audio Session，並報告 `idle`；播放器隨後恢復本地播放。

### Android：Google Cast 中轉流程

使用者未連線時點選按鈕，會開啟裝置對話框，並記錄連線後載入媒體的意圖。如果已連線，則直接請求載入媒體。`useCast` 監聽會話啟動、恢復、結束和連線失敗事件，透過 Remote Media Client 訂閱媒體狀態和進度，並在元件卸載時移除監聽器。

載入請求包含 `contentId / contentUrl`、根據 URL 副檔名推斷的 MIME 型別、標題、封面、`startTime` 和 `autoplay: true`。最多嘗試載入 3 次：先立即嘗試，再分別等待 500 和 1200 毫秒後重試。副檔名推斷覆蓋 HLS、DASH 和 WebM，其他情況提交 MP4。MIME 型別推斷並不能確認接收端支援該媒體。

Android 在連線期間暫停本地播放：`EpisodePlayer` 將 `isConnecting || isCasting || isConnected` 傳遞給本地播放器。載入成功或媒體狀態回呼會更新投屏標誌，但僅憑該標誌不能證明電視正在顯示影片。當前載入失敗主要輸出控制檯日誌。如果應用需要向使用者顯示錯誤，或在失敗後自動恢復本地播放，需要補充相應處理。

主動停止時，先抑制自動恢復並清除 UI 狀態，再呼叫 `endCurrentSession(true)`，並在有限範圍內檢查會話是否終止。抑制邏輯會忽略延遲到達的會話恢復和媒體回呼，直到使用者再次主動選擇裝置或啟動投屏。完成有限檢查不等於已經確認接收端停止播放。

### 本地恢復和頁面生命週期

兩個平臺都使用當前快照或遠端進度、儲存的遠端進度以及本地進度中的最大值進行恢復。這種策略傾向於避免向後跳轉，不能保證總是恢復到接收端的精確最終位置。遠端向後拖動等場景需要單獨驗證。恢復時使用現有播放器實例。

* **iOS 恢復**

   對於需要恢復的 `idle` 或 `failed` 快照，播放器先請求恢復 Audio Session，再跳轉本地進度並取消靜音。此播放交接分支僅在 `shouldResumeLocal` 為 true、投屏前本地正在播放且播放器當前已暫停時呼叫播放。獨立的頁面焦點和前景處理邏輯也會恢復播放；如果應用需要嚴格保留使用者的暫停狀態，請一併檢查這些入口。

* **Android 恢復**

   投屏標誌清除後，活動的本地播放器跳轉進度並直接呼叫播放，不會保留投屏前已暫停的意圖。如果應用要求兩個平臺採用相同的暫停恢復策略，需要顯式實現。

頁面使用 `isCasting || isConnected` 顯示全屏投屏覆蓋層、關閉選集和解鎖對話框、禁用列表翻頁，並防止本地播放完成後自動切換下一集。這些 UI 限制基於已連線或投屏狀態，不能據此確認每個連線過渡階段都被鎖定。

僅使用停止投屏操作會保留當前播放頁。iOS 會儲存待執行的導航操作，僅在 `idle` 且 `routeActive` 為 false 後執行。返回操作不會強制改變系統路由，使用者仍需透過停止投屏入口選擇本地輸出。Android 頁面返回按鈕在停止嘗試結束後再執行導航；其他頁面移除事件也會請求停止，並透過退出保護避免對同一會話重複停止。

為防止隱藏頁面恢復播放，iOS 媒體配置和狀態訂閱僅作用於擁有導航焦點的活動播放器。回到前景時的恢復也會檢查導航焦點、活動狀態和投屏暫停條件。頁面失去焦點時，即使尚未收到正在播放的回呼，也會暫停本地播放器。當前背景 AppState 處理邏輯會暫停本地播放器，但不會統一終止遠端會話。

### 參考程式碼和驗證

|檔案 |檢查內容 |
|---|---|
|`hooks/useCast.ts` |跨平臺狀態、Android 會話和媒體請求，以及 iOS 快照對映。 |
|`components/cast/CastButton.tsx`<br><br>`CastActiveOverlay.tsx` |啟動入口、投屏覆蓋層和各平臺的停止入口。 |
|`components/player/VideoPlayer.tsx`<br><br>`EpisodePlayer.tsx` |解析後的 URL、進度、靜音、暫停和本地恢復。 |
|`app/drama_player.tsx` |共享控制器、UI 限制和導航處理。 |
|`ios/videoonern/AirPlayRelay.m`<br><br>`AirPlayRoutePickerViewManager.m` |原生狀態機、Audio Session、中轉播放器和系統選擇器。 |
|`android/app/src/main/java/com/byteplus/videoone/rn/CastOptionsProvider.kt`<br><br>`plugins/withGoogleCast.js` |接收端、通知和原生專案配置。 |

原始碼回歸檢查覆蓋 AirPlay 狀態機、中轉清理和過期回呼、投屏覆蓋層互動，以及頁面焦點恢復。整合後，請在實體手機和目標接收端上驗證以下場景，檢查影片、音訊和進度。狀態標誌和測試通過不能替代接收端測試。

|場景 |驗證內容 |
|---|---|
|開始投屏 |劇集和起始進度正確，接收端顯示影片，交接後本地無殘留音訊。 |
|取消、失敗和網路斷開 |選擇器取消、啟動超時、接收端載入失敗和 URL 過期後的狀態、音訊和恢復操作。 |
|停止和路由變化 |iOS 選擇本地輸出與未改變路由而僅關閉面板的區別；Android 停止後延遲到達的會話恢復回呼。 |
|進度和暫停意圖 |接收端向前和向後拖動、投屏前暫停的行為，以及各平臺恢復策略的影響。 |
|頁面生命週期 |覆蓋層、劇集限制、停止後留在當前頁、待執行導航、前景與背景切換，以及隱藏頁面不發出音訊。 |

## 理解程式碼結構

為高效修改 React Native 短劇 Demo，建議按**頁面 → 元件 → 服務 → 工具**的順序理解專案，先建立頁面級資料流的整體認識，再檢視單個 API 檔案。

### 關鍵目錄

|**目錄** |**用途** |**關注重點** |
|---|---|---|
|`app/` |頁面和路由入口 |理解短劇入口、頻道頁和播放頁之間的關係 |
|`components/player/` |播放器相關元件 |關注播放控制、續播、選集和螢幕方向邏輯 |
|`components/modals/` |解鎖和選集對話框 |關注變現和短劇消費流程 |
|`components/feed/` |內容流和推薦展示元件 |關注推薦卡片和資訊面板適配 |
|`components/drama/` |短劇業務元件 |關注短劇封面、短劇列表和輪播展示 |
|`services/` |服務抽象層 |API 替換的主要入口 |
|`hooks/` |可複用的狀態邏輯 |關注頻道資料獲取和主題相關邏輯 |
|`utils/` |工具和播放器配置 |關注播放器設定、資料轉換和圖片處理 |

### 建議閱讀順序

1. 先閱讀 `app/drama_channel.tsx` 和 `app/drama_player.tsx`，理解路由和互動鏈路。

2. 再閱讀 `services/dramaService.ts`、`unlockService.ts` 和 `userService.ts`，理解頁面資料來源。

3. 隨後閱讀 `components/player/` 和 `components/modals/`，理解播放、選集和解鎖行為。

4. 最後檢視 `hooks/`、`types/` 和 `utils/`，補全對狀態管理、型別定義和工具實現的認識。

## 建議整合檢查清單

* 完成投屏整合，確保 iOS AirPlay 和 Android Chromecast 中轉播放均正常。

* 驗證投屏斷點續播，確保結束投屏後應用內播放器從正確位置恢復。

* 驗證投屏與 PiP 的互斥邏輯，防止同時啟用。

* 在沒有可用投屏裝置或發生網路錯誤時，提供合理的錯誤提示。

* 先跑通官方 Demo，確認播放、許可證和原生環境均正常。

* 定義自己的頻道、短劇、劇集、解鎖狀態和使用者資訊業務 API 模型。

* 在 `services/` 層完成統一的資料對映。

* 在實體裝置上驗證續播、選集、螢幕方向變化和解鎖流程。

* 替換推薦位、運營內容和視覺樣式，以適配品牌。

* 釋出前補充資料分析、監控和生產配置。

## 後續步驟

如果希望快速將 Demo 轉為可投入生產的業務應用，接下來重點完成三件事：確定前後端資料契約並完成服務層對映，定義解鎖流程和使用者權益體系，在實體裝置上反覆驗證滑動切換、續播、解鎖彈窗和推薦銜接。這些部分穩定後，Demo 就具備了演進為實際短劇產品的基礎。

> **说明**

> 建議結合[在 React Native 上構建您的第一個應用](https://docs.byteplus.com/docs/byteplus-vos/docs-running-the-demo-react-native-zh-TW)閱讀本文：該文件介紹如何執行專案，本文介紹如何將短劇能力整合到自己的業務中。

---
title: "取得 SDK 授權"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management-zh-TW"
---

若要在您的應用程式中使用 BytePlus MediaLive SDK，您必須先取得有效授權。此授權會為您的特定應用程式啟用 SDK 功能。本主題將引導您完成整個流程，從在控制台建立 SDK 應用程式，到取得 SDK 整合所需的授權。

> **注意**

> 只有在使用下列 BytePlus MediaLive SDK 時，才需要建立 SDK 應用程式並取得授權：

* > Player SDK for iOS

* > Player SDK for Android

* > Player SDK for React Native

* > Player SDK for Flutter

* > Player SDK for Web（2.11.0 或更新版本）

## 先決條件

* 對於 Android 或 iOS 應用程式，請準備下列資訊：

   * **Android**：您應用程式的套件名稱。您可以在專案 `app` 目錄下的 `build.gradle` 檔案中，找到 `applicationId` 值。

   * **iOS**：您應用程式的 Bundle ID。您可以在 Xcode 中應用程式目標的設定中，找到 `Bundle Identifier` 值。

* 對於 Web 應用程式，請準備下列資訊：

   * **Web**（適用於瀏覽器頁面）：萬用字元網域，例如 `*.example.com`，涵蓋您計劃嵌入播放器的所有頁面。

   * **WebOTT**（Web Over\-The\-Top，適用於在 Tizen 和 webOS 智慧電視系統上執行的 Web 應用程式，僅 Player SDK for Web 2.12.0 及更新版本支援）

      * **Tizen**：您的應用程式識別碼。您可以在專案的 `config.xml` 檔案中，找到 `applicationId` 值。

      * **webOS**：您的應用程式識別碼。您可以在專案的 `appinfo.json` 檔案中，找到 `id` 值。

## 步驟 1：建立或繫結 SDK 應用程式

1. 登入 [BytePlus MediaLive 控制台](https://console.byteplus.com/live)。

2. 在左側導覽窗格中，按一下 **SDK 管理**。

3. 按一下 **建立 SDK 應用程式** 以建立 SDK 應用程式；如果您已在 BytePlus VOD 控制台中建立應用程式，請按一下 **繫結現有應用程式**。

4. 設定基本資訊。

   **Android 或 iOS 應用程式**

對於 Android 或 iOS 應用程式，請完成下列步驟。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a82a7363c8a1444eaef0ea238d643f5c~tplv-goo7wpa0wc-topic.webp)

      * **SDK 類型**：選取 **App** 作為 SDK 類型。此類型的應用程式用於整合用戶端 SDK。

      * **應用程式名稱**：

         * 如果您要建立新應用程式，請輸入唯一名稱。名稱長度必須為 1–128 個字元，可包含字母（A\-Z、a\-z）、數字（0\-9）、中文字元，以及特定特殊字元。

         * 如果您要繫結現有應用程式，請選取應用程式 ID。您可以在 BytePlus VOD 控制台的應用程式清單頁面中找到此 ID。

      * **專案**：選取 SDK 應用程式的專案。這可確保只有具備此專案存取權的子帳戶可管理該應用程式。

      * **PackageName** 和 **Bundle ID**：輸入 Android 應用程式的套件名稱，以及 iOS 應用程式的 Bundle ID。這會將 SDK 授權繫結至您的應用程式，以防止未經授權的使用。如果您的應用程式支援兩個平台，請同時提供兩者；如果只支援單一平台，則只提供一項。

         > **注意**

         > 請確保輸入的 **PackageName** 和 **Bundle ID** 在全域唯一。

   **Web 應用程式**

對於 Web 應用程式，請完成下列步驟。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/87f6bb90aa7f40db931ce4da906f3864~tplv-goo7wpa0wc-topic.webp)

      * **SDK 類型**：選取 **Web** 作為 SDK 類型。此類型的應用程式用於整合 Player SDK for Web。

      * **應用程式名稱**：

         * 如果您要建立新應用程式，請輸入唯一名稱。名稱長度必須為 1–128 個字元，可包含字母（A\-Z、a\-z）、數字（0\-9）、中文字元，以及特定特殊字元。

         * 如果您要繫結現有應用程式，請選取應用程式 ID。您可以在 BytePlus VOD 控制台的應用程式清單頁面中找到此 ID。

      * **專案**：選取 SDK 應用程式的專案。這可確保只有具備此專案存取權的子帳戶可管理該應用程式。

      * **萬用字元網域**：根據您的情境輸入下列資訊。

         * **Web**（適用於瀏覽器頁面）：若要授權播放，請輸入萬用字元網域，涵蓋您計劃嵌入播放器的所有頁面。這可允許播放器在任何相符的一級子網域上執行。

            **範例**：如果您輸入 `*.example.com`：

            * **相符**：`a.example.com`、`b.example.com`

            * **不相符**：`a.b.example.com`（多層級子網域）、`example.com`（根網域）

               **規則**：

            * 此值必須以星號（`*`）開頭，且不得超過 128 個字元。

            * 萬用字元（`*`）必須用於您擁有的網域，且不得用於公用後綴或頂層網域。

               * 正確：`*.example.com`（因為 `example.com` 是您擁有的特定網域）。

               * 不正確：`*.com` 或 `*.com.cn`（因為 `.com` 是頂層網域，而 `.com.cn` 是公用後綴，兩者都不屬於單一實體）。

         * **WebOTT**（適用於在 Tizen 和 webOS 智慧電視系統上執行的 Web 應用程式，僅 Player SDK for Web 2.12.0 及更新版本支援）：輸入您的應用程式識別碼。

         > **注意**

         > 請確保輸入的萬用字元網域或應用程式識別碼在全域唯一。

5. 如果您要建立新應用程式，請按一下 **建立應用程式**。如果您要繫結現有應用程式，請按一下 **下一步**。

6. 設定授權，並將授權繫結至您的 SDK 應用程式。

   > **说明**

   * > 每個授權只能繫結至一個 SDK 應用程式。

   * > SDK 授權的有效期間只有在授權繫結至 SDK 應用程式後才會開始。

   * > 授權用於管理 SDK 及其加值服務的使用權限和期限。若要了解每種授權類型支援的功能，請參閱[用戶端 SDK：SDK 概觀](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-introduction)和 [Player SDK for Web：SDK 概觀](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-web-sdk-overview)。若要了解每種授權類型的價格，請參閱 [SDK 授權](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-licenses)。

   * > 如果您需要整合早於 2.11.0 版本的 Player SDK for Web，則不需要繫結授權。您可以直接取得應用程式 ID 以進行 SDK 整合。不過，建議您將 Player SDK for Web 升級至 2.11.0 或更新版本，以取得更好的功能和服務。

   **試用授權**

試用授權**僅供測試用途**，有效期為**一個月**。例如，在 2026 年 5 月 10 日 10:00 繫結至您應用程式的授權，將於 2026 年 6 月 10 日 10:00 到期。

   請依照下列步驟取得試用授權：

      1. 選取 **Trial** 作為授權類型，然後按一下 **取得授權**。您將被導向至**授權購買**頁面。

         ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/16b9df9aacb04ab6a2c6a76077845250~tplv-goo7wpa0wc-topic.webp)

      2. 在購買頁面上，按一下 **立即取得** 以繼續免費取得授權。

         ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b997614ab172403f8aca0a33415b9cb6~tplv-goo7wpa0wc-topic.webp)

      3. 完成免費授權的結帳流程後，返回設定頁面。選取您剛取得的試用授權，然後按一下 **確認**。

         ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f206935371934e1ab2bd4917df8d9935~tplv-goo7wpa0wc-topic.webp)

         > **说明**

         > 如果新的試用授權未立即顯示在清單中，請按一下重新整理圖示以更新頁面。

         > ![](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3afbc908af9f4304bae35f8dc76b10d9~tplv-goo7wpa0wc-topic.webp)

   在試用授權到期前，或當您準備將應用程式發布至正式環境時，您必須將授權升級為基礎版或進階版。如需詳細資訊，請參閱[將試用授權升級為基礎或進階授權](https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses#777c7de7)。

   **基礎授權**

基礎授權適用於**正式環境**，**有效期為一年**。例如，在 2026 年 5 月 10 日 10:00 繫結的授權，將有效至 2027 年 5 月 10 日 10:00。您可以隨時續訂基礎授權。如需詳細資訊，請參閱[續訂授權](https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses#b2dde14f)。

   若要取得基礎授權，請選取 **Basic** 作為授權類型，並選擇下列其中一種方法：

      * 直接購買

         1. 按一下 **立即購買**。

            ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5bedee922aa84a8184d924132120ef07~tplv-goo7wpa0wc-topic.webp)

         2. 完成購買後，返回設定頁面。從清單中選取基礎授權，然後按一下 **確認**。

            ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3a4ab8a8ff8b4d708dd4876ccf6006f9~tplv-goo7wpa0wc-topic.webp)

            > **说明**

            > 如果您新購買的授權未立即顯示在清單中，請按一下重新整理圖示以更新頁面。

            > ![](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3afbc908af9f4304bae35f8dc76b10d9~tplv-goo7wpa0wc-topic.webp)

      * 繫結流量包：您可以將 100 TB 或更大的直播流量包繫結至應用程式，以取得免費的一年期基礎授權。如需直播流量包的詳細資訊，請參閱[資源包](https://docs.byteplus.com/docs/byteplus-media-live/docs-resource-packs)。

         > **说明**

         > 此方法**僅**適用於 App 類型應用程式。

         * **如果您已有符合資格的流量包**：從清單中選取流量包，然後按一下 **確認**。

         * **如果您沒有符合資格的流量包**：

            1. 按一下 **立即購買** 以購買一個流量包。

               ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aa45000672b94d6eae8a6509bae35357~tplv-goo7wpa0wc-topic.webp)

            2. 完成購買後，返回設定頁面。從清單中選取流量包，然後按一下 **確認**。

               > **说明**

               > 如果您新購買的流量包未立即顯示在清單中，請按一下重新整理圖示以更新頁面。

               > ![](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3afbc908af9f4304bae35f8dc76b10d9~tplv-goo7wpa0wc-topic.webp)

   **進階授權**

進階授權適用於**正式環境**，**有效期為一年**。例如，在 2026 年 5 月 10 日 10:00 繫結的授權，將有效至 2027 年 5 月 10 日 10:00。您可以隨時續訂進階授權。如需詳細資訊，請參閱[續訂授權](https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses#b2dde14f)。

   請依照下列步驟取得進階授權：

      1. 選取 **Premium** 作為授權類型。

      2. 按一下 **立即購買**。

         ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a98e6675afe345348571f5ef165106c8~tplv-goo7wpa0wc-topic.webp)

      3. 完成購買後，返回設定頁面。選取進階授權，然後按一下 **確認**。

         ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/31b655fa42144106a5f1b0836dca473b~tplv-goo7wpa0wc-topic.webp)

         > **说明**

         > 如果您新購買的授權未立即顯示在清單中，請按一下重新整理圖示以更新頁面。

         > ![](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3afbc908af9f4304bae35f8dc76b10d9~tplv-goo7wpa0wc-topic.webp)

7. 您的應用程式現在會顯示在 **SDK 管理**頁面的應用程式清單中。在清單中找到您的應用程式，並找出 **App ID** 和**應用程式名稱**。您需要這兩項資訊來整合及初始化 SDK。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7ac12129476144c8b5a06412796f84e3~tplv-goo7wpa0wc-topic.webp)

## 步驟 2：取得授權

BytePlus MediaLive SDK 必須搭配 SDK 授權使用。您取得的授權僅對已繫結的 SDK 應用程式有效。

在 [SDK 管理](https://console.byteplus.com/live/main/sdk)頁面上，找到目標應用程式。

* 對於 Android 或 iOS 應用程式，按一下下載圖示以下載授權檔案。然後使用授權檔案整合 SDK。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/44a07076e89243e38d48f42a5ad23276~tplv-goo7wpa0wc-topic.webp)

* 對於 Web 應用程式，按一下下載圖示以下載授權檔案，或按一下**詳細資料**以取得用於整合 Player SDK for Web 的授權 URL。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/954db88e8e494a199525032b09044587~tplv-goo7wpa0wc-topic.webp)

> **说明**

> 請確保應用程式狀態為**已啟用**。

* > 如果狀態為**已過期**，您必須先續訂授權。如需詳細資訊，請參閱[續訂授權](https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses#b2dde14f)。

* > 如果狀態為**未啟用**，請按一下**操作**欄中的省略號圖示（...），然後選取**啟用**以設定並繫結授權。如需如何設定並繫結授權的詳細資訊，請參閱[步驟 1：建立或繫結 SDK 應用程式](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management#91608dc8)。

## 相關操作

在 **SDK 管理**頁面上，您可以在**操作**欄中執行下列操作。

* **編輯**：按一下**編輯**以變更應用程式名稱、**PackageName**、**Bundle ID**、萬用字元網域或 WebOTT 應用程式識別碼。

   * 如果授權已啟用，變更後系統會根據更新後的應用程式資訊重新產生授權。您需要取代 SDK 授權檔案或授權 URL。原授權會在一段時間內保持有效，而新授權會保留與原授權相同的到期時間。

   * 如果授權已過期，當您續訂授權時，系統會根據更新後的應用程式資訊產生新授權。續訂完成後，您需要取代 SDK 授權檔案或授權 URL。

* **刪除**：按一下省略號（...）圖示，然後選取**刪除**以永久刪除應用程式。

   > **注意**

   > 如果您不小心刪除應用程式，您可以透過**繫結現有應用程式**復原應用程式，並繼續使用原 App ID。繫結應用程式時，您需要重新設定 **PackageName**、**Bundle ID**、萬用字元網域或 WebOTT 應用程式識別碼。系統不會保留刪除前的設定資訊。如果 SDK 應用程式剛刪除，可能不會立即顯示在**繫結現有應用程式**對話方塊中。在此情況下，請稍後再試。

* **續訂**：當您的授權即將到期或已到期時，按一下**續訂**以續訂授權。如需詳細資訊，請參閱[續訂授權](https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses#b2dde14f)。

* **升級**：按一下**升級**以將試用授權升級為基礎或進階授權。如需詳細資訊，請參閱[將試用授權升級為基礎或進階授權](https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses#777c7de7)。

* **啟用**：如果授權尚未繫結至應用程式，請按一下省略號（...）圖示，然後選取**啟用**以設定並繫結授權。如需如何設定並繫結授權的詳細資訊，請參閱[步驟 1：建立或繫結 SDK 應用程式](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management#91608dc8)。

## 接下來的步驟

使用您從控制台取得的授權檔案、授權 URL、應用程式 ID 和應用程式名稱來整合並初始化 SDK。如需詳細資訊，請參閱：

* iOS：[整合 Player SDK for iOS](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-ios)和[初始化 Player SDK for iOS](https://docs.byteplus.com/docs/byteplus-media-live/docs-initializing-for-ios)

* Android：[整合 Player SDK for Android](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-android)和[初始化 Player SDK for Android](https://docs.byteplus.com/docs/byteplus-media-live/docs-initializing-for-android)

* Flutter：[整合 Player SDK for Flutter](https://docs.byteplus.com/docs/byteplus-media-live/integrating-the-player-sdk-for-flutter)和[初始化 Player SDK for Flutter](https://docs.byteplus.com/docs/byteplus-media-live/initializing-the-player-sdk-for-flutter)

* React Native：[整合 Player SDK for React Native](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-rn)和[初始化 Player SDK for React Native](https://docs.byteplus.com/docs/byteplus-media-live/docs-initializing-for-rn)

* Player SDK for Web：[整合 Player SDK for Web](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-player-sdk-for-web_1)

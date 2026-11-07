---
title: "使用 DRM 加密您的直播串流"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-encrypting-your-live-streams-using-drm-zh-TW"
---

為了防止高價值內容（例如付費活動及專屬直播）遭到未經授權的再分發，業界標準的安全解決方案是數位權利管理（DRM）加密。本主題提供在 BytePlus MediaLive 啟用 DRM 保護的完整流程。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">BytePlus MediaLive 支援以下 DRM 系統：Widevine、FairPlay 和 PlayReady。</div>


<span id="d1baef6b"></span>
## 限制


* BytePlus MediaLive 僅在 HLS（搭配 MPEG\-TS）及 LL\-DASH（搭配 CMAF）提供 DRM 加密的播放地址。

* 建議您使用標準 DRM 播放器於網頁瀏覽器播放 DRM 加密的直播串流。原生 Android 播放器或其他平台的效能可能無法保證。


<span id="7aed754a"></span>
## 流程

流程包含以下步驟：


1. 向您的 DRM 授權供應商取得 DRM 金鑰。

2. 在 BytePlus MediaLive 控制台設定 DRM。

3. 產生經 DRM 加密的播放地址。

4. 為授權用戶解密內容。


<span id="941c05bb"></span>
### 取得 DRM 金鑰

您必須先向 [Intertrust](https://www.expressplay.com/) 取得 DRM 金鑰。如需取得金鑰的詳細操作說明，請參閱 [Acquiring a DRM key](https://docs.byteplus.com/docs/byteplus-media-live/docs-acquiring-a-drm-key)。

若要在 Apple 裝置上啟用加密，亦需取得 FairPlay 憑證。接著，您需要將該憑證上傳至 BytePlus MediaLive 控制台及 Intertrust。如需取得憑證及其他相關資訊的操作說明，請參閱 [Acquiring a FairPlay certificate](https://docs.byteplus.com/docs/byteplus-media-live/docs-acquiring-a-fairplay-certificate)。

<span id="3b790e5c"></span>
### 在 BytePlus MediaLive 控制台設定 DRM


1. 將 DRM 金鑰及 FairPlay 憑證上傳至 BytePlus MediaLive。如需上傳金鑰及憑證的詳細操作說明，請參閱 [Managing DRM licenses](https://docs.byteplus.com/docs/byteplus-media-live/docs-managing-drm-licenses)。

2. 在 BytePlus MediaLive 控制台，為您欲加密的網域名稱及 AppName 設定轉碼任務。詳細資訊請參閱 [Configuring a transcoding task](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-transcoding)。舉例來說，假設您要為 AppName「drm\-test」加密超高畫質（UHD）串流。請依下列方式設定：

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/107f86e4900b4fed9f8f81d50f162adb~tplv-goo7wpa0wc-image.image) </span>

   * **Domain name space**：example.push.com

   * **AppName**：drm\-test

   * **Suffix**：_uhd

3. 為您欲加密的網域名稱及 AppName 設定 DRM 加密。如需詳細操作說明，請參閱 [Configuring a DRM encryption task](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-a-drm-encryption-task)。本範例請依下列方式設定：

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4a1ad5b655e54e6580fe768977e6354d~tplv-goo7wpa0wc-image.image) </span>

   * **Domain name space**：example.push.com

   * **AppName**：drm\-test

   * **Transcoding**：_uhd


<span id="4763a627"></span>
### 產生加密的播放地址

您可以使用地址產生器產生 DRM 加密的播放地址。


1. 前往 [Address Generator](https://console.byteplus.com/live/main/locationGenerate) 並輸入對應資訊：

   * **選擇網域名稱**：example.pull.com。此網域名稱應為與您在前一步輸入的 example.push.com 相關聯的拉流網域名稱。如需這些概念間關係的更多資訊，請參閱 [Domain name space](https://docs.byteplus.com/docs/byteplus-media-live/docs-glossary#Vhost)。

   * **AppName**：drm\-test

   * **StreamName**：請輸入您的串流名稱

   * **Transcoding template**：_uhd

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8e4db9069fee45f18bf37818642db0b7~tplv-goo7wpa0wc-image.image) </span>

2. 點擊 **Generate address**。

3. 找到包含 DRM 標籤的 M3U8 地址。將此地址作為播放地址使用。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c9d4b1f5a5f547d38e86d00745cbf60d~tplv-goo7wpa0wc-image.image) </span>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">其他格式的播放位址不加密。為防止使用者透過這些位址存取直播流，你可以為網域名稱啟用 URL 驗證，或限制使用者僅能存取特定協定。詳情請參閱 <a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-url-authentication">URL 驗證</a> 與 <a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-protocol-restrictions">協定限制</a>。</div>


* <div data-tips="true" data-tips-type="tip">若需 CMAF 格式的播放位址，請<a href="https://console.byteplus.com/workorder/create">聯繫技術支援</a>。</div>



<span id="70daa99f"></span>
### 內容解密

為了讓授權用戶觀看加密的直播串流，播放器需呼叫 BytePlus OpenAPI 以取得 DRM 授權。對於 iOS 用戶，播放器亦需取得 FairPlay 憑證。


* 如需取得 DRM 授權，請呼叫 [DescribeLicenseDRM](https://docs.byteplus.com/docs/byteplus-media-live/docs-describelicensedrm) 端點。

* 如需取得 FairPlay 憑證，請呼叫 [DescribeCertDRM](https://docs.byteplus.com/docs/byteplus-media-live/docs-describecertdrm) 端點。


由於你的 BytePlus AK/SK 無法儲存在用戶端裝置上，你需要先在伺服器端產生 OpenAPI 驗證資訊，然後將該資訊傳遞給用戶端裝置。你可以依照 [簽署 BytePlus MediaLive 請求](https://docs.byteplus.com/docs/byteplus-media-live/docs-signing-byteplus-medialive-requests) 的說明操作，或使用 [Server SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-server-sdk) 來計算簽名。

假設你使用 [Go SDK](https://github.com/byteplus-sdk/byteplus-sdk-golang) 來呼叫 BytePlus MediaLive OpenAPI。請使用以下程式碼產生用戶端用於取得 DRM 授權與 FairPlay 憑證的查詢 URL。


1. 定義參數值。

   ```Go
   var (
     serviceInfo = &ServiceInfo{
      Timeout: 5 * time.Second,
      Host:    "open.byteplusapi.com",
      Header: http.Header{
       "Accept": []string{"application/json"},
      },
      Credentials: Credentials{Region: RegionApSingapore, Service: "live"},
     }
     
     // API endpoints that need to be signed
     apiList = map[string]*ApiInfo{
      "DescribeLicenseDRM": {
       Method: http.MethodPost,
       Path:   "/",
       Query: url.Values{
        "Action":     []string{"DescribeLicenseDRM"},
        "Version":    []string{"2023-01-01"},
        "Vhost":      []string{"drm.test.com"},
        "Domain":     []string{"drmpull.videoarch.com"},
        "App":        []string{"app-drm"},
        "StreamName": []string{"s-drm-1221"},
        "DRMType":    []string{"fp"}, // The DRM encryption type
       },
      },
      "DescribeCertDRM": {
       Method: http.MethodGet,
       Path:   "/",
       Query: url.Values{
        "Action":  []string{"DescribeCertDRM"},
        "Version": []string{"2023-01-01"},
        "Vhost":   []string{"drm.test.com"},
        "App":     []string{"app-drm"},
       },
      },
     }
   )
   ```
   

2. 產生用戶端用於取得 DRM 授權與 FairPlay 憑證的查詢 URL。

   ```Go
   func TestClient_GetSignUrl(t *testing.T) {
     client := NewClient(serviceInfo, apiList)
     client.SetAccessKey("your ak")
     client.SetSecretKey("your sk")
     urlStr, _ := client.GetSignUrl("DescribeLicenseDRM", nil)
     fmt.Println("https://live-gateway-byteplus.byteintlapi.com/drm_api/?" + urlStr)
     urlStr, _ = client.GetSignUrl("DescribeCertDRM", nil)
     fmt.Println("https://live-gateway-byteplus.byteintlapi.com/drm_api/?" + urlStr)
   }
   ```

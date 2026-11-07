---
title: "簽署 BytePlus MediaLive 請求"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-signing-byteplus-medialive-requests-zh-TW"
---

為確保您對 BytePlus MediaLive 的 API 呼叫的安全性與完整性，您必須對您的請求進行簽名。本主題提供詳細的逐步說明，指導您如何手動建立簽名並將其添加至您的 HTTP 或 HTTPS 請求。遵循此流程可驗證您的身份，並防止您的請求在傳輸過程中遭到篡改。

<span id="Background"></span>
## 背景

當您向 BytePlus MediaLive 發送 API 請求時，為了驗證請求者的身份並保護 API 請求在傳輸過程中不被惡意篡改，BytePlus 的簽名機制要求請求者對請求參數計算簽名，然後將簽名與 API 請求一同傳送至 API 伺服器進行驗證。當 BytePlus MediaLive 收到請求時，會使用相同資訊計算簽名，並與您的請求中的簽名進行比對。若值不一致，請求將被拒絕。

<span id="Preparation"></span>
## 準備


1. 註冊 BytePlus 帳戶。如需更多資訊，請參閱[註冊 BytePlus 帳戶](https://docs.byteplus.com/byteplus-platform/docs/signing-up-your-account)。

2. 登入[BytePlus 控制台](https://console.byteplus.com/home)。

3. 點擊頁面右上角的使用者名稱，並選擇**IAM**。

4. 在左側導覽窗格中，點擊**金鑰管理**。

5. 取得 AccessKey ID 與 AccessKey secret，這些用於 API 請求驗證。


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/5ddc848-accesskey.png) </span>

<span id="Process"></span>
## 流程

以下流程說明如何建立已簽名的請求。

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/dac1414-Process.JPEG) </span>

<span id="Procedure"></span>
## 操作步驟

本節以`DescribeLiveDomainLog`為例，說明如何對 BytePlus MediaLive API 請求進行簽名。

`DescribeLiveDomainLog`的原始請求（尚未簽名）如下。

```plain
GET http://open.byteplusapi.com/?Action=DescribeLiveDomainLog&Version=2020-08-01
Host: open.byteplusapi.com
Content-Type: application/x-www-form-urlencoded; charset=utf-8
X-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
X-Date: 20201230T081805Z
```


<span id="Step 1: Create a canonical request"></span>
### Step 1: 建立標準請求

要開始簽名流程，請建立標準格式的請求。這可確保 BytePlus MediaLive 計算的簽名與您計算的簽名一致。若兩者不一致，請求將被拒絕。

以下偽代碼展示如何建立標準請求：

```plain
CanonicalRequest = HTTPRequestMethod + '\n' + CanonicalURI + '\n' + CanonicalQueryString + '\n' + CanonicalHeaders + '\n' + SignedHeaders + '\n' + HexEncode(Hash(RequestPayload))
```


完成以下步驟以建立標準請求：


1. 從 HTTP 請求方法（`HTTPRequestMethod`）開始，例如`GET`與`POST`。在本例中，`DescribeLiveDomainLog`的 HTTP 請求方法為`GET`。

   ```plain
   GET
   ```
   

2. 添加 API 請求的標準 URI（`CanonicalURI`）。標準 URI 是 URI 絕對路徑部分的 URI 編碼版本，位於主機之後、問號（`?`）之前（若有查詢字串參數）。

   根據[RFC 3986](https://tools.ietf.org/html/rfc3986)標準化 URI 路徑，移除多餘與相對路徑部分。若絕對路徑未以斜線（`/`）結尾，請在末尾添加斜線。

   若絕對路徑為空，則使用斜線（`/`）。在本例中，`DescribeLiveDomainLog`的 URI 主機後無任何內容，因此絕對路徑為空，標準 URI 如下：

   ```plain
   /
   ```
   

3. 添加 API 請求的標準查詢字串（`CanonicalQueryString`）。在本例中，`DescribeLiveDomainLog`的查詢字串如下：

   ```plain
   Action=DescribeLiveDomainLog&Version=2020-08-01
   ```
   

   要構建標準查詢字串，請完成以下步驟：

   1. 根據[RFC 3986](https://tools.ietf.org/html/rfc3986)對每個參數名稱與值進行 URL 編碼。

   2. 按 ASCII 順序排列參數名稱。對於同一參數名稱的不同值，請在請求中保留其原始順序。

   3. 將已排序的參數名稱與其值以等號（`=`）連接，並以與號（`&`）將參數對串接為一個字串。

      在此範例中，`DescribeLiveDomainLog` 的標準查詢字串如下。

   ```plain
   Action=DescribeLiveDomainLog&Version=2020-08-01
   ```
   

4. 新增標準標頭（`CanonicalHeaders`）。標準標頭包含已簽名請求中的所有 HTTP 標頭。

   以下偽代碼展示如何新增標準標頭：

   ```plain
   CanonicalHeaders = CanonicalHeadersEntry0 + CanonicalHeadersEntry1 + ... + CanonicalHeadersEntryN
   CanonicalHeadersEntry = Lowercase(HeaderName) + ':' + Trimall(HeaderValue) + '\n'
   ```
   

   說明：

   * `Lowercase`：將所有標頭名稱轉為小寫。

   * `Trimall`：移除標頭值前後的多餘空格。

      **Warning**：必須將小寫標頭名稱按 ASCII 順序排序，並在每個標頭結尾加上換行符號（`\n`）。

      在此範例中，標準標頭如下：

   ```plain
   content-type:application/x-www-form-urlencoded; charset=utf-8\n
   host:open.byteplusapi.com\n
   x-content-sha256:e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855\n
   x-date:20201230T081805Z\n
   ```
   

5. 新增簽名標頭（`SignedHeaders`）。`SignedHeaders` 的值為包含於標準標頭中的標頭清單。透過新增簽名標頭，您可指定請求中哪些標頭會用於簽名流程，以忽略代理伺服器額外新增的標頭。

   若 `host` 與 `x-date` 標頭包含於 HTTP 標頭中，則必須作為簽名標頭納入。

   以下偽代碼展示如何新增簽名標頭：

   ```plain
   SignedHeaders = Lowercase(HeaderName0) + ';' + Lowercase(HeaderName1) + ";" + ... + Lowercase(HeaderNameN)
   ```
   

   將所有標頭名稱轉為小寫，按 ASCII 順序排序，並以分號（`;`）分隔。

   在此範例中，簽名標頭如下：

   ```plain
   content-type;host;x-content-sha256;x-date
   ```
   

6. 使用 SHA256 演算法，針對 HTTP 或 HTTPS 請求主體中的 payload（位元組陣列）建立雜湊值。雜湊後的 payload 必須以小寫十六進位字串表示。

   ```plain
   HashedPayload = HexEncode(Hash(RequestPayload))
   ```
   

   說明：

   * `Hash` 代表 SHA256 演算法。

   * `HexEncode` 代表轉換為小寫字元的十六進位編碼。例如，`HexEncode("z")` 會回傳 `7a`，而非 `7A`。

      GET 與 POST 請求皆有 `RequestPayload`。在此範例中，payload 為空。因此，請以空字串作為雜湊函數的輸入。雜湊後的 payload 為 `e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855`。

7. 要組建標準請求（`CanonicalRequest`），請將步驟 1 至 6 的所有組件合併為單一字串，並於每個組件結尾加上換行符號。

   在此範例中，產生的標準請求如下：

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">在以下範例中，由於<code>CanonicalHeaders</code>必須以換行符（<code>\n</code>）結尾，並與<code>SignedHeaders</code>以另一個換行符（<code>\n</code>）串接，因此連續兩個換行符（<code>\n\n</code>）自然形成一個空行。   </div>
   

   ```plain
   GET
   /
   Action=DescribeLiveDomainLog&Version=2020-08-01
   content-type:application/x-www-form-urlencoded; charset=utf-8
   host:open.byteplusapi.com
   x-content-sha256:e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
   x-date:20201230T081805Z
   
   content-type;host;x-content-sha256;x-date
   e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
   ```
   


<span id="Step 2: Create a string to sign"></span>
### Step 2: 建立簽名字串

簽名字串包含有關您的請求及於 [Step 1: 建立標準請求](/docs/byteplus\-media\-live/docs\-signing\-byteplus\-medialive\-requests\-zh\-TW#Step 1: Create a canonical request) 中建立的標準請求的中繼資料。

以下偽代碼展示如何建立簽名字串：

```plain
StringToSign = Algorithm + '\n' + RequestDate + '\n' + CredentialScope + '\n' + HexEncode(Hash(CanonicalRequest))
```


說明：


* `Algorithm`：簽名演算法。目前僅支援 `HMAC-SHA256`。

* `RequestDate`：API 請求發送時的 UTC 時間，對應請求標頭中的 `X-Date` 值。格式：`YYYYMMDD'T'HHMMSS'Z'` 範例：`20201230T081805Z`

* `CredentialScope`：認證範圍，格式為 `YYYYMMDD/region/service/request`。此處 `YYYYMMDD` 的值必須與 `RequestDate` 中的 `YYYYMMDD` 相同。對於 BytePlus MediaLive，`region` 一律使用 `ap-singapore-1`，`service` 一律使用 `live`。範例：`20201230/ap-singapore-1/live/request`。

* `HexEncode(Hash(CanonicalRequest))`：使用 SHA256 演算法計算於 [Step 1: Create a canonical request](/docs/byteplus\-media\-live/docs\-signing\-byteplus\-medialive\-requests#Step 1: Create a canonical request) 建立的標準請求的雜湊值，並將結果轉為小寫十六進位字串。範例：`ba542a51d36e6c5ba0901612efe1c86c5e6502ce5c842e77975dc7acc2503a1e`


**警告**：請以換行符號（`\n）`分隔欄位。

在此範例中，產生的待簽名字串如下：

```plain
HMAC-SHA256
20201230T081805Z
20201230/ap-singapore-1/live/request
ba542a51d36e6c5ba0901612efe1c86c5e6502ce5c842e77975dc7acc2503a1e
```


<span id="Step 3: Calculate a signing key"></span>
### Step 3: 計算簽名金鑰

在計算簽名之前，您必須根據您的 AccessKey 密鑰計算簽名金鑰。簽名金鑰會根據日期、區域和服務而有所不同，這比您的 AccessKey 密鑰更安全。

請使用您的 AccessKey 密鑰建立一系列基於雜湊的訊息驗證碼（HMAC）。以下偽程式碼展示如何計算簽名金鑰：

```plain
kSecret = *Your AccessKey Secret*
kDate = HMAC(kSecret, Date)
kRegion = HMAC(kDate, Region)
kService = HMAC(kRegion, Service)
kSigning = HMAC(kService, "request")
```


說明：


* `HMAC(key, data)` 代表 HMAC\-SHA256 函數，並以二進位格式回傳輸出。每個雜湊函數的結果會作為下一個函數的 `key`。

* `Date` 的格式為 `YYYYMMDD`，其值與 [Step 2: Create a string to sign](/docs/byteplus\-media\-live/docs\-signing\-byteplus\-medialive\-requests#Step 2: Create a string to sign) 中 `RequestDate` 的 `YYYYMMDD` 相同。

* 請將 `ap-singapore-1` 作為 `Region`，並將 `live` 作為 `Service`。


**注意**：在某些程式語言中，`key` 和 `data` 的順序可能不同。

在此範例中，計算簽名金鑰的輸入如下，`kSecret` 為 `TkdKbE1qSmpOVFJrTUdGbE5ABCDZbUV5Wm1RelpUQXlPR1ExTURsa01qVQ==`。此處的 `kSecret` 僅供示範用途。計算簽名金鑰時請替換為您自己的 AccessKey 密鑰。

```plain
HMAC(HMAC(HMAC(HMAC(kSecret,"20201230"),"ap-singapore-1"),"live"),"request")
```


經過上述 HMAC 雜湊運算後產生的簽名金鑰如下，顯示二進位簽名金鑰中每個位元組的十六進位表示。

```plain
1e952b8ff47aaee5d7cf0b43aa295d6820ef5a0940bfaf59d4623c3d50d41e3
```


<span id="Step 4: Calculate the signature"></span>
### Step 4: 計算簽名值

請將 [Step 3: Calculate a signing key](/docs/byteplus\-media\-live/docs\-signing\-byteplus\-medialive\-requests#Step 3: Calculate a signing key) 中建立的簽名金鑰，以及 [Step 2: Create a string to sign](/docs/byteplus\-media\-live/docs\-signing\-byteplus\-medialive\-requests#Step 2: Create a string to sign) 中建立的待簽名字串作為 HMAC\-SHA256 函數的輸入，然後將二進位值轉換為小寫字元的十六進位表示。

以下偽程式碼展示如何計算簽名值：

```plain
Signature = HexEncode(HMAC(Signingkey, StringToSign))
```


**注意**：在某些程式語言中，`Signingkey` 和 `StringToSign` 的順序可能不同。

在此範例中，產生的簽名值如下：

```plain
11a2e7bb9db7ee7ea2e4d7f3d6989a65dc3bb5feedf3aae50ba1b3313fe0093a
```


<span id="Step 5: Add the signature to the HTTP or HTTPS request"></span>
### Step 5: 將簽名值加入 HTTP 或 HTTPS 請求

計算簽名值後，請透過下列其中一種方式將其加入 HTTP 或 HTTPS 請求中，以驗證該請求：


* HTTP 標頭 `Authorization`

* 查詢字串


<span id="Adding signing information to the Authorization header"></span>
#### 將簽名資訊加入 `Authorization` 標頭

以下偽程式碼展示如何組建 `Authorization` 標頭：

```plain
Authorization: Algorithm Credential={AccessKeyId}/{CredentialScope}, SignedHeaders={SignedHeaders}, Signature={Signature}
```


說明：


* `Algorithm`：簽名演算法 `HMAC-SHA256`。

* `AccessKeyId`：您的 AccessKey ID。如需更多資訊，請參閱[準備工作](https://docs.byteplus.com/docs/byteplus-media-live/docs-signing-byteplus-medialive-requests#Preparation)。

* `CredentialScope`：憑證範圍。如需更多資訊，請參閱 [Step 2: Create a string to sign](/docs/byteplus\-media\-live/docs\-signing\-byteplus\-medialive\-requests#Step 2: Create a string to sign)。

* `SignedHeaders`：已簽名標頭。如需更多資訊，請參閱 [Step 1: Create a canonical request](/docs/byteplus\-media\-live/docs\-signing\-byteplus\-medialive\-requests#Step 1: Create a canonical request)。

* `Signature`：計算後的簽名值，用於向 BytePlus MediaLive 驗證您的身分。如需更多資訊，請參閱 [Step 4: Calculate the signature](/docs/byteplus\-media\-live/docs\-signing\-byteplus\-medialive\-requests#Step 4: Calculate the signature)。


**注意**：`Authorization` 標頭是在計算簽名值後組建的，因此不包含於已簽名標頭中。

在此範例中，`Authorization` 標頭如下：

```plain
Authorization: HMAC-SHA256 Credential=AKAPY2RhYmQzODhhYTg4NGZmNTk3ZGUxODk3ODgzYTA****/20201230/ap-singapore-1/live/request, SignedHeaders=content-type;host;x-content-sha256;x-date, Signature=11a2e7bb9db7ee7ea2e4d7f3d6989a65dc3bb5feedf3aae50ba1b3313fe0093a
```


然後，`DescribeLiveDomainLog` 的已簽名請求如下：

```plain
GET http://open.byteplusapi.com/?Action=DescribeLiveDomainLog&Version=2020-08-01
Authorization: HMAC-SHA256 Credential=AKAPY2RhYmQzODhhYTg4NGZmNTk3ZGUxODk3ODgzYTA****/20201230/ap-singapore-1/live/request, SignedHeaders=content-type;host;x-content-sha256;x-date, Signature=11a2e7bb9db7ee7ea2e4d7f3d6989a65dc3bb5feedf3aae50ba1b3313fe0093a
Host: open.byteplusapi.com
Content-Type: application/x-www-form-urlencoded; charset=utf-8
X-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
X-Date: 20201230T081805Z
```


<span id="Adding signing information to the query string"></span>
#### 將簽名資訊加入查詢字串

以下偽代碼展示如何構建包含簽名資訊的查詢字串，並將其添加至原始查詢字串的末尾：

```plain
X-Algorithm=algorithm&X-Credential=credential&X-Date=date&X-Expires=time&X-SignedHeaders=signedheaders&X-Signature=signature
```


說明：


* `Algorithm`：簽名演算法為`HMAC-SHA256`。

* `Credential` *：* 由您的 AccessKey ID 與憑證範圍組成，即`AccessKeyId/CredentialScope`。如需 AccessKey ID 與憑證範圍的詳細資訊，請參閱[Preparation](https://docs.byteplus.com/docs/byteplus-media-live/docs-signing-byteplus-medialive-requests#Preparation)以及[Step 2: Create a string to sign](/docs/byteplus\-media\-live/docs\-signing\-byteplus\-medialive\-requests#Step 2: Create a string to sign)。

* `X-Date`：API 請求發送時的 UTC 時間。您可在請求中找到該參數值。本範例中，該值為`20201230T081805Z`。

* `X-Expires`：簽名的有效期限。此為選填參數，預設值為 900（單位：秒）。若需設定參數值，建議為安全考量設置較小的值，因為產生的查詢字串包含完成 BytePlus MediaLive 請求所需的全部資訊。

* `SignedHeaders`：簽名標頭。如需詳細資訊，請參閱[Step 1: Create a canonical request](/docs/byteplus\-media\-live/docs\-signing\-byteplus\-medialive\-requests#Step 1: Create a canonical request)。

* `Signature`：計算所得的簽名。簽名可驗證您在 BytePlus MediaLive 的身份。如需詳細資訊，請參閱[Step 4: Calculate the signature](/docs/byteplus\-media\-live/docs\-signing\-byteplus\-medialive\-requests#Step 4: Calculate the signature)。


請使用等號（=）連接參數與其值，並以＆符號（&）分隔各參數值對。根據[RFC 3986](https://tools.ietf.org/html/rfc3986)，對每個參數名稱與值進行 URL 編碼。本範例中，僅需將`Credential`值中的斜線（`/`）轉換為`%2F`，以及`SignedHeaders`值中的分號（`;`）轉換為`%3B`。

本範例中，產生的查詢字串如下：

```plain
Action=DescribeLiveDomainLog&Version=2020-08-01&X-Algorithm=HMAC-SHA256&X-Credential=AKAPY2RhYmQzODhhYTg4NGZmNTk3ZGUxODk3ODgzYTA****%2F20201230%2Fap-singapore-1%2Flive%2Frequest&X-Date=20201230T081805Z&X-Expires=60&X-SignedHeaders=content-type%3Bhost%3Bx-content-sha256%3Bx-date&X-Signature=11a2e7bb9db7ee7ea2e4d7f3d6989a65dc3bb5feedf3aae50ba1b3313fe0093a
```


接著，`DescribeLiveDomainLog`的簽名請求如下：

```plain
GET http://open.byteplusapi.com/?Action=DescribeLiveDomainLog&Version=2020-08-01&X-Algorithm=HMAC-SHA256&X-Credential=AKAPY2RhYmQzODhhYTg4NGZmNTk3ZGUxODk3ODgzYTA****%2F20201230%2Fap-singapore-1%2Flive%2Frequest&X-Date=20201230T081805Z&X-Expires=60&X-SignedHeaders=content-type%3Bhost%3Bx-content-sha256%3Bx-date&X-Signature=11a2e7bb9db7ee7ea2e4d7f3d6989a65dc3bb5feedf3aae50ba1b3313fe0093a
Host: open.byteplusapi.com
Content-Type: application/x-www-form-urlencoded; charset=utf-8
X-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
```


<span id="Additional resources"></span>
## 其他資源

若您能在[here](https://docs.byteplus.com/byteplus-media-live/docs/server-sdk)找到對應程式語言的 SDK，則無需手動完成簽名流程，這些 SDK 會自動處理簽名。

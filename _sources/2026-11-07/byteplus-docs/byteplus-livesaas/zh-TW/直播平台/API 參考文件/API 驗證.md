---
title: "API 驗證"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/api-yan-zheng-zh-TW"
---

要驗證您對 BytePlus Live 的 API 請求，您必須建立有效的簽名，並將其包含於您的 HTTP 或 HTTPS 請求中。本指南提供詳細的逐步流程，用於產生此簽名，確保您的請求能被伺服器成功驗證。

<span id="Background"></span>
## 背景

當您向 BytePlus Live 發送 API 請求時，為了驗證請求者的身份並保護 API 請求在傳輸過程中不被惡意篡改，BytePlus 的簽名機制要求請求者對請求參數計算簽名，然後將簽名與 API 請求一同傳送至 API 伺服器進行驗證。

當 BytePlus Live 收到請求時，會使用相同資訊計算簽名，並與您的請求中的簽名進行比對。若簽名值不一致，請求將被拒絕。

<span id="Preparation"></span>
## 先決條件


* 註冊 BytePlus 帳戶。如需更多資訊，請參閱[註冊 BytePlus 帳戶](https://docs.byteplus.com/en/byteplus-platform/docs/signing-up-your-account)。

* 前往[BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/) \> **使用者檔案** \> **IAM** \> **金鑰管理**，取得 API 請求驗證所需的 AccessKey ID（AK）與 Secret Access Key（SK）。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/c0c5750-Obtain_the_AccessKey_ID_and_AccessKey_secret.JPEG) </span>


<span id="Process"></span>
## 流程

以下流程展示如何建立已簽名的請求。

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/dac1414-Process.JPEG) </span>

<span id="Procedure"></span>
## 操作步驟

本節以`GetActivityAPI`為例，說明如何對 BytePlus Live API 請求進行簽名。

`GetActivityAPI` 在簽名前的原始請求如下。

```Plain
Get http://livesaas.byteplusapi.com/?Action=GetActivityAPI&Version=2020-06-01&ActivityId=1231231231
Host: livesaas.byteplusapi.com
Content-Type: application/x-www-form-urlencoded; charset=utf-8
X-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
X-Date: 20201230T081805Z
```


<span id="Step 1: Create a canonical request"></span>
### Step 1: 建立標準請求

要開始簽名流程，請以標準格式建立請求。這可確保 BytePlus Live 計算的簽名與您計算的簽名一致。若簽名不一致，請求將被拒絕。

以下偽代碼展示如何建立標準請求：

```Plain
CanonicalRequest = HTTPRequestMethod + '\n' + CanonicalURI + '\n' + CanonicalQueryString + '\n' + CanonicalHeaders + '\n' + SignedHeaders + '\n' + HexEncode(Hash(RequestPayload))
```


完成以下步驟以建立標準請求：


1. 從 HTTP 請求方法（`HTTPRequestMethod`）開始，例如 `GET` 和 `POST`。在本例中，`GetActivityAPI` 的 HTTP 請求方法為 `GET`。

   ```Plain
   GET
   ```
   

2. 加入 API 請求的標準 URI（`CanonicalURI`）。標準 URI 是 URI 絕對路徑部分的 URI 編碼版本，位於主機之後、問號（`?`）之前（如有），問號開始的是查詢字串參數。

   根據 [RFC 3986](https://tools.ietf.org/html/rfc3986) 規範標準化 URI 路徑。移除多餘及相對路徑部分。若絕對路徑未以斜線（`/`）結尾，請在末尾加上斜線。

   若絕對路徑為空，則使用斜線（`/`）。在本例中，`GetActivityAPI` 的 URI 主機後無任何內容，因此絕對路徑為空，標準 URI 如下：

   ```Plain
   /
   ```
   

3. 加入 API 請求的標準查詢字串（`CanonicalQueryString`）。在本例中，`GetActivityAPI` 的查詢字串如下：

   ```Plain
   Action=GetActivityAPI&Version=2020-06-01&ActivityId=1231231231
   ```
   

   要構建標準查詢字串，請完成以下步驟：

   1. 根據 [RFC 3986](https://tools.ietf.org/html/rfc3986) 對每個參數名稱和值進行 URL 編碼。

   2. 按 ASCII 順序排列參數名稱。對於同一參數名稱的不同值，請保持請求中的原始順序。

   3. 將排序後的參數名稱及其值以等號（`=`）連接，並用與號（`&`）將參數對串接成一個字串。

      在此範例中，`GetActivityAPI` 的標準查詢字串如下。

   ```Plain
   Action=GetActivityAPI&ActivityId=1231231231&Version=2020-06-01
   ```
   

4. 新增標準標頭（`CanonicalHeaders`），其包含簽名請求中的所有 HTTP 標頭。

   以下偽代碼展示如何新增標準標頭：

   ```Plain
   CanonicalHeaders = CanonicalHeadersEntry0 + CanonicalHeadersEntry1 + ... + CanonicalHeadersEntryN
   CanonicalHeadersEntry = Lowercase(HeaderName) + ':' + Trimall(HeaderValue) + '\n'
   ```
   

   此處，

   * `Lowercase`：將所有標頭名稱轉換為小寫。

   * `Trimall`：移除標頭值前後的多餘空格。

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">您必須將小寫標頭名稱依 ASCII 順序排序，並在每個標頭結尾加上換行符（``   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">）。   </div>
   

   在此範例中，標準標頭如下：

   ```Plain
   content-type:application/x-www-form-urlencoded; charset=utf-8\n
   host:livesaas.byteplusapi.com\n
   x-content-sha256:e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855\n
   x-date:20201230T081805Z\n
   ```
   

5. 新增簽名標頭（`SignedHeaders`）。`SignedHeaders` 的值為包含於標準標頭中的標頭清單。透過新增簽名標頭，可指定請求中哪些標頭參與簽名流程，以忽略代理伺服器新增的額外標頭。

   若 `host` 和 `x-date` 標頭作為 HTTP 標頭包含於請求中，則必須將其納入簽名標頭。

   以下偽代碼展示如何新增簽名標頭：

   ```Plain
   SignedHeaders = Lowercase(HeaderName0) + ';' + Lowercase(HeaderName1) + ";" + ... + Lowercase(HeaderNameN)
   ```
   

   將所有標頭名稱轉換為小寫，依 ASCII 順序排序，並以分號（`;`）分隔。

   在此範例中，簽名標頭如下：

   ```Plain
   content-type;host;x-content-sha256;x-date
   ```
   

6. 使用 SHA256 演算法，從 HTTP 或 HTTPS 請求主體中的位元組陣列（payload）建立雜湊值。雜湊後的 payload 必須以小寫十六進位字串表示。

   ```Plain
   HashedPayload = HexEncode(Hash(RequestPayload))
   ```
   

   此處，

   * `Hash` 代表 SHA256 演算法。

   * `HexEncode` 代表轉換為小寫字元的十六進位編碼。例如，`HexEncode("z")` 回傳值為 `7a`，而非 `7A`。

      GET 與 POST 請求皆有 `RequestPayload`。在此範例中，payload 為空。因此，適合以空字串作為雜湊函式的輸入。雜湊後的 payload 為 `e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855`。

7. 要建構標準請求（`CanonicalRequest`），請將步驟 1 至 6 的所有組件組合為單一字串，每個組件以換行字元結尾。

   在此範例中，產生的標準請求如下：

   ```Plain
   GET
   /
   Action=GetActivityAPI&ActivityId=1231231231&Version=2020-06-01
   content-type:application/x-www-form-urlencoded; charset=utf-8
   host:livesaas.byteplusapi.com
   x-content-sha256:e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
   x-date:20201230T081805Z
   
   content-type;host;x-content-sha256;x-date
   e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
   ```
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">標準標頭與簽名標頭之間必須始終保留一個額外的空行。   </div>
   

<span id="Step 2: Create a string to sign"></span>
### Step 2: 建立簽名字串

簽名字串包含您的請求的中繼資訊，以及在 **Step 1: Create a canonical request** 建立的標準請求。

以下偽代碼展示如何建立簽名字串：

```Plain
StringToSign = Algorithm + '\n' + RequestDate + '\n' + CredentialScope + '\n' + HexEncode(Hash(CanonicalRequest))
```


此處，


* `Algorithm`：簽名演算法。目前僅支援 `HMAC-SHA256`。

* `RequestDate`：API 請求發送時的 UTC 時間，即請求標頭中的 `X-Date` 值。格式：`YYYYMMDD'T'HHMMSS'Z'`。範例：`20201230T081805Z`。

* `CredentialScope`：憑證範圍，格式為 `{YYYYMMDD}/{region}/{service}/request`。在此情況下，`YYYYMMDD` 的值必須與 `RequestDate` 中的 `YYYYMMDD` 相同。對於 BytePlus Live，`region` 一律使用 `ap-singapore-1`，`service` 一律使用 `livesaas`。範例：`20201230/ap-singapore-1/livesaas/request`。

* `HexEncode(Hash(CanonicalRequest))`：使用 SHA256 演算法計算在 **Step 1: Create a canonical request** 建立的標準請求雜湊值。然後，將結果轉換為小寫十六進位字串。範例：`ba542a51d36e6c5ba0901612efe1c86c5e6502ce5c842e77975dc7acc2503a1e`。


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">請以換行符（``</div>


<div data-tips="true" data-tips-type="warning"><code>)</code>分隔各欄位。</div>


在此範例中，產生的簽名字串如下：

```Plain
HMAC-SHA256
20201230T081805Z
20201230/ap-singapore-1/livesaas/request
ba542a51d36e6c5ba0901612efe1c86c5e6502ce5c842e77975dc7acc2503a1e
```


<span id="Step 3: Calculate a signing key"></span>
### Step 3: 計算簽名金鑰

在計算簽名之前，必須先根據您的 Secret Access Key 計算簽名金鑰。簽名金鑰是根據日期、區域和服務專屬生成的，這比你的密鑰存取金鑰更為安全。

使用你的密鑰存取金鑰來建立一系列基於雜湊的訊息驗證碼（HMACs）。以下偽代碼展示如何計算簽名金鑰：

```Plain
kSecret = *Your Secret Access Key*
kDate = HMAC(kSecret, Date)
kRegion = HMAC(kDate, Region)
kService = HMAC(kRegion, Service)
kSigning = HMAC(kService, "request")
```


此處，


* `HMAC(key, data)` 代表一個 HMAC\-SHA256 函數，該函數以二進位格式返回輸出。每個雜湊函數的結果都作為下一個的 `key`。

* `Date` 的格式為 `YYYYMMDD`，其值與 `RequestDate` 中 `YYYYMMDD` 的值相同，該 `RequestDate` 用於 **Step 2: Create a string to sign**。

* 請使用 `ap-singapore-1` 作為 `Region`，以及 `livesaas` 作為 `Service`。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">在某些程式語言中，<code>key</code> 與 <code>data</code> 的順序可能不同。</div>


在本範例中，用於計算簽名金鑰的輸入如下所示。`kSecret` 為 `TkdKbE1qSmpOVFJrTUdGbE5ABCDZbUV5Wm1RelpUQXlPR1ExTURsa01qVQ==`，僅供示範用途。實際計算簽名金鑰時，請替換為你自己的密鑰存取金鑰。

```Plain
HMAC(HMAC(HMAC(HMAC(kSecret,"20201230"),"ap-singapore-1"),"livesaas"),"request")
```


經過上述 HMAC 雜湊運算後產生的簽名金鑰如下所示。注意，這裡顯示的是二進位簽名金鑰中每個位元組的十六進位表示。

```Plain
1e952b8ff47aaee5d7cf0b43aa295d6820ef5a0940bfaf59d4623c3d50d41e3
```


<span id="Step 4: Calculate the signature"></span>
### Step 4: Calculate the signature

使用前述於 **Step 3: Calculate a signing key** 產生的簽名金鑰，以及於 **Step 2: Create a string to sign** 產生的待簽名字串作為 HMAC\-SHA256 函數的輸入，然後將二進位值轉換為小寫字元的十六進位表示。

以下偽代碼展示如何計算簽名：

```Plain
Signature = HexEncode(HMAC(Signingkey, StringToSign))
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">在某些程式語言中，<code>Signingkey</code> 與 <code>StringToSign</code> 的順序可能不同。</div>


在本範例中，產生的簽名如下：

```Plain
11a2e7bb9db7ee7ea2e4d7f3d6989a65dc3bb5feedf3aae50ba1b3313fe0093a
```


<span id="Step 5: Add the signature to the HTTP or HTTPS request"></span>
### Step 5: Add the signature to the HTTP or HTTPS request

計算簽名後，請透過以下任一方式將其加入 HTTP 或 HTTPS 請求中，以驗證請求的發送者：


* HTTP 標頭 `Authorization`。

* 查詢字串。


<span id="Adding signing information to the Authorization header"></span>
#### 將簽名資訊加入 `Authorization` 標頭

以下偽代碼展示如何構建 `Authorization` 標頭：

```Plain
Authorization: Algorithm Credential={AccessKeyId}/{CredentialScope}, SignedHeaders={SignedHeaders}, Signature={Signature}
```


此處，


* `Algorithm`：簽名演算法 `HMAC-SHA256`。

* `AccessKeyId`：你的 AccessKey ID。如需更多資訊，請參閱 **Prerequisites**。

* `CredentialScope`：憑證範圍。如需更多資訊，請參閱 **Step 2: Create a string to sign**。

* `SignedHeaders`：已簽名標頭。如需更多資訊，請參閱 **Step 1: Create a canonical request**。

* `Signature`：計算所得的簽名。該簽名可向 BytePlus Live 驗證你的身份。如需更多資訊，請參閱 **Step 4: Calculate the signature**。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>Authorization</code> 標頭是在計算簽名後才建立，因此不包含於已簽名標頭中。</div>


在本範例中，`Authorization` 標頭如下：

```Plain
Authorization: HMAC-SHA256 Credential=AKAPY2RhYmQzODhhYTg4NGZmNTk3ZGUxODk3ODgzYTA****/20201230/ap-singapore-1/livesaas/request, SignedHeaders=content-type;host;x-content-sha256;x-date, Signature=11a2e7bb9db7ee7ea2e4d7f3d6989a65dc3bb5feedf3aae50ba1b3313fe0093a
```


然後，`GetActivityAPI` 的已簽名請求如下：

```Plain
Get http://livesaas.byteplusapi.com/?Action=GetActivityAPI&Version=2020-06-01&ActivityId=1231231231
Authorization: HMAC-SHA256 Credential=AKAPY2RhYmQzODhhYTg4NGZmNTk3ZGUxODk3ODgzYTA****/20201230/ap-singapore-1/livesaas/request, SignedHeaders=content-type;host;x-content-sha256;x-date, Signature=11a2e7bb9db7ee7ea2e4d7f3d6989a65dc3bb5feedf3aae50ba1b3313fe0093a
Host: livesaas.byteplusapi.com
Content-Type: application/x-www-form-urlencoded; charset=utf-8
X-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
X-Date: 20201230T081805Z
```


<span id="Adding signing information to the query string"></span>
#### 將簽名資訊加入查詢字串

以下偽代碼展示如何構建包含簽名資訊的查詢字串，然後將其加到原始查詢字串的末尾：

```Plain
X-Algorithm=algorithm&X-Credential=credential&X-Date=date&X-Expires=time&X-SignedHeaders=signedheaders&X-Signature=signature
```


此處，


* `Algorithm`：簽名演算法 `HMAC-SHA256`。

* Credential：你的 AccessKey ID 與憑證範圍的組合，格式為 `AccessKeyId/CredentialScope`。如需 AccessKey ID 和憑證範圍的更多資訊，請參閱 Prerequisites 和 Step 2: Create a string to sign。

* `X-Date`：API 請求發送時的 UTC 時間。你可以在請求中找到該參數值。在本範例中，該值為 `20201230T081805Z`。

* X\-Expires：簽名的有效期限（秒）。這是一個可選參數，預設值為900。若要設定參數值，建議選擇較小的數值以確保安全，因為產生的查詢字串包含成功呼叫 BytePlus Live 所需的全部資訊。

* `SignedHeaders`：已簽名的標頭。如需更多資訊，請參閱**Step 1: Create a canonical request**。

* `Signature`：計算出的簽名。簽名可確認您在 BytePlus Live 的身份。如需更多資訊，請參閱**Step 4: Calculate the signature**。


請使用等號（=）連接參數與其值，並以＆符號（&）分隔參數值對。請依 RFC 3986 對每個參數名稱與值進行 URL 編碼。在此範例中，您必須將 Credential 值（AccessKeyId/CredentialScope）中的斜線（/）編碼為 %2F，並將 SignedHeaders 值中的分號（;）編碼為 %3B。

在此範例中，產生的查詢字串如下：

```Plain
Action=GetActivityAPI&Version=2020-06-01&ActivityId=1231231231&X-Algorithm=HMAC-SHA256&X-Credential=AKAPY2RhYmQzODhhYTg4NGZmNTk3ZGUxODk3ODgzYTA****%2F20201230%2Fap-singapore-1%2Flivesaas%2Frequest&X-Date=20201230T081805Z&X-Expires=60&X-SignedHeaders=content-type%3Bhost%3Bx-content-sha256%3Bx-date&X-Signature=11a2e7bb9db7ee7ea2e4d7f3d6989a65dc3bb5feedf3aae50ba1b3313fe0093a
```


接著，`GetActivityAPI` 的簽名請求如下：

```Plain
Get http://livesaas.byteplusapi.com/?Action=GetActivityAPI&Version=2020-06-01&ActivityId=1231231231&X-Algorithm=HMAC-SHA256&X-Credential=AKAPY2RhYmQzODhhYTg4NGZmNTk3ZGUxODk3ODgzYTA****%2F20201230%2Fap-singapore-1%2Flivesaas%2Frequest&X-Date=20201230T081805Z&X-Expires=60&X-SignedHeaders=content-type%3Bhost%3Bx-content-sha256%3Bx-date&X-Signature=11a2e7bb9db7ee7ea2e4d7f3d6989a65dc3bb5feedf3aae50ba1b3313fe0093a
Host: livesaas.byteplusapi.com
Content-Type: application/x-www-form-urlencoded; charset=utf-8
X-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
```

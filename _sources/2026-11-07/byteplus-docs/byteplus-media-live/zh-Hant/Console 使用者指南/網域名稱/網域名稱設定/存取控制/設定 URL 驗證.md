---
title: "設定 URL 驗證"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-url-authentication-zh-TW"
---

為了防止直播流資源遭到未經授權的使用，您可以啟用 URL 驗證。此功能會將驗證參數新增至您的推流與拉流地址，確保僅有經驗證的請求能夠被服務。本主題說明驗證流程，並提供透過 BytePlus MediaLive 控制台設定 A 型、B 型與 C 型 URL 驗證的逐步操作指引。

<span id="4ef0cf9e"></span>
# 適用範圍

URL 驗證適用於推流與拉流的網域名稱。


* 為推流網域名稱設定 URL 驗證：控制哪些 URL 能夠推送串流，以防止未經授權的推流並保護您的內容來源。目前僅能為推流網域名稱設定 B 型 URL 驗證。

* 為拉流網域名稱設定 URL 驗證：控制哪些 URL 能夠拉取串流，確保觀眾僅能透過特定 URL 觀看。拉流網域名稱可設定 A 型、B 型與 C 型 URL 驗證。


<span id="882ce378"></span>
# 前置條件

您已新增網域名稱。如需更多資訊，請參閱 [新增網域名稱](https://docs.byteplus.com/docs/byteplus-media-live/docs-domain-zh-TW)。

<span id="f9dd2d8d"></span>
# URL 驗證流程

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ebd6ea56ff424d2e8dc7334085832fd5~tplv-goo7wpa0wc-image.image) </span>


1. 您的伺服器會產生驗證 URL 並提供給使用者。

2. 使用者利用驗證 URL 向 BytePlus MediaLive 伺服器發送推流或拉流請求。

3. BytePlus MediaLive 伺服器會驗證 URL 中的驗證參數，並與請求中的參數比對，以判斷請求是否有效。

   * 若請求有效，BytePlus MediaLive 伺服器會回應，允許使用者成功推流或拉流。

   * 若請求無效，伺服器會回傳 403 錯誤並拒絕該請求。這可防止使用者推流或拉流，並保護直播流資源。


<span id="e7e3f739"></span>
# 操作流程


1. 登入 [BytePlus MediaLive 控制台](https://console.byteplus.com/live)。

2. 在左側導覽列中，點選 **網域名稱**。

3. 於 **網域名稱**頁面，找到需設定推流或拉流的網域名稱，並於**操作**欄點選**設定**，進入網域設定頁面。

4. 點選 **存取控制**分頁。

5. 開啟 **URL 驗證**開關，或於**URL 驗證**區域點選**編輯**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b89826da54b947279e3aa61e56ecab5e~tplv-goo7wpa0wc-image.image) </span>

6. 在出現的 **編輯 URL 驗證**對話框中，根據您的業務需求選擇以下任一驗證類型，並完成相關設定。

   * [A 型 URL 驗證](https://docs.byteplus.com/docs/byteplus-media-live/docs-url-authentication-zh-TW#1747184f)

   * [B 型 URL 驗證](https://docs.byteplus.com/docs/byteplus-media-live/docs-url-authentication-zh-TW#1c5d686d)

   * [C 型 URL 驗證](https://docs.byteplus.com/docs/byteplus-media-live/docs-url-authentication-zh-TW#a4f520fc)

      所有這些驗證類型皆採用 MD5 加密演算法。

      完成 URL 驗證設定約 5 分鐘後，使用者僅能透過驗證後的 URL 推流或拉流；原始 URL 將無法再使用。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">預設情況下，推流網域名稱已啟用 URL 驗證。   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">目前，推流網域名稱僅支援 B 型 URL 驗證。   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">若上述驗證類型無法滿足您的業務需求，請<a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980">提交工單</a>聯絡技術支援，完成自訂 URL 驗證的設定。   </div>
   

7. 取得驗證 URL。

   您可以依照各驗證類型的指引手動組建驗證 URL，或依下列步驟使用地址產生器。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">對於已配置自訂 URL 驗證的網域名稱，若需取得驗證 URL，您可依據自訂驗證規則自行拼接 URL，或<a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980">提交工單</a>聯絡技術支援。   </div>
   

   1. 在左側導覽列中，點選 **地址產生器**。

   2. 選擇 **推流地址**或**拉流地址**。

   3. 選擇網域名稱，並設定 **AppName**、**StreamName**及有效期限。如需更多資訊，請參閱 [Generating stream addresses](https://docs.byteplus.com/docs/byteplus-media-live/docs-address-generator)。

   4. 點選 **產生推流地址**或**產生拉流地址**。

   5. 於頁面右側取得驗證 URL。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b484ff0075ff494d885701d5665904fe~tplv-goo7wpa0wc-image.image) </span>


<span id="1747184f"></span>
## A 型 URL 驗證

<span id="8f01aaf5"></span>
### 運作方式

驗證 URL 格式：

```Plain
OriginalURL?auth_key={timestamp}-{rand}-{uid}-{md5hash}
```



|欄位 |說明 |範例值 |
|---|---|---|
|auth_key |簽名參數的名稱。您可在控制台的 **編輯 URL 驗證**對話框中設定名稱。 |`auth_key` |
|timestamp |Unix 時間戳，單位為秒。支援十進位或十六進位，且您必須在控制台的 **編輯 URL 驗證**對話框中選擇相同的時間格式。<br><br>此欄位需與控制台 **編輯 URL 驗證**對話框中設定的有效期搭配使用，以計算實際的簽名失效時間。簽名失效後，使用者將無法透過驗證 URL 拉流。<br><br>簽名失效時間 = `timestamp` + 有效期。例如，若 `timestamp` 的值為 `1758296819`（2025\-09\-19 23:46:59），有效期為 600 秒，則簽名失效時間為 `1758297419`（2025\-09\-19 23:56:59）。 |`1758296819` |
|rand |隨機數。您可使用 UUID（通用唯一識別碼）格式，且此欄位不得包含連字號（\-）。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">當您在控制台使用地址生成器生成認證 URL 時，此欄位的值始終設為 <code>0</code>。</div><br> |`123e4567` |
|uid |使用者 ID。保留參數，目前尚未使用。請將值設為 `0`。 |`0` |
|md5hash |使用 MD5 加密演算法計算所得的 32 字元小寫字串。<br><br>計算公式如下。<br><br>```Plain```<br>```sstring = "{URI}-{timestamp}-{rand}-{uid}-{key}"```<br>```md5hash = md5sum(sstring)```<br><br><br><br>* `URI`：原始 URL 的路徑部分，從網域名稱之後開始。例如，若原始 URL 為 `http://pull.example.com/live/test.flv`，則 URI 值為 `/live/test.flv`。<br><br>* `key`：主金鑰或備用金鑰，可在控制台的**Edit URL authentication**對話框中進行設定。例如，`123abc`。<br><br><br>在此範例中，`{URI}-{timestamp}-{rand}-{uid}-{key}`的值為`/live/test.flv-1758296819-123e4567-0-123abc`。將此值產生 MD5 雜湊後，會得到一個 32 字元的小寫字串，`md5hash`的值為`fbe5e26c0b7abe1431c3c897f7bdc278`。 |`fbe5e26c0b7abe1431c3c897f7bdc278` |


驗證 URL 範例：

```Plain
http://pull.example.com/live/test.flv?auth_key=1758296819-123e4567-0-fbe5e26c0b7abe1431c3c897f7bdc278
```


<span id="7cb9e341"></span>
### 驗證流程


1. 當 BytePlus MediaLive 伺服器收到用戶的驗證 URL 請求後，會對 `{URI}-{timestamp}-{rand}-{uid}-{key}` 的值進行 MD5 雜湊，生成一個 32 字元的小寫字串。在本範例中，最終生成的字串為 `fbe5e26c0b7abe1431c3c897f7bdc278`。

2. BytePlus MediaLive 伺服器會驗證驗證 URL 中的驗證參數。同時滿足以下兩項檢查時，驗證通過。

   * 判斷伺服器計算出的簽名值是否與請求中的簽名值一致。若一致，則驗證通過。在本主題範例中，簽名值為 `auth_key=1758296819-123e4567-0-fbe5e26c0b7abe1431c3c897f7bdc278`。

   * 判斷簽名是否有效。伺服器會將當前時間與簽名失效時間（`timestamp` + 有效期）進行比較。若簽名失效時間晚於當前時間，則認為簽名有效，驗證通過。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">對於用於拉取長時間串流的 RTMP 和 FLV 等協議，當使用者發起拉流請求時，BytePlus MediaLive 伺服器會驗證驗證參數。驗證通過後，使用者可持續拉流，不會受到簽名失效時間的影響。因此，只要請求是在簽名失效前發起，拉流過程將不會因簽名失效而中斷。只有新發起的拉流請求會因簽名失效而失敗。   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">HLS 協議用於分段影片播放，使用者會持續發起新的拉流請求以取得影片分段。每次使用者發起拉流請求時，BytePlus MediaLive 伺服器都會驗證驗證參數。因此，一旦簽名失效，請求將被拒絕，導致播放中斷。由於直播播放時會頻繁請求新分段，建議您設定較長的簽名失效時間，以避免直播期間播放失敗。   </div>
   

3. 根據驗證結果判斷請求是否有效。

   * 驗證通過：請求有效，伺服器回應請求。用戶可成功拉流。

   * 驗證失敗：請求無效。返回 403 錯誤，請求被拒絕。用戶無法拉流，從而保護直播流資源。


<span id="8ad6a89e"></span>
### 主控台設定

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/18d57f989cc14a7cb9a4f454b6bee9b7~tplv-goo7wpa0wc-image.image) </span>


|設定項目 |說明 |
|---|---|
|主金鑰 |主金鑰。<br><br>值必須為 1\-100 字元，可包含數字（0–9）、小寫字母（a–z）及大寫字母（A–Z）。<br><br>您也可以點擊文字框右側的圖示，隨機生成一組包含數字、小寫及大寫字母的 24 字元金鑰。 |
|備用金鑰 |備用金鑰，用於無縫更新主金鑰。<br><br>值必須為 1\-100 字元，可包含數字（0–9）、小寫字母（a–z）及大寫字母（A–Z）。<br><br>您也可以點擊文字框右側的圖示，隨機生成一組包含數字、小寫及大寫字母的 24 字元金鑰。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">為避免在更換主鍵時造成線上服務中斷，可使用備用金鑰生成驗證 URL，以實現平滑過渡。在過渡期間，可將驗證 URL 替換為由備用金鑰生成的版本。主鍵更換後，請逐步將驗證 URL 替換為由新主鍵生成的版本。</div><br> |
|簽名參數 |簽名參數的名稱。預設值為`auth_key`。<br><br>值必須為 1\-100 字元，可包含：<br><br><br>* 數字（0\-9）<br><br>* 小寫字母（a\-z）<br><br>* 大寫字母（A\-Z）<br><br>* 底線（_）<br><br>* 連字號（\-）<br><br>* 點（.）<br><br>* 逗號（,）<br><br>* 驚嘆號（!）<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">值必須包含至少一個字母。</div><br> |
|有效期間 |簽名的有效期間。單位：秒。預設值為`600`。取值範圍：[0, 2592000]。<br><br>此參數需與驗證 URL 中的`timestamp`參數搭配使用，可用於計算實際簽名失效時間。簽名失效後，使用者將無法透過驗證過的 URL 拉流。<br><br>簽名失效時間 = `timestamp` + 有效期間。例如，若`timestamp`的值為`1758296819`（2025\-09\-19 23:46:59），有效期間為 600 秒，則簽名失效時間為`1758297419`（2025\-09\-19 23:56:59）。 |
|時間戳基準 |`timestamp`的時間格式。預設值為**Decimal**。有效值：<br><br><br>* **Decimal**<br><br>* **Hexadecimal** |


<span id="1c5d686d"></span>
## B 型 URL 驗證

<span id="28f7c6dd"></span>
### 運作原理

驗證 URL 格式：

```Plain
OriginalURL?sign=md5(/{AppName}/{StreamName}{key}{timestamp})&expire=timestamp
```



|欄位 |說明 |範例值 |
|---|---|---|
|sign |簽名參數的名稱。你可以在控制台的**Edit URL authentication**對話框中配置名稱。 |`sign` |
|AppName |直播流地址中`AppName`欄位的值。<br><br>該值必須為1至30個字元，且可包含：<br><br><br>* 數字（0\-9）<br><br>* 小寫字母（a\-z）<br><br>* 大寫字母（A\-Z）<br><br>* 底線（_）<br><br>* 連字號（\-）<br><br>* 點（.）<br><br><br>例如，若原始URL為`http://pull.example.com/live/test.flv`，則`AppName`的值為`live`。 |`live` |
|StreamName |直播流地址中`StreamName`欄位的值。<br><br>該值必須為1至100個字元，且可包含：<br><br><br>* 數字（0\-9）<br><br>* 小寫字母（a\-z）<br><br>* 大寫字母（A\-Z）<br><br>* 底線（_）<br><br>* 連字號（\-）<br><br><br>例如，若原始URL為`http://pull.example.com/live/test.flv`，則`StreamName`的值為`test`。 |`test` |
|key |主金鑰或備用金鑰，可在控制台的**Edit URL authentication**對話框中配置。 |`123abc` |
|timestamp |Unix時間戳，單位為秒。支援十進位或十六進位，且必須在控制台的**Edit URL authentication**對話框中選擇相同的時間格式。<br><br>此欄位需與在控制台**Edit URL authentication**對話框中配置的有效期搭配使用，以計算實際的簽名失效時間。簽名失效後，使用者將無法透過已驗證的URL推流或拉流。<br><br>簽名失效時間 = `timestamp` + 有效期。例如，若`timestamp`的值為`1758296819`（2025\-09\-19 23:46:59），有效期為600秒，則簽名失效時間為`1758297419`（2025\-09\-19 23:56:59）。 |`1758296819` |
|expire |時間戳參數的名稱。你可以在控制台的**Edit URL authentication**對話框中配置名稱。 |`expire` |


根據 `md5(/{AppName}/{StreamName}{key}{timestamp})` 計算簽名值。在本主題範例中，`/{AppName}/{StreamName}{key}{timestamp}` 的值為 `/live/test123abc1758296819`。對該值進行 MD5 雜湊，生成一個 32 字元的小寫字串，結果為 `1e2ea5d60de5adcf5e4b7688ccd76915`。

驗證 URL 範例：

```Plain
http://pull.example.com/live/test.flv?sign=1e2ea5d60de5adcf5e4b7688ccd76915&expire=1758296819
```


<span id="a83c35b7"></span>
### 驗證流程


1. 當 BytePlus MediaLive 伺服器收到用戶的驗證 URL 請求後，會對 `/{AppName}/{StreamName}{key}{timestamp}` 的值進行 MD5 雜湊，生成一個 32 字元的小寫字串。在本主題範例中，最終生成的字串為 `1e2ea5d60de5adcf5e4b7688ccd76915`。

2. BytePlus MediaLive 伺服器會驗證驗證 URL 中的驗證參數。同時滿足以下兩項檢查時，驗證通過。

   * 判斷伺服器計算出的簽名值是否與請求中的簽名值一致。若一致，則驗證通過。在本主題範例中，簽名值為 `sign=1e2ea5d60de5adcf5e4b7688ccd76915& expire=175829681 9`。

   * 判斷簽名是否有效。伺服器會將當前時間與簽名失效時間（`timestamp` + 有效期）進行比較。若簽名失效時間晚於當前時間，則認為簽名有效，驗證通過。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">對於如RTMP和FLV等用於推流或拉流長時間流的協議，當使用者發起推流或拉流請求時，BytePlus MediaLive伺服器會驗證認證參數。驗證通過後，使用者可持續推流或拉流，不受簽名失效時間影響。因此，只要請求是在簽名失效前發起，推流或拉流將不會因簽名失效而中斷。只有新發起的推流或拉流請求會因簽名失效而失敗。   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">HLS協議用於分段影片播放，使用者會持續發起新的拉流請求以取得影片分段。每次使用者發起拉流請求時，BytePlus MediaLive伺服器都會驗證認證參數。因此，一旦簽名失效，請求將被拒絕，導致播放中斷。由於直播播放過程中會頻繁請求新分段，建議你設定較長的簽名失效時間，以避免直播期間播放失敗。   </div>
   

3. 根據驗證結果判斷請求是否有效。

   * 驗證通過：請求有效，伺服器回應請求。用戶可成功推流或拉流。

   * 驗證失敗：請求無效。返回 403 錯誤，請求被拒絕。用戶無法推流或拉流，從而保護直播流資源。


<span id="3f8e2d6e"></span>
### 主控台設定

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d6fd24ca2a51482a9de27eacf1ace271~tplv-goo7wpa0wc-image.image) </span>


|配置項 |說明 |
|---|---|
|主金鑰 |主金鑰。<br><br>該值必須為1至100個字元，且可包含數字（0–9）、小寫字母（a–z）及大寫字母（A–Z）。<br><br>你也可以點擊文字框右側的圖示，隨機生成包含數字、小寫及大寫字母的24字元金鑰。 |
|備用金鑰 |備用金鑰，用於無縫更新主金鑰。<br><br>值必須為 1\-100 個字元，且可包含數字（0–9）、小寫字母（a–z）及大寫字母（A–Z）。<br><br>您也可以點擊文字框右側的圖示，隨機生成包含數字、小寫字母及大寫字母的 24 字元金鑰。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">為避免在更換主鍵時造成線上服務中斷，可使用備用金鑰生成驗證 URL，以實現平滑過渡。在過渡期間，可將驗證 URL 替換為由備用金鑰生成的版本。主鍵更換後，請逐步將驗證 URL 替換為由新主鍵生成的版本。</div><br> |
|簽名參數 |簽名參數的名稱。預設值為 `sign`。<br><br>值必須為 1\-100 個字元，且可包含：<br><br><br>* 數字（0\-9）<br><br>* 小寫字母（a\-z）<br><br>* 大寫字母（A\-Z）<br><br>* 底線（_）<br><br>* 連字號（\-）<br><br>* 點（.）<br><br>* 逗號（,）<br><br>* 驚嘆號（!）<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">值必須包含至少一個字母。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">signature 參數與 timestamp 參數不可使用相同名稱。</div><br> |
|時間戳參數 |時間戳參數的名稱。預設值為 `expire`。<br><br>值必須為 1\-100 個字元，且可包含：<br><br><br>* 數字（0\-9）<br><br>* 小寫字母（a\-z）<br><br>* 大寫字母（A\-Z）<br><br>* 底線（_）<br><br>* 連字號（\-）<br><br>* 點（.）<br><br>* 逗號（,）<br><br>* 驚嘆號（!）<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">值必須包含至少一個字母。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">signature 參數與 timestamp 參數不可使用相同名稱。</div><br> |
|有效期 |簽名的有效期。單位：秒。預設值為 `600`。值範圍：[0, 2592000]。<br><br>此參數需與驗證 URL 中的 `timestamp` 參數搭配使用，可用於計算實際簽名失效時間。簽名失效後，使用者將無法透過驗證 URL 推流或拉流。<br><br>簽名失效時間 = `timestamp` + 有效期。例如，若 `timestamp` 的值為 `1758296819`（2025\-09\-19 23:46:59），有效期為 600 秒，則簽名失效時間為 `1758297419`（2025\-09\-19 23:56:59）。 |
|時間戳基底 |`timestamp` 的時間格式。預設值為 **Decimal**。有效值：<br><br><br>* **Decimal**<br><br>* **Hexadecimal**<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">推流用的域名僅支援數字時間格式。</div><br> |


<span id="a4f520fc"></span>
## C 型 URL 驗證

<span id="b10ab2b8"></span>
### 運作原理

驗證 URL 格式：

```SQL
OriginalURL?txSecret=md5({key}{StreamName}{timestamp})&txTime=timestamp
```



|欄位 |描述 |範例值 |
|---|---|---|
|txSecret |簽名參數的名稱。您可於控制台的 **Edit URL authentication** 對話框中設定名稱。 |`txSecret` |
|key |主金鑰或備用金鑰，可於控制台的 **Edit URL authentication** 對話框中設定。 |`123abc` |
|StreamName |直播流地址中 `StreamName` 欄位的值。<br><br>值必須為 1\-100 個字元，且可包含：<br><br><br>* 數字（0\-9）<br><br>* 小寫字母（a\-z）<br><br>* 大寫字母（A\-Z）<br><br>* 底線（_）<br><br>* 連字號（\-）<br><br><br>例如，若原始 URL 為 `http://pull.example.com/live/test.flv`，則 `StreamName` 的值為 `test`。 |`test` |
|timestamp |Unix 時間戳，單位為秒。支援十進位或十六進位，且必須於控制台的 **Edit URL authentication** 對話框中選擇相同的時間格式。<br><br>此欄位需與控制台 **Edit URL authentication** 對話框中設定的有效期搭配使用，以計算實際簽名失效時間。簽名失效後，使用者將無法透過驗證 URL 拉流。<br><br>簽名失效時間 = `timestamp` + 有效期。例如，若 `timestamp` 的值為 `68cd7af3`（2025\-09\-19 23:46:59），有效期為 600 秒，則簽名失效時間為 `68cd7d4b`（2025\-09\-19 23:56:59）。 |`68cd7af3` |
|txTime |時間戳參數的名稱。您可於控制台的 **Edit URL authentication** 對話框中設定名稱。 |`txTime` |


根據 `md5({key}{StreamName}{timestamp})` 計算簽名值。在本主題範例中，`{key}{StreamName}{timestamp}` 的值為 `123abctest68cd7af3`。對該值進行 MD5 雜湊，生成一個 32 字元的小寫字串，結果為 `73af6af9c874d9d4cc50f8490325cd7b`。

驗證 URL 範例：

```Plain
http://pull.example.com/live/test.flv?txSecret=73af6af9c874d9d4cc50f8490325cd7b&txTime=68cd7af3
```


<span id="cdbc1626"></span>
### 驗證流程


1. BytePlus MediaLive 伺服器在收到使用者的驗證 URL 請求後，會對 `{key}{StreamName}{timestamp}` 的值進行 MD5 雜湊運算，生成一個 32 字元的小寫字串。在本主題的範例中，最終生成的字串為 `73af6af9c874d9d4cc50f8490325cd7b`。

2. BytePlus MediaLive 伺服器會驗證驗證 URL 中的驗證參數。只有同時通過以下兩項檢查，驗證才會通過。

   * 判斷伺服器計算出的簽名值是否與請求中的簽名值一致。若一致，則驗證通過。在本主題的範例中，簽名值為 `txSecret=73af6af9c874d9d4cc50f8490325cd7b&txTime=68cd7af3`。

   * 判斷簽名是否有效。伺服器會將目前時間與簽名失效時間（`timestamp` + 有效期）進行比較。若簽名失效時間晚於目前時間，則判定簽名有效，驗證通過。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">對於如 RTMP 和 FLV 等用於拉取長時長串流的協議，當用戶發起拉流請求時，BytePlus MediaLive 伺服器會驗證認證參數。驗證通過後，用戶可以持續拉流，不會受到簽名失效時間的影響。因此，只要請求是在簽名失效前發起，拉流過程將不會因簽名失效而中斷。只有新發起的拉流請求會因簽名失效而失敗。   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">HLS 協議用於分段式影片播放，用戶會持續發起新的拉流請求以獲取影片分段。每當用戶發起拉流請求時，BytePlus MediaLive 伺服器都會驗證認證參數。因此，一旦簽名失效，請求將被拒絕，導致播放中斷。由於直播播放過程中會頻繁請求新分段，建議您設置較長的簽名失效時間，以避免直播過程中播放失敗。   </div>
   

3. 根據驗證結果判斷請求是否有效。

   * 驗證通過：請求有效，伺服器會回應該請求。使用者可以成功拉流。

   * 驗證失敗：請求無效。返回 403 錯誤，並拒絕該請求。使用者無法拉流，從而保護直播流資源。


<span id="4c04cb54"></span>
### 控制台設定

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7060192fc9b5436b87d30286b0d8e4a4~tplv-goo7wpa0wc-image.image) </span>


|配置項 |說明 |
|---|---|
|主金鑰 |主金鑰。<br><br>值必須為 1\-100 個字元，可包含數字（0–9）、小寫字母（a–z）及大寫字母（A–Z）。<br><br>您也可以點擊文本框右側的圖示，隨機生成包含數字、小寫及大寫字母的 24 位金鑰。 |
|備用金鑰 |備用金鑰，用於無縫更新主金鑰。<br><br>值必須為 1\-100 個字元，可包含數字（0–9）、小寫字母（a–z）及大寫字母（A–Z）。<br><br>您也可以點擊文本框右側的圖示，隨機生成包含數字、小寫及大寫字母的 24 位金鑰。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">為避免在更換主鍵時造成線上服務中斷，可使用備用金鑰生成驗證 URL，以實現平滑過渡。在過渡期間，可將驗證 URL 替換為由備用金鑰生成的版本。主鍵更換後，請逐步將驗證 URL 替換為由新主鍵生成的版本。</div><br> |
|簽名參數 |簽名參數的名稱。預設值為 `txSecret`。<br><br>值必須為 1\-100 個字元，可包含：<br><br><br>* 數字（0\-9）<br><br>* 小寫字母（a\-z）<br><br>* 大寫字母（A\-Z）<br><br>* 底線（_）<br><br>* 連字號（\-）<br><br>* 點號（.）<br><br>* 逗號（,）<br><br>* 驚嘆號（!）<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">值必須包含至少一個字母。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">signature 參數與 timestamp 參數不可使用相同名稱。</div><br> |
|時間戳參數 |時間戳參數的名稱。預設值為 `txTime`。<br><br>值必須為 1\-100 個字元，可包含：<br><br><br>* 數字（0\-9）<br><br>* 小寫字母（a\-z）<br><br>* 大寫字母（A\-Z）<br><br>* 底線（_）<br><br>* 連字號（\-）<br><br>* 點號（.）<br><br>* 逗號（,）<br><br>* 驚嘆號（!）<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">值必須包含至少一個字母。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">signature 參數與 timestamp 參數不可使用相同名稱。</div><br> |
|有效期 |簽名的有效期。單位：秒。預設值為 `600`。取值範圍：[0, 2592000]。<br><br>此參數需與認證 URL 中的 `timestamp` 參數搭配使用，可用於計算實際簽名失效時間。簽名失效後，用戶將無法通過認證 URL 拉流。<br><br>簽名失效時間 = `timestamp` + 有效期。例如，若 `timestamp` 的值為 `68cd7af3`（2025\-09\-19 23:46:59），有效期為 600 秒，則簽名失效時間為 `68cd7d4b`（2025\-09\-19 23:56:59）。 |
|時間戳基準 |`timestamp` 的時間格式。預設值為 **Hexadecimal**。可選值：<br><br><br>* **十進位**<br><br>* **十六進位** |

---
title: "CDN 憑證託管"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cdn-cert-hosting_zh-tw"
---

在預設情況下，您透過 BytePlus CDN 上傳的憑證會託管在 BytePlus 憑證中心。除此之外，CDN 還提供了憑證託管的能力，但需要您 [提交工單](https://console.byteplus.com/workorder/create) 來啟用此能力。

CDN 除了能託管伺服器憑證以外，還能託管 CA 憑證。如果您要啟用 CDN 中依賴 CA 憑證的特性（例如 [存取雙向認證](https://docs.byteplus.com/en/docs/byteplus-cdn/mtls_zh-tw)），您需要先將相應的 CA 憑證上傳到 CDN 進行託管。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">主賬號下最多能上傳 500 本憑證到 CDN 進行託管。</div>


在您啟用 CDN 憑證託管功能前，BytePlus CDN 控制台左側導覽列的 **安全中心** 下只有 **憑證中心** 選單項目；啟用後，**安全中心** 下會新增獨立的 **憑證管理** 選單項目，該頁面即為 CDN 憑證託管頁面。

**憑證管理** 頁面頂部提供以下兩個操作入口：


* **設定憑證**：將託管在 CDN 中的憑證與一個或多個網域名稱關聯。具體操作步驟參見 [透過設定憑證關聯網域名稱](https://docs.byteplus.com/en/docs/18/106490#%E9%80%8F%E9%81%8E%E8%A8%AD%E5%AE%9A%E6%86%91%E8%AD%89%E9%97%9C%E8%81%AF%E7%B6%B2%E5%9F%9F%E5%90%8D%E7%A8%B1)。

* **上傳憑證託管**：將憑證上傳到 CDN 進行託管。具體操作步驟參見 [上傳憑證託管](https://docs.byteplus.com/en/docs/18/106490#%E4%B8%8A%E5%82%B3%E6%86%91%E8%AD%89%E8%A8%97%E7%AE%A1)。


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260604131547-1412517724747.png) </span>

頁面下方的憑證列表展示了所有已託管在 CDN 中的憑證，列表欄位說明如下：


|**欄位** |**說明** |
|---|---|
|憑證 ID |表示該憑證在 CDN 託管中的 ID，格式為 `cert_hosting-` 開頭的字串。 |
|憑證名稱 |表示憑證的名稱。 |
|憑證狀態 |表示憑證的目前狀態，可以是以下某個狀態：<br><br><br>* **執行中**：憑證有效。<br><br>* **即將到期**：離憑證到期日不足一個月。<br><br>* **已過期**：憑證已過期。<br><br><br>您可以點擊欄位標頭的篩選圖示，按 **執行中**、**即將到期**、**已過期** 進行篩選。 |
|憑證來源 |對於 CDN 託管的憑證，該欄位值是 **CDN 服務託管**。 |
|憑證類型 |表示憑證的類型，可以是 **伺服器憑證** 或 **CA 憑證**。 |
|可設定網域名稱 |表示 CDN 中可以與該憑證關聯的網域名稱。 |
|已關聯網域名稱 |表示 CDN 中已與該憑證關聯的網域名稱。 |
|開始時間 |表示憑證的簽發時間。 |
|操作 |可對該憑證進行的操作：<br><br><br>* **關聯網域名稱**：將該憑證與一個或多個網域名稱關聯。具體操作步驟參見 [透過憑證列表關聯網域名稱](https://docs.byteplus.com/en/docs/18/106490#%E9%80%8F%E9%81%8E%E6%86%91%E8%AD%89%E5%88%97%E8%A1%A8%E9%97%9C%E8%81%AF%E7%B6%B2%E5%9F%9F%E5%90%8D%E7%A8%B1)。<br><br>* **刪除**：刪除該 CDN 託管憑證。 |


<span id="上傳憑證託管"></span>
## 上傳憑證託管

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">無論您上傳的是伺服器憑證還是 CA 憑證，都建議憑證檔案包含完整的憑證鏈。</div>



1. 在 BytePlus CDN 控制台的左側導覽列，選擇 **安全中心** \> **憑證管理**。

2. 在 **憑證管理** 頁面，點擊 **上傳憑證託管**。

3. 在 **上傳憑證託管** 頁面，參考 [設定說明](https://docs.byteplus.com/en/docs/18/106490#%E8%A8%AD%E5%AE%9A%E8%AA%AA%E6%98%8E) 進行設定，然後點擊 **上傳**。


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260604131619-1646875181240.png) </span>

<span id="設定說明"></span>
### 設定說明


|**設定** |**說明** |
|---|---|
|憑證來源 |目前僅支援 **CDN 服務託管**。 |
|憑證類型 |表示您要上傳的憑證類型。該設定有以下選項：<br><br><br>* **伺服器憑證**：用於網域名稱的 HTTPS 存取。<br><br>* **CA 憑證**：用於 CDN 中依賴 CA 憑證的特性（例如 [存取雙向認證](https://docs.byteplus.com/en/docs/byteplus-cdn/mtls_zh-tw)）。 |
|上傳方式 |表示憑證的上傳方式。該設定有以下選項：<br><br><br>* **手動輸入**：表示貼上憑證檔案和私密金鑰檔案中的內容。<br><br>* **檔案上傳**：表示上傳憑證檔案和私密金鑰檔案。 |
|憑證檔案 / CA 憑證 |表示憑證檔案。憑證檔案必須包含完整的憑證鏈，副檔名是 .crt 或者 .pem，內容以 `-----BEGIN CERTIFICATE-----` 開頭。<br><br><br>* 當 **憑證類型** 是 **伺服器憑證** 時，該欄位名為 **憑證檔案**。<br><br>* 當 **憑證類型** 是 **CA 憑證** 時，該欄位名為 **CA 憑證**。 |
|憑證私密金鑰 |表示憑證的私密金鑰檔案。私密金鑰檔案的副檔名是 .key 或者 .pem，內容以 `-----BEGIN XXX PRIVATE KEY-----` 開頭。<br><br>該欄位僅在 **憑證類型** 是 **伺服器憑證** 時顯示。 |
|備註名稱 |表示憑證的備註。 |


<span id="關聯網域名稱"></span>
## 關聯網域名稱

將 CDN 託管的憑證與網域名稱關聯後，該憑證才能用於網域名稱的相關安全設定。**憑證管理** 頁面提供了以下兩種關聯入口。

<span id="透過設定憑證關聯網域名稱"></span>
### 透過設定憑證關聯網域名稱

適用於一次性為多個網域名稱批次關聯同一本憑證的場景。

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260604131758-962692390314.png) </span>


1. 在 BytePlus CDN 控制台的左側導覽列，選擇 **安全中心** \> **憑證管理**。

2. 在 **憑證管理** 頁面，點擊 **設定憑證**。

3. 在 **設定憑證** 頁面，按以下三個步驟完成設定：

   1. **選擇憑證**：

      * **憑證來源**：固定為 **CDN 服務託管**。

      * **憑證類型**：選擇 **伺服器憑證** 或 **CA 憑證**。

      * **設定模式**：選擇 **單憑證** 或 **雙憑證**。

      * **選擇憑證**：根據所選的 **設定模式**，操作有所不同。

         * **單憑證**：在 **選擇憑證** 列表中，單選一本要關聯的憑證。如果列表中沒有所需憑證，請先返回 [上傳憑證託管](https://docs.byteplus.com/en/docs/18/106490#%E4%B8%8A%E5%82%B3%E6%86%91%E8%AD%89%E8%A8%97%E7%AE%A1) 完成上傳。

         * **雙憑證**：從 **待選憑證** 列表中點擊對應憑證行的 **新增至已選**，將憑證新增至 **已選憑證** 列表中。如果列表中沒有所需憑證，可點擊 **上傳其他憑證** 直接上傳。

         設定完成後，點擊 **下一步**。

   2. **關聯網域名稱**：在 **關聯網域名稱** 步驟的左側 **全部** 列表中勾選需要關聯該憑證的網域名稱，被勾選的網域名稱會出現在右側 **已選** 列表中。

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">列表中只展示可與該憑證關聯的網域名稱，已下線的網域名稱不會展示。      </div>
      

      選擇完成後，點擊 **下一步**。

   3. **設定預檢測**：平台會對所選網域名稱的目標設定進行預檢測，**檢測結果** 列表會展示每個網域名稱的 **變更確認** 狀態（例如 **可變更無風險**）。

      對於不希望本次變更的網域名稱，可點擊該網域名稱所在行的 **取消變更**。確認無誤後，點擊 **確認** 完成關聯。


<span id="透過憑證列表關聯網域名稱"></span>
### 透過憑證列表關聯網域名稱

適用於在憑證列表中對單本憑證快速關聯或調整網域名稱的場景。

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260604131847-1305536805288.png) </span>


1. 在 BytePlus CDN 控制台的左側導覽列，選擇 **安全中心** \> **憑證管理**。

2. 在 **憑證管理** 頁面的憑證列表中，找到目標憑證，並在該憑證的 **操作** 列點擊 **關聯網域名稱**。

3. 在 **關聯網域名稱** 頁面，按以下兩個步驟完成設定：

   1. **關聯網域名稱**：在左側 **全部** 列表中勾選需要關聯該憑證的網域名稱，被勾選的網域名稱會出現在右側 **已選** 列表中。

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">列表中只展示可與該憑證關聯的網域名稱，已下線的網域名稱不會展示；列表中還會標註每個網域名稱上目前已關聯憑證的狀態（如 <strong>已過期</strong>），便於您篩選。      </div>
      

      選擇完成後，點擊 **下一步**。

   2. **設定預檢測**：平台會對所選網域名稱的目標設定進行預檢測，**檢測結果** 列表會展示每個網域名稱的 **變更確認** 狀態。對於不希望本次變更的網域名稱，可點擊該網域名稱所在行的 **取消變更**。確認無誤後，點擊 **確認** 完成關聯。

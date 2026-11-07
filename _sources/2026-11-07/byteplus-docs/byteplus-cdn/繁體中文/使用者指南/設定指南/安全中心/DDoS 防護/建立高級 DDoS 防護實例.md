---
title: "建立高級 DDoS 防護實例"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/Create_an_Advanced_DDoS_Protection_instance_cn_tw"
---

本檔案介紹如何在 BytePlus CDN 管理主控台的 **DDoS** **防護** 頁面建立高級 DDoS 防護實例。

建立高級 DDoS 防護實例後，您的 BytePlus 帳號即訂閱並啟用高級 DDoS 防護服務。

<span id="背景資訊"></span>
## 背景資訊

針對網路層和傳輸層 DDoS 攻擊，CDN 提供標準 DDoS 防護和高級 DDoS 防護。如需使用高級 DDoS 防護，您需要訂閱 CDN\-Security\-Plan Advanced Edition 或建立高級 DDoS 防護實例。

關於標準 DDoS 防護和高級 DDoS 防護的更多說明，請參考 [標準 DDoS 防護和高級 DDoS 防護比較](https://docs.byteplus.com/en/docs/byteplus-cdn/DDos_protection_levels_cn_tw)。

<span id="使用限制"></span>
## 使用限制


* 目前，如需使用高級 DDoS 防護功能，請[提交工單](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000735)進行申請。

* 一個 BytePlus 帳號下，只能建立一個高級 DDoS 防護實例。


<span id="注意事項"></span>
## 注意事項


* 當您為網域名稱開啟高級 DDoS 防護且訂閱方案非 CDN\-Security\-Plan Advanced Edition 時，將會產生安全流量費用。安全流量的費用按 CDN 傳輸給用戶端的資料量計算。計費詳情，請參考 [計費說明](https://docs.byteplus.com/en/docs/byteplus-ddos-protection/docs-pricing)。

* 為網域名稱開啟高級 DDoS 防護後，您無需修改網域名稱的 DNS 解析設定。但是，DNS 會停止將網域名稱解析為 IPv6 位址（即使您在 CDN 的策略中啟用了 IPv6）。所有流量會指向 IPv4 高防 IP 位址。

* 開啟高級 DDoS 防護會帶來一定的網域名稱存取延遲。用戶端所在區域和網路環境會影響到延遲大小。


更多資訊，請參考[使用高級 DDoS 防護時的注意事項](https://docs.byteplus.com/en/docs/byteplus-cdn/DDos_protection_levels_cn_tw#%E4%BD%BF%E7%94%A8%E9%AB%98%E7%B4%9A-ddos-%E9%98%B2%E8%AD%B7%E6%99%82%E7%9A%84%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A0%85)。

<span id="操作步驟"></span>
## 操作步驟


1. 登入 [BytePlus CDN 管理主控台](https://console.byteplus.com/cdn)。

2. 在左側導覽列，選擇 **安全中心** \> **DDoS** **防護**。

3. 在 **DDoS** **防護** 頁面的 **實例管理** 區域，點擊 **訂閱實例**。

4. 在 **建立 CDN 高級 DDoS 防護實例** 頁面，設定以下參數：

   * **防護網域名稱數量**：設定需要被防護的網域名稱的數量。網域名稱數量不小於 50 且須為 5 的倍數。

      預設情況下，一個高級 DDoS 防護實例最多可以防護 50 個網域名稱。如果有更多的網域名稱需要防護，您需要額外付費。計費說明，請參見[計費詳情](https://docs.byteplus.com/en/docs/byteplus-ddos-protection/docs-pricing)。

   * **訂閱時長**：指定訂閱時長。

      該頁面上的其他參數的值由系統指定，無法手動修改。對這些參數的說明如下：

   * **地區**：高級 DDoS 防護提供服務的區域。目前，高級 DDoS 防護只能在除中國大陸以外的區域使用。

   * **設定模式**：高級 DDoS 防護的設定模式。CDN 服務下的高級 DDoS 防護功能的設定模式為 **CDN聯動**。

   * **預留資源**：預留的專用 IP 位址。當您訂閱高級 DDoS 防護後，CDN 會為您分配一個專屬的防護 IP 位址。

   * **防護能力**：高級 DDoS 防護提供的防護能力。固定值為 **全力防護**。**全力防護** 意味著清洗中心的最大防護容量都會被用來防護 DDoS 攻擊。

   * **資料傳輸費用**：安全流量的費用。安全流量的費用按 CDN 傳輸给用戶端的資料量計算。

5. 確認設定無誤後，勾選 **我已閱讀並同意服務條款、服務等級協議、客戶協議**，然後點擊 **建立**。

6. 按頁面提示完成支付。建立完成的實例會顯示在 **DDoS 防護** 頁面的實例清單中。


<span id="後續操作"></span>
## 後續操作


1. [新增網域名稱](https://docs.byteplus.com/en/docs/byteplus-cdn/Manage_protected_domains_cn_tw#%E6%96%B0%E5%A2%9E%E7%B6%B2%E5%9F%9F%E5%90%8D%E7%A8%B1)：建立高級 DDoS 防護實例後，您需要手動新增需要防護的網域名稱。

2. （可選）[查看監控資料](https://docs.byteplus.com/en/docs/byteplus-ddos-protection/docs-viewing-ddos-attack-protection-information)：您可以透過 Dashboard 查看 DDoS 防護資料如攻擊流量、攻擊次數、回源流量、出站流量、攻擊事件等。

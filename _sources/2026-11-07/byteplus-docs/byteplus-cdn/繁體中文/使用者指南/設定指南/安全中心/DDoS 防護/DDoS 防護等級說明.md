---
title: "DDoS 防護等級說明"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DDos_protection_levels_cn_tw"
---

BytePlus CDN 根據您使用的加值服務或方案版本，提供不同等級的 DDoS 防護。

加值服務包括 CDN 高級 DDoS 防護、WAF 防護等。方案包括 CDN\-Security\-Plan Standard Edition 和 CDN\-Security\-Plan Advanced Edition。

<span id="7c8edd49"></span>
## **網路層和傳輸層 DDoS 防護**


|**服務類型** |**防護能力** |**適用對象** |
|---|---|---|
|CDN 原生防護 |* 最小防護頻寬：不承諾<br><br>* 最大防護頻寬：10 Gbps（依據平台容量調整） |所有使用者 |
|CDN 標準 DDoS 防護 |* 最小防護頻寬：50 Gbps<br><br>* 最大防護頻寬：依據平台容量調整 |* 訂閱 CDN\-Security\-Plan Standard Edition 的使用者<br><br>* 單獨申請開啟 CDN 標準 DDoS 防護的使用者 |
|CDN 高級 DDoS 防護 |* 最小防護頻寬：100 Gbps<br><br>* 最大防護頻寬：Tbps 級別（盡力防護） |* 訂閱 CDN\-Security\-Plan Advanced Edition 的使用者<br><br>* 單獨採購 CDN 高級 DDoS 防護的使用者 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>概念說明：</strong></div>



* <div data-tips="true" data-tips-type="tip"><strong>防護頻寬</strong>：指在單次攻擊事件中，CDN 平台能夠處理的入向異常流量所消耗頻寬的總和。您帳號下所有網域名稱的異常流量都會被計算在內。</div>


* <div data-tips="true" data-tips-type="tip"><strong>最小防護頻寬</strong>：CDN 平台穩定提供的防護能力。</div>


* <div data-tips="true" data-tips-type="tip"><strong>最大防護頻寬</strong>：CDN 平台透過動態調度可達到的最高防護能力。<strong>最大防護頻寬為參考值。</strong></div>



<div data-tips="true" data-tips-type="tip"><strong>注意事項：</strong></div>



* <div data-tips="true" data-tips-type="tip">使用 CDN 高級 DDoS 防護時，請確保已為相關網域名稱開啟防護功能。相關操作，請參考<a href="https://docs.byteplus.com/en/docs/byteplus-cdn/Manage_protected_domains_cn_tw#%E6%96%B0%E5%A2%9E%E7%B6%B2%E5%9F%9F%E5%90%8D%E7%A8%B1">添加網域名稱到高級 DDoS 防護實例</a>。</div>


* <div data-tips="true" data-tips-type="tip">當攻擊流量超出 CDN 平台防護能力且可能影響平台穩定性時，將觸發黑洞、網域名稱下線、服務停用等保護機制。您的站點業務可能會因此中斷。為降低影響，建議您：</div>


   * <div data-tips="true" data-tips-type="tip">提前訂閱加值服務，提升安全防護等級。</div>


   * <div data-tips="true" data-tips-type="tip">在攻擊停止後，<a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000735">提交工單</a>申請解除保護機制帶來的限制。</div>



<span id="0bc0c4c2"></span>
## **應用層 DDoS 防護**


|**服務類型** |**防護能力** |**適用對象** |
|---|---|---|
|CDN 原生防護 |* 最小防護請求數：不承諾<br><br>* 最大防護請求數：10 萬 QPS（依據平台容量調整） |所有使用者 |
|搭配 Edge WAF 的應用層 DDoS 防護 |* 最小防護請求數：50 萬 QPS<br><br>* 最大防護請求數：300 萬 QPS（依據平台容量調整） |* 訂閱 BytePlus Edge WAF 的使用者<br><br>* 訂閱 CDN\-Security\-Plan Standard Edition 的使用者<br><br>* 訂閱 CDN\-Security\-Plan Advanced Edition 的使用者 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>概念說明：</strong></div>



* <div data-tips="true" data-tips-type="tip"><strong>防護請求數</strong>：指在單次攻擊事件中，CDN 平台能夠處理的異常請求總數。您帳號下所有網域名稱的異常請求都會被計算在內。</div>


* <div data-tips="true" data-tips-type="tip"><strong>最小防護請求數</strong>：CDN 平台穩定提供的防護能力。</div>


* <div data-tips="true" data-tips-type="tip"><strong>最大防護請求數</strong>：CDN 平台透過動態調度可達到的最高防護能力。<strong>最大防護請求數為參考值。</strong></div>



<div data-tips="true" data-tips-type="tip"><strong>注意事項：</strong></div>



* <div data-tips="true" data-tips-type="tip">使用搭配 Edge WAF 的應用層 DDoS 防護時，請確保已為相關網域名稱開啟防護功能，並按需設定安全策略。相關操作，請參考<a href="https://docs.byteplus.com/en/docs/waf/Adding_a_CDN_domain_name_to_a_WAF_instance">新增網域名稱到 WAF 實例</a>和<a href="https://docs.byteplus.com/en/docs/waf/docs-configuring-rate-limit-policies">設定限流策略</a>。</div>


* <div data-tips="true" data-tips-type="tip">當攻擊流量超出 CDN 平台防護能力且可能影響平台穩定性時，將觸發沙箱處置、強制限流、網域名稱下線、服務停用等保護機制。您的站點業務可能會因此中斷。為降低影響，建議您：</div>


   * <div data-tips="true" data-tips-type="tip">提前訂閱加值服務，提升安全防護等級。</div>


   * <div data-tips="true" data-tips-type="tip"><a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000735">提交工單</a>申請解除保護機制帶來的限制。</div>



<span id="7279419d"></span>
## 更多資訊

<span id="51bd7ce6"></span>
### 標準 DDoS 防護和高級 DDoS 防護比較

針對網路層和傳輸層 DDoS 攻擊，CDN 提供標準 DDoS 防護和高級 DDoS 防護。相較於標準 DDoS 防護，高級 DDoS 防護能夠提供更高的 DDoS 防護能力。

下表列出了標準 DDoS 防護和高級 DDoS 防護的具體差異。


| |**標準** **DDoS** **防護** |**高級** **DDoS** **防護** |
|---|---|---|
|**服務範圍** |* 服務對象：訂閱 CDN\-Security\-Plan Standard Edition 的使用者或單獨申請開啟 CDN 標準 DDoS 防護的使用者<br><br>* 服務區域：全球（不包含中國大陸） |* 服務對象：訂閱 CDN\-Security\-Plan Advanced Edition 的使用者或訂閱高級 DDoS 防護的使用者<br><br>* 服務區域：全球（不包含中國大陸） |
|**訂閱與計費** |如果您訂閱了 CDN\-Security\-Plan Standard Edition 或單獨申請開啟了 CDN 標準 DDoS 防護，在您的網域名稱接入 CDN 後，標準 DDoS 防護將自動開啟。您無需額外設定和付費。 |* 訂閱 CDN\-Security\-Plan Advanced Edition<br><br><br>系統會自動建立高級 DDoS 防護實例。無需單獨支付高級 DDoS 防護的費用。<br><br><br>* 單獨採購高級 DDoS 防護<br><br><br>您需要建立高級 DDoS 防護實例並支付使用費。高級 DDoS 防護的費用包括實例費用（預付費）、安全流量費用（後付費）和超出預設配額（50個）的網域名稱的費用（預付費）。安全流量費按 CDN 傳輸給用戶端的資料量計算。計費詳情，請參考 [計費說明](https://docs.byteplus.com/en/docs/byteplus-ddos-protection/docs-pricing)。 |
|**防護方式** |標準 DDoS 防護基於 CDN 分散式節點上的自建 DDoS 防護系統實現。該系統採用了基於快速資料路徑（eXpress Data Path，簡稱 XDP） 技術的防護外掛程式，能夠處理高並行流量。 |CDN 擁有全球多區域分佈的大容量清洗中心。清洗中心部署了專用的 DDoS 清洗引擎。<br><br>當 DDoS 攻擊發生時，攻擊流量經 Anycast IP 分散到清洗中心，由 DDoS 清洗引擎攔截。只有正常流量會被傳輸到 CDN。 |
|**防護能力** |標準 DDoS 防護提供以下防護能力：<br><br><br>* 防護常見量級的網路層和傳輸層 DDoS 攻擊。 |高級 DDoS 防護提供以下防護能力：<br><br><br>* 防護大規模的網路層和傳輸層 DDoS 攻擊。<br><br>* 提供 Tbps 級防護頻寬資源。<br><br>* 提供專屬的防護 IP 資源。<br><br>* 預設情況下，一個高級 DDoS 防護實例可以防護 50 個網域名稱。如果您需要防護更多的網域名稱，可以額外付費提升網域名稱配額。 |
|**防護範圍** |防護常見的攻擊，包括 SYN Flood、ACK Flood、RST Flood、空連線攻擊、TCP 畸形包攻擊、LAND 攻擊等 |防護常見的攻擊，包括 SYN Flood、ACK Flood、RST Flood、RST/FIN Flood、SYN\-ACK Flood、UDP Flood、UDP 分片、UDP 反射、ICMP 分片、ICMP Flood、Ping of Death、Smurf、Teardrop、IP Options、LAND 攻擊等 |
|**監控警示** |標準 DDoS 防護不支援攻擊監控和警示功能。如果您的服務疑似因大規模網路攻擊而被限制使用和停用，請[提交工單](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000735)諮詢。 |高級 DDoS 防護支援攻擊監控和警示功能。您可以透過監控面板（Dashboard）來查看高級 DDoS 防護實例的即時監控資料。當攻擊流量達到閾值後，系統會向您傳送警示通知。更多資訊，請參見[查看監控資料](https://docs.byteplus.com/en/docs/byteplus-ddos-protection/docs-viewing-ddos-attack-protection-information)。 |


<span id="12536d10"></span>
### 使用高級 DDoS 防護時的注意事項

使用高級 DDoS 防護時，請您關注以下方面的注意事項：


* IPv6

   開啟高級 DDoS 防護後，無需手動修改網域名稱的 DNS 解析設定。但是，DNS 會停止將網域名稱解析為 IPv6 位址（即使您在 CDN 的策略中啟用了 IPv6），所有用戶端流量會指向 IPv4 高防 IP 位址。

* 效能

   開啟高級 DDoS 防護會帶來一定的網域名稱存取延遲。用戶端所在區域和網路環境會影響到延遲大小。

* 服務區域

   * DDoS 功能的服務區域不包含中國大陸：

      * 如果您為網域名稱指定的加速區域為「全球」，僅在除中國大陸以外的區域會啟用清洗中心。即，只有來自這些區域的用戶端流量會經過清洗中心。

      * 如果您為網域名稱指定的加速區域為「中國大陸」，則無法為該網域名稱開啟 DDoS 防護功能。

   * 為網域名稱開啟 DDoS 防護後，您將無法切換網域名稱的加速區域。

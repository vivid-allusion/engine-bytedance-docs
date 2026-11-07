---
title: "WAF防護"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-web-application-firewall-waf--zh-tw"
---

<span id="功能介紹"></span>
## 功能介紹

BytePlus CDN 整合了 BytePlus Web 應用防火牆（WAF）的安全防護能力，為接入網域名稱提供針對應用層攻擊的防護能力。CDN 透過在內容分發網路鏈路中嵌入 WAF 防護模組，實現對存取請求的篩選與控制。

在您為接入 CDN 的網域名稱啟用 WAF 防護功能後，所有針對該網域名稱發起的 HTTP 和 HTTPS 存取請求都會經過 WAF 防護模組的處理。具體流程如下：


1. **請求路由**：用戶端發起的存取請求到達 CDN 邊緣伺服器後，首先經過 CDN 分發策略中的請求控制規則處理。然後，通過的請求會被轉發到 WAF 防護模組進行安全偵測。

2. **WAF偵測**：WAF 防護模組依據預設的防護規則對請求進行深度分析，然後根據分析結果對請求進行處理。防護規則包括存取控制、CC 攻擊防護、漏洞防護、Bot 管理和API 防護規則等。

   * **合法請求處理**：經 WAF 防護模組判定為合法的請求將被放行，繼續在 CDN 中進行處理。CDN 會根據快取策略判斷是否直接從邊緣伺服器的快取中獲取內容，或向來源伺服器請求內容。

   * **非法請求處理**：經 WAF 防護模組判定為非法的請求將被阻斷或被記錄在攻擊日誌中。請求被阻斷時，系統支援向用戶端返回自訂回應頁面，同時產生詳細的攻擊日誌。攻擊日誌包含被攻擊網域名稱、發起攻擊的 IP 位址、攻擊發生時間等資訊，便於後續安全稽核與溯源分析。


透過將 WAF 防護功能深度整合於 CDN 架構中，CDN 在保障內容分發效率的前提下，實現對 Web 應用的即時安全防護。

<span id="應用場景"></span>
## 應用場景

WAF 防護功能主要用於以下場景：存取控制、CC 攻擊防護、漏洞防護、Bot 管理和 API 防護。

<span id="存取控制"></span>
### 存取控制

存取控制規則能夠實現對 HTTP 請求的精準識別和控制。您可以設定自訂規則，基於存取來源和 HTTP 請求特徵來允許或封鎖特定請求。

存取來源可以是 IP 位址、IP 位址段或地理位置。HTTP 請求特徵包含請求路徑、請求 URI、請求協定、請求方法、請求參數、請求標頭、自訂 Header、自訂 Cookie 等。

<span id="cc-攻擊防護"></span>
### CC 攻擊防護

CC 攻擊（Challenge Collapsar） 是一種針對 Web 應用程式伺服器的七層 DDoS 攻擊。攻擊者透過傳送大量看似合法的 HTTP 請求來消耗目標伺服器的資源，最終導致伺服器無法正常回應合法使用者的請求。

您可以自訂 CC 防護規則。系統根據您設定的 HTTP 請求特徵和統計條件，對偵測到的 CC 攻擊執行相應動作，從而實現精準的流量封鎖或限制。

<span id="漏洞防護"></span>
### 漏洞防護

內建的防護規則為您的 Web 應用提供全方位保護，有效防禦針對常見漏洞（包括 CVE 揭露漏洞和 OWASP TOP 10 漏洞）的 Web 攻擊威脅。

防護規則類型涵蓋 SQL 注入、命令注入、伺服器端請求偽造（SSRF）、跨網站指令碼攻擊（XSS）、XML 實體注入（XXE）、檔案目錄周遊、LDAP 注入、XPath 注入、伺服器端範本注入（SSTI）、運算式注入等。

<span id="bot-管理"></span>
### Bot 管理

Bot 管理規則能夠有效阻止來自外部 Bot 的惡意請求和行為，確保只有合法請求正常轉發。託管 Bot 管理規則對常見 Bot 進行分類並按照預設設定執行相應動作。

您也可以根據業務需求自訂 Bot 管理規則，基於 HTTP 請求特徵實現精細化 Bot 管理。

<span id="api-防護"></span>
### API 防護

API 防護規則能夠根據設定的 API 路徑、請求方法和參數來檢查 API 請求，對符合指定特徵的 API 請求執行攔截或觀察動作。

API 防護能夠利用智慧偵測和學習能力來識別存在風險的 API 請求行為，並將相關 API 記錄到自動新增的 API 防護規則中。您也可以手動建立 API 防護規則。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">更詳細的防護能力說明和規則設定指引，請參考 <a href="https://docs.byteplus.com/en/docs/waf/docs-what-is-byteplus-web-application-firewall">BytePlus WAF 文件</a>。</div>


<span id="使用流程"></span>
## 使用流程

<span id="設定-waf-防護"></span>
### 設定 WAF 防護

如需使用 WAF 防護功能防護您的網域名稱，您需要執行以下操作：


1. [建立 WAF 執行個體](https://docs.byteplus.com/en/docs/waf/docs-system-management)。

2. [將網域名稱新增到 WAF 執行個體](https://docs.byteplus.com/en/docs/waf/Adding_a_CDN_domain_name_to_a_WAF_instance)。

3. [設定防護規則](https://docs.byteplus.com/en/docs/waf/docs-introduction-to-custom-waf-rules)。


<span id="檢視接入網域名稱的-waf-防護狀態"></span>
### 檢視接入網域名稱的 WAF 防護狀態

在 CDN 主控台的 [WAF 防護](https://console.byteplus.com/cdn/cdn-bp/security/waf-protection)頁面，您可以檢視已接入到 CDN 的網域名稱是否開啟了 WAF 防護。

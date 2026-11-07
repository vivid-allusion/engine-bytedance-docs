---
title: "DDoS 防護概述"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DDos_protection_overview_cn_tw"
---

<span id="什麼是-ddos-攻擊？"></span>
## 什麼是 DDoS 攻擊？

分散式阻斷服務攻擊（Distributed Denial of Service，簡稱 DDoS）是一種網路攻擊類型。攻擊者利用多台受感染的裝置（如電腦）同時向目標伺服器傳送大量資料封包或請求。這些 DDoS 攻擊會迅速耗盡目標伺服器的頻寬、CPU 和記憶體等資源，導致目標伺服器無法處理正常流量或回應正常請求。

DDoS 攻擊通常發生在 OSI 模型的網路層（第三層）、傳輸層（第四層）和應用層（第七層）：


* **網路層攻擊**

   攻擊者利用大量偽造的 IP 位址向目標伺服器傳送大量資料封包，導致目標伺服器的網路頻寬被耗盡，無法处理正常的網路流量。

* **傳輸層攻擊**

   攻擊者利用大量偽造的 IP 位址向目標伺服器傳送大量 TCP 或 UDP 連線請求，消耗目標伺服器的連線資源，導致伺服器無法處理正常的連線請求。

* **應用層攻擊**

   攻擊者利用大量偽造的請求，向目標伺服器傳送大量 HTTP 請求，消耗目標伺服器的 CPU 和記憶體等資源，導致伺服器無法回應正常請求。


DDoS 攻擊可能導致業務中斷，帶來嚴重的經濟損失。遊戲、電商、金融等產業的網際網路應用和網路基礎設施是 DDoS 攻擊的主要目標。

<span id="byteplus-cdn-提供的-ddos-防護"></span>
## BytePlus CDN 提供的 DDoS 防護

BytePlus CDN（下文簡稱 CDN）透過 DDoS 防護和 WAF 防護功能，提供完善的 DDoS 攻擊防護。DDoS 防護功能能夠攔截網路層和傳輸层的 DDoS 攻擊。WAF 防護功能能夠攔截應用層的 DDoS 攻擊。透過這些防護措施，CDN 能夠幫助您有效降低 DDoS 攻擊帶來的風險，保障您的來源伺服器安全與業務穩定。

<span id="網路層和傳輸層-ddos-防護"></span>
### 網路層和傳輸層 DDoS 防護

當您使用 CDN 服務來分發 Web 內容時，您的來源伺服器被隱藏在 CDN 服務後，避免遭受直接的攻擊。

然而，攻擊者仍可能向您的網域名稱或網域名稱所關聯的 CDN 服務 IP 位址發起攻擊。當您的網域名稱引發大規模針對服務 IP 位址的 DDoS 攻擊時，受影響的 IP 位址可能會被停用並造成暫時的服務中斷。在該情況下，您的業務可能也會受到影響。

針對向 IP 位址發起的網路層和傳輸層 DDoS 攻擊，CDN 提供兩種級別的安全防護服務：


* **標準 DDoS 防護**：基於 CDN 邊緣節點上的自建 DDoS 防護系統實現對 DDoS 攻擊的防護。標準 DDoS 防護提供基礎的 DDoS 防護能力，能夠防護常見量級的 DDoS 攻擊。

* **高級 DDoS 防護**：基於全球多地域分佈的大容量清洗中心，提供針對大規模 DDoS 攻擊的防護能力。如果標準 DDoS 防護提供的防護能力不能滿足您的業務正常執行需求，您可以訂閱高級 DDoS 防護。


關於標準 DDoS 防護和高級 DDoS 防護的更多介紹，请參閱 [標準 DDoS 防護和高級 DDoS 防護比較](https://docs.byteplus.com/en/docs/byteplus-cdn/DDos_protection_levels_cn_tw)。

<span id="應用層-ddos-防護"></span>
### 應用層 DDoS 防護

向網域名稱發起的应用層 DDoS 攻擊有以下特點：攻擊流量往往難以與正常的用戶端存取流量區分。因此，攻擊流量可能會到達來源伺服器，對來源伺服器安全造成嚴重威脅。此外，還可能會造成高額的 CDN 帳單。

為應對這種攻擊威脅，CDN 的 WAF 防護功能提供了應用層 DDoS 防護能力。您可以利用系統預設防護策略和自訂防護策略來識別和過濾攻擊流量。

關於 WAF 防護功能的詳細介紹，請參閱 [WAF 防護](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-web-application-firewall-waf--zh-tw)。

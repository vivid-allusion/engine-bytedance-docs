---
title: "IP 限制"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-ip-blocklist-and-allowlist-zh-TW"
---

為提升串流服務的安全性，您可以設定 IP blocklist 或 allowlist。本主題提供逐步操作說明，協助您限制或授權您的網域名稱進行串流推送與拉取，確保只有合法用戶能存取您的內容。


* 加入 blocklist 的 IP 位址將無法存取該網域。

* 若已設定 allowlist，僅 allowlist 中的 IP 位址可存取該網域。

* 這些清單支援 IPv4 位址及 IP 網路段。


<span id="b3e4fbb7"></span>
# 適用於


* 串流推送用的網域名稱

* 串流拉取用的網域名稱


<span id="ed9f0df7"></span>
# 先決條件

您已新增網域名稱。如需更多資訊，請參閱 [新增網域名稱](https://docs.byteplus.com/docs/byteplus-media-live/docs-domain-zh-TW)。

<span id="26c3b955"></span>
# 操作流程


1. 登入 [BytePlus MediaLive 控制台](https://console.byteplus.com/live)。

2. 於左側導覽窗格中，點選 **Domains**。

3. 找到您要檢視的網域名稱，並於 **Actions** 欄點選 **Settings**。

4. 點選 **Access control** 分頁。

5. 於 **IP restrictions** 開關右側，點選 **Edit**。

6. 在出現的 **Edit IP blocklist and allowlist** 對話框中，設定以下參數。

   * **List type**：選擇 **Blocklist** 或 **Allowlist**。這兩個選項互斥。若選擇 **Blocklist**，blocklist 中的 IP 位址將無法存取該網域。若選擇 **Allowlist**，僅 allowlist 中的 IP 位址可存取該網域。

   * **Rules**：輸入規則所需的 IPv4 位址或 IP 網路段。最多可設定 100 條規則。若需設定超過 100 條規則，請 [聯絡技術支援](https://console.byteplus.com/workorder/create)以申請提升限制。

7. 點選 **Confirm**。

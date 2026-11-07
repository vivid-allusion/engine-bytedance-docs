---
title: "HTTPS 設定"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-https-zh-TW"
---

你可以將 SSL/TLS 憑證綁定至你的網域名稱並啟用 HTTPS，以提升直播期間的安全性。

<span id="d1bc3916"></span>
# 適用於


* 拉流網域名稱

* 推流網域名稱


<span id="47193979"></span>
# 概述

**HTTPS**

HTTPS（HyperText Transfer Protocol Secure）是一種用於電腦網路安全通訊的傳輸協議。它在 HTTP 基礎上增加了 SSL/TLS 協議，透過數位憑證與加密演算法等技術，確保資料在傳輸過程中的安全性與完整性。


* **確保資料安全**：將 SSL/TLS 憑證綁定至網域並啟用 HTTPS，直播期間傳輸的資料會被加密，防止資料被竊取或篡改，從而保障使用者的隱私與安全。

* **提升使用者信任**：使用 HTTPS 可提升使用者對你的直播平台的信任，增強使用者滿意度與忠誠度。

* **符合法律與監管要求**：在某些情況下，使用 HTTPS 屬於法律要求，例如金融與電子商務領域。


**HTTP/2**

HTTP/2 是 HTTP 超文本傳輸協議的最新版本，於 2015 年 5 月正式發布。此更新版本基於 HTTP/1.x 的能力，並提供二進位分幀層、標頭壓縮、多路復用及伺服器推送等增強功能。雖然 HTTP/2 並不強制網站使用 HTTPS，但主流瀏覽器對 HTTP/2 的相容性取決於是否實作 SSL/TLS。目前，使用 HTTP/2 的網站也預期需啟用 HTTPS。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">HTTP/2 僅適用於拉流網域名稱。</div>


**TLS 版本**

TLS 協議的不同版本在相容性與安全性上有所差異。舊版本具有較佳相容性但安全性較低，最新版本則提供更高安全性但可能存在相容性問題。目前大多數現代瀏覽器已支援 TLS 1.3。

當你透過瀏覽器存取已啟用 HTTPS 加速的網域時，快取節點會選擇與瀏覽器 TLS 版本及加速網域設定相符的最高 TLS 版本。若快取節點無法找到相容的 TLS 版本，TLS 握手將失敗，導致無法建立連線。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">TLS 版本設定僅適用於拉流網域名稱。</div>


<span id="8658adf5"></span>
# 前置條件


* 已新增網域名稱

* SSL/TLS 憑證。欲了解更多資訊，請參閱 [管理 SSL/TLS 憑證](https://docs.byteplus.com/docs/byteplus-media-live/docs-managing-certificates)。


<span id="5f81b8bf"></span>
# 操作流程


1. 登入 [BytePlus MediaLive 控制台](https://console.byteplus.com/live)。

2. 在左側導覽窗格中，選擇 **設定** \> **網域**。

3. 於出現的 **網域** 頁面，找到你要設定的網域名稱，並於 **操作** 欄點擊 **設定**。

4. 在開啟的頁面中，點擊 **HTTPS** 標籤。

5. 於 **HTTPS** 開關右側點擊 **編輯**。

6. 在 **編輯 HTTPS 資訊** 對話框中，**HTTPS** 開關預設為啟用。選擇你要使用的 SSL/TLS 憑證。你也可以：

   * 為目前網域名稱啟用 **HTTP/2**。

   * 設定 **TLS 版本範圍**。

7. 點擊 **確認**。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">只有當你的網域名稱被加入憑證的 <strong>主體替代名稱</strong> 欄位時，你的 SSL/TLS 憑證才會出現在 <strong>憑證</strong> 清單中。</div>


* <div data-tips="true" data-tips-type="tip">HTTPS 設定約需 10 分鐘生效。若設定未生效，請聯絡技術支援協助。</div>

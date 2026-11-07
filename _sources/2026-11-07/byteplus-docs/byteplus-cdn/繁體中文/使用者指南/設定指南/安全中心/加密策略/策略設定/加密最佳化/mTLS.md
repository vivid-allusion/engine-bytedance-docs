---
title: "mTLS"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/mtls_zh-tw"
---

本文件介紹如何在 BytePlus CDN 中為網域名稱設定 mTLS （雙向 TLS）特性。此特性適用於需要嚴格身分驗證的情境，例如企業內部應用，可使 CDN 僅允許攜帶特定憑證的用戶端存取 CDN，進一步提升用戶端與 CDN 之間的通訊安全性。

啟用此特性後，當用戶端與 CDN 建立 SSL 連線時，CDN 會校驗用戶端憑證。如果用戶端憑證並非由您設定的根 CA 憑證簽發，CDN 將拒絕該請求。

啟用此特性時，您需要在 CDN 中設定根 CA 憑證。設定模式支援單憑證與雙憑證。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">在雙憑證設定模式下，您可以設定兩本使用不同金鑰演算法的根 CA 憑證，但兩本憑證不能具有相同的指紋。</div>


<span id="前提條件"></span>
## 前提條件

要啟用 mTLS，您已將根 CA 憑證上傳至 CDN 進行託管。關於上傳步驟，請參閱 [CDN 憑證託管](https://docs.byteplus.com/en/docs/byteplus-cdn/cdn-cert-hosting_zh-tw)。

<span id="操作步驟"></span>
## 操作步驟


1. 開啟 **Mutual TLS** 設定頁面。操作步驟請參閱 [網域名稱設定](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_zh-tw)。

2. 將 **狀態** 設定為啟用。

3. 選擇 **憑證來源**。目前僅支援 **CDN 服務託管**。

4. 設定 **設定模式**。

   * **單憑證**：設定一本根 CA 憑證。

   * **雙憑證**：設定兩本使用不同金鑰演算法的根 CA 憑證。

5. 在 **選擇 CA 憑證** 下拉式清單中選擇對應的根 CA 憑證。如果清單中沒有所需的憑證，可點擊下方的 **上傳其他憑證** 直接上傳。

6. 設定完成後，點擊 **儲存**。


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">以下任一情況都會<strong>導致設定報錯</strong>：</div>



* <div data-tips="true" data-tips-type="warning">網域名稱未啟用 HTTPS 加密服務。</div>


* <div data-tips="true" data-tips-type="warning">mTLS 的設定模式與伺服器憑證的設定模式不一致。例如，mTLS 的設定模式為雙憑證，而伺服器憑證的設定模式為單憑證。</div>


* <div data-tips="true" data-tips-type="warning">mTLS 中設定的 CA 憑證所使用的金鑰演算法未涵蓋伺服器憑證所使用的金鑰演算法。例如，您在 mTLS 中設定的兩本 CA 憑證皆為 RSA 演算法，而伺服器憑證分別設定了 RSA 與 ECC 兩本，此時 ECC 流量沒有可用的 CA 憑證。</div>



<div data-tips="true" data-tips-type="warning">在以下情況下，<strong>用戶端憑證校驗會失敗</strong>：</div>



* <div data-tips="true" data-tips-type="warning">您所設定的根 CA 憑證的憑證鏈深度超過三級。例如，憑證鏈為 <code>rootCA > iCA1 > iCA2 > 用戶端憑證</code>。其中，iCA1 與 iCA2 皆為中繼 CA。</div>



<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260604130647-257937674697.png) </span>

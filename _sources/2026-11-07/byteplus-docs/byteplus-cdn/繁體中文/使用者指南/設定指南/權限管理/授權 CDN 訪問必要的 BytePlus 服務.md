---
title: "授權 CDN 訪問必要的 BytePlus 服務"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/allow-cdn-access-to-byteplus-service_zh-tw"
---

在 BytePlus CDN 中，如果您執行以下操作，您需要授權 CDN 存取對應的 BytePlus 服務：


* 指定 BytePlus 物件儲存（TOS）中的一個儲存桶作為一個來源伺服器：您需要授權 CDN 存取 TOS 服務。

* 上傳憑證或者關聯一個 BytePlus 憑證中心中的憑證：您需要授權 CDN 存取憑證中心服務。

* 創建邊緣函數：您需要授權 CDN 存取邊緣函數服務。


為了避免您以及 IAM 使用者在執行以上操作時遇到權限問題，我們建議您事先授予 CDN 權限存取這些服務。

<span id="操作步驟"></span>
## 操作步驟

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">強烈推薦使用主帳戶操作以下步驟。當以下步驟完成後，如果主帳戶和 IAM 使用者在 CDN 中操作憑證、管理邊緣函數、設置 TOS 儲存桶為來源伺服器時，無需再次執行這些步驟，也不會遇到服務授權問題。</div>


<div data-tips="true" data-tips-type="warning">對於子帳戶，除非被授予了 IAMFullAccess 系統策略，子帳戶沒有權限授予 CDN 存取其他 BytePlus 服務。因此，如果一個沒有被授予 IAMFullAccess 策略的子帳戶操作以下步驟，授權會失敗。同時，不建議授予 IAM 使用者 IAMFullAccess 策略，因為該策略的權限範圍太廣。</div>



1. 打開 [該連結](https://console.byteplus.com/iam/service/attach_role/?ServiceName=CDN)。

2. 點擊 **立即授權**。

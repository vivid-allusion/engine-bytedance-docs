---
title: "API 錯誤碼"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/api-error-code_zh-tw"
---

本文件說明了 BytePlus CDN 中常見的錯誤碼。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">在您判斷一個 API 請求是否成功時，建議您使用 <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/api-response_zh-tw#%E5%88%A4%E6%96%B7-api-%E8%AB%8B%E6%B1%82%E6%98%AF%E5%90%A6%E6%88%90%E5%8A%9F">判斷 API 請求是否成功</a> 中描述的方法。</div>


<span id="公共錯誤碼"></span>
## 公共錯誤碼

參見 [公共錯誤碼](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes)。

<span id="權限異常"></span>
## 權限異常

以下錯誤碼表示子用戶沒有權限使用 API 操作目標資源。


|Code |Message |說明 |
|---|---|---|
|NotFound.Domain |帳戶下無此網域名稱：xxx,xxx |嘗試存取的資源不屬於該帳號。 |
|AccessDenied.IAMUnauthorized |根據存取的資源，您會收到以下某個錯誤訊息：<br><br><br>* 您沒有權限操作網域名稱:  *<domain\>* <br><br>* 您沒有權限執行該操作<br><br>* 您沒有權限操作該專案:  *<project\>*  |子帳號無權限存取指定的網域名稱、專案或使用該 API。 |


<span id="參數異常"></span>
## 參數異常

以下錯誤碼表示用戶請求不符合 CDN 中的設定。


|Code |Message |參數說明 |
|---|---|---|
|InvalidParameter.<param\> |參數錯誤 |API 的參數不正確。錯誤類別在 `<param>` 中指示。 |
|InvalidParameter.Certificate |憑證內容解析錯誤。 |在解析憑證內容的時候遇到了錯誤。 |
|InvalidParameter.Certificate.KeyNotMatch |憑證與私鑰不相符。 |您上傳的憑證公鑰與私鑰不相符。 |
|InvalidParameter.Https.CertInfo.ChainMissing |網域名稱設定失敗，憑證鏈不完整。 |無法設定網域名稱，原因是憑證檔案中的憑證鏈不完整。 |
|InternalError.<param\> |內部錯誤，請稍後重試或聯絡工程師進行進一步諮詢。 |系統出現異常。問題類別在 `<param>` 中指示。請 [提交工單](https://console.byteplus.com/workorder/create)。 |
|InvalidParameter.BillingCode |參數錯誤：BillingCode 內容不合法。 |參數錯誤：`BillingCode` 值不合法。 |
|InvalidParameter.BillingRegion |參數錯誤：BillingRegion。 |參數錯誤：`BillingRegion` 值不合法。 |


<span id="網域名稱驗證"></span>
## 網域名稱驗證


|Code |Message |參數說明 |
|---|---|---|
|InvalidParameter.Domain.NeedVerified |請先驗證網域名稱的歸屬權，驗證成功後可新增網域名稱。 |網域名稱未通過所有權驗證。 |
|InvalidParameter.Domain.RetrieveUnsupported |網域名稱暫不支援取回。 |您無法對該網域名稱進行所有權驗證。 |
|InvalidParameter.Domain.DnsNotMatch |解析驗證不相符，請確認重試。 |您設定的 TXT 記錄不正確。 |


<span id="已廢棄的錯誤碼"></span>
## 已廢棄的錯誤碼

以下列表中的錯誤碼已經廢棄。這些錯誤碼不會在 CDN 中出現了。


|Code |Message |
|---|---|
|CDN.ResourceNotFound |帳戶下無此網域名稱：xxx,xxx |
|CDN.PermissionDenied |您沒有權限執行該操作。 |
|CDN.PermissionDenied |您沒有權限執行該操作。 |
|CDN.InvalidParameters |參數錯誤 |
|CDN.InvalidParam.Certificate |Certificate參數錯誤 |
|CDN.InvalidParam.PrivateKey |PrivateKey參數錯誤 |
|CDN.InvalidParam.Source |Source參數錯誤 |
|CDN.InvalidParam.CertificateChainError |憑證鏈無法補齊 |
|CDN.InternalError |未知錯誤，請聯絡技術支援 |
|CDN.InvalidParam.CertificateExpired |憑證已過期 |
|CDN.InvalidParam.BillingCode |BillingCode 參數錯誤 |
|CDN.InvalidParam.BillingRegion |BillingRegion 參數錯誤 |
|CDN.InvalidParam.ExportType |ExportType 參數錯誤 |

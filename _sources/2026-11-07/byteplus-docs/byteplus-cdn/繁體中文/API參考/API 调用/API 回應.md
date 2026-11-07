---
title: "API 回應"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/api-response_zh-tw"
---

本文件說明了 BytePlus CDN API 的回應。

<span id="回應標頭"></span>
## 回應標頭

每個 API 的回應中包含的回應標頭說明如下。

<span id="回應狀態碼"></span>
## 回應狀態碼

CDN 的回應狀態碼說明如下：


* 2xx：表示 CDN 已成功回應了 API 請求。但是成功回應未必保證 API 請求是成功的。參見 [判斷 API 請求是否成功](https://docs.byteplus.com/en/docs/18/46500#%E5%88%A4%E6%96%B7-api-%E8%AB%8B%E6%B1%82%E6%98%AF%E5%90%A6%E6%88%90%E5%8A%9F)。

* 4xx：表示 CDN 無法返回用戶端請求的內容。原因是用戶端請求不合法。例如：

   * 請求的檔案不存在。

   * 請求方法不正確。

   * 請求中缺少必要的參數。例如缺少 `Action` 參數。

   * 請求者沒有操作目標資源的權限。

* 5xx：表示請求已經失敗了。失敗的原因是 CDN 發生了內部錯誤。例如 CDN 服務不可用。


<span id="判斷-api-請求是否成功"></span>
## 判斷 API 請求是否成功

在您判斷 API 請求是否成功時，不建議您使用 CDN 的回應狀態碼。我們建議您使用以下判斷標準：


* 如果一個 API 請求成功，回應本文的 `ResponseMetadata` 結構體中不包含 `Error` 欄位。

* 其餘情況都被認為是請求失敗。您可以在 `ResponseMetadata` 結構體的 `Error` 欄位中找到相應的錯誤訊息。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">您的 API 請求可能會遇到以下情況：</div>



* <div data-tips="true" data-tips-type="tip">CDN 的回應狀態碼是 2xx，但是 <code>ResponseMetadata</code> 結構體中包含 <code>Error</code> 欄位。</div>



<div data-tips="true" data-tips-type="tip">在這種情況下，該 API 請求是失敗的。原因就是用戶端請求不符合 CDN 中的設定。例如：</div>



* <div data-tips="true" data-tips-type="tip">某個請求參數的值不合法。</div>


* <div data-tips="true" data-tips-type="tip">在您為網域名稱設定憑證時，憑證檔案沒有包含完整的憑證鏈。</div>



關於 CDN 中的常見錯誤，參見 [API 請求錯誤碼](https://docs.byteplus.com/en/docs/byteplus-cdn/api-error-code_zh-tw)。

<span id="範例回應"></span>
## 範例回應

<span id="api-請求成功的範例回應"></span>
### API 請求成功的範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "2021041510110201022510703416005FB0",
        "Action": "DescribeCdnData",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "singapore"
    },
    "Result": {...}
}
```


<span id="api-請求失敗的範例回應"></span>
### API 請求失敗的範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "2021041510110201022510703416005FB0",
        "Action": "DescribeCdnData",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "singapore",
        "Error": {
            "Code": "ResourceNotFound",
            "Message": "resource is not found"
        }
    }
}
```

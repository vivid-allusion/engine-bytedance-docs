---
title: "Range 來源伺服器請求"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/Range-get_zh-tw"
---

本文件介紹 CDN 中的 Range 請求來源伺服器特性。在大檔案下載、流媒體播放等場景中，啟用該功能可有效提升檔案的分發效率，降低 CDN 的來源伺服器流量、減輕來源伺服器的壓力。

<span id="656448bc"></span>
## 關於 Range 請求

Range 請求指的是那些包含了 Range 請求標頭的 HTTP 請求。該請求標頭指定了請求的檔案範圍，表示請求的是檔案的一個分片，而非整個檔案。例如，`Range:bytes=0-149` 表示請求的是檔案前 150 位元組。如果 Range 請求成功，伺服器的回應狀態碼是 206。

<span id="1c7040cd"></span>
## 注意事項


* 如果請求檔案不可快取，無論 Range 請求來源伺服器是否啟用，CDN 都會向來源伺服器透傳使用者 Range 請求。

* 如果來源伺服器不支援 Range 請求，啟用 Range 請求來源伺服器後，來源伺服器請求可能會失敗。

* 啟用 Range 請求來源伺服器後，針對同一個檔案，其所有分片的快取過期時間均以該檔案第一個被快取的分片為準。


<span id="7fcd1280"></span>
## 未啟用 Range 請求來源伺服器時 CDN 的行為

未啟用 Range 請求來源伺服器時，無論使用者請求是否為 Range 請求，只要 CDN 沒有快取過完整檔案，CDN 就會向來源伺服器請求完整檔案。

<span id="ff4d7338"></span>
## 啟用 Range 請求來源伺服器後的 CDN 行為

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">對於 2025\-09\-10 後新增的網域名稱，如果您對這些網域名稱啟用了 Range 請求來源伺服器，CDN 在請求來源伺服器時會增加探測機制。該機制可避免當檔案不可快取或者來源伺服器檔案有更新時來源伺服器下行流量增大的問題。</div>


<span id="a183c3b9"></span>
### 2025\-09\-10 起 CDN 對新增網域名稱的 Range 請求來源伺服器機制

對於用戶端 Range 請求，在請求來源伺服器時，CDN 會先傳送一個探測 Range 請求（Range: 0\-0）。基於來源伺服器回應，CDN 判斷請求檔案是否可快取。


* 如果檔案不可快取，CDN 向來源伺服器透傳使用者 Range 請求。

* 如果檔案可快取，CDN 基於已快取分片檢查檔案在來源伺服器上是否有更新。

   * 如果檔案無更新，CDN 按照您指定的分片大小（預設 1 MB）依次傳送來源伺服器請求。在獲得相應數量的分片後，CDN 返回用戶端所請求的分片。

   * 如果檔案有更新，CDN 按照使用者 Range 請求中指定的分片大小請求來源伺服器。


<span id="750b9b8c"></span>
### CDN 對 2025\-09\-10 前建立網域名稱的 Range 請求來源伺服器機制

請求來源伺服器時，CDN 將使用者 Range 請求的分片起始位置按照您指定的分片大小（預設 1 MB）向下取整，作為**第一個**來源伺服器 Range 請求的分片起始位置。收到來源伺服器回應時，


* 如果回應狀態碼是 200，CDN 回應完整檔案。

* 如果狀態碼是 206，CDN 判斷請求檔案是否可快取。

   * 如果檔案不可快取，CDN 向來源伺服器透傳使用者 Range 請求。

   * 如果檔案可快取，CDN 基於已快取分片檢查檔案在來源伺服器上是否有更新。

      * 如果檔案無更新，CDN 依次傳送**後續**來源伺服器 Range 請求。

      * 如果檔案有更新，CDN 先清理分片快取，再依次傳送**後續**來源伺服器 Range 請求。

         在獲得相應數量的分片後，CDN 返回用戶端所請求的分片。

* 如果回應狀態碼是 416，則 CDN 判斷請求檔案是否可快取。

   * 如果檔案不可快取，CDN 向來源伺服器透傳使用者 Range 請求。

   * 如果檔案可快取，CDN 回應 416 狀態碼。

* 如果是其他狀態碼，CDN 向來源伺服器透傳使用者 Range 請求。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">來源伺服器 Range 請求可能會發生分片越界行為。可能發生分片越界行為。例如：完整檔案的大小是 1.5 MB，使用者請求的檔案範圍是 14,000,000\-15,000,000。在這個情況下，對於 CDN 傳送的第一個來源伺服器 Range 請求，檔案範圍是 14,000,000\-15,048,576，超出了檔案的大小。</div>


<div data-tips="true" data-tips-type="tip">如果來源伺服器是阿里雲物件儲存（OSS），越界發生時 OSS 可能會有非預期回應。參見下方 OSS 相容配置中描述的解決方法。</div>


<span id="9d2e5f24"></span>
### AlibabaCloud OSS 相容配置

假設以下場景：


* 您的來源伺服器是 OSS 儲存桶。

* 來源伺服器 Range 請求的檔案範圍超過了完整檔案的大小。


在這個場景中，OSS 會回應 200 狀態碼並返回完整檔案。這會導致 OSS 的下行流量增大，可能會觸發 OSS 限流，影響來源伺服器請求的資料傳輸速度。

因此，如果您的來源伺服器是 OSS 中的儲存桶，推薦您為您的網域名稱設定 [來源伺服器 HTTP 請求標頭](https://docs.byteplus.com/en/docs/byteplus-cdn/origin-response-header_zh-tw)：「x\-oss\-range\-behavior:standard」。參見 [該標頭對於 OSS 行為的影響](https://www.alibabacloud.com/help/tc/oss/how-to-obtain-oss-resources-by-segmenting-http-range-requests)。

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_21e219d38eb626853beb6349020576c5.png) </span>

<span id="926a384d"></span>
## 操作步驟


1. 開啟 **回源 Range** 設定頁面。操作步驟參見 [網域名稱設定](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_zh-tw)。

2. 設定 **狀態** 為 **開啟**。

3. 設定分片大小，預設是 1 MB。較大的分片可以減少來源伺服器請求次數，但可能在網路不穩定時增加失敗重傳的成本；較小的分片則相反。

   * 如果單位是 MB，您可以指定的範圍是 1~40 MB，且必須是整數。

   * 如果單位是 KB，您只能指定 512 KB。

4. 點擊 **提交編輯**。


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_bc0e00df773d131ee2f0abebf46740a2.png) </span>

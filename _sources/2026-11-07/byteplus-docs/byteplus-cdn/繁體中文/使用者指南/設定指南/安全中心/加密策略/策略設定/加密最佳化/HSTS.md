---
title: "HSTS"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/HSTS_zh-tw"
---

本文件介紹如何在 BytePlus CDN 中對網域名稱啟用 HSTS。

<span id="hsts-概述"></span>
## HSTS 概述

HSTS 的全稱是 HTTP Strict Transport Security，是一種網路安全的策略機制。HSTS 的目的是保護使用者在存取 HTTPS 站點的期間免受降級攻擊和 cookie 劫持。在您對站點啟用 HSTS 後，站點的回應中會包含 `Strict-Transport-Security` 回應標頭。`Strict-Transport-Security` 回應標頭告知瀏覽器其向站點發送的每個請求都必須使用 HTTPS 協議。

`Strict-Transport-Security` 回應標頭還包含兩個參數。關於這兩個參數的描述，參見 [配置說明](https://docs.byteplus.com/en/docs/18/36329#%E9%85%8D%E7%BD%AE%E8%AA%AA%E6%98%8E)。

<span id="hsts-與-http-重新導向到-https-配置"></span>
## HSTS 與 "HTTP 重新導向到 HTTPS" 配置

CDN 提供的 "協議重新導向" 功能中，有一個 "HTTP 重新導向到 HTTPS" 的配置（以下簡稱 "HTTP 重新導向"）。該配置的作用是 CDN 將收到 HTTP 請求重新導向到 HTTPS 請求。

在進一步闡述 HSTS 之前，有必要先解釋 HSTS 與 "HTTP 重新導向" 的區別。

HTTP 是一個不安全的協議。當使用者在瀏覽器中指定 HTTP 協議向一個站點發送請求時，該請求可能會被劫持並重新導向到惡意站點。為了避免 HTTP 請求存取網域名稱，CDN 提供了以下兩個配置：


* HTTP 重新導向：在啟用 "協議重新導向" 後，您需要設置 **策略** 為 **將 HTTP 重新導向到 HTTPS**。

* HSTS。


<span id="http-重新導向的局限"></span>
### HTTP 重新導向的局限

在您配置了 HTTP 重新導向後，如果瀏覽器向 CDN 發送了一個 HTTP 請求，CDN 會返回 301 或者 302 回應狀態碼通知瀏覽器將 HTTP 請求跳轉到 HTTPS 請求。關於更多 HTTP 重新導向的資訊，參見 [協議重新導向](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-protocol-redirect_1-cn)。

但是，即使您配置了 HTTP 重新導向，使用者依然可以在瀏覽器中指定 HTTP 協議向 CDN 發送 HTTP 請求。雖然會被跳轉到 HTTPS 請求，這些 HTTP 請求在到達 CDN 前依然有被劫持的風險。

<span id="hsts-的優勢"></span>
### HSTS 的優勢

相比 HTTP 重新導向，HSTS 提供了一個更安全的方案。在您為網域名稱啟用 HSTS 後，CDN 的回應中會包含 `Strict-Transport-Security` 回應標頭。如果瀏覽器成功使用 HTTPS 協議對 CDN 發送過一次請求，瀏覽器就會快取該回應標頭。假設之後使用者再次在瀏覽器中指定 HTTP 協議存取 CDN。在發送請求前，瀏覽器會將 HTTP 轉換成 HTTPS。由於轉換過程在瀏覽器側發生，就能極大降低瀏覽器向 CDN 發送的 HTTP 請求的數量。同時，也降低了 HTTP 請求被劫持的風險。

<span id="hsts-回應標頭起作用的前提條件"></span>
#### HSTS 回應標頭起作用的前提條件

雖然 HSTS 方案更安全，但是要使瀏覽器遵循 `Strict-Transport-Security` 回應標頭將 HTTP 轉換成 HTTPS，以下條件必須滿足：


* 瀏覽器已快取了 `Strict-Transport-Security` 回應標頭。

* 已快取的回應標頭未過期。關於 `Strict-Transport-Security` 回應標頭的快取有效時間，參見 [配置說明](https://docs.byteplus.com/en/docs/18/36329#%E9%85%8D%E7%BD%AE%E8%AA%AA%E6%98%8E)。


在網域名稱啟用了 HSTS 後，CDN 在回應任何請求時都會返回 `Strict-Transport-Security` 回應標頭。但要使瀏覽器快取該回應標頭，瀏覽器必須成功使用 HTTPS 協議向 CDN 發送過一次請求。因此，在您啟用 HSTS 時，推薦您也啟用協議重新導向並設置 **策略** 為 **將 HTTP 重新導向到 HTTPS**。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">當您在 CDN 控制台中啟用 HSTS 時，CDN 會提示您是否需要啟用 HTTP 重新導向配置。參見 <a href="https://docs.byteplus.com/en/docs/18/36329#%E6%93%8D%E4%BD%9C%E6%AD%A5%E9%A9%9F">操作步驟</a>。</div>


<span id="瀏覽器與-cdn-的互動過程"></span>
#### 瀏覽器與 CDN 的互動過程

在您啟用了 HSTS 與 HTTP 重新導向後，如果使用者使用瀏覽器向 CDN 發送了一個 HTTP 請求，瀏覽器與 CDN 的互動過程如下：


1. 瀏覽器檢查是否存在已快取的 `Strict-Transport-Security` 回應標頭。

2. 由於瀏覽器快取中不存在該回應標頭，瀏覽器向 CDN 發送該 HTTP 請求。

3. CDN 收到該請求後，由於 HTTP 重新導向的配置，CDN 的回應狀態碼是 301 或 302。同時，由於 HSTS 的配置，回應中包含了 `Strict-Transport-Security` 回應標頭。此時，由於還未成功使用 HTTPS 協議向 CDN 發送過一次請求，瀏覽器不快取該回應標頭。

4. 由於 301 或 302 回應狀態碼，瀏覽器向 CDN 發送 HTTPS 請求。在回應中，CDN 同樣包含了 `Strict-Transport-Security` 回應標頭。假設該回應標頭的有效時間是 10 分鐘，並且該 HTTPS 請求成功獲取了請求的檔案。

5. 由於 HTTPS 請求成功，瀏覽器對 `Strict-Transport-Security` 回應標頭進行快取。


在 10 分鐘內，假設該使用者使用瀏覽器再次向 CDN 發送 HTTP 請求。此時，瀏覽器與 CDN 的互動過程如下：


1. 瀏覽器檢查是否存在已快取的 `Strict-Transport-Security` 回應標頭。

2. 由於瀏覽器快取中存在該回應標頭，瀏覽器檢查該回應標頭是否已過期。

3. 由於該回應標頭未過期，瀏覽器就將 HTTP 轉換為 HTTPS 並向 CDN 發送該請求。


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">如果快取的 <code>Strict-Transport-Security</code> 回應標頭已過期，當該使用者向 CDN 發送 HTTP 請求時，會重複 "瀏覽器與 CDN 的互動過程" 中描述的步驟。</div>


* <div data-tips="true" data-tips-type="warning">需要注意的是，即使您已啟用了 HSTS 與 HTTP 重新導向，CDN 收到的 HTTP 請求是無法杜絕的。因為在以下任意情況下，瀏覽器不會將 HTTP 轉換成 HTTPS：</div>


   * <div data-tips="true" data-tips-type="warning">瀏覽器快取中不存在 <code>Strict-Transport-Security</code> 回應標頭。</div>


   * <div data-tips="true" data-tips-type="warning">瀏覽器快取中的 <code>Strict-Transport-Security</code> 回應標頭已過期。</div>



<span id="前提條件"></span>
### 前提條件

要開啟該配置，網域名稱必須已經開啟了 HTTPS 加密服務。

<span id="操作步驟"></span>
## 操作步驟


1. 打開 **HSTS** 設定頁面。操作步驟參見 [網域名稱設定](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_zh-tw)。

2. 在 **HSTS** 下方，設置 **狀態** 為 **開啟**。

&nbsp;

   如果此時您還未啟用協議重新導向，或者您已經啟用了協議重新導向但是 **策略** 不是 **將 HTTP 重新導向到 HTTPS**，CDN 會詢問您是否要配置HTTP 重新導向。其原因參見 "HSTS 回應標頭起作用的前提條件"。

   * 如果您點擊 **確認**，CDN 會配置 HTTP 重新導向。在您點擊 **確認** 前，請充分評估 HTTP 重新導向這個設置對您業務的影響。

   * 如果您點擊 **忽略**，CDN 會保留當前協議重新導向的設置。

3. 參照以下配置說明。

4. 配置完成後，點擊 **儲存**。


<span id="配置說明"></span>
### 配置說明


|**配置** |**說明** |
|---|---|
|快取過期時間 |表示 `Strict-Transport-Security` 回應標頭在客戶端瀏覽器中的快取過期時間。該配置對應`Strict-Transport-Security` 回應標頭的 `max-age` 參數。在發送一個 HTTP 請求前，瀏覽器會檢查其快取的 `Strict-Transport-Security` 回應標頭是否已經過期。如果該回應標頭已過期，瀏覽器不會將 HTTP 轉換成 HTTPS。<br><br>&nbsp;<br><br>您最長可以設置的時間是 31,536,000 秒，表示 365 天。如果您設置過期時間為 `0`，其效果等同於禁用 HSTS。<br><br>&nbsp;<br><br>需要留意的是，對於瀏覽器收到的每個回應，如果回應中包含 `Strict-Transport-Security` 回應標頭，瀏覽器會使用收到的回應標頭的過期時間來替換快取的回應標頭的過期時間。 |
|子網域 |表示 HSTS 配置是否應用於子網域站點。該配置有以下選項：<br><br><br>* **不使用**：表示 HSTS 配置不應用於子網域站點。<br><br>* **應用**：表示 HSTS 配置應用於子網域站點。此時，回應標頭會包含 `includeSubDomains` 參數。<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">如果您設置 <strong>子網域</strong> 為 <strong>包含</strong>，CDN 返回的回應標頭是告知瀏覽器向所有子網域發送的請求也必須使用 HTTPS 協議。此時，請確保子網域站點必須是可以使用 HTTPS 協議訪問的。並且，子網域也要有一個類似配置將子網域的 HTTP 請求重新導向到 HTTPS 請求。</div><br> |


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d5c90b16e9e84e128420ac18e1eab90d~tplv-goo7wpa0wc-image.image) </span>

**舉例**


* 例子 1：您指定過期時間是 6 秒並且包含子網域。此時，CDN 實際返回的回應標頭如下：

   * `Strict-Transport-Security: max-age=6;includeSubDomains`

* 例子 2：您指定過期時間是 1 天並且不包含子網域。此時，CDN 實際返回的回應標頭如下：

   * `Strict-Transport-Security: max-age=86400`


<span id="更多資訊"></span>
## 更多資訊

<span id="如何在瀏覽器中管理-hsts-配置"></span>
### 如何在瀏覽器中管理 HSTS 配置

下面以 Google Chrome 和 Microsoft Edge 為例，闡述如何在瀏覽器中管理 HSTS 配置。

在 Chrome 或 Edge 中，訪問以下 URL：


* `chrome://net-internals/#hsts`


在打開的頁面中，您可以：


* 將一個網域名稱添加到瀏覽器的 HSTS 快取中。

* 從瀏覽器的 HSTS 快取中刪除指定的網域名稱。

* 查詢一個網域名稱是否存在於瀏覽器的 HSTS 快取中。

   * 如果該網域名稱不存在，查詢結果是 `Not found`。

   * 如果該網域名稱存在，查詢結果會展示該網域名稱的 HSTS 配置資訊。在配置資訊中，`dynamic_sts_observed` 表示瀏覽器快取該網域名稱的時間，時間格式是 Unix 時間標記。`dynamic_sts_expiry` 表示該網域名稱在 HSTS 快取中的過期時間。


在您查詢一個網域名稱時，結果資料可能會有 1 分鐘的延遲。

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bceca7d3f4666d763c878521f8ae8164.png) </span>

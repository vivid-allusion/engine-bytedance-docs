---
title: "URL 驗證概覽"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/signed-url-authentication-overview_zh-tw"
---

本文件介紹如何在 BytePlus CDN 中配置 URL 驗證。

<span id="背景"></span>
## 背景

CDN 提供了 "Referer 防盜鏈"、"Origin 防盜鏈" 和 "IP 黑白名單" 對用戶請求進行過濾。但是在某些情況下，Referer、Origin 和 IP 可以被偽造，容易造成您站點內容被惡意盜用。如果您對於站點內容的安全性有很高的要求，可以採用 URL 驗證。

<span id="工作原理"></span>
## 工作原理

當一個客戶端發送請求至伺服器端時，客戶端按照您設定的驗證規則計算簽名，並在請求中包含這個簽名。伺服器端收到請求後，對簽名進行校驗。只有在校驗通過的情況下，才允許客戶端請求。

本文件通過 [示例代碼](https://docs.byteplus.com/en/docs/18/36282#%E7%B0%BD%E5%90%8D%E8%A8%88%E7%AE%97%E7%A4%BA%E4%BE%8B%E4%BB%A3%E7%A2%BC) 演示了客戶端簽名邏輯的實現。同時也描述了如何在 CDN 中配置請求的驗證邏輯。

<span id="驗證流程"></span>
### 驗證流程


1. 您在 CDN 控制台對域名配置 URL 驗證。CDN 提供了多種驗證類型的供您選擇和配置。每種驗證類型提供不同的簽名算法。

2. 客戶端發送帶簽名的請求到域名。

3. 根據配置的 URL 驗證規則，CDN 做以下驗證：

   * 驗證 CDN 計算得到的簽名和客戶端請求中包含的簽名是否一致。該驗證使用的邏輯如下：

      * MD5 值轉化成小寫進行比較。

   * 判斷請求是否過期。如果滿足以下條件，則請求未過期：

      * CDN 收到請求的時間 <= 請求中包含的時間標記 + 簽名的有效時間

4. 如果驗證通過，CDN 允許該請求。如果不通過，則拒絕請求，返回 403 回應狀態碼。


URL 驗證能夠有效防止您站點的內容被惡意用戶盜刷。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">URL 驗證在 CDN 進行，您站點的配置無需變動。</div>


* <div data-tips="true" data-tips-type="tip">開啟 URL 驗證後，所有客戶端的請求都必須包含簽名。否則請求會失敗。</div>


* <div data-tips="true" data-tips-type="tip">如果驗證類型是 E 類型，CDN 會在來源伺服器請求中包含使用者請求中的簽名。</div>


* <div data-tips="true" data-tips-type="tip">如果驗證類型不是 E 類型，CDN 不會在來源伺服器請求中包含簽名。如果来源伺服器也啟用了 URL 驗證，來源伺服器請求會失敗。您需要關閉来源伺服器上的 URL 驗證。</div>



<span id="前提條件"></span>
## 前提條件

如果您的站點已經配置了 URL 驗證，您必須關閉它，然後按照以下步驟在 CDN 中對網域名稱配置相同的 URL 驗證邏輯。

<span id="操作步驟"></span>
## 操作步驟


1. 打開 **URL 驗證** 設定頁面。操作步驟參見 [網域名稱設定](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_zh-tw)。

2. 在 **URL 驗證** 下方，設置 **狀態** 為 **開啟**。

3. 選擇一個 URL 驗證類型，並進行相應的配置。

   * [A 類型](https://docs.byteplus.com/en/docs/byteplus-cdn/Type-A_zh-tw)

   * [B 類型](https://docs.byteplus.com/en/docs/byteplus-cdn/Type-B_zh-tw)

   * [C 類型](https://docs.byteplus.com/en/docs/byteplus-cdn/Type-C_zh-tw)

   * [D 類型](https://docs.byteplus.com/en/docs/byteplus-cdn/Type-D_zh-tw)

   * [E 類型](https://docs.byteplus.com/en/docs/byteplus-cdn/Type-E_zh-tw)

   * [F 類型](https://docs.byteplus.com/en/docs/byteplus-cdn/typef_zh-tw)

4. 配置完成後，點擊 **保存**。


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_0e94fb02521a0124fe988943e40a203b.png) </span>

<span id="簽名計算示例代碼"></span>
## 簽名計算示例代碼

用戶端請求中包含的簽名可以由一個獨立的簽名伺服器提供，也可以由用戶端生成。您可以參考以下示例代碼中展示的簽名算法，在用戶端或者簽名伺服器使用相應的編程語言實現簽名計算邏輯。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Python 示例代碼要求 Python 3.0。</div>


<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_764b0d07610e99ad909f897f2c2b4789.txt" name="URL-Auth-for-PHP.txt">URL-Auth-for-PHP.txt</Attachment>


<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_f4de2bc0c6c583787678290aa04fb025.txt" name="URL-Auth-for-Go.txt">URL-Auth-for-Go.txt</Attachment>


<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_17238c7e88c379eca0ff1708ce4fbb68.txt" name="URL-Auth-for-Python.txt">URL-Auth-for-Python.txt</Attachment>


<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/68b02630a2a34e6b862915dec9f1845f~tplv-goo7wpa0wc-image.image" name="URL-Auth-for-Java.txt">URL-Auth-for-Java.txt</Attachment>

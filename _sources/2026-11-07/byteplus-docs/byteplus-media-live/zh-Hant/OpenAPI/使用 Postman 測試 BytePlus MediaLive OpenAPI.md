---
title: "使用 Postman 測試 BytePlus MediaLive OpenAPI"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-using-postman-to-test-the-byteplus-medialive-openapi-zh-TW"
---

若要快速測試 BytePlus MediaLive OpenAPI，可以使用官方的 Postman 集合。本主題提供逐步操作說明，指導如何將集合分叉到你的工作區、配置認證憑證（AK/SK），並發送範例 API 請求。

<span id="ee247ee9"></span>
## 先決條件


* 一個 Postman 帳戶。

* 一個 BytePlus 帳戶。如需更多資訊，請參閱[註冊 BytePlus 帳戶](https://docs.byteplus.com/en/byteplus-platform/docs/signing-up-your-account)。

* [啟用 BytePlus MediaLive 服務](https://docs.byteplus.com/en/byteplus-media-live/docs/getting-started#da5a6a63)。

* 服務啟用後，登入[BytePlus 控制台](https://console.byteplus.com/)，點擊頁面右上角的帳戶名稱，然後選擇**IAM** \> **金鑰管理**以取得帳戶的 Access Key ID（AK）和 Secret Access Key（SK），這些憑證用於 API 請求認證。


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7f6dc1b6f2bc466785242136a7995c07~tplv-goo7wpa0wc-image.image) </span>

<span id="f11782de"></span>
## 操作流程


1. 登入[Postman 線上平台](https://www.postman.com/byteplus-medialive-docs/workspace/byteplus-medialive)。

2. 在左側點擊**BytePlus MediaLive OpenAPI**，然後點擊**Fork**，將整個集合分叉到自己的工作區。


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4c6064319e6e44f982725c3f053fcbff~tplv-goo7wpa0wc-image.image) </span>


3. 在自己的工作區中，選擇 DescribeDomain API，然後點擊**Headers**標籤頁。

4. 將**Headers**標籤頁中的 AK 和 SK 值替換為你在[先決條件](https://docs.byteplus.com/docs/byteplus-media-live/docs-using-postman-to-test-the-byteplus-medialive-openapi#Prerequisites)中取得的 AK 和 SK。

5. 點擊**Body**標籤頁，並在`DomainList`中將域名替換為你自己的域名。

6. 點擊**Send**以發送請求。


你可以在頁面底部查看回應。

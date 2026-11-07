---
title: "使用 Postman 调用 BytePlus Live API"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/shi-yong-postman-hu-jiao-byteplus-live-api-zh-TW"
---

要測試和除錯 BytePlus Live API，可以使用廣受歡迎的 API 客戶端 Postman。本指南提供逐步操作說明，指導如何分支官方集合、設定驗證標頭，以及發送您的第一個請求。

<span id="152c47a4"></span>
## 先決條件


* 一個 Postman 帳戶。

* 一個 BytePlus 帳戶。如需更多資訊，請參閱[註冊 BytePlus 帳戶](https://docs.byteplus.com/en/byteplus-platform/docs/signing-up-your-account)。

* AccessKey ID（AK）與 Secret Access Key（SK）。要取得這些資訊，請前往[BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/) \> **使用者檔案** \> **IAM** \> **金鑰管理**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/36d6e087508a4a61914ea025d4158706~tplv-goo7wpa0wc-image.image) </span>


<span id="fbe4cf82"></span>
## 背景

Postman 提供直觀的介面來發送 API 請求，並可輕鬆檢查與分析回應。它支援多種請求方法，包括 GET、POST、PUT 和 DELETE，並允許您在請求中新增標頭、參數及其他資料。憑藉其強大的功能與直觀介面，Postman 已成為 API 開發與測試不可或缺的工具。

<span id="afff1f6d"></span>
## 操作流程


1. 可使用 Postman 線上版或離線版。

   * Postman 線上版：登入[Postman 線上平台](https://www.postman.com/livesaas/workspace/byteplus-live/overview)。在左側點擊**BytePlus Live Open API**，再點擊**Fork**，將 BytePlus Live 集合分支到您的工作區。您必須分支集合，因為目前無法從公開工作區發送請求。如需建立分支的詳細資訊，請參閱[建立分支](https://docs.byteplus.com/docs/byteplus-livesaas/docs-using-postman-to-call-byteplus-live-apis#creating-a-fork)。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6ae8dcfea7534baf9fbb01edfc310152~tplv-goo7wpa0wc-image.image) </span>

   * Postman 離線版：點擊**Import**並選擇以下檔案。

      <Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eed499b8cade40f6ad95d12aa5b36727~tplv-goo7wpa0wc-image.image" name="openapi-call-example.postman_collection.json">openapi-call-example.postman_collection.json</Attachment>
      

&nbsp;

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4d93480913664f6c9e15b3d1aa00ef44~tplv-goo7wpa0wc-image.image) </span>

2. 點擊**檢視更多操作**圖示，並選擇**Duplicate**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a8c95d7e5c2c4d24a49e9054805f730a~tplv-goo7wpa0wc-image.image) </span>

3. 根據需求修改 API 名稱、請求方法、請求 URI、查詢參數及 body 參數。如需更多資訊，請參閱您欲呼叫之 API 的相關文件。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f521e8d41bab40858db6b4da32fd6674~tplv-goo7wpa0wc-image.image) </span>

4. 在**Headers**標籤頁中，將`AccessKey`與`SecretKey`的值替換為您於[先決條件](https://docs.byteplus.com/docs/byteplus-livesaas/docs-using-postman-to-call-byteplus-live-apis#152c47a4)部分取得的資訊。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7b6869ae77ac4b169f829fe5806c1692~tplv-goo7wpa0wc-image.image) </span>

5. 點擊**Send**以發送請求。

6. 在頁面底部檢視回應。


<span id="ae8fd9f5"></span>
## 故障排除

若回應返回錯誤，請參閱[共用錯誤與狀態碼](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-error-and-status-codes)以取得更多資訊。

為避免常見錯誤，請確保符合以下要求：


* AK 與 SK 必須與[先決條件](https://docs.byteplus.com/docs/byteplus-livesaas/docs-using-postman-to-call-byteplus-live-apis#152c47a4)部分取得的金鑰一致。

* 所有必要參數皆已新增。

* 新增的參數及其對應值皆正確。

* 請求方法與請求 URI 皆正確。


若問題仍然存在，請聯絡您的業務代表協助。若您沒有業務代表，請點擊[此處](https://www.byteplus.com/en/contact)填寫聯絡表單，BytePlus 業務團隊成員將與您聯繫。

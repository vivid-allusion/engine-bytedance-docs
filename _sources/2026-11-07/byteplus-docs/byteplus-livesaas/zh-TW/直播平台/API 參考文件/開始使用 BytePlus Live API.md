---
title: "開始使用 BytePlus Live API"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/kai-shi-shi-yong-byteplus-live-api-zh-TW"
---

BytePlus Live API 是基於 HTTP 的 RESTful API，並採用簽名演算法進行身份驗證。API 的請求與回應內容均採用 JSON 格式。本主題將帶您了解如何呼叫 BytePlus Live API 的流程。


1. 瞭解限制與配額

2. 註冊帳戶

3. 完成身份驗證

4. 首次呼叫 API


<span id="274a4dca"></span>
## 瞭解限制與配額

每個 API 的呼叫頻率限制為每個帳戶 ID 每分鐘 120 次（除非另有說明）。

<span id="399d79a6"></span>
## 註冊帳戶

在呼叫 BytePlus Live API 之前，請依照 [註冊 BytePlus 帳戶](https://docs.byteplus.com/en/byteplus-platform/docs/signing-up-your-account) 的指引註冊帳戶。

您可以使用 BytePlus 帳戶或具備特定權限的 IAM 使用者來呼叫 API。例如，若要使用 IAM 使用者呼叫 [UpdateHostAccount](https://docs.byteplus.com/en/docs/byteplus-livesaas/updatehostaccount) 以新增或更新主機帳戶，該 IAM 使用者必須擁有 **Marketing toolkits** \> **Edit** 權限。如需新增 IAM 使用者的詳細資訊，請參閱 [管理使用者、組織與角色](https://docs.byteplus.com/docs/byteplus-livesaas/guan-li-shi-yong-zhe-zu-zhi-yu-jue-se-zh-TW)。

<span id="bc65fb59"></span>
## 完成身份驗證

BytePlus Live API 的身份驗證會為 API 請求加簽，以驗證您的身份並防止請求在傳輸過程中遭到惡意攔截。如需詳細資訊，請參閱 [API 驗證](https://docs.byteplus.com/docs/byteplus-livesaas/api-yan-zheng-zh-TW)。

進行 API 身份驗證時，請使用發起呼叫帳戶的 Access Key ID 與 Secret Access Key（可為您的 BytePlus 帳戶或 IAM 使用者）。

<span id="4d5a8fc2"></span>
## 首次呼叫 API

BytePlus Live API 需要特定的請求結構。如需詳細資訊，請參閱 [API HTTP 請求](https://docs.byteplus.com/docs/byteplus-livesaas/api-http-qing-qiu-zh-TW)。

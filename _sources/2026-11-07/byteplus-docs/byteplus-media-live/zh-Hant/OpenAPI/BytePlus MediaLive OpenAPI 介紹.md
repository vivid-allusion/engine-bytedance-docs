---
title: "BytePlus MediaLive OpenAPI 介紹"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-getting-started-with-your-api-zh-TW"
---

BytePlus MediaLive OpenAPI 可讓你管理你的網域名稱與串流，使用如轉碼、錄製等增值服務，查詢使用數據與串流統計資料，以及更多功能。

如需 BytePlus MediaLive OpenAPI 端點的完整列表，請參閱 [BytePlus MediaLive OpenAPI 概述](https://docs.byteplus.com/byteplus-media-live/docs/openapi-overview)。

我們建議你使用 [Server SDK](https://docs.byteplus.com/byteplus-media-live/docs/server-sdk) 來呼叫 OpenAPI。Server SDK 提供如簽名生成與常見 OpenAPI 操作等功能。

<span id="Getting started"></span>
## 快速入門


1. 為你的 BytePlus 帳戶啟用 BytePlus MediaLive。詳細資訊請參閱 [啟用服務](https://docs.byteplus.com/docs/byteplus-media-live/docs-getting-started#da5a6a63)。

2. 服務啟用後，請登入 [BytePlus 控制台](https://console.byteplus.com/)，點擊頁面右上角的帳戶名稱，然後選擇 **IAM** \> **金鑰管理**，以取得你的帳戶 Access Key ID（AK）與 Secret Access Key（SK），這些資訊用於 API 請求驗證。


<span id="Limitation"></span>
## 限制

每個 API 端點都有呼叫頻率限制，若超過限制將會觸發限流。請參閱各端點的參考文件以獲取相應的呼叫頻率。

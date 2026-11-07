---
title: "AI live 帳戶資料隔離"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/doc-118704"
---

AI Live 會根據帳戶層級隔離資料，以防止未經授權存取或修改其他使用者的資料。

存取控制模型如下：


* **子帳戶**僅能存取由自己建立或擁有的資料。

* **管理員帳戶**可以存取與帳戶相關的所有資料，包括屬於子帳戶的資料。

* **關於 AI 人物配額**，每個帳戶都有獨立的配額，且僅消耗自身的配額。不同帳戶的配額互不影響。例如，若總配額為 13，且分配給兩個子帳戶各 5 個配額，管理員帳戶則保留 3 個配額供自身使用。每個子帳戶最多可獨立訓練其分配的 5 個配額，與其他帳戶無關。目前，您可聯繫 BytePlus Support，提供子帳戶電子郵件地址及所需配額數量以進行配額分配。


對於非 AI Live 房間，您可以為使用者分配角色，以分配及管理資源存取權限。詳細資訊請參閱[新增角色](https://docs.byteplus.com/docs/byteplus-livesaas/guan-li-shi-yong-zhe-zu-zhi-yu-jue-se-zh-TW#08751041)。

<span id="433a996b"></span>
### 依功能區分的帳戶可見性

下表說明各功能中子帳戶與管理員帳戶的資料可見性。


|**功能** |**資源** |**子帳戶可見性** |**管理員帳戶可見性** |
|---|---|---|---|
|AI Live |AI 人物、語音、知識庫、產品，以及來自 TikTok Shop、Shopify 與內部系統的整合商店 |僅限自身資料。例如，子帳戶僅能查看其自行建立的 AI 人物、語音、知識庫、產品及整合商店；無法查看其他子帳戶或管理員帳戶所建立的 AI 人物、語音、知識庫、產品及整合商店。 |帳戶下所有資源。 |
|AI Analysis |主播評分與直播審核任務 |僅限自身資料。例如，子帳戶僅能查看其建立的主播評分與直播審核任務，無法查看其他子帳戶建立的任務。 |帳戶下所有資源。 |


<span id="2851f01d"></span>
## 服務中心

AI Live 與 AI Analysis 的**服務中心**頁面僅限管理員帳戶使用。子帳戶無法存取**服務中心**頁面。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2fb09b6b3d6a4e888569431499623528~tplv-goo7wpa0wc-image.image) </span>

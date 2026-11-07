---
title: "將觀眾踢出或封鎖觀眾的 IP 位址"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/jiang-guan-zhong-ti-chu-huo-feng-suo-guan-zhong-de-zh-TW"
---

為了維持秩序並確保直播期間有良好的觀看體驗，您可以透過將擾亂秩序的觀眾踢出房間或封鎖其 IP 位址來管理這些觀眾。本指南提供逐步操作說明，協助您使用這些功能，快速移除不守規則的參與者。

<span id="43e253f7"></span>
## 先決條件


* 需有 BytePlus 帳戶或具備 Live control \> Edit 權限的 IAM 使用者。如需新增 IAM 使用者的詳細資訊，請參閱 [管理使用者、組織與角色](https://docs.byteplus.com/docs/byteplus-livesaas/guan-li-shi-yong-zhe-zu-zhi-yu-jue-se-zh-TW)。

* 聊天互動選單。如需更多資訊，請參閱 [管理聊天區域](https://docs.byteplus.com/docs/byteplus-livesaas/guan-li-liao-tian-qu-yu-zh-TW)。


<span id="8169c2a5"></span>
## 使用情境

在直播期間，可能會出現擾亂直播間並影響其他觀眾體驗的行為，例如：


* 濫發訊息

* 發送不當評論

* 散播虛假資訊

* 騷擾其他觀眾


為了維持直播順利進行，您可以將觀眾踢出直播間或封鎖觀眾的 IP 位址。

<span id="076aca59"></span>
## 操作流程

您可以在聊天互動選單或 **觀眾列表**頁面執行這些操作。這兩個位置皆可在 BytePlus Live 控制台及網頁版直播頁面使用。

各位置的操作步驟大致相同。本主題以 BytePlus Live 控制台的聊天互動選單為例。


1. 登入 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)。

2. 在直播間列表中，點擊以開啟直播間。

3. 於 **Live control**頁面的聊天互動選單中，點擊評論右側的省略號圖示，然後選擇 **踢出** 或 **封鎖 IP**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/90ae8cf49d0c48dea8f62a77920cb072~tplv-goo7wpa0wc-image.image) </span>

   * 將觀眾踢出直播間：選擇 **踢出**後，發送評論的觀眾會被踢出直播間，且無法再次進入。該評論也會從公開聊天中刪除。若要允許觀眾重新進入直播間，請點擊該觀眾發送評論右側的省略號圖示，並選擇 **取消踢出**。

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">觀眾會以其使用者 ID 和裝置 ID 進行識別。若被踢出的觀眾以不同登入方式或裝置重新加入，系統會將其視為新觀眾並允許進入房間。      </div>
      

   * 封鎖觀眾的 IP 位址：選擇 **封鎖 IP**後，發送評論的觀眾會被踢出直播間，且來自被封鎖 IP 位址的任何人都無法進入直播間。該評論也會從公開聊天中刪除。若要解除 IP 位址封鎖，請點擊該觀眾發送評論右側的省略號圖示，並選擇 **解除封鎖**。


<span id="2e625261"></span>
## 觀眾所見內容


|功能 |於電腦端 |於行動裝置端 |
|---|---|---|
|被踢出直播間 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1fefad6f79fb48f5a197beb1df8a2ede~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a10c51f2ad34744b04f2af8486740af~tplv-goo7wpa0wc-image.image) </span> |
|IP 位址被封鎖 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/523aa832b4b646e5ab22d166a0ff2d3d~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/efe708030403412c9304a418155a8dbf~tplv-goo7wpa0wc-image.image) </span> |

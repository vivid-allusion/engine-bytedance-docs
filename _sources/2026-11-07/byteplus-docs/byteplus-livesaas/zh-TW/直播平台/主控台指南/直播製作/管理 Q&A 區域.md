---
title: "管理 Q&A 區域"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/guan-li-q-a-qu-yu-zh-TW"
---

為了提升直播期間觀眾的互動，可以使用 Q&A 功能。本指南提供逐步操作說明，協助你新增 Q&A 選單、設定相關選項，並即時管理討論。你將學會如何管理從問題數量限制、用戶權限，到釘選、禁言及匯出 Q&A 資料等即時操作。

<span id="51a16f7b"></span>
## 前提條件

你必須擁有 BytePlus 帳戶，或是具備下列權限的 IAM 使用者。如需新增 IAM 使用者的詳細資訊，請參閱 [管理使用者、組織與角色](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。


* Producer \> 編輯權限：用於設定 Q&A 選單。

* Live control \> 編輯權限：用於執行發佈及回覆問題等操作。


<span id="7eab7b5b"></span>
## 操作流程


1. 登入 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)。

2. 在直播間列表中，點選一個直播間以開啟。

3. 依下列步驟新增 Q&A 選單：

   1. 在左側導覽窗格，點選 **Producer** \> **Menus**。

   2. 點選 **Edit menu**。

   3. 在彈出對話框中點選 **Add**。

   4. 輸入選單名稱，並於 **Menu type** 下拉選單選擇 **Q&A**。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/83e67d33653a4e9fa29cdc32d26bc06a~tplv-goo7wpa0wc-image.image) </span>

   5. （可選）拖曳以調整選單順序。

   6. 點選 **Confirm**。

   7. 於 **Menus** 頁面點選 **Save**。

4. 在 Q&A 選單下，你可以設定以下選項。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d7d1d38fe1c44cb8a5c051c57c4842fb~tplv-goo7wpa0wc-image.image) </span>

   * 開啟 **Viewers ask questions** 開關，允許觀眾在觀看頁面發問。若此開關關閉，觀眾僅能回覆主持人發佈的問題。

   * 於 **Maximum number of questions per viewer** 欄位，設定每位觀眾可發問的最大數量。

   * 於 **Minimum sending interval** 欄位，設定用戶連續留言的最短間隔時間。數值範圍：[1,300]。例如，若設定為 3，則主持人與觀眾需間隔 3 秒（自上次提交後）才能再次發問或回覆。

   * 於 **Text box placeholder** 欄位，自訂 Q&A 輸入框顯示的預設文字。

   * 於 **Host's nickname** 欄位，變更 Q&A 區域中主持人的顯示名稱。

   * 選擇 Q&A 區域在電腦端的顯示模式。

5. 在 **Live control** 頁面，你可以於 Q&A 面板執行下列操作。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9052fa9f05d4411e9554486de6ac6eaa~tplv-goo7wpa0wc-image.image) </span>

   * 依狀態或內容篩選問題。支援模糊搜尋。

   * 依時間或熱門程度排序問題或回覆。

   * 發佈問題。

   * 回覆問題。

   * 將問題或回覆釘選至頂部。

   * 對問題或回覆按讚。

   * 從觀看頁面刪除問題或回覆。刪除問題時，其所有回覆也會一併從觀看頁面移除。

   * 將觀眾設為禁言或解除禁言。將滑鼠移至問題或回覆旁的省略號圖示，選擇 **Mute**，即可將發送者設為禁言。被禁言的觀眾無法發問或回覆問題。若要解除禁言，將滑鼠移至該觀眾發送的問題或回覆旁的省略號圖示，並選擇 **Unmute**。

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">觀眾會根據其 UID 被靜音，而 UID 會因登入方式而異。例如，您將僅以暱稱登入直播間的觀眾靜音。該觀眾隨後選擇以手機號碼登入直播間。如此一來，該觀眾的 UID 與被靜音的 UID 不同，因此可以發表及回覆問題。      </div>
      

   * 點選輸入框上方由左數第二個圖示，可切換是否允許觀眾發問。

   * 點擊文字框上方由左數第三個圖示，以啟用或停用人工審核功能。啟用此功能後，新的提問與回覆僅作者可見，直到審核通過。點擊問題或回覆旁的 **√** 以通過審核。審核通過後，該問題或回覆將在觀看頁面對所有人可見。

   * 點擊**Export data**圖示，將問答數據匯出至本地檔案。

   * 點擊**Clear comments**圖示，清除觀看頁面的問答區。


<span id="9979ed78"></span>
## 觀眾所見內容


<Tabs>
<Tab zoneid="s1WrX0oGah" title="On PCs">
<TabTitle>On PCs</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/613cc0a1ce654177b887ad69d53e1313~tplv-goo7wpa0wc-image.image) </span>


</Tab>
<Tab zoneid="ZVz0WXHczv" title="On mobile devices">
<TabTitle>On mobile devices</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9a806fea82f74e31a98213ef03a074a0~tplv-goo7wpa0wc-image.image) </span>


</Tab>
</Tabs>

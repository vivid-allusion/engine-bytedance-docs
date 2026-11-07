---
title: "新增 IAM 使用者、組織或角色"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/guan-li-shi-yong-zhe-zu-zhi-yu-jue-se-zh-TW"
---

本文檔說明如何新增 IAM 使用者、組織或角色，包括將組織和角色分配給使用者，這能讓 IAM 使用者的權限管理更加細緻且靈活。

<span id="25abd8c1"></span>
## 前提條件

需具備 BytePlus 帳戶或擁有 **帳戶總覽** \> **編輯** 權限的 IAM 使用者。如需更多資訊，請參閱 [註冊 BytePlus 帳戶](https://docs.byteplus.com/en/byteplus-platform/docs/signing-up-your-account)。

<span id="241e6b39"></span>
## 新增使用者


1. 登入 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)。

2. 在 BytePlus Live 的選單列中，點擊 **授權**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1055d6b0ea5d4435a6b7c2e8aa636081~tplv-goo7wpa0wc-image.image) </span>

3. 於 **使用者**頁面，點擊 **新增使用者**。

4. 在彈出的 **新增使用者**對話框中，點擊 **新增使用者**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e52312be7bc475780d3566fb9d77214~tplv-goo7wpa0wc-image.image) </span>

5. 完成以下設定後，點擊 **確定**。此時，使用者將同時新增至 BytePlus Live 的 **授權** \> **使用者**頁面，以及 BytePlus 的 [IAM > 身份管理 > 使用者](https://console.byteplus.com/iam/identitymanage/user)頁面。

   
   |**配置** |**說明** |**注意事項** |
   |---|---|---|
   |用戶類型 |選擇 **電子郵件**。目前僅能透過電子郵件新增用戶。 |用戶新增後無法更改電子郵件地址。請確保輸入正確的電子郵件地址。 |
   |用戶帳號 |輸入用戶的電子郵件地址，該地址將作為 **子帳戶用戶名**，用於在 [IAM 用戶登入](https://console.byteplus.com/auth/login/user/?redirectURI=%2Flivesaas%2FaccountManagement%2FroleManage)頁面登入 BytePlus Live 控制台。 |無 |
   |用戶暱稱 |輸入用戶的暱稱。 |暱稱不得超過 16 個字元，且僅可包含英文字母、數字及中文字符。 |
   |所屬組織 |選擇用戶所屬的組織。如需了解如何新增組織，請參閱 [管理組織](https://docs.byteplus.com/docs/byteplus-livesaas/guan-li-shi-yong-zhe-zu-zhi-yu-jue-se-zh-TW#442b626b)。 |無 |
   |角色 |選擇一個或多個角色分配給此用戶。如需了解如何建立角色，請參閱 [新增角色](https://docs.byteplus.com/docs/byteplus-livesaas/guan-li-shi-yong-zhe-zu-zhi-yu-jue-se-zh-TW#08751041)。 |若未選擇角色，系統將指派預設角色給用戶，且用戶僅能查看及編輯自己建立的直播間。 |
   

   使用者新增後，將收到一封電子郵件，並可使用該郵件中的登入網址、電子郵件地址及密碼登入 BytePlus Live 控制台。

6. 您也可以執行以下操作：

   * 可依暱稱或電子郵件地址搜尋使用者。支援模糊搜尋。

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">英文字母不區分大小寫。      </div>
      

   * 在 **操作**欄中點擊 **編輯**，然後在彈出的 **編輯使用者**對話框中按需修改使用者的暱稱、組織及角色。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/706bfdd557344c66900d996200aee63c~tplv-goo7wpa0wc-image.image) </span>

   * 在 **操作**欄中點擊 **重設密碼**，以重設使用者登入控制台所用的密碼。系統將發送一封包含隨機新密碼的電子郵件給使用者。目前僅 BytePlus 主帳戶可自訂 IAM 使用者的密碼。如需更多資訊，請參閱 [如何自訂 IAM 用戶的密碼？](https://docs.byteplus.com/docs/byteplus-livesaas/guan-li-shi-yong-zhe-zu-zhi-yu-jue-se-zh-TW#fd3d4ba8)。

   * 在 **操作**欄中點擊 **刪除**，以刪除使用者。

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">在此刪除後，用戶仍可登入 BytePlus 控制台使用其他服務。您也可以在此頁面使用相同的電子郵件地址再次新增用戶。      </div>
      

<span id="08751041"></span>
## 新增角色


1. 登入 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)。

2. 在 BytePlus Live 的選單列中，點擊 **授權**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1055d6b0ea5d4435a6b7c2e8aa636081~tplv-goo7wpa0wc-image.image) </span>

3. 於左側導覽窗格中，點擊 **子帳戶** \> **角色**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f47f09a1251e4b0a87b2e7be022e013d~tplv-goo7wpa0wc-image.image) </span>

4. 於 **角色**頁面，點擊 **建立角色**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/81d081d61dab4f389b1380316980afdf~tplv-goo7wpa0wc-image.image) </span>

5. 在彈出的 **新增角色**對話框中，完成以下設定後，點擊 **確定**。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">用戶必須擁有該頁面的編輯權限，才能剪輯影片、啟動直播及匯出資料。   </div>
   

   
   |**配置項** |**說明** |
   |---|---|
   |角色名稱 |輸入角色名稱。角色名稱不得超過 16 個字元，且僅可包含英文字母、數字及中文字符。 |
   |權限分配 |配置指派給此角色用戶的權限及可見範圍。<br><br><br>* **直播間權限：** 配置直播間權限及可見範圍。<br><br>   被指派此角色的使用者，對可見範圍內的直播間擁有特定權限。例如，選擇組織 A 作為可見範圍，並選擇 **直播控制** \> **編輯**、**製作人** \> **僅檢視**，以及 **洞察** \> **無權限** 作為直播間權限。則被指派此角色的使用者，對 **直播控制** 頁面擁有編輯權限，對 **製作人**模組的所有頁面僅有檢視權限，對 **洞察**模組的任何頁面均無權限，且僅限於組織 A 內使用者所建立的所有直播間。<br><br>   * 選擇直播間權限。<br><br>   * 選擇可見範圍。<br><br>      * **本人**：被指派此角色的使用者僅能存取或編輯自己建立的所有直播間。此選項預設已選，且無法取消選取。<br><br>      * **所有使用者**：勾選此核取方塊後，被指派此角色的使用者可存取或編輯其他使用者（包括 BytePlus 主帳號及其 IAM 使用者）建立的所有直播間。<br><br>      * **指定使用者**：勾選此核取方塊，並從相應下拉清單中選擇使用者。被指派此角色的使用者僅能存取或編輯所選使用者建立的直播間。<br><br>         可依暱稱或電子郵件地址搜尋使用者。支援模糊搜尋，且英文字母不區分大小寫。<br><br>      * **指定組織**：勾選此核取方塊，並從相應下拉清單中選擇組織。被指派此角色的使用者僅能存取或編輯所選組織內使用者建立的直播間。<br><br>         可依名稱搜尋組織。支援模糊搜尋，且英文字母不區分大小寫。<br><br>      * **指定直播間**：勾選此核取方塊，並從相應下拉清單中選擇直播間。被指派此角色的使用者僅能存取或編輯所選直播間。<br><br>         可依名稱搜尋直播間。支援模糊搜尋，且英文字母不區分大小寫。<br><br>* 帳號權限：選擇帳號權限。<br><br>   被指派此角色的使用者，對 BytePlus Live 控制台的特定頁面擁有特定權限。例如，選擇 **媒體庫** \> **影片庫** \> **編輯**、**資料中心** \> **使用者肖像** \> **僅檢視**，以及 **帳號中心** \> **帳號總覽** \> **無權限** 作為帳號權限。則被指派此角色的使用者，對 **影片庫**頁面擁有編輯權限，對 **使用者肖像**頁面僅有檢視權限，對 **帳號總覽**頁面無權限。<br><br>   選擇 **媒體庫** \> **影片庫** \> **僅檢視**或**編輯**時，可選擇使用者範圍及分類範圍。若同時選擇使用者範圍及分類範圍，最終可見範圍將為兩者的交集。<br><br>   選擇 **媒體庫** \> **直播暫存** \> **僅檢視**或**編輯**、**媒體庫** \> **雲剪輯** \> **僅檢視**或**編輯**，以及 **媒體庫** \> **獎品庫** \> **僅檢視**或**編輯**後，請選擇使用者範圍。<br><br>   * 使用者範圍：定義被指派此角色的使用者可存取或編輯的影片、雲剪輯專案或獎品範圍。<br><br>      * **本人**：被指派此角色的使用者僅能存取或編輯自己上傳或建立的影片及雲剪輯專案。使用者上傳或建立的影片及雲端剪輯專案同樣受所選帳戶權限限制。此選項預設已勾選，且無法取消選取。<br><br>      * **所有使用者**: 勾選此核取方塊後，指派此角色的使用者可以存取或編輯其他使用者（包括 BytePlus 帳戶及其 IAM 使用者，但不包括自身）上傳或建立的影片及雲端剪輯專案。<br><br>      * **指定使用者**: 勾選此核取方塊，並從相應下拉清單中選擇使用者。指派此角色的使用者僅能存取或編輯所選使用者上傳或建立的影片及雲端剪輯專案。<br><br>         您可以依暱稱或電子郵件地址搜尋使用者。支援模糊搜尋，且英文字母不區分大小寫。<br><br>      * **指定組織**: 勾選此核取方塊，並從相應下拉清單中選擇組織。指派此角色的使用者僅能存取或編輯所選組織內使用者上傳或建立的影片及雲端剪輯專案。<br><br>         您可以依名稱搜尋組織。支援模糊搜尋，且英文字母不區分大小寫。<br><br>   * **分類範圍**: 指派此角色的使用者僅能存取或編輯所選分類及其子分類下的影片。您可以依名稱搜尋分類。支援模糊搜尋，且英文字母不區分大小寫。若未設定分類範圍，指派此角色的使用者預設可存取或編輯所有分類下的影片。所有使用者皆可存取或編輯預設分類下的影片。 |
   

6. 您也可以執行以下操作：

   * 可依角色名稱搜尋角色。支援模糊搜尋，且英文字母不區分大小寫。

   * 在 **操作**欄中點擊 **編輯**。在彈出的 **編輯角色**對話框中按需修改角色名稱、權限及可見範圍。

   * 在 **操作**欄中點擊 **刪除**，以刪除角色。


<span id="08ecb0ea"></span>
### 內建角色

除了您自行建立的角色外，BytePlus Live 還提供以下內建角色：


* 超級管理員：此角色擁有編輯 BytePlus Live 控制台直播間及所有頁面的權限。此角色不可修改或刪除。

* 預設角色：此角色通常用於瀏覽及編輯直播間和媒體庫。此角色不可刪除。

* 運營：此角色通常用於瀏覽 BytePlus Live 控制台的直播間及頁面。

* 數據：此角色通常用於瀏覽及匯出數據。

* 助手：此角色通常用於直播期間發送問卷、投票、抽獎等互動工具。


<span id="c86a1f31"></span>
## 新增組織


1. 登入 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)。

2. 在 BytePlus Live 的選單列中，點擊 **授權**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1055d6b0ea5d4435a6b7c2e8aa636081~tplv-goo7wpa0wc-image.image) </span>

3. 在左側導覽窗格中，點擊 **子帳戶** \> **組織**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9f0c9309bbd4940912b8d32c38b7299~tplv-goo7wpa0wc-image.image) </span>

4. 在 **組織**頁面，點擊 **新增組織**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/94bb4d99d2b44b57aa3046722a35a284~tplv-goo7wpa0wc-image.image) </span>

5. 在出現的 **新增組織**對話框中，輸入組織名稱並點擊 **確定**。

   組織名稱不得超過 20 個字元，且僅可包含英文字母、數字及中文字符。

6. 您也可以執行以下操作：

   * 依組織名稱搜尋組織。支援模糊搜尋，且英文字母不區分大小寫。

   * 在 **操作**欄位中點擊 **編輯**。根據需要更改組織名稱，並在出現的 **編輯組織**對話框中查看已加入此組織的用戶。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5bde8ea9fcbe43b4ab7e95208a69b003~tplv-goo7wpa0wc-image.image) </span>

   * 在 **操作**欄位中點擊 **刪除**以刪除組織。


<span id="5f820fa0"></span>
## 常見問題

<span id="fd3d4ba8"></span>
### 如何自訂 IAM 用戶的密碼？

目前僅 BytePlus 帳戶可自訂 IAM 用戶的密碼。


1. 以 BytePlus 帳戶登入 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)。

2. 點擊控制台右上角的頭像，並選擇 **IAM**。

3. 在 **身份管理** \> **用戶**頁面，點擊 IAM 用戶的用戶名，或在 **操作**欄位中點擊 **查看詳情**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0ff2952462984a2b9942285d42bbb43d~tplv-goo7wpa0wc-image.image) </span>

4. 在 **用戶詳情**頁面，點擊 **控制台登入**標籤，然後點擊 **重設密碼**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6756ecc6c58f4d0eaf379eae4b0c9b7d~tplv-goo7wpa0wc-image.image) </span>

5. 在出現的 **重設密碼**對話框中，輸入新密碼並點擊 **確定**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9e6ec608b379427abe1bc655e598f7ff~tplv-goo7wpa0wc-image.image) </span>

---
title: "從 iOS 手機進行直播"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/cong-ios-shou-ji-jin-xing-zhi-bo-zh-TW"
---

若要隨時隨地從您的 iOS 手機開始直播，您可以使用 BytePlus Live 應用程式。本指南將帶您完整操作流程，從登入及設置直播間，到使用互動功能如 Beauty AR、商品及小工具。您將學習如何針對電商、線上課程等場景管理您的直播，實現與觀眾的即時互動。

<span id="Prerequisite"></span>
## 先決條件


* 請確保您的手機 iOS 版本為 11.0 或以上。

* 以電子郵件登入應用程式時，請確保您擁有具備下列權限的 IAM 使用者，或是 BytePlus 帳戶的 root 使用者。如需新增 IAM 使用者的詳細資訊，請參閱 [管理使用者、組織與角色](https://docs.byteplus.com/docs/byteplus-livesaas/guan-li-shi-yong-zhe-zu-zhi-yu-jue-se-zh-TW)。

   * **Live control** \> **Edit** 權限：啟動直播所需。

   * **Producer** \> **Edit** 權限：更換封面圖片或直播間名稱所需。


<span id="Downloading the app"></span>
## 下載與安裝

在 App Store 搜尋 **BytePlus Live**，下載並安裝應用程式。BytePlus Live 應用程式於下列國家或地區提供並支援：


* 中國香港

* 中國台灣

* 中國澳門

* 日本

* 韓國

* 印尼

* 新加坡

* 馬來西亞

* 菲律賓

* 泰國

* 越南

* 阿拉伯聯合大公國

* 科威特

* 沙烏地阿拉伯

* 土耳其

* 卡達


<span id="Starting a live stream"></span>
## 操作流程


1. 您可透過以下任一方式登入 BytePlus Live 應用程式：

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0694699de85c4e1e8971639c62847115~tplv-goo7wpa0wc-image.image) </span>

   * **活動 ID 登入**：輸入活動 ID 和啟動密鑰以加入特定直播間。登入 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)以獲取該直播間的活動 ID 和啟動密鑰。請參考下方的截圖。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bb83748cb7b84bcaa3a3e5c3c28b79c7~tplv-goo7wpa0wc-image.image) </span>

   * **帳號登入**：輸入 IAM 使用者的電子郵件和密碼，以及建立該 IAM 使用者的 BytePlus 帳號的 root 使用者的電子郵件和密碼。

   * **透過 QR code**：點擊應用程式右上角的掃描圖示，然後掃描包含直播資訊的 QR code 以進入特定直播間。

      登入 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)以取得直播間的 QR code。請參考下方螢幕截圖。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a9196456b7ad4df49f201c5a0786886f~tplv-goo7wpa0wc-image.image) </span>

2. 建立直播間或進入現有直播間。

   若要建立直播間，請依下列步驟操作。

   1. 點擊頁面底部的 + 圖示。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d3317d242e1c4ad792b0562b3b8f3921~tplv-goo7wpa0wc-image.image) </span>

   2. 設定直播間名稱與直播時間，並選擇是否於直播結束後自動將回放釋出至觀看頁面。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f3de712c5465421888200a5fdd369449~tplv-goo7wpa0wc-image.image) </span>

   3. 點擊 **建立**。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">您於以活動 ID 或 QR code 登入後，將直接進入現有直播間。   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">以 IAM 使用者登入時，只能檢視可見範圍內的直播間。如需設定可見範圍的詳細資訊，請參閱 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/guan-li-shi-yong-zhe-zu-zhi-yu-jue-se-zh-TW#08751041">管理角色</a>。   </div>
   

3. 依需求完成下列設定後，點擊 **開始直播**，即可依設定啟動直播。您也可點擊頁面左上角的退出圖示以離開當前頁面。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4edd9ce17c78426ab852b705e359ba1c~tplv-goo7wpa0wc-image.image) </span>

   
   |功能 |描述 |
   |---|---|
   |變更基本資訊 |變更直播間的基本資訊。<br><br><br>* 點選 **變更** 以變更封面圖片。<br><br>* 點選編輯圖示以變更直播間名稱。<br><br>* 點選 **基本資訊** 以變更以下基本資訊：<br><br>   * 直播間名稱。<br><br>   * 直播間描述。可選擇是否在直播間顯示描述。<br><br>   * 主辦帳號頭像。可上傳不超過 2 MB 的 JPG 或 PNG 檔案。<br><br>   * 主辦帳號名稱。<br><br>   * 封面圖片。可上傳不超過 2 MB 的 JPG 或 PNG 檔案。<br><br>   * 品牌標籤。此處僅可選擇標籤。如需新增標籤，請前往 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/) 新增分類標籤。如需詳細資訊，請參閱 [標記直播間](https://docs.byteplus.com/docs/byteplus-livesaas/biao-ji-zhi-bo-jian-zh-TW)。<br><br><br>為讓不同觀看頁面語言的觀眾能以其特定語言看到直播間名稱、直播間描述及主辦帳號名稱，請依下列步驟操作：<br><br><br>1. 在 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)，開啟 **語言**開關，並於直播間的 **製作人** \> **基本資訊**頁面選擇所需語言。<br><br>2. 依指示順序編輯直播間名稱、直播間描述或主辦帳號名稱的不同語言版本，並以豎線（\|）分隔。例如，若於前一步選擇了英文與簡體中文，編輯直播間名稱時請輸入 `Live room A\|直播间 A`。設定觀看頁面語言為英文的觀眾將看到直播間名稱為 `Live room A`，而設定為簡體中文的觀眾則會看到直播間名稱為 `直播间 A`。<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">你可以在直式模式下查看並更換直式封面，在橫式模式下查看並更換橫式封面。   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">要更改帳號頭像和名稱，請確保<a href="https://console.byteplus.com/livesaas/liveManagement/">BytePlus Live 控制台</a>已啟用主帳號功能。如需更多資訊，請參閱<a href="https://docs.byteplus.com/docs/byteplus-livesaas/jiang-zhu-ban-ren-zhang-hu-guan-lian-zhi-zhi-bo-ji-zh-TW">將主辦人帳戶關聯至直播間</a>。   </div><br>    |
   |切換前後鏡頭 |點選 **翻轉**以切換鏡頭。預設為前置鏡頭。 |
   |使用美顏 AR |點選 **美顏 AR**以使用美顏 AR 與濾鏡。<br><br><br>* 美顏 AR：使用美顏 AR 技術提升外觀。<br><br>* 濾鏡：可選擇多種濾鏡，為影像增添風格與氛圍。 |
   |管理商品 |點選 **商品**以管理商品。<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bd473929c718478887a72e64443711c1~tplv-goo7wpa0wc-image.image) </span><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">此功能僅於直式模式下提供。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">請確保已在<a href="https://console.byteplus.com/livesaas/liveManagement/">BytePlus Live 控制台</a>為直播間新增商品卡片選單。如需更多資訊，請參閱<a href="https://docs.byteplus.com/docs/byteplus-livesaas/guan-li-chan-pin-ka-pian-zh-TW">管理產品卡片</a>。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">若直播間有多個商品卡片選單，請點選選單名稱以管理其中的商品。</div><br><br><br>* 可手動新增商品或從商品庫新增。每個商品卡選單最多可新增 500 件商品。<br><br>   * 手動新增商品：點選 **手動新增**。設定商品資訊後，點選 **提交**。<br><br>      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/48955b1109ad4b8296e2606b00a29240~tplv-goo7wpa0wc-image.image) </span><br><br>      觀眾於觀看頁面點選商品後，將被導向商品網址。<br><br>      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">請上傳不超過 2 MB 的 JPG 或 PNG 檔案作為商品圖片。      </div><br>      <br><br>      為讓不同觀看頁面語言的觀眾能以其特定語言看到商品名稱、現價、原價並存取不同商品網址，請依下列步驟操作：<br><br>      1. 在 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)，開啟 **語言**開關，並於直播間的 **製作人** \> **基本資訊**頁面選擇所需語言。<br><br>      2. 依指示順序設定商品名稱、現價、原價或商品網址的不同語言版本，並以豎線（\|）分隔。例如，若您在前一步選擇了英文和簡體中文，則在設定產品名稱時，請輸入`Product A\|商品 A`。當觀看頁面的語言設為英文時，使用者將看到產品名稱為`Product A`；而當語言設為簡體中文時，則會看到產品名稱為`商品 A`。<br><br>   * 從產品庫新增產品：點選**Add from library**，即可從[BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/)中已新增的產品庫加入產品。<br><br>      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b5599aab720340d299099e911b31d41e~tplv-goo7wpa0wc-image.image) </span><br><br>* 上架或下架產品：點選**List**或**Unlist**，即可在觀看頁面顯示或隱藏產品。<br><br>* 搜尋產品：點選**Search**，可根據產品名稱在所有產品卡片的選單中搜尋產品。支援模糊搜尋。<br><br>* 可根據產品類別篩選產品。<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">此功能僅於<a href="https://console.byteplus.com/livesaas/liveManagement/">BytePlus Live 控制台</a>設定商品類別後提供。如需更多資訊，請參閱<a href="https://docs.byteplus.com/docs/byteplus-livesaas/guan-li-chan-pin-ka-pian-zh-TW">管理產品卡片</a>。   </div><br>   <br><br>* 刪除產品：可一次刪除一個或多個產品。<br><br>   * 一次刪除一個產品：點選產品右側的更多（...）圖示，再點選**Delete**。<br><br>   * 一次刪除多個產品：點選**More**並選擇**Batch manage**。選取多個產品後，點選**Delete**。<br><br>* 調整順序：點選**More**並選擇**Reorder**。長按並拖曳產品以變更順序，然後點選**Save**。<br><br>* 編輯產品：點選產品右側的更多（...）圖示，再點選**Edit**。<br><br>* 置頂產品：點選產品右側的更多（...）圖示，再點選**Pin**。該產品將會被置頂於產品卡片選單，並在觀看頁面以浮動視窗顯示。您也可以點選**Unpin**來取消置頂產品。 |
   |管理元件 |點選**Widgets**。在彈出的對話框中，您可以：<br><br><br>* 點選**Upload image**以上傳本地圖片。<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/11c1292af62c4f8b80957f26c5742262~tplv-goo7wpa0wc-image.image) </span><br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">請上傳不超過 10 MB 的 PNG、HEIC 或 GIF 格式圖片。   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">同一裝置新增的小工具會在不同直播間間共用。   </div><br>   <br><br>* 點選元件右下角的刪除圖示以刪除該元件。<br><br>* 點選元件即可將其加入目前頁面。<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">同一小工具可於當前頁面重複新增多次。   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">當前頁面最多可新增 10 個 GIF 格式的小工具。   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">每個新增至當前頁面的小工具都屬於一個圖層。   </div><br>   <br><br><br>點選目前頁面的元件後，您可以：<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8ed30e1d28544470a0122e2e67b438d0~tplv-goo7wpa0wc-image.image) </span><br><br><br>* 點選元件右上角的刪除圖示以將其從目前頁面刪除。<br><br>* 拖曳元件右下角的縮放圖示，或使用兩指比例縮放元件。<br><br>* 拖曳以移動元件。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若你以同一裝置再次進入直播間，小工具配置可與離開時相同。</div><br> |
   |管理圖層 |點選**Layers**。在彈出的對話框中，您可以：<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/99e1a33a164b4246be9711e1a1c128bf~tplv-goo7wpa0wc-image.image) </span><br><br><br>* 長按並拖曳圖層，或在圖層上點選**Up**或**Down**以調整圖層順序。若元件重疊，位於較高圖層的元件會顯示於較低圖層元件之上。<br><br>* 點選**Hide**或**Show**以隱藏或顯示圖層。該圖層上的元件也會在目前頁面被隱藏或顯示。<br><br>* 點選**Delete**以刪除圖層。該圖層上的元件也會從目前頁面被刪除。<br><br>* 點選**Clear widgets**以刪除所有元件。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">最多支援 20 個圖層。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">若你以同一裝置再次進入直播間，圖層配置可與離開時相同。</div><br> |
   |切換橫向與直向模式 |點選**Landscape**或**Portrait**以切換橫向與直向模式。直向模式為預設設定。 |
   |選擇直播影片的解析度 |點選**Resolution**以修改直播影片的解析度。供參考，720p為預設設定。 |
   |清除畫面 |於螢幕上連續點擊兩下以清除畫面，這將隱藏本頁面上除小工具外的所有元件。<br><br>要撤銷此操作，可點擊撤銷圖示或再次雙擊螢幕。<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1835de52e8f1459bbb6ca1f669937a2a~tplv-goo7wpa0wc-image.image) </span> |
   

4. 直播期間，您可執行下列操作。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4782645545534474a802c23170216201~tplv-goo7wpa0wc-image.image) </span>

   
   |序號 |功能 |描述 |
   |---|---|---|
   |1 |直播間資訊 |您可以執行以下操作：<br><br><br>* 若已啟用主辦帳號功能，可查看帳號頭像及名稱。如需啟用此功能的詳細資訊，請參閱[將主辦人帳戶關聯至直播間](https://docs.byteplus.com/docs/byteplus-livesaas/jiang-zhu-ban-ren-zhang-hu-guan-lian-zhi-zhi-bo-ji-zh-TW)。<br><br>* 即時查看線上觀眾人數。<br><br>* 若已啟用直播結束時間功能，可查看距離直播結束的倒數計時器。如需有關如何啟用此功能的更多資訊，請參閱 [自動結束直播](https://docs.byteplus.com/docs/byteplus-livesaas/zi-dong-jie-shu-zhi-bo-zh-TW)。<br><br>* 點選右上角的結束圖示以結束直播。<br><br>* 查看直播間人氣。<br><br>* 查看目前網路狀態。<br><br>* 查看本次直播的時長。 |
   |2 |聊天區 |閱讀及發送留言。<br><br>為確保不同觀看頁面語言的觀眾能以其特定語言看到主辦者的留言，請依下列步驟操作：<br><br><br>1. 登入[BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/)。<br><br>2. 於直播間列表中，點擊以開啟直播間。<br><br>3. 於左側導覽窗格中，點選**Producer** \> **Basic information**。開啟**Languages**開關並選擇所需語言。<br><br>4. 於左側導覽窗格中，點選**Producer** \> **Menus**。於聊天互動選單下開啟**Comment translation**開關。觀看頁面聊天區的留言將自動翻譯為對應語言。<br><br>5. 為提升主辦者留言在不同語言的準確度，主辦者可依指示順序於聊天區編輯不同語言的留言，並以豎線（\|）分隔。例如，若在步驟3選擇英文及簡體中文，主辦者於聊天區發送`Hello\|你好`，則觀看頁面語言設為英文的觀眾將於聊天區看到`Hello`，而語言設為簡體中文的觀眾將於聊天區看到`你好`。 |
   |3 |商品 |點選商品圖示以管理商品。詳情請參閱步驟3。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">此功能僅於直式模式下提供。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">請確保已在<a href="https://console.byteplus.com/livesaas/liveManagement/">BytePlus Live 控制台</a>為直播間新增商品卡片選單。如需更多資訊，請參閱<a href="https://docs.byteplus.com/docs/byteplus-livesaas/guan-li-chan-pin-ka-pian-zh-TW">管理產品卡片</a>。</div><br> |
   |4 |設定 |點選右下角的設定圖示，然後：<br><br><br>* 選擇**Flip**以切換前後鏡頭。<br><br>* 選擇**Beauty AR**以使用美顏AR及濾鏡。<br><br>   * Beauty AR：使用美顏AR技術提升您的外觀。<br><br>   * Filters：從多種濾鏡中選擇，為您的畫面增添風格與氛圍。<br><br>* 選擇**Widgets**以管理小工具。詳情請參閱步驟3。<br><br>* 選擇**Layers**以管理圖層。詳情請參閱步驟3。<br><br>* 選擇**Mirror**以水平翻轉直播畫面。<br><br>* 選擇**Flash**以啟用手機的閃光燈功能。<br><br>* 選擇**Mute**以靜音您的麥克風，使觀眾無法聽到您的聲音。<br><br>* 選擇**清除畫面**以隱藏所有元件（小工具除外），讓你能專注於內容。<br><br>   你也可以雙擊螢幕來清除畫面。<br><br>   要撤銷此操作，可點擊撤銷圖示或再次雙擊螢幕。<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/305fe5a96b13480fb6529c71ead99b3f~tplv-goo7wpa0wc-image.image) </span><br><br>* 選擇**清除評論**以清除直播間中的評論。 |
   

5. 直播結束後，您可查看直播間的下列數據。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/95740480cab841ec8669bd9b90f754fd~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">若你在同一直播間多次開播，所有場次的數據會被匯總。   </div>

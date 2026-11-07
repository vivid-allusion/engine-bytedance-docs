---
title: "在 VOD 中錄製直播影片"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/recordinvod-zh-TW"
---

為了將您的直播串流保存以便隨選播放及後續處理，您可以設定 BytePlus MediaLive，讓其自動錄製並保存至 BytePlus VOD。本主題提供如何建立錄製範本、設定回調，以及啟動錄製任務的逐步操作說明。直播串流錄製完成後，您可以利用 VOD 的功能進行轉碼、編輯及加上浮水印，然後將最終影片分發給您的觀眾。

<span id="86d66040"></span>
## 先決條件


* 若要將錄製檔案存儲於 VOD，請啟用 [VOD 服務](https://console.byteplus.com/vodpaas/totalOverview/)。

* 已新增推流用的網域名稱，並完成 CNAME 設定。詳細資訊請參考 [新增網域名稱](https://docs.byteplus.com/docs/byteplus-media-live/docs-domain#bb9e1337) 和 [新增 CNAME 記錄](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-adding-a-cname-record)。

* 請於 VOD 控制台完成網域名稱設定，詳細資訊請參考 [分發加速](https://docs.byteplus.com/en/docs/byteplus-vod/docs-accelerated-distribution)。


<span id="1d4ffeb7"></span>
## 操作流程

<span id="6791add7"></span>
### 建立錄製範本

以下步驟說明如何在控制台建立錄製範本。您也可以透過呼叫 [CreateRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createrecordpresetv2-2023-zh-TW) API 建立錄製範本。


1. 登入 [BytePlus MediaLive 控制台](https://console.byteplus.com/live)。

2. 於左側導覽窗格選擇 **功能設定**，並切換至 **錄製**標籤頁。

3. 在頁面頂部找到 **網域名稱空間**，並於下拉選單中選擇網域名稱空間。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">您需要選擇 VOD 作為儲存位置，並在面板中點擊<strong>VOD</strong>。   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ed009ab1f32f4ae78e7a724924a1ca86~tplv-goo7wpa0wc-image.image) </span>

4. 點擊 **新增設定**，開啟 **新增錄製設定**對話框。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">首次操作時，您需要完成授權流程，以允許 MediaLive 存取 VOD 服務。請依螢幕上的指示完成流程，然後進行下一步。   </div>
   

5. 依頁面提示設定 AppName、VOD 空間及工作流範本等參數。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3fce24b3399d43ea808f026569e4400b~tplv-goo7wpa0wc-image.image) </span>


下表說明各項設定參數。


|參數 |||說明 |
|---|---|---|---|
|AppName |||請填寫本錄製配置的 AppName。支援大小寫字母、數字、連字號（\-）及底線（_），最長 30 個字元。<br><br><br>* 您可以使用星號（\*）將錄製策略套用至命名空間內所有 AppName。這會為命名空間建立全域策略。<br><br>* 若同時為某個 AppName 配置全域策略與單獨策略，預設會以單獨策略進行錄製。 |
|StreamName |||請指定要錄製的直播 StreamName。同一個 App 最多可指定 20 個串流名稱。 |
|錄製串流類型 |||請選擇直播錄製的類型。支援以下兩種類型。<br><br><br>* 原始串流<br><br>* 轉碼串流<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">錄製轉碼流時會產生轉碼拉流，可能會產生費用。若刪除轉碼配置，該流將不會被錄製。</div><br> |
|VOD 空間 |||選擇 VOD 空間作為儲存位置。錄製檔案將儲存於所選空間。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若尚未擁有，請<a href="https://docs.byteplus.com/en/byteplus-vod/docs/space-management">建立 VOD 空間</a>。</div><br><br><br>. |
|錄製格式 |HLS |檔案產生模式 |HLS 格式支援分段錄製與全程錄製。 |
|||固定時間 |單一錄製檔案的最長時長。當錄製時長超過此值時，會產生新的錄製檔案。分段錄製與全程錄製支援的值範圍不同：<br><br><br>* 分段錄製：支援 5 至 360 分鐘。<br><br>* 全程錄製：無限制。 |
|||等待時間 |當**檔案產生模式**設為**全程錄製**時，您可以指定錄製中斷後恢復錄製的等待時間。中斷超過等待時間後，錄製任務將結束並產生錄製檔案。此等待時間的有效範圍為 0 至 3600 秒。 |
|||TS 切片時長 |直播錄製每個 TS 分段的時長。可設定值為 5 至 30 秒 |
|||VOD 分類 |[選擇錄製檔案儲存的 VOD 分類。](https://docs.byteplus.com/en/docs/byteplus-vod/docs-system)[分類配置方法請參考 VOD 分類](https://docs.byteplus.com/en/docs/byteplus-vod/docs-system)。 |
|||工作流範本 |此參數為選填。請從下拉清單中選擇工作流範本。<br><br><br>* 若於此處選擇工作流名稱，錄製檔案上傳至 BytePlus VOD 後將套用對應工作流。<br><br>* 若未於此處選擇工作流範本，錄製檔案上傳至 BytePlus VOD 後將套用預設工作流範本。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">您可以使用 VOD 的預設工作流範本，或參考<a href="https://docs.byteplus.com/en/docs/byteplus-vod/docs-workflow">工作流範本</a>進行自訂。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">您為 MediaLive 錄製所配置的工作流範本優先於 VOD 中配置的預設工作流範本。</div><br> |
|||檔案名稱 |請輸入檔案路徑。預設路徑為`record/{PubDomain}/{App}/{Stream}/{StartTime}_{EndTime}`。您可以手動新增路徑組件，最長可達 200 個字元。手動新增的路徑必須符合以下要求。<br><br><br>* 你可以刪除固定的路徑組件，例如 {App}/{Stream}。<br><br>* 路徑不能以正斜線（/）或反斜線（\）開頭。<br><br>* 不支援如 "//" 和 "/./" 等字串；<br><br>* 不支援如 \b、\t、\n、\v、\f 和 \r 等字元。<br><br>* ".." 不支援作為檔案名稱。<br><br>* 目錄階層必須至少包含兩層，例如 `live/{App}/{Stream}` |
||MP4 |固定時間 |單一錄製檔案的最長時長。當錄製時長超過此值時，將會產生新的錄製檔案。支援的時長範圍為 5 到 360 分鐘。 |
|||VOD 分類 |選擇直播錄製檔案存儲至 VOD 的分類。有關分類的配置方式，請參考 VOD [Categories](https://docs.byteplus.com/en/docs/byteplus-vod/docs-system)。 |
|||工作流範本 |非必填，請在下拉列表中選擇工作流範本。<br><br><br>* 若於此處選擇工作流名稱，錄製檔案上傳至 BytePlus VOD 後將套用相應的工作流。<br><br>* 若未於此處選擇工作流範本，錄製檔案上傳至 BytePlus VOD 後將套用預設工作流範本。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">您可以使用 VOD 的預設工作流範本，或參考<a href="https://docs.byteplus.com/en/docs/byteplus-vod/docs-workflow">工作流範本</a>進行自訂。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">您於 MediaLive 錄製中配置的工作流範本優先於 VOD 中配置的預設工作流範本。</div><br> |
|||檔案名稱 |請輸入檔案路徑。預設路徑為 `record/{PubDomain}/{App}/{Stream}/{StartTime}_{EndTime}`。你可以手動新增路徑組件，最長可達 200 個字元。手動新增的路徑必須符合以下要求。<br><br><br>* 你可以刪除固定的路徑組件，例如 {App}/{Stream}。<br><br>* 路徑不能以正斜線（/）或反斜線（\）開頭。<br><br>* 不支援如 "//" 和 "/./" 等字串；<br><br>* 不支援如 \b、\t、\n、\v、\f 和 \r 等字元。<br><br>* ".." 不支援作為檔案名稱。<br><br>* 目錄階層必須至少包含兩層，例如 `live/{App}/{Stream}` |
||FLV |固定時間 |單一錄製檔案的最長時長。當錄製時長超過此值時，將會產生新的錄製檔案。支援的時長範圍為 5 到 360 分鐘。 |
|||VOD 分類 |選擇直播錄製檔案存儲至 VOD 的分類。有關分類的配置方式，請參考 VOD [Categories](https://docs.byteplus.com/en/docs/byteplus-vod/docs-system)。 |
|||工作流範本 |非必填，請在下拉列表中選擇工作流範本。<br><br><br>* 若於此處選擇工作流名稱，錄製檔案上傳至 BytePlus VOD 後將套用相應的工作流。<br><br>* 若未於此處選擇工作流範本，錄製檔案上傳至 BytePlus VOD 後將套用預設工作流範本。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">您可以使用 VOD 的預設工作流範本，或參考<a href="https://docs.byteplus.com/en/docs/byteplus-vod/docs-workflow">工作流範本</a>進行自訂。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">您於 MediaLive 錄製中配置的工作流範本優先於 VOD 中配置的預設工作流範本。</div><br> |
|||檔案名稱 |請輸入檔案路徑。預設路徑為 `record/{PubDomain}/{App}/{Stream}/{StartTime}_{EndTime}`。你可以手動新增路徑組件，最長可達 200 個字元。手動新增的路徑必須符合以下要求。<br><br><br>* 你可以刪除固定的路徑組件，例如 {App}/{Stream}。<br><br>* 路徑不能以正斜線（/）或反斜線（\）開頭。<br><br>* 不支援如 "//" 和 "/./" 等字串；<br><br>* 不支援如 \b、\t、\n、\v、\f 和 \r 等字元。<br><br>* ".." 不支援作為檔案名稱。<br><br>* 目錄階層必須至少包含兩層，例如 `live/{App}/{Stream}` |



6. 點擊 OK 按鈕完成設定。設定結果可於列表中查看。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c16108cc6649479f8b7ba739f7e5ef59~tplv-goo7wpa0wc-image.image) </span>


<span id="a5e43951"></span>
### 設定錄製回調

以下步驟說明如何在 BytePlus MediaLive 控制台新增回調設定。您也可以呼叫 [UpdateCallback](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatecallback-2023) API 進行設定。


1. 登入 [BytePlus MediaLive 控制台](https://console.byteplus.com/live)。

2. 於左側導覽窗格選擇 **設定** \> **功能設定**。點擊 **回調**標籤頁。

3. 在頁面頂部找到 **網域名稱空間**，並於下拉選單中選擇網域名稱空間。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c846b992def44347a4bfc578354621f7~tplv-goo7wpa0wc-image.image) </span>

4. 點擊新增設定，開啟新增回調設定對話框。

5. 依頁面提示設定回調地址、回調類型及 AppName 等參數。

   各參數說明請參見下表。

   
   |參數 |說明 |
   |---|---|
   |回調地址 |用於接收回調訊息的回調地址。支援 HTTP 和 HTTPS 協議。 |
   |回調類型 |回調類型請選擇**錄製事件**。 |
   |回調金鑰 |回調金鑰。支援大小寫字母及數字，最長可達 32 個字元。 |
   |AppName |應用名稱。此名稱必須與建立錄製範本時所使用的名稱相同。 |
   

6. 點擊 **確認**以保存回調設定。您可於列表中查看新新增的設定。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/639d18064d01434fadb769baf18d3219~tplv-goo7wpa0wc-image.image) </span>


<span id="50d2d99f"></span>
### 產生推流地址

本節說明如何從 BytePlus MediaLive 控制台產生推流地址。您也可以透過呼叫 [GeneratePushURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generatepushurl-2023) API 產生推流地址。


1. 登入 [BytePlus MediaLive 控制台](https://console.byteplus.com/live)。

2. 於導覽列選擇 [地址產生器](https://console.byteplus.com/live/main/locationGenerate)。

3. 依頁面提示選擇地址類型及網域名稱，並輸入 AppName（需與建立錄製範本時所用相同）、自訂 StreamName 及過期時間。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eea908c886ba4d12bb51041b411e3b6e~tplv-goo7wpa0wc-image.image) </span>

4. 點擊 **產生地址**，即可於 **結果**區取得推流地址。


<span id="3d28d39b"></span>
### 開始推流

使用產生的推流地址進行推流。MediaLive 支援以下推流配置。


* 於 BytePlus MediaLive 控制台使用 [網頁推流](https://console.byteplus.com/live/main/WebPushStream)功能進行推流

* 使用串流工具（例如 [OBS](https://obsproject.com/)）進行推流

* 使用[Client SDK](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-client-sdks-4d36c282)推送串流


<span id="dc72915d"></span>
### 取得影片 Vid

直播結束後，錄製檔案會儲存於對應的 VOD 空間。您可以透過影片 ID（Vid）找到該影片。取得 Vid 有三種方式：


<Tabs>
<Tab zoneid="T5vgJhFWcK" title="方法一：透過 BytePlus MediaLive 控制台獲取">
<TabTitle>方法一：透過 BytePlus MediaLive 控制台獲取</TabTitle>

1. 登入[BytePlus MediaLive 控制台](https://console.byteplus.com/live)

2. 選擇**直播管理** \> **錄製**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ff1d3c5677a142f4b8b82bd85fb23ea7~tplv-goo7wpa0wc-image.image) </span>

3. 根據提示填寫網域名稱、AppName、StreamName，並選擇時間範圍。點擊**搜尋**以獲取錄製結果。網域名稱及時間範圍為必填項。

4. 點擊**搜尋**開始查詢。

5. 您可在結果列表中查看對應錄製的 Vid。您也可以點擊**進入 VOD 查看**，進入 VOD 控制台以查看錄製結果。


</Tab>
<Tab zoneid="EKfkHxJ8pi" title="方法二：透過錄製回調方法獲取">
<TabTitle>方法二：透過錄製回調方法獲取</TabTitle>

若您配置了錄製回調，MediaLive 在產生錄製檔案時會將錄製檔案資訊發送至您的回調伺服器。

您可在回調訊息中獲取錄製檔案的 Vid。有關回調訊息的詳細說明，請參閱回調內容的文件。


</Tab>
<Tab zoneid="Odow3LYR2o" title="方法三：透過 API 獲取">
<TabTitle>方法三：透過 API 獲取</TabTitle>

您可透過呼叫[DescribeRecordTaskFileHistory](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describerecordtaskfilehistory-2023-zh-TW) API 獲取錄製檔案的 Vid。


</Tab>
</Tabs>

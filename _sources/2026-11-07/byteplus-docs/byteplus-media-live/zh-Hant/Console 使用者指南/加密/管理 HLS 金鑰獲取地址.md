---
title: "管理 HLS 金鑰獲取地址"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-hls-keyaddress-zh-TW"
---

為了以標準加密方式保護您的 HLS 直播流，您需要在 MediaLive 中配置金鑰獲取地址。本主題說明 HLS 加密的實現原理，並指導您完成金鑰獲取地址及更新週期的設置流程。

<span id="6c918260"></span>
## 實現原理

MediaLive 的 HLS 加密功能採用 HLS 協議的一般加密方案。該方案使用 AES\-128 加密算法對每個 TS（傳輸流）進行加密，並將解密資訊添加到生成的播放列表檔案中。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0bc33011b5894f68b09c66dad019c0ed~tplv-goo7wpa0wc-image.image) </span>

在此方案中，MediaLive 整合 KMS 服務以生成並定期輪換加密金鑰。

加密與解密流程如下：


1. 客戶端通過 HLS 拉流地址發起加密直播流的拉流請求。

2. 收到請求後，MediaLive 使用自身生成的金鑰對直播流進行加密，並將包含解密資訊的 M3U8 檔案返回給客戶端。在該檔案中，#EXT\-X\-KEY 標籤包含加密資訊，URI 為從自建金鑰管理服務請求金鑰的地址。M3U8 檔案的部分內容示例如下。

   ```Bash
   #EXTM3U
   #EXT-X-VERSION:3
   #EXT-X-MEDIA-SEQUENCE:107326
   #EXT-X-TARGETDURATION:2
   #EXT-X-PROGRAM-DATE-TIME:2024-05-07T17:59:02.927+08:00
   #EXT-X-KEY:METHOD=AES-128,URI="https://example.kms.com/get_hls_enc_key?key_id=08e765a4da*****c4028755c3c",IV=0x00000000000000000000000000000000
   #EXTINF:2.000,
   HD_1080p_1715075942927_3070957834_107326.ts?ps=11&app=live&stream=HD_1080p&vhost=push.example.com
   ```
   

3. 客戶端根據 M3U8 檔案中的解密資訊，向自建金鑰管理服務請求金鑰。

4. 自建金鑰管理服務向 MediaLive 請求金鑰。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">自建金鑰管理服務必須支持金鑰緩存功能。這樣服務即可直接返回金鑰給後續拉流請求，無需每次都從 MediaLive 獲取。   </div>
   

5. 自建金鑰管理服務將從 MediaLive 獲取的金鑰返回給客戶端，客戶端再使用該金鑰解密並播放 M3U8 檔案。


<span id="7fb5ff63"></span>
## 前置條件

<span id="73462349"></span>
### 自建金鑰管理服務

要使用 HLS 加密，您必須自建金鑰管理服務以處理解密與播放。該服務必須支持以下功能：


* 支持從 MediaLive 獲取金鑰：HLS 加密金鑰由 MediaLive 提供，因此您的金鑰管理服務需調用 MediaLive 提供的 GetHLSEncryptDataKey API 來獲取加密金鑰。

* 支持獲取金鑰的緩存功能：為避免所有拉流行為都從 MediaLive 獲取金鑰，您的金鑰管理服務應具備緩存功能，讓客戶端可直接從您的服務獲取金鑰。


<span id="a889ced5"></span>
### 認證（可選）

您也可以使用 MediaLive 提供的遠端認證來驗證拉流請求。如需使用此功能，請通過[提交工單](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)聯繫技術支持。

<span id="8a91d8c7"></span>
## 操作流程


1. 登入[BytePlus MediaLive 控制台](https://console.byteplus.com/live)。

2. 在左側導航欄，點擊**設定**\>**加密**。在出現的**加密**頁面，點擊**HLS 標準**標籤。

3. 點擊**編輯**，將彈出對話框。

4. 填寫金鑰獲取地址及金鑰更新週期。

5. 點擊**確認**以保存設定。


<span id="d4be5c99"></span>
## 後續操作


1. 新增 HLS 加密配置。操作說明請參見[管理加密設定](https://docs.byteplus.com/docs/byteplus-media-live/docs-manage-subtitle-configuration-zh-TW)。

2. 生成加密 HLS 流的拉流地址。操作說明請參見[Generating stream addresses](https://docs.byteplus.com/docs/byteplus-media-live/docs-address-generator)。

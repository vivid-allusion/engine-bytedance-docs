---
title: "在 Web 上實現媒體上下滑動"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/docs-interactive-video-solution-web-zh-TW"
---

要構建具有垂直滾動、評論和點贊等功能的媒體上下滑動資訊流，您可以從提供的 Demo 入手。本指南將說明如何自定義 Demo 的播放器、語言設定和部署配置，以高效地在您的 Web 專案中實現類似解決方案。

<span id="7dd1b50a"></span>
# 前提條件


* 已開通 BytePlus VOD 的有效 BytePlus 賬號。請參考 BytePlus VOD 入門中的[步驟 1：啟用 BytePlus VOD 服務](https://docs.byteplus.com/en/docs/byteplus-vod/docs-getting-started#b4e9d150)。

* 按照[執行 Demo (Web/H5)](https://docs.byteplus.com/docs/byteplus-vos/docs-running-the-demo-web-zh-TW)中的流程成功執行 Demo 專案。


<span id="5f2dd2d3"></span>
# 實現

專案成功執行後，您可以透過修改幾個關鍵配置檔案，自定義屬於自己的 Feed 流網站。

<span id="d49ff281"></span>
## 播放器配置

本節將概述 Demo 中的播放器配置。

> 如需更詳細的配置，請參閱 BytePlus VOD [Web Player SDK API 參考](https://docs.byteplus.com/en/docs/byteplus-vod/docs-web-api-reference)。



|引數 |資料型別 |預設值 |說明 |
|---|---|---|---|
|el |HTMLElement |\- |VePlayer 插入用於展示和互動的 HTML 元素。 |
|getVideoByToken |[getVideoByToken](https://docs.byteplus.com/en/docs/byteplus-vod/docs-web-api-reference#getvideobytoken) |\- |用於獲取所需播放影片的配置。詳細說明請參閱[getVideoByToken](https://docs.byteplus.com/en/docs/byteplus-vod/docs-web-api-reference#getvideobytoken)。 |
|poster |string |\- |封面圖片的 URL。 |
|mobile |```JSON```<br>```{```<br>```   gradient: string```<br>```}```<br> |\- |移動端 Web 播放器的互動外掛。<br><br>`gradient`：是否啟用漸變陰影。支援的取值：<br><br><br>* normal：正常陰影效果<br><br>* none：無陰影<br><br>* top：頂部陰影<br><br>* bottom：底部陰影 |
|autoplay |boolean |false |是否啟用自動播放。<br><br><br>* true：是<br><br>* false：否<br><br>> 由於瀏覽器策略，自動播放可能無法始終成功，具體取決於瀏覽器環境、使用者行為及瀏覽器配置等因素。 |
|loop |boolean |false |是否啟用迴圈播放。<br><br><br>* true：是<br><br>* false：否 |
|enableDegradeMuteAutoplay |boolean |false |當帶聲音自動播放失敗時，是否降級為靜音自動播放。支援的取值：<br><br><br>* true：是<br><br>* false：否<br><br><br>當 `enableDegradeMuteAutoplay` 和 `autoplay` 均設定為 `true` 時，若當前瀏覽器不支援帶音訊自動播放，播放器將降級為靜音自動播放。請注意，靜音自動播放也可能失敗。 |
|closeVideoClick |boolean |false |* 桌面端：是否透過點選播放器區域切換播放/暫停。<br><br>* 移動端：是否透過關閉影片的點選/touchend 行為切換播放/暫停。 |
|closeVideoDblclick |boolean |false |* 桌面端：是否禁用透過雙擊播放器進入全屏模式的功能。<br><br>* 移動端：是否禁用透過雙擊切換播放/暫停的功能。 |
|controls |boolean |true |控制欄外掛，預設註冊。 |
|ignores |string[] |[] |用於禁用外掛。VePlayer 內建了多種常用功能的外掛。如需禁用某個內建外掛，可將外掛名稱（不區分大小寫）作為引數傳入。 |
|start |```JSON```<br>```{```<br>```  disableAnimate: boolean,```<br>```  isShowPause: boolean,```<br>```}```<br> |false |播放器中央用於切換播放/暫停的按鈕。<br><br>`disableAnimate`: 是否禁用點選動畫效果。<br><br><br>* true：是<br><br>* false：否（預設）<br><br><br>`isShowPause`: 暫停時是否保持介面可見。<br><br><br>* true：是<br><br>* false：否（預設） |


<span id="84c261da"></span>
## 多語言配置

如需修改翻譯或新增多語言，可修改 `translation.ts` 檔案中的配置，或使用實現國際化功能的庫，如[@formatjs/intl](https://www.npmjs.com/package/@formatjs/intl)。

<span id="383ec30e"></span>
## 部署

生成構建產物，只需執行 `pnpm run build`。在部署階段，請注意 `vite.config.ts` 檔案中的 `base` 和 `build` 配置。以下是需要關注的兩個關鍵點：


* 構建輸出目錄預設設定為“output”。如需調整，可在 `build` 配置下修改 `outDir` 屬性。

* 配置靜態資源的公共基礎路徑：如果您的資源直接託管在同一伺服器上，可保持預設根路徑(`/`)。但如果使用 CDN，請獲取您的加速域名，並將配置中的\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*佔位符替換為實際域名。


```JavaScript
export default defineConfig({
  base: isProd ? '***************' : '/',
  server: {
    port: 8000,
  },
  build: {
    outDir: 'output',
  },
});
```

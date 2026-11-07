---
title: "使用 AI IDE 編輯函數程式碼"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/use_ai_ide_for_code_zh-tw"
---

本文件介紹如何使用邊緣函式主控台提供的 AI 助理編輯函式程式碼。

AI 助理內建了邊緣函式執行階段 API 的範例程式碼，可以藉助大型語言模型幫助您產生、修復和解釋函式程式碼。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">AI 助理產生的程式碼僅供參考。請您在使用前仔細核對，確保其準確性和適用性。</div>


* <div data-tips="true" data-tips-type="warning">AI 助理提供的程式碼解釋僅供參考。請您以邊緣函式官方文件為準。</div>



<span id="使用限制"></span>
## 使用限制

您每天的使用限制如下：


* **會話數量**：您最多可發起 10 個會話。

* **訊息數量**：您在每個會話中最多可傳送 100 則訊息。

* **訊息長度**：每則訊息不超過 250 個全形字元或 500 個半形字元。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">訊息長度的限制不包括被新增為上下文的程式碼。   </div>
   

<span id="操作步驟"></span>
## 操作步驟

請參閱以下步驟使用 AI 助理。

<span id="步驟一：開啟-ai-助理面板"></span>
### 步驟一：開啟 AI 助理面板

在邊緣函式主控台，您可以點選程式碼編輯器右上角的 AI 助理圖示來開啟 AI 助理面板。

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_32185af78535d644c8cac1a17e17ab60.png) </span>

<span id="步驟二：透過-ai-助理產生程式碼"></span>
### 步驟二：透過 AI 助理產生程式碼

請參閱以下步驟透過 AI 助理產生程式碼。


1. 在 AI 助理面板的對話方塊中輸入您的需求，然後點選 **傳送** 圖示。AI 助理會產生符合您需求的函式程式碼。例如，您可以輸入以下需求：


```text
產生程式碼用於修改使用者請求中的 HTTP 請求標頭和返回給使用者的回應中的回應標頭：
- 在請求標頭中新增一個自訂請求標頭"x-via-function-start"，值為目前時間戳
- 在回應標頭中新增一個自訂回應標頭"x-via-function-done"，值為目前時間戳
```



2. 點選產生的程式碼右上角的 **應用程式碼** 圖示，將程式碼套用到編輯器。


接下來，您可以對程式碼進行偵錯。請參閱 [編輯和偵錯函式程式碼](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-develop-and-test-function-cn-zh-tw)。

<span id="其他操作"></span>
## 其他操作

<span id="透過-ai-助理修復程式碼"></span>
### 透過 AI 助理修復程式碼

如果您在偵錯中發現問題，需要修復程式碼問題，請參閱以下步驟。


1. 選取程式碼編輯器中的部分或全部程式碼，點選 **修復程式碼**，AI 助理會對程式碼進行修復。

2. 點選產生的程式碼右上角的 **套用程式碼** 圖示，將最佳化或修復後的程式碼套用到編輯器。


<span id="透過-ai-助理解釋程式碼"></span>
### 透過 AI 助理解釋程式碼

如果您希望藉助 AI 助理了解某個程式碼片段或整個程式碼檔案的邏輯，可選取程式碼編輯器中的部分或全部程式碼，點選 **解釋程式碼**。AI 助理會對程式碼進行解釋。

<span id="將程式碼新增為會話上下文"></span>
### 將程式碼新增為會話上下文

如果您需要將某個程式碼片段或整個程式碼檔案新增為聊天的上下文，您可以選取程式碼編輯器中的部分或全部程式碼，點選 **新增至聊天**。您可以使用自然語言描述您的需求，例如修改程式碼、最佳化程式碼等。

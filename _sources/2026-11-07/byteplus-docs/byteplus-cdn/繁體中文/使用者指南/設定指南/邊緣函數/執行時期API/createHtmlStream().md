---
title: "createHtmlStream()"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/HtmlStream-zh-tw"
---

解析和重寫流式 HTML 文件。

您可以使用此方法為 CSS 選擇器註冊回呼函式。呼叫此方法後，邊緣函數執行時將使用內建的 HTML 解析器來解析 HTML 文件。當 HTML 解析器解析到與 CSS 選擇器相符的元素時，將會呼叫處理 HTML 文件或 HTML 元素的回呼函式。這些回呼函式可用於在元素前後插入內容、變更元素屬性或刪除元素。

<span id="語法"></span>
## 語法

```JavaScript
createHtmlStream(ReadableStream, Object | null, Object | null)
```


<span id="參數"></span>
## 參數

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">參數必須依序提供，且不可省略中間的參數。</div>



* 第一個參數是 [ReadableStream](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Streams-cn-zh-tw#readablestream) 物件，代表要重寫的流式 HTML 文件。此 `ReadableStream` 物件不能被已讀取或被取消。此參數為必選。

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><code>createHtmlStream()</code> 不允許您傳入一個已被讀取或被取消的 <code>ReadableStream</code> 物件。   </div>
   

* 第二個參數是 [DocumentHandler](https://docs.byteplus.com/en/docs/18/45032#documenthandler) 物件，代表 HTML 文件級別的解析事件處理常式。如果您不需要監聽 HTML 文件級別的解析事件，可以將 `undefined` 或 `null` 傳遞給此參數。

* 第三個參數是一個陣列，其中每個元素都是一個包含兩個元素的子陣列。如果您不需要為任何元素設定解析事件處理常式，可以將 `undefined` 或 `null` 傳遞給此參數。此子陣列中包含的兩個元素代表：

   * [由 CSS 選擇器選取的標籤](https://docs.byteplus.com/en/docs/18/45032#css)。CSS 選擇器用於比對 HTML 元素。

   * 與 CSS 選擇器相符的 [ElementHandler](https://docs.byteplus.com/en/docs/18/45032#elementhandler) 物件。它代表 HTML 元素級別的解析事件處理常式，用於監聽和處理由 CSS 選擇器比對的 DOM 元素的解析事件。


<span id="傳回值"></span>
## 傳回值

此方法會傳回一個 [ReadableStream](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Streams-cn-zh-tw#readablestream) 物件，代表處理後的流式 HTML 文件。您可以將此方法傳回的 `ReadableStream` 物件作為對用戶端的回應傳回。

<span id="錯誤處理"></span>
## 錯誤處理

在回調函數中拋出的異常會導致整個流中斷為避免這種情況，建議您在回調函數內部使用 try...catch 陳述式來擷取和處理例外。

<span id="範例程式碼"></span>
# 範例程式碼

您可以參考下列範例程式碼，以了解如何使用 `createHtmlStream()` 方法重寫流式 HTML 頁面。

<span id="重寫-html-頁面中的外部連結"></span>
### 重寫 HTML 頁面中的外部連結

當網站啟用 IPv6 後，若頁面中通過外部連結引用的第三方資源僅支援 IPv4，純 IPv6 網路環境下的使用者存取這些資源時會失敗，導致頁面出現無法載入內容的空白區域。為解決此問題，一種有效的方案是將這些外部連結重定向至一個支援 IPv4/IPv6 雙棧的 IP 轉發服務。該服務接收來自 IPv6 用戶的請求，再代表用戶去訪問僅支援 IPv4 的資源，並把結果返回給用戶。

下面的範例程式碼示範了如何使用 `createHtmlStream()` 方法比對並修改頁面中所有 `<a>` 標籤的 `href` 屬性，從而將連結指向您指定的 IP 轉發服務位址。`createHtmlStream()` 方法對流式 HTML 的處理在邊緣函式執行時內部基於零複製原則完成，而且不依賴網頁載入 JavaScript 程式碼，因此不會對首位元組時間（TTFB）造成影響。

```javascript
addEventListener('fetch', (event) => {
  event.respondWith(handle(event));
});

async function handle(event) {
  // 獲取原始 HTML 頁面。
  const req = await fetch('https://origin.example.com');

  // 透過 CSS 選擇器比對需要重寫的元素，然後重寫 HTML 頁面內容。
  const htmlStream = createHtmlStream(
      req.body,  // 參數 1：需要重寫的 ReadableStream 物件，即來源伺服器回應的 body。
      undefined, // 參數 2：文件級別的處理器，此處未使用。
      [['a',      // 參數 3：一個陣列，包含 CSS 選擇器和對應的處理器。
        {
          // onElement 處理器：當解析到 <a> 標籤時觸發。
          onElement(element) {
            console.assert(element.tagName == 'a');
            if (element.hasAttribute('href')) {
              const href = element.getAttribute('href');
              // 將 href 屬性值修改為 IP 轉發服務的位址。
              element.setAttribute(
                  'href', `https://ipforwardservice.example.com?url=${href}` );
            }
          }
        }
      ]]);

  // 返回修改後的 ReadableStream 物件作為對客戶端的應答。
  return htmlStream;
}
```


<span id="非同步獲取內容並將獲取的內容注入-html-頁面"></span>
### 非同步獲取內容並將獲取的內容注入 HTML 頁面

`createHtmlStream()` 方法使您能夠在邊緣節點上動態修改 HTML 回應。一個常見的應用場景是：在 HTML 中定義一個預留位置標籤，然後在邊緣非同步獲取資料，並將獲取到的資料注入到 HTML 中，以取代該預留位置。此方法使您無需修改您的應用服務邏輯，即可實現動態內容的分發。

例如，假設您的 HTML 頁面中包含一個自訂的 `<fetch>` 標籤。您希望在邊緣節點獲取该標籤 `url` 屬性所指向的內容，然後用獲取到的內容取代该標籤。

**處理前**

```html
<html>
  <head></head>
  <body>
    <!-- 頁面中包含一個自訂的 fetch 標籤 -->
    <fetch url="https://api.example.com/data"></fetch>
  </body>
</html>
```


**處理後**

```html
<html>
  <head></head>
  <body>
  <!-- fetch 標籤被其 url 指向的內容取代 -->
    data
  </body>
</html>
```


下面的範例程式碼示範了如何實現以上效果。

```javascript
addEventListener('fetch', (event) => {
  event.respondWith(handle(event));
});

async function handle(event) {
  // 獲取原始 HTML 頁面。
  const req = await fetch(event.request);

  // 透過 CSS 選擇器比對需要重寫的元素，然後重寫 HTML 頁面內容。
  const htmlStream = createHtmlStream(
      req.body,  // 參數 1：需要重寫的 ReadableStream 物件。
      undefined, // 參數 2：文件級別的處理器，此處未使用。
      [[
        'fetch', // 參數 3：CSS 選擇器，此處比對所有 <fetch> 標籤。
        {
          // onElement 處理器：當解析到 <fetch> 標籤時觸發。
          async onElement(element) {
            console.assert(element.tagName == 'fetch');
            if (element.hasAttribute('url')) {
              const url = element.getAttribute('url');
              // 非同步獲取 url 指向的內容。
              const content = await fetch(url);
              const text = await content.text();
              // 使用獲取的內容取代 <fetch> 標籤。
              element.replace(text, {isHtml: true});
            }
          }
        }
      ]]);

  // 返回修改後的 ReadableStream 物件作為對客戶端的應答。
  return htmlStream;
}
```


<span id="解析事件處理常式"></span>
# 解析事件處理常式

<span id="documenthandler"></span>
## DocumentHandler

HTML 文件級別的解析事件處理常式，用於處理 HTML 文件的所有解析事件，包括 `<html>` 標籤之外的內容。

您可以使用下列回呼函式。每個回呼函式都是可選的，且每個回呼函式都可以是非同步函式。HTML 文件解析事件處理常式的回呼函式不會由 CSS 選擇器觸發。

<span id="ondoctype-doctype"></span>
### onDoctype(doctype)

在解析 HTML 文件的 DOCTYPE 節點時呼叫。

<span id="參數"></span>
#### 參數

`doctype`：一個 [HtmlDoctype](https://docs.byteplus.com/en/docs/18/45032#htmldoctype) 物件。

<span id="ondocend-docend"></span>
### onDocend(docend)

在整個 HTML 文件都已解析完成時呼叫。此回呼的唯一功能是為 HTML 文件新增頁尾。

<span id="參數"></span>
#### 參數

`docend`：一個 [HtmlDocend](https://docs.byteplus.com/en/docs/18/45032#htmldocend) 物件。

<span id="oncomment-comment"></span>
### onComment(comment)

在解析 HTML 文件的註解節點時呼叫。

<span id="參數"></span>
#### 參數

`comment`：一個 [HtmlComment](https://docs.byteplus.com/en/docs/18/45032#htmlcomment) 物件。

<span id="ontext-text"></span>
### onText(text)

在解析 HTML 文件的文字節點時呼叫。

文字節點的內容在流式解析期間可能會以多個片段傳輸，因此對於同一個文字節點，`onText()` 可能會被多次呼叫。例如，對於一段 HTML `<html>This is long text</html>`，如果 `This is long text` 分兩部分傳回，那麼雖然 `This is long text` 是一個文字節點，但 `onText()` 會被呼叫兩次。您可以使用 [lastInTextNode](https://docs.byteplus.com/en/docs/18/45032#lastintextnode) 屬性來判斷是否為最後一次呼叫。

<span id="參數"></span>
#### 參數

`text`：一個 [HtmlText](https://docs.byteplus.com/en/docs/18/45032#htmltext) 物件。

<span id="elementhandler"></span>
## ElementHandler

HTML 元素級別的解析事件處理常式，用於監聽和處理由 CSS 選擇器比對的 DOM 元素的解析事件。

您可以使用下列回呼函式。每個回呼函式都是可選的，且每個回呼函式都可以是非同步函式。

<span id="oncomment-comment"></span>
### onComment(comment)

當解析到由 CSS 選擇器比對的元素內的註解節點時，會呼叫此回呼。

<span id="參數"></span>
#### 參數

`comment`：一個 [HtmlComment](https://docs.byteplus.com/en/docs/18/45032#htmlcomment) 物件。

<span id="ontext-text"></span>
### onText(text)

當解析到由 CSS 選擇器比對的元素內的文字節點時，會呼叫此回呼。

文字節點的內容在流式解析期間可能會以多個片段傳輸，因此對於同一個文字節點，`onText()` 可能會被多次呼叫。例如，對於一段 HTML `<div>This is long text</div>`，如果 `This is long text` 分兩部分傳回，那麼雖然 `This is long text` 是一個文字節點，但 `onText()` 會被呼叫兩次。您可以使用 [lastInTextNode](https://docs.byteplus.com/en/docs/18/45032#lastintextnode) 屬性來判斷是否為最後一次呼叫。

<span id="參數"></span>
#### 參數

`text`：一個 [HtmlText](https://docs.byteplus.com/en/docs/18/45032#htmltext) 物件。

<span id="onelement-element"></span>
### onElement(element)

當解析到由 CSS 選擇器選取的標籤時，會呼叫此回呼函式。如果 CSS 選擇器比對多個標籤，`onElement()` 將會被多次呼叫。


* `element`：一個 [HtmlElement](https://docs.byteplus.com/en/docs/18/45032#htmlelement) 物件。


<span id="html-節點物件"></span>
# HTML 節點物件

<span id="htmldoctype"></span>
## HtmlDoctype

代表一個 DOCTYPE 節點。包含 `name`、`publicId` 和 `systemId` 屬性。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">例如，在下列 DOCTYPE 節點中，<code>name</code> 是 <code>HTML</code>；<code>publicId</code> 是 <code>-//W3C//DTD HTML 4.01 Transitional//EN</code>；<code>systemId</code> 是 <code>https://www.w3.org/TR/html4/loose.dtd</code>。</div>


<div data-tips="true" data-tips-type="tip">```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "https://www.w3.org/TR/html4/loose.dtd">
```
</div>


<span id="name"></span>
### name

一個 [String 物件](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/String)，代表 DOCTYPE 節點的名稱。

<span id="publicid"></span>
### publicId

一個 [String 物件](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/String)，代表 DOCTYPE 節點的公開 ID。

<span id="systemid"></span>
### systemId

一個 [String 物件](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/String)，代表 DOCTYPE 節點的系統 ID。

<span id="htmldocend"></span>
## HtmlDocend

代表 HTML 文件解析的結束。包含下列方法：

<span id="append-string-contentoption"></span>
### append(String, ContentOption)

在 HTML 文件中插入頁尾。


* 第一個參數是一個 [String 物件](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/String)，代表要插入的內容。

* 第二個參數是一個 `ContentOption` 物件。此物件包含唯一的屬性 `isHtml`。此屬性是一個 [Boolean 物件](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Boolean)，表示第一個參數的內容類型是否為 HTML：

   * true：表示第一個參數的內容類型為 HTML。第一個參數的內容將不會進行 HTML 逸出。

   * false：表示第一個參數的內容類型不是 HTML。第一個參數的內容將在插入 HTML 文件之前進行 HTML 逸出。


例如：

```JavaScript
append("not html", {isHtml: false});
```


<span id="htmlcomment"></span>
## HtmlComment

代表已解析的註解節點。包含下列方法和屬性：

<span id="set-string"></span>
### set(String)

變更註解的內容。

<span id="before-string-contentoption"></span>
### before(String, ContentOption)

在註解節點之前插入內容。

<span id="參數"></span>
#### 參數


* 第一個參數是一個 [String 物件](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/String)，代表要插入的內容。

* 第二個參數是一個 `ContentOption` 物件。此物件包含唯一的屬性 `isHtml`。此屬性是一個 [Boolean 物件](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Boolean)，表示第一個參數的內容類型是否為 HTML：

   * true：表示第一個參數的內容類型為 HTML。第一個參數的內容將不會進行 HTML 逸出。

   * false：表示第一個參數的內容類型不是 HTML。第一個參數的內容將在插入 HTML 文件之前進行 HTML 逸出。


<span id="after-string-contentoption"></span>
### after(String, ContentOption)

在註解節點之後插入內容。

<span id="參數"></span>
#### 參數


* 第一個參數是一個 [String 物件](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/String)，代表要插入的內容。

* 第二個參數是一個 `ContentOption` 物件。此物件包含唯一的屬性 `isHtml`。此屬性是一個 [Boolean 物件](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Boolean)，表示第一個參數的內容類型是否為 HTML：

   * true：表示第一個參數的內容類型為 HTML。第一個參數的內容將不會進行 HTML 逸出。

   * false：表示第一個參數的內容類型不是 HTML。第一個參數的內容將在插入 HTML 文件之前進行 HTML 逸出。


<span id="replace-string-contentoption"></span>
### replace(String, ContentOption)

取代註解節點。

<span id="參數"></span>
#### 參數


* 第一個參數是用於取代節點的 [String 物件](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/String)。此字串將取代整個節點。

* 第二個參數是一個 `ContentOption` 物件。此物件包含唯一的屬性 `isHtml`。此屬性是一個 [Boolean 物件](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Boolean)，表示第一個參數的內容類型是否為 HTML：

   * true：表示第一個參數的內容為 HTML。第一個參數的內容將不會進行 HTML 逸出。

   * false：表示第一個參數的內容不是 HTML。第一個參數的內容將在插入 HTML 文件之前進行 HTML 逸出。


<span id="remove"></span>
### remove()

刪除註解節點。

<span id="removed"></span>
### removed

一個 [Boolean 物件](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Boolean)，表示標籤是否已刪除。


* true：標籤已刪除。

* false：標籤未刪除。


<span id="value"></span>
### value

一個 [String 物件](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/String)，代表註解節點的內容。

<span id="htmltext"></span>
## HtmlText

代表一個文字節點。包含下列方法和屬性：

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">在流式解析中，同一個文字節點的內容可能會被分割成多個片段。您需要使用 <a href="https://docs.byteplus.com/en/docs/18/45032#lastInTextNode">lastInTextNode</a> 屬性來判斷整個文字節點的內容是否已完全解析。</div>


<span id="before-string-contentoption"></span>
### before(String, ContentOption)

在文字節點之前插入內容。

<span id="參數"></span>
#### 參數


* 第一個參數是一個 [String 物件](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/String)，代表要插入的內容。

* 第二個參數是一個 `ContentOption` 物件。此物件包含唯一的屬性 `isHtml`。此屬性是一個 [Boolean 物件](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Boolean)，表示第一個參數的內容類型是否為 HTML：

   * true：表示第一個參數的內容類型為 HTML。第一個參數的內容將不會進行 HTML 逸出。

   * false：表示第一個參數的內容類型不是 HTML。第一個參數的內容將在插入 HTML 文件之前進行 HTML 逸出。


<span id="after-string-contentoption"></span>
### after(String, ContentOption)

在文字節點之後插入內容。

<span id="參數"></span>
#### 參數


* 第一個參數是一個 [String 物件](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/String)，代表要插入的內容。

* 第二個參數是一個 `ContentOption` 物件。此物件包含唯一的屬性 `isHtml`。此屬性是一個 [Boolean 物件](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Boolean)，表示第一個參數的內容類型是否為 HTML：

   * true：表示第一個參數的內容類型為 HTML。第一個參數的內容將不會進行 HTML 逸出。

   * false：表示第一個參數的內容類型不是 HTML。第一個參數的內容將在插入 HTML 文件之前進行 HTML 逸出。


<span id="replace-string-contentoption"></span>
### replace(String, ContentOption)

取代文字節點。

<span id="參數"></span>
#### 參數


* 第一個參數是用於取代節點的 [String 物件](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/String)。此 String 物件將取代整個節點。

* 第二個參數是一個 `ContentOption` 物件。此物件包含唯一的屬性 `isHtml`。此屬性是一個 [Boolean 物件](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Boolean)，表示第一個參數的內容類型是否為 HTML：

   * true：表示第一個參數的內容為 HTML。第一個參數的內容將不會進行 HTML 逸出。

   * false：表示第一個參數的內容不是 HTML。第一個參數的內容將在插入 HTML 文件之前進行 HTML 逸出。


<span id="remove"></span>
### remove()

刪除文字節點。

<span id="value"></span>
### value

一個 [String 物件](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/String)，代表文字節點的內容。如果目前 `HtmlText` 物件中包含的片段是文字節點的最後一個片段，則此屬性會傳回一個空字串。

<span id="removed"></span>
### removed

一個 [Boolean 物件](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Boolean)，表示文字節點是否已刪除。


* true：文字節點已刪除。

* false：文字節點未刪除。


<span id="lastintextnode"></span>
### lastInTextNode

一個 [Boolean 物件](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Boolean)，表示目前 `HtmlText` 物件中包含的片段是否為文字節點的最後一個片段。


* true：目前 `HtmlText` 物件中包含的片段是文字節點的最後一個片段。

* false：目前 `HtmlText` 物件中包含的片段不是文字節點的最後一個片段。


`onText()` 回呼可能會針對同一個文字節點觸發多次。如果您需要取得整個文字節點的內容，可以緩衝內容，直到文字節點的 `lastInTextNode` 屬性為 true。

<span id="範例"></span>
### 範例

以下範例展示如何使用 `onText` 回呼來擷取和轉換 HTML 文件中的文字內容。在此範例中，所有文字節點的內容都將轉換為大寫。

```javascript
addEventListener('fetch', (event) => {
  event.respondWith(handle(event));
});

async function handle(event) {
  // 獲取原始 HTML 頁面。
  const req = await fetch(event.request);

  // 建立一個 buffer 用於在 onText 事件中拼接文字塊。
  // onText 在單個文字節點上可能觸發多次，因此需要拼接。
  let buffer = [];
  const htmlStream = createHtmlStream(
      req.body,  // 參數 1：傳入 ReadableStream，即原始回應的 body。
      undefined, // 參數 2：DocumentHandler，此處不處理文件級事件。
      [[         // 參數 3：ElementHandler 陣列，用於處理特定元素。
        '*',   // 使用 CSS 選擇器 '*' 匹配所有元素。
        {
          // onText 處理器：當解析到文字節點時觸發。
          onText(text) {
            // 將當前文字塊存入 buffer。
            buffer.push(text.value);
            // lastInTextNode 為 true 表示這是當前文字節點的最後一個文字塊。
            if (text.lastInTextNode) {
              // 拼接所有文字塊，形成完整的文字。
              const data = buffer.join("");
              // 將文字轉換為大寫，並替換原始文字。
              text.replace(data.toUpperCase());
              // 重置 buffer，為處理下一個文字節點做準備。
              buffer = [];
            }
          }
        }
      ]]);

  // 返回修改後的 ReadableStream 物件作為對客戶端的應答。
  return htmlStream;
}
```


<span id="htmlelement"></span>
## HtmlElement

代表與 CSS 選擇器選取的標籤對應的 HTML 元素。包含下列方法和屬性：

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">假設目前的 HTML 元素是一個 div 節點，<code>after()</code>、<code>before()</code>、<code>append()</code>、<code>prepend()</code> 和 <code>setInnerContent()</code> 的內容插入位置如下圖所示。</div>


<div data-tips="true" data-tips-type="tip"><img src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_86b8dec24c73c57a2a3731e077b30a1e.jpeg" width="500px" /></div>


<span id="setattribute-string-string"></span>
### setAttribute(String, String)

設定 HTML 元素的屬性值。

<span id="參數"></span>
#### 參數


* 第一個參數是屬性名稱。

* 第二個參數是屬性值。


<span id="after-string-contentoption"></span>
### after(String, ContentOption)

在此標籤之後插入內容。

<span id="參數"></span>
#### 參數


* 第一個參數是一個 [String 物件](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/String)，代表要插入的內容。

* 第二個參數是一個 `ContentOption` 物件。此物件包含唯一的屬性 `isHtml`。此屬性是一個 [Boolean 物件](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Boolean)，表示第一個參數的內容類型是否為 HTML：

   * true：表示第一個參數的內容類型為 HTML。第一個參數的內容將不會進行 HTML 逸出。

   * false：表示第一個參數的內容類型不是 HTML。第一個參數的內容將在插入 HTML 文件之前進行 HTML 逸出。


<span id="append-string-contentoption"></span>
### append(String, ContentOption)

在此標籤內的內容之後插入內容。

<span id="參數"></span>
#### 參數


* 第一個參數是一個 [String 物件](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/String)，代表要插入的內容。

* 第二個參數是一個 `ContentOption` 物件。此物件包含唯一的屬性 `isHtml`。此屬性是一個 [Boolean 物件](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Boolean)，表示第一個參數的內容類型是否為 HTML：

   * true：表示第一個參數的內容類型為 HTML。第一個參數的內容將不會進行 HTML 逸出。

   * false：表示第一個參數的內容類型不是 HTML。第一個參數的內容將在插入 HTML 文件之前進行 HTML 逸出。


<span id="prepend-string-contentoption"></span>
### prepend(String, ContentOption)

在此標籤內的內容之前插入內容。

<span id="參數"></span>
#### 參數


* 第一個參數是一個 [String 物件](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/String)，代表要插入的內容。

* 第二個參數是一個 `ContentOption` 物件。此物件包含唯一的屬性 `isHtml`。此屬性是一個 [Boolean 物件](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Boolean)，表示第一個參數的內容類型是否為 HTML：

   * true：表示第一個參數的內容類型為 HTML。第一個參數的內容將不會進行 HTML 逸出。

   * false：表示第一個參數的內容類型不是 HTML。第一個參數的內容將在插入 HTML 文件之前進行 HTML 逸出。


<span id="setinnercontent-string-contentoption"></span>
### setInnerContent(String, ContentOption)

修改標籤內的內容。

<span id="參數"></span>
#### 參數


* 第一個參數是一個 [String 物件](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/String)，代表要設定的內容。

* 第二個參數是一個 `ContentOption` 物件。此物件包含唯一的屬性 `isHtml`。此屬性是一個 [Boolean 物件](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Boolean)，表示第一個參數的內容類型是否為 HTML：

   * true：表示第一個參數的內容類型為 HTML。第一個參數的內容將不會進行 HTML 逸出。

   * false：表示第一個參數的內容類型不是 HTML。第一個參數的內容將在插入 HTML 文件之前進行 HTML 逸出。


<span id="removeandkeepcontent"></span>
### removeAndKeepContent()

刪除標籤但保留其子節點內容。

<span id="replace-string-contentoption"></span>
### replace(String, ContentOption)

取代標籤。

<span id="參數"></span>
#### 參數


* 第一個參數是用於取代節點的 [String 物件](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/String)。此字串將取代整個節點。

* 第二個參數是一個 `ContentOption` 物件。此物件包含唯一的屬性 `isHtml`。此屬性是一個 [Boolean 物件](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Boolean)，表示第一個參數的內容類型是否為 HTML：

   * true：表示第一個參數的內容為 HTML。第一個參數的內容將不會進行 HTML 逸出。

   * false：表示第一個參數的內容不是 HTML。第一個參數的內容將在插入 HTML 文件之前進行 HTML 逸出。


<span id="remove"></span>
### remove()

刪除節點。

<span id="hasattribute-string"></span>
### hasAttribute(String)

檢查屬性是否存在並傳回一個 [Boolean 物件](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Boolean)。


* true：屬性存在。

* false：屬性不存在。


參數是一個 [String 物件](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/String)，代表屬性的名稱。

<span id="getattribute-string"></span>
### getAttribute(String)

傳回一個 [String 物件](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/String)，代表屬性的值，如果屬性不存在則傳回 null。

參數是一個 [String 物件](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/String)，代表屬性的名稱。

<span id="removeattribute-string"></span>
### removeAttribute(String)

刪除一個屬性。

參數是一個 [String 物件](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/String)，代表屬性的名稱。

<span id="iterator"></span>
### [@iterator]

用於遍歷 [HtmlElement](https://docs.byteplus.com/en/docs/18/45032#htmlelement) 物件的屬性。對於每個屬性，該迭代器傳回一個包含 2 個元素的 Array 對象，`[0]` 表示屬性的名字，`[1]` 表示屬性的值。

```JavaScript
for (const attribute of element) {
    console.log(attribute[0]);
    console.log(attribute[1]);
}

// 如果上述範例迭代 <a attr='1', attr2='2'> 標籤
// 它將列印
// attr
// 1
// attr2
// 2
```


<span id="tagname"></span>
### tagName

一個 [String 物件](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/String)。取得或設定目前的標籤名稱。

<span id="namespaceuri"></span>
### namespaceUri

一個 [String 物件](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/String)。取得標籤的 XML 命名空間。

<span id="removed"></span>
### removed

一個 [Boolean 物件](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Boolean)，表示標籤是否已刪除。


* true：標籤已刪除。

* false：標籤未刪除。


<span id="如何使用-css-選擇器"></span>
# 如何使用 CSS 選擇器

&nbsp;

CSS 選擇器用於比對 HTML 元素。常見用法如下：

<span id="選取指定類型的所有標籤"></span>
### 選取指定類型的所有標籤

`"a"` 選取所有 a 標籤。

<span id="選取特定標籤下的子節點"></span>
### 選取特定標籤下的子節點

`"a div"` 選取 a 標籤下的 div 標籤。

<span id="選取所有標籤"></span>
### 選取所有標籤

`"*"`

<span id="選取某個標籤下的子節點"></span>
### 選取某個標籤下的子節點

`"a > b"`：選取 b 標籤。b 標籤的父節點名為 a。

<span id="選取具有指定屬性和類型的所有標籤"></span>
### 選取具有指定屬性和類型的所有標籤

`"a[x]"`：選取具有屬性 x 的所有 a 標籤。

<span id="選取具有指定類別和類型的所有標籤"></span>
### 選取具有指定類別和類型的所有標籤

`"a.u"`：選取具有類別屬性 u 的所有 a 標籤。

<span id="選取具有指定-id-和類型的所有標籤"></span>
### 選取具有指定 ID 和類型的所有標籤

`"a#u"`：選取具有 ID u 的所有 a 標籤。

<span id="選取具有指定屬性名稱、屬性值和類型的所有標籤"></span>
### 選取具有指定屬性名稱、屬性值和類型的所有標籤

`"a[y=\"z\"]"`：選取屬性名稱為 y 且屬性值為 z 的所有 a 標籤。

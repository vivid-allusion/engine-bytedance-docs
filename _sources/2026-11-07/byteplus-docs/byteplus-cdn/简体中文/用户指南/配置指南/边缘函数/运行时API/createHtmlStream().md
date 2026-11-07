---
title: "createHtmlStream()"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/HtmlStream"
---

解析和重写流式 HTML 文档。

您可以通过该方法为 CSS 选择器注册回调函数。该方法被调用后，边缘函数运行时会使用内置的 HTML 解析器解析 HTML 文档。当 HTML 解析器解析到与 CSS 选择器匹配的元素时，用于处理 HTML 文档或 HTML 元素的回调函数会被调用。这些回调函数可以用于在元素前后插入内容、更改元素属性或删除元素。

<span id="语法"></span>
## 语法

```JavaScript
createHtmlStream(ReadableStream, Object | null, Object | null)
```


<span id="参数"></span>
## 参数

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">参数必须按顺序提供，不能省略中间的参数。</div>



* 第一个参数是一个 [ReadableStream](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Streams-cn#readablestream) 对象，表示需要被重写的流式 HTML 文档。该参数为必选。

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><code>createHtmlStream()</code> 不允许您传入一个已被读取或被取消的 <code>ReadableStream</code> 对象。   </div>
   

* 第二个参数是一个 [DocumentHandler](https://docs.byteplus.com/en/docs/18/36057#documenthandler) 对象，表示 HTML 文档级别的解析事件处理器。如果您不需要监听 HTML 文档级别的解析事件，可以向该参数传入 `undefined` 或者 `null`。

* 第三个参数是一个数组，其中的每个元素都是一个包含两个元素的子数组。如果您不需要为任何 HTML 元素设置解析事件处理器，可以向该参数传入 `undefined` 或者 `null`。该子数组包含的两个元素分别表示：

   * 一个 [CSS 选择器选择的标签](https://docs.byteplus.com/en/docs/18/36057#css)。CSS 选择器用于匹配 HTML 元素。

   * 与 CSS 选择器匹配的 [ElementHandler](https://docs.byteplus.com/en/docs/18/36057#elementhandler) 对象。表示 HTML 元素级别的解析事件处理器，用于监听并处理 CSS 选择器匹配到的 DOM 元素的解析事件。


<span id="返回值"></span>
## 返回值

该方法会返回一个 [ReadableStream](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Streams-cn#readablestream) 对象，表示处理完成的流式 HTML 文档。您可以把该方法返回的 `ReadableStream` 对象作为响应返回给客户端。

<span id="错误处理"></span>
## 错误处理

在回调函数中抛出的异常会导致整个流被中断。为了避免这种情况，建议您在回调函数内部使用 try...catch 语句来捕获和处理异常。

<span id="示例代码"></span>
# 示例代码

您可以参考下面的示例代码了解如何使用 `createHtmlStream()` 对流式 HTML 页面进行重写。

<span id="重写-html-页面中的外部链接"></span>
### 重写 HTML 页面中的外部链接

当网站启用 IPv6 后，若页面中通过外部链接引用的第三方资源仅支持 IPv4，纯 IPv6 网络环境下的用户访问这些资源时会失败，导致页面出现无法加载内容的空白区域。这一现象被称为“天窗”问题。为解决此问题，一种有效的方案是将这些外部链接重定向至一个支持 IPv4/IPv6 双栈的 IP 转发服务。该服务接收来自 IPv6 用户的请求，再代表用户去访问仅支持 IPv4 的资源，并把结果返回给用户。

下面的示例代码演示了如何使用 `createHtmlStream()` 方法匹配并修改页面中所有 `<a>` 标签的 `href` 属性，从而将链接指向您指定的 IP 转发服务地址。`createHtmlStream()` 方法对流式 HTML 的处理在边缘函数运行时内部基于零拷贝原则完成，而且不依赖网页加载 JavaScript 代码，因此不会对首字节时间（TTFB）造成影响。

```javascript
addEventListener('fetch', (event) => {
  event.respondWith(handle(event));
});

async function handle(event) {
  // 获取原始 HTML 页面。
  const req = await fetch('https://origin.example.com');

  // 通过 CSS 选择器匹配需要重写的元素，然后重写 HTML 页面内容。
  const htmlStream = createHtmlStream(
      req.body,  // 参数 1：需要重写的 ReadableStream 对象，即源站响应的 body。
      undefined, // 参数 2：文档级别的处理器，此处未使用。
      [['a',      // 参数 3：一个数组，包含 CSS 选择器和对应的处理器。
        {
          // onElement 处理器：当解析到 <a> 标签时触发。
          onElement(element) {
            console.assert(element.tagName == 'a');
            if (element.hasAttribute('href')) {
              const href = element.getAttribute('href');
              // 将 href 属性值修改为 IP 转发服务的地址。
              element.setAttribute(
                  'href', `https://ipforwardservice.example.com?url=${href}` );
            }
          }
        }
      ]]);

  // 返回修改后的 ReadableStream 对象作为对客户端的响应。
  return htmlStream;
}
```


<span id="异步获取内容并将获取的内容注入-html-页面"></span>
### 异步获取内容并将获取的内容注入 HTML 页面

`createHtmlStream()` 方法使您能够在边缘节点上动态修改 HTML 响应。一个常见的应用场景是：在 HTML 中定义一个占位符标签，然后在边缘异步获取数据，并将获取到的数据注入到 HTML 中，以替换该占位符。此方法使您无需修改您的应用服务逻辑，即可实现动态内容的分发。

例如，假设您的 HTML 页面中包含一个自定义的 `<fetch>` 标签。您希望在边缘节点获取该标签 `url` 属性所指向的内容，然后用获取到的内容替换掉该标签。

**处理前**

```html
<html>
  <head></head>
  <body>
    <!-- 页面中包含一个自定义的 fetch 标签 -->
    <fetch url="https://api.example.com/data"></fetch>
  </body>
</html>
```


**处理后**

```html
<html>
  <head></head>
  <body>
  <!-- fetch 标签被其 url 指向的内容替换 -->
    data
  </body>
</html>
```


下面的示例代码演示了如何实现以上效果。

```javascript
addEventListener('fetch', (event) => {
  event.respondWith(handle(event));
});

async function handle(event) {
  // 获取原始 HTML 页面。
  const req = await fetch(event.request);

  // 通过 CSS 选择器匹配需要重写的元素，然后重写 HTML 页面内容。
  const htmlStream = createHtmlStream(
      req.body,  // 参数 1：需要重写的 ReadableStream 对象。
      undefined, // 参数 2：文档级别的处理器，此处未使用。
      [[
        'fetch', // 参数 3：CSS 选择器，此处匹配所有 <fetch> 标签。
        {
          // onElement 处理器：当解析到 <fetch> 标签时触发。
          async onElement(element) {
            console.assert(element.tagName == 'fetch');
            if (element.hasAttribute('url')) {
              const url = element.getAttribute('url');
              // 异步获取 url 指向的内容。
              const content = await fetch(url);
              const text = await content.text();
              // 使用获取的内容替换 <fetch> 标签。
              element.replace(text, {isHtml: true});
            }
          }
        }
      ]]);

  // 返回修改后的 ReadableStream 对象作为对客户端的响应。
  return htmlStream;
}
```


<span id="解析事件处理器"></span>
# 解析事件处理器

<span id="documenthandler"></span>
## DocumentHandler

HTML 文档级别的解析事件 Handler，用于处理 HTML 文档的全部解析事件，包括 `<html>` 标签外的内容。

您可以使用如下回调函数。每个回调函数都是可选的，且每个回调函数可以是异步函数。HTML 文档解析事件 Handler 的回调函数不会被 CSS 选择器触发。

<span id="ondoctype-doctype"></span>
### onDoctype(doctype)

当 HTML 文档的 DOCTYPE 节点被解析到时被调用。

<span id="参数"></span>
#### 参数

`doctype`：一个 [HtmlDoctype](https://docs.byteplus.com/en/docs/18/36057#htmldoctype) 对象。

<span id="ondocend-docend"></span>
### onDocend(docend)

当整个 HTML 文档被解析完毕后被调用。该回调函数的唯一作用是向 HTML 文档加入 footer。

<span id="参数"></span>
#### 参数

`docend`：一个 [HtmlDocend](https://docs.byteplus.com/en/docs/18/36057#htmldocend) 对象。

<span id="oncomment-comment"></span>
### onComment(comment)

当 HTML 文档的 Comment 节点被解析到时被调用。

<span id="参数"></span>
#### 参数

`comment`：一个 [HtmlComment](https://docs.byteplus.com/en/docs/18/36057#htmlcomment) 对象。

<span id="ontext-text"></span>
### onText(text)

当 HTML 文档的 Text 节点被解析到时被调用。

一个 Text 节点的内容在流式解析的过程中可能分多个片段传输，因此 `onText()` 可能针对同一个 Text 节点被调用多次。例如，对于一段 HTML `<html>This is long text</html>`，如果 `This is long text` 被切成两部分返回，那么虽然 `This is long text`是一个 Text 节点，但是 `onText()` 会被调用两次。您可以通过 [lastInTextNode](https://docs.byteplus.com/en/docs/18/36057#lastintextnode) 属性去分辨是不是最后一次调用。

<span id="参数"></span>
#### 参数

`text`：一个 [HtmlText](https://docs.byteplus.com/en/docs/18/36057#htmltext) 对象。

<span id="elementhandler"></span>
## ElementHandler

HTML 元素级别的解析事件处理器，用于监听并处理 CSS 选择器匹配到的 DOM 元素的解析事件。

您可以使用如下回调函数。每个回调函数都是可选的，且每个回调函数都可以是异步函数。

<span id="oncomment-comment"></span>
### onComment(comment)

当 CSS 选择器匹配到的元素内的 Comment 节点被解析到时，该回调被调用。

<span id="参数"></span>
#### 参数

`comment`：一个 [HtmlComment](https://docs.byteplus.com/en/docs/18/36057#htmlcomment) 对象。

<span id="ontext-text"></span>
### onText(text)

当 CSS 选择器匹配到的元素内的 Text 节点被解析到时，该回调被调用。

一个 Text 节点的内容在流式解析的过程中可能分多个片段传输，因此 `onText()` 可能针对同一个 Text 节点被调用多次。例如，对于一段 HTML `<div>This is long text</div>`，如果 `This is long text` 被切成两部分返回，那么虽然 `This is long text`是一个 Text 节点，但是 `onText()` 会被调用两次。您可以通过 [lastInTextNode](https://docs.byteplus.com/en/docs/18/36057#lastintextnode) 属性去分辨是不是最后一次调用。

<span id="参数"></span>
#### 参数

`text`：一个 [HtmlText](https://docs.byteplus.com/en/docs/18/36057#htmltext) 对象。

<span id="onelement-element"></span>
### onElement(element)

当 CSS 选择器选择的标签被解析到时，该回调函数被调用。如果 CSS 选择器匹配到多个标签，`onElement()` 会被多次调用。


* `element`：一个 [HtmlElement](https://docs.byteplus.com/en/docs/18/36057#htmlelement) 对象。


<span id="html-节点对象"></span>
# HTML 节点对象

<span id="htmldoctype"></span>
## HtmlDoctype

表示一个 DOCTYPE 节点。包含 `name`、`publicId` 和 `systemId` 属性。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">例如，在下面的 DOCTYPE 节点中，<code>name</code> 是 <code>HTML</code>；<code>publicId</code> 是 <code>-//W3C//DTD HTML 4.01 Transitional//EN</code>；<code>systemId</code> 是 <code>https://www.w3.org/TR/html4/loose.dtd</code>。</div>


<div data-tips="true" data-tips-type="tip">```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "https://www.w3.org/TR/html4/loose.dtd">
```
</div>


<span id="name"></span>
### name

一个 [String 对象](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)，表示 DOCTYPE 节点的名称。

<span id="publicid"></span>
### publicId

一个 [String 对象](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)，表示 DOCTYPE 节点的 public id。

<span id="systemid"></span>
### systemId

一个 [String 对象](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)，表示 DOCTYPE 节点的 system id。

<span id="htmldocend"></span>
## HtmlDocend

表示 HTML 文档解析结束。包含以下方法：

<span id="append-string-contentoption"></span>
### append(String, ContentOption)

向 HTML 文档插入 footer。


* 第一个参数是一个 [String 对象](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)，表示要插入的内容。

* 第二个参数是一个 `ContentOption` 对象。该对象包含唯一属性 `isHtml`。该属性是一个 [Boolean 对象](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)，用于表示第一个参数的内容类型是否是 HTML：

   * true：表示第一个参数的内容类型是 HTML。第一个参数的内容不会被 HTML 转义。

   * false：表示第一个参数的内容类型不是 HTML。第一个参数的内容会在插入到 HTML 文档前被 HTML 转义。


例如：

```JavaScript
append("not html", {isHtml: false});
```


<span id="htmlcomment"></span>
## HtmlComment

表示解析到的 Comment 节点。包含以下方法和属性：

<span id="set-string"></span>
### set(String)

更改注释的内容。

<span id="before-string-contentoption"></span>
### before(String, ContentOption)

在 Comment 节点之前插入内容。

<span id="参数"></span>
#### 参数


* 第一个参数是一个 [String 对象](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)，表示要插入的内容。

* 第二个参数是一个 `ContentOption` 对象。该对象包含唯一属性 `isHtml`。该属性是一个 [Boolean 对象](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)，用于表示第一个参数的内容类型是否是 HTML：

   * true：表示第一个参数的内容类型是 HTML。第一个参数的内容不会被 HTML 转义。

   * false：表示第一个参数的内容类型不是 HTML。第一个参数的内容会在插入到 HTML 文档前被 HTML 转义。


<span id="after-string-contentoption"></span>
### after(String, ContentOption)

在 Comment 节点之后插入内容。

<span id="参数"></span>
#### 参数


* 第一个参数是一个 [String 对象](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)，表示要插入的内容。

* 第二个参数是一个 `ContentOption` 对象。该对象包含唯一属性 `isHtml`。该属性是一个 [Boolean 对象](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)，用于表示第一个参数的内容类型是否是 HTML：

   * true：表示第一个参数的内容类型是 HTML。第一个参数的内容不会被 HTML 转义。

   * false：表示第一个参数的内容类型不是 HTML。第一个参数的内容会在插入到 HTML 文档前被 HTML 转义。


<span id="replace-string-contentoption"></span>
### replace(String, ContentOption)

替换 Comment 节点。

<span id="参数"></span>
#### 参数


* 第一个参数是用于替换节点的 [String 对象](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)。该 String 会替换整个节点。

* 第二个参数是一个 `ContentOption` 对象。该对象包含唯一属性 `isHtml`。该属性是一个 [Boolean 对象](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)，用于表示第一个参数的内容类型是否是 HTML：

   * true：表示第一个参数的内容是 HTML。第一个参数的内容不会被 HTML 转义。

   * false：表示第一个参数的内容不是 HTML。第一个参数的内容会在插入到 HTML 文档前被 HTML 转义。


<span id="remove"></span>
### remove()

删除 Comment 节点。

<span id="removed"></span>
### removed

一个 [Boolean 对象](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)，表示该标签是否被删除。


* true：该标签被删除。

* false：该标签未被删除。


<span id="value"></span>
### value

一个 [String 对象](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)，表示 Comment 节点的内容。

<span id="htmltext"></span>
## HtmlText

表示一个 Text 节点。包含以下方法和属性：

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">在流式解析中，同一个 Text 节点的内容可能被分为多个片段。您需要使用 <a href="https://docs.byteplus.com/en/docs/18/36057#lastInTextNode">lastInTextNode</a> 属性去判断整个 Text 节点的内容是否被完全解析。</div>


<span id="before-string-contentoption"></span>
### before(String, ContentOption)

在 Text 节点之前插入内容。

<span id="参数"></span>
#### 参数


* 第一个参数是一个 [String 对象](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)，表示要插入的内容。

* 第二个参数是一个 `ContentOption` 对象。该对象包含唯一属性 `isHtml`。该属性是一个 [Boolean 对象](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)，用于表示第一个参数的内容类型是否是 HTML：

   * true：表示第一个参数的内容是 HTML。第一个参数的内容不会被 HTML 转义。

   * false：表示第一个参数的内容不是 HTML。第一个参数的内容会在插入到 HTML 文档前被 HTML 转义。


<span id="after-string-contentoption"></span>
### after(String, ContentOption)

在 Text 节点之后插入内容。

<span id="参数"></span>
#### 参数


* 第一个参数是一个 [String 对象](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)，表示要插入的内容。

* 第二个参数是一个 `ContentOption` 对象。该对象包含唯一属性 `isHtml`。该属性是一个 [Boolean 对象](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)，用于表示第一个参数的内容类型是否是 HTML：

   * true：表示第一个参数的内容是 HTML。第一个参数的内容不会被 HTML 转义。

   * false：表示第一个参数的内容不是 HTML。第一个参数的内容会在插入到 HTML 文档前被 HTML 转义。


<span id="replace-string-contentoption"></span>
### replace(String, ContentOption)

替换 Text 节点。

<span id="参数"></span>
#### 参数


* 第一个参数是用于替换节点的 [String 对象](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)。该 String 对象会替换整个节点。

* 第二个参数是一个 `ContentOption` 对象。该对象包含唯一属性 `isHtml`。该属性是一个 [Boolean 对象](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)，用于表示第一个参数的内容类型是否是 HTML：

   * true：表示第一个参数的内容是 HTML。第一个参数的内容不会被 HTML 转义。

   * false：表示第一个参数的内容不是 HTML。第一个参数的内容会在插入到 HTML 文档前被 HTML 转义。


<span id="remove"></span>
### remove()

删除 Text 节点。

<span id="value"></span>
### value

一个 [String 对象](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)，表示 Text 节点的内容。如果当前的 `HtmlText` 对象所包含的分片是 Text 节点的最后一个分片，则该属性返回空字符串。

<span id="removed"></span>
### removed

一个 [Boolean 对象](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)，表示该 Text 节点是否被删除。


* true：该 Text 节点被删除。

* false：该 Text 节点未被删除。


<span id="lastintextnode"></span>
### lastInTextNode

一个 [Boolean 对象](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)，表示当前的 `HtmlText` 对象所包含的分片是否是 Text 节点的最后一个分片。


* true：当前的 `HtmlText` 对象所包含的分片是 Text 节点的最后一个分片。

* false：当前的 `HtmlText` 对象所包含的分片不是 Text 节点的最后一个分片。


`onText()` 回调可能针对同一个 Text 节点多次触发。如果您需要获取整个 Text 节点的内容，可以用缓冲区缓冲内容，直到 Text 节点的 `lastInTextNode` 属性为 true。

<span id="示例"></span>
### 示例

```JavaScript
addEventListener('fetch', (event) => {
  event.respondWith(handle(event));
});

async function handle(event) {
  // 获取原始 HTML 页面。
  const req = await fetch(event.request);

  // 创建一个 buffer 用于在 onText 事件中拼接文本块。
  // onText 在单个文本节点上可能触发多次，因此需要拼接。
  let buffer = [];
  const htmlStream = createHtmlStream(
      req.body,  // 参数 1：传入 ReadableStream，即原始响应的 body。
      undefined, // 参数 2：DocumentHandler，此处不处理文档级事件。
      [[         // 参数 3：ElementHandler 数组，用于处理特定元素。
        '*',   // 使用 CSS 选择器 '*' 匹配所有元素。
        {
          // onText 处理器：当解析到文本节点时触发。
          onText(text) {
            // 将当前文本块存入 buffer。
            buffer.push(text.value);
            // lastInTextNode 为 true 表示这是当前文本节点的最后一个文本块。
            if (text.lastInTextNode) {
              // 拼接所有文本块，形成完整的文本。
              const data = buffer.join("");
              // 将文本转换为大写，并替换原始文本。
              text.replace(data.toUpperCase());
              // 重置 buffer，为处理下一个文本节点做准备。
              buffer = [];
            }
          }
        }
      ]]);

  // 返回修改后的 ReadableStream 对象作为对客户端的响应。
  return htmlStream;
}
```


<span id="htmlelement"></span>
## HtmlElement

表示 CSS 选择器选择的标签所对应的 HTML 元素。包含以下方法和属性：

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">假设当前的 HTML 元素是 div 节点，<code>after()</code>、<code>before()</code>、<code>append()</code>、<code>prepend()</code>、<code>setInnerContent()</code> 的内容插入位置如下图所示。</div>


<div data-tips="true" data-tips-type="tip"><img src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_86b8dec24c73c57a2a3731e077b30a1e.jpeg" width="500px" /></div>


<span id="setattribute-string-string"></span>
### setAttribute(String, String)

设置 HTML 元素的属性的值。

<span id="参数"></span>
#### 参数


* 第一个参数是属性名称。

* 第二个参数是属性的值。


<span id="after-string-contentoption"></span>
### after(String, ContentOption)

在该标签之后插入内容。

<span id="参数"></span>
#### 参数


* 第一个参数是一个 [String 对象](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)，表示要插入的内容。

* 第二个参数是一个 `ContentOption` 对象。该对象包含唯一属性 `isHtml`。该属性是一个 [Boolean 对象](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)，用于表示第一个参数的内容类型是否是 HTML：

   * true：表示第一个参数的内容是 HTML。第一个参数的内容不会被 HTML 转义。

   * false：表示第一个参数的内容不是 HTML。第一个参数的内容会在插入到 HTML 文档前被 HTML 转义。


<span id="append-string-contentoption"></span>
### append(String, ContentOption)

在该标签内的内容之后插入内容。

<span id="参数"></span>
#### 参数


* 第一个参数是一个 [String 对象](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)，表示要插入的内容。

* 第二个参数是一个 `ContentOption` 对象。该对象包含唯一属性 `isHtml`。该属性是一个 [Boolean 对象](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)，用于表示第一个参数的内容类型是否是 HTML：

   * true：表示第一个参数的内容是 HTML。第一个参数的内容不会被 HTML 转义。

   * false：表示第一个参数的内容不是 HTML。第一个参数的内容会在插入到 HTML 文档前被 HTML 转义。


<span id="prepend-string-contentoption"></span>
### prepend(String, ContentOption)

在该标签内的内容之前插入内容。

<span id="参数"></span>
#### 参数


* 第一个参数是一个 [String 对象](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)，表示要插入的内容。

* 第二个参数是一个 `ContentOption` 对象。该对象包含唯一属性 `isHtml`。该属性是一个 [Boolean 对象](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)，用于表示第一个参数的内容类型是否是 HTML：

   * true：表示第一个参数的内容是 HTML。第一个参数的内容不会被 HTML 转义。

   * false：表示第一个参数的内容不是 HTML。第一个参数的内容会在插入到 HTML 文档前被 HTML 转义。


<span id="setinnercontent-string-contentoption"></span>
### setInnerContent(String, ContentOption)

修改标签内的内容。

<span id="参数"></span>
#### 参数


* 第一个参数是一个 [String 对象](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)，表示要设置的内容。

* 第二个参数是一个 `ContentOption` 对象。该对象包含唯一属性 `isHtml`。该属性是一个 [Boolean 对象](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)，用于表示第一个参数的内容类型是否是 HTML：

   * true：表示第一个参数的内容是 HTML。第一个参数的内容不会被 HTML 转义。

   * false：表示第一个参数的内容不是 HTML。第一个参数的内容会在插入到 HTML 文档前被 HTML 转义。


<span id="removeandkeepcontent"></span>
### removeAndKeepContent()

删除标签，但是保留其子节点内容。

<span id="replace-string-contentoption"></span>
### replace(String, ContentOption)

替换标签。

<span id="参数"></span>
#### 参数


* 第一个参数是用于替换节点的 [String 对象](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)。该 String 会替换整个节点。

* 第二个参数是一个 `ContentOption` 对象。该对象包含唯一属性 `isHtml`。该属性是一个 [Boolean 对象](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)，用于表示第一个参数的内容类型是否是 HTML：

   * true：表示第一个参数的内容是 HTML。第一个参数的内容不会被 HTML 转义。

   * false：表示第一个参数的内容不是 HTML。第一个参数的内容会在插入到 HTML 文档前被 HTML 转义。


<span id="remove"></span>
### remove()

删除节点。

<span id="hasattribute-string"></span>
### hasAttribute(String)

检查属性是否存在，并返回一个 [Boolean 对象](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)。


* true：该属性存在。

* false：该属性不存在。


参数是一个 [String 对象](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)，表示属性的名称。

<span id="getattribute-string"></span>
### getAttribute(String)

返回一个 [String 对象](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)，表示属性的值，如果属性的值不存在则返回 null。

参数是一个 [String 对象](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)，表示属性的名称。

<span id="removeattribute-string"></span>
### removeAttribute(String)

删除属性。

参数是一个 [String 对象](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)，表示属性的名称。

<span id="iterator"></span>
### [@iterator]

用于遍历 [HtmlElement](https://docs.byteplus.com/en/docs/18/36057#htmlelement) 对象的属性。对于[HtmlElement](https://docs.byteplus.com/en/docs/18/36057#htmlelement) 对象的每个属性，该迭代器返回一个包含 2 个元素的 Array 对象，`[0]` 表示属性的名字，`[1]` 表示属性的值。

```JavaScript
for (const attribute of element) {
    console.log(attribute[0]);
    console.log(attribute[1]);
}

// 上述例子如果迭代 <a attr='1', attr2='2'>标签
// 会打印出
// attr
// 1
// attr2
// 2
```


<span id="tagname"></span>
### tagName

一个 [String 对象](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)。获取或设置当前的标签名。

<span id="namespaceuri"></span>
### namespaceUri

一个 [String 对象](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)。获取标签的 XML namespace。

<span id="removed"></span>
### removed

一个 [Boolean 对象](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)，表示标签是否被删除。


* true：该标签被删除。

* false：该标签未被删除。


<span id="如何使用-css-选择器"></span>
# 如何使用 CSS 选择器

&nbsp;

CSS 选择器用于匹配 HTML 元素。常见的使用方式如下：

<span id="选择指定类型的所有标签"></span>
### 选择指定类型的所有标签

`"a"` 表示选择所有的 a 标签。

<span id="选择特定标签下的子节点"></span>
### 选择特定标签下的子节点

`"a div"` 表示 a 标签下的 div 标签。

<span id="选择所有的标签"></span>
### 选择所有的标签

`"*"`

<span id="选择某个标签之下的孩子节点"></span>
### 选择某个标签之下的孩子节点

`"a > b"`：表示选择 b 标签。b 标签有一个父节点叫 a。

<span id="选择所有指定属性和类型的标签"></span>
### 选择所有指定属性和类型的标签

`"a[x]"`：表示选择所有带有属性 x，并且名为 a 的标签

<span id="选择所有指定-class-和类型的标签"></span>
### 选择所有指定 class 和类型的标签

`"a.u"`：表示选择所有 a 标签，且其 class 属性为 u。

<span id="选择所有指定-id-和类型的标签"></span>
### 选择所有指定 id 和类型的标签

`"a#u"`：表示选择所有 a 标签，且其 id 为 u。

<span id="选择所有指定属性名、属性值和类型的标签"></span>
### 选择所有指定属性名、属性值和类型的标签

`"a[y=\"z\"]"`：表示选择所有 a 标签，其属性名为 y 且属性值为 z。

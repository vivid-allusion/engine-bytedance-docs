---
title: "createHtmlStream()"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/function-createHtmlStream"
---

Parses and rewrites streamed HTML documents.

You can use this method to register callback functions for CSS selectors. After this method is called, the Edge Functions runtime will use the built\-in HTML parser to parse the HTML document. When the HTML parser parses an element that matches a CSS selector, the callback function for processing the HTML document or HTML element is called. These callback functions can be used to insert content before or after an element, change element attributes, or delete an element.

<span id="syntax"></span>
## Syntax

```JavaScript
createHtmlStream(ReadableStream, Object | null, Object | null)
```


<span id="parameters"></span>
## Parameters

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">You must provide the values in the exact order they are defined. You cannot skip the parameter in the middle.</div>



* The first parameter is a [ReadableStream](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Streams#readablestream) object, which represents the streamed HTML document to be rewritten. This `ReadableStream` object cannot have been read or canceled. This parameter is required.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><code>createHtmlStream()</code> does not allow you to pass in a <code>ReadableStream</code> object that has been read or canceled.   </div>
   

* The second parameter is a [DocumentHandler](https://docs.byteplus.com/en/docs/18/36364#documenthandler) object, which represents the HTML document\-level parsing event handler. If you do not need to listen for HTML document\-level parsing events, you can pass `undefined` or `null` to this parameter.

* The third parameter is an array, where each element is a sub\-array containing two elements. If you do not need to set a parsing event handler for any HTML element, you can pass `undefined` or `null` to this parameter. The two elements contained in this sub\-array represent:

   * A [tag selected by a CSS selector](https://docs.byteplus.com/en/docs/18/36364#css). The CSS selector is used to match HTML elements.

   * An [ElementHandler](https://docs.byteplus.com/en/docs/18/36364#elementhandler) object that matches the CSS selector. It represents the HTML element\-level parsing event handler, which is used to listen for and process the parsing events of DOM elements matched by the CSS selector.


<span id="return-value"></span>
## Return value

This method returns a [ReadableStream](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Streams#readablestream) object, which represents the processed streamed HTML document. You can return the `ReadableStream` object returned by this method as a response to the client.

<span id="error-handling"></span>
## Error handling

Exceptions thrown in the callback function will interrupt the entire stream. To avoid this, it is recommended that you use a try...catch statement inside the callback function to catch and handle exceptions.

<span id="sample-code"></span>
# Sample code

You can refer to the following sample code to understand how to use `createHtmlStream()` method to rewrite a streamed HTML page.

<span id="rewrite-external-links-in-an-html-page"></span>
### Rewrite external links in an HTML page

When a website is IPv6\-enabled, if third\-party resources referenced via external links in the page only support IPv4, users in a pure IPv6 network environment will fail to access these resources. This results in blank areas on the page where content cannot be loaded. To resolve this, an effective solution is to redirect these external links to an IP forwarding service that supports both IPv4/IPv6 dual\-stack. This service receives requests from IPv6 users, then accesses IPv4\-only resources on behalf of the users, and returns the results to the users.

The following example code demonstrates how to use the `createHtmlStream()` method to match and modify the `href` attribute of all `<a>` tags on a page, thereby redirecting the links to your specified IP forwarding service address. The `createHtmlStream()` method processes streaming HTML within the edge function runtime based on the zero\-copy principle and does not rely on JavaScript code loaded by the web page, so it does not affect the Time to First Byte (TTFB).

```javascript
addEventListener('fetch', (event) => {
  event.respondWith(handle(event));
});

async function handle(event) {
  // Fetch the original HTML page.
  const req = await fetch('https://origin.example.com');

  // Match elements to be rewritten through CSS selectors, and then rewrite the HTML page content.
  const htmlStream = createHtmlStream(
      req.body,  // Parameter 1: The ReadableStream object to be rewritten, i.e., the body of the origin response.
      undefined, // Parameter 2: Document-level handler, not used here.
      [['a',      // Parameter 3: An array containing CSS selectors and corresponding handlers.
        {
          // onElement handler: Triggered when an <a> tag is parsed.
          onElement(element) {
            console.assert(element.tagName == 'a');
            if (element.hasAttribute('href')) {
              const href = element.getAttribute('href');
              // Modify the href attribute value to the address of the IP forwarding service.
              element.setAttribute(
                  'href', `https://ipforwardservice.example.com?url=${href}` );
            }
          }
        }
      ]]);

  // Return the modified ReadableStream object as the response to the client.
  return htmlStream;
}
```


<span id="asynchronously-fetch-content-and-inject-the-fetched-content-into-the-html-page"></span>
### Asynchronously fetch content and inject the fetched content into the HTML page

The `createHtmlStream()` method enables you to dynamically modify the HTML response at the edge nodes. A common application is to define a placeholder tag in the HTML, asynchronously fetch data at the edge, and then inject the fetched data into the HTML to replace the placeholder. This method allows you to distribute dynamic content without modifying your application service logic.

For example, suppose your HTML page contains a custom `<fetch>` tag. You want to fetch the content pointed to by the `url` attribute of this tag at the edge node, and then replace the tag with the fetched content.

**Before processing**

```html
<html>
  <head></head>
  <body>
    <!-- The page contains a custom fetch tag -->
    <fetch url="https://api.example.com/data"></fetch>
  </body>
</html>
```


**After processing**

```html
<html>
  <head></head>
  <body>
  <!-- The fetch tag is replaced by the content pointed to by its url -->
    data
  </body>
</html>
```


The following example code demonstrates how to achieve the above effect.

```javascript
addEventListener('fetch', (event) => {
  event.respondWith(handle(event));
});

async function handle(event) {
  // Fetch the original HTML page.
  const req = await fetch(event.request);

  // Match elements to be rewritten through CSS selectors, and then rewrite the HTML page content.
  const htmlStream = createHtmlStream(
      req.body,  // Parameter 1: The ReadableStream object to be rewritten.
      undefined, // Parameter 2: Document-level handler, not used here.
      [[
        'fetch', // Parameter 3: CSS selector, matching all <fetch> tags here.
        {
          // onElement handler: Triggered when a <fetch> tag is parsed.
          async onElement(element) {
            console.assert(element.tagName == 'fetch');
            if (element.hasAttribute('url')) {
              const url = element.getAttribute('url');
              // Asynchronously fetch the content pointed to by the url.
              const content = await fetch(url);
              const text = await content.text();
              // Replace the <fetch> tag with the fetched content.
              element.replace(text, {isHtml: true});
            }
          }
        }
      ]]);

  // Return the modified ReadableStream object as the response to the client.
  return htmlStream;
}
```


<span id="parsing-event-handler"></span>
# Parsing event handler

<span id="documenthandler"></span>
## DocumentHandler

An HTML document\-level parsing event handler, used to handle all parsing events of an HTML document, including content outside the `<html>` tag.

You can use the following callback functions. Each callback function is optional, and each callback function can be an asynchronous function. The callback functions of the HTML document parsing event handler will not be triggered by CSS selectors.

<span id="ondoctype-doctype"></span>
### onDoctype(doctype)

Called when the DOCTYPE node of the HTML document is parsed.

<span id="parameters"></span>
#### Parameters

`doctype`: An [HtmlDoctype](https://docs.byteplus.com/en/docs/18/36364#htmldoctype) object.

<span id="ondocend-docend"></span>
### onDocend(docend)

Called when the entire HTML document has been parsed. The only function of this callback is to add a footer to the HTML document.

<span id="parameters"></span>
#### Parameters

`docend`: An [HtmlDocend](https://docs.byteplus.com/en/docs/18/36364#htmldocend) object.

<span id="oncomment-comment"></span>
### onComment(comment)

Called when a Comment node of the HTML document is parsed.

<span id="parameters"></span>
#### Parameters

`comment`: An [HtmlComment](https://docs.byteplus.com/en/docs/18/36364#htmlcomment) object.

<span id="ontext-text"></span>
### onText(text)

Called when a Text node of the HTML document is parsed.

The content of a Text node may be transmitted in multiple chunks during streaming parsing, so `onText()` may be called multiple times for the same Text node. For example, for a piece of HTML `<html>This is long text</html>`, if `This is long text` is returned in two parts, then although `This is long text` is a Text node, `onText()` will be called twice. You can use the [lastInTextNode](https://docs.byteplus.com/en/docs/18/36364#lastintextnode) attribute to determine if it is the last call.

<span id="parameters"></span>
#### Parameters

`text`: An [HtmlText](https://docs.byteplus.com/en/docs/18/36364#htmltext) object.

<span id="elementhandler"></span>
## ElementHandler

An HTML element\-level parsing event handler, used to listen for and process parsing events of DOM elements matched by a CSS selector.

You can use the following callback functions. Each callback function is optional, and each callback function can be an asynchronous function.

<span id="oncomment-comment"></span>
### onComment(comment)

This callback is called when a Comment node within an element matched by a CSS selector is parsed.

<span id="parameters"></span>
#### Parameters

`comment`: An [HtmlComment](https://docs.byteplus.com/en/docs/18/36364#htmlcomment) object.

<span id="ontext-text"></span>
### onText(text)

This callback is called when a Text node within an element matched by a CSS selector is parsed.

The content of a Text node may be transmitted in multiple chunks during streaming parsing, so `onText()` may be called multiple times for the same Text node. For example, for a piece of HTML `<div>This is long text</div>`, if `This is long text` is returned in two parts, then although `This is long text` is a Text node, `onText()` will be called twice. You can use the [lastInTextNode](https://docs.byteplus.com/en/docs/18/36364#lastintextnode) attribute to determine if it is the last call.

<span id="parameters"></span>
#### Parameters

`text`: An [HtmlText](https://docs.byteplus.com/en/docs/18/36364#htmltext) object.

<span id="onelement-element"></span>
### onElement(element)

This callback function is called when a tag selected by a CSS selector is parsed. If the CSS selector matches multiple tags, `onElement()` will be called multiple times.


* `element`: An [HtmlElement](https://docs.byteplus.com/en/docs/18/36364#htmlelement) object.


<span id="html-node-objects"></span>
# HTML node objects

<span id="htmldoctype"></span>
## HtmlDoctype

Represents a DOCTYPE node. Contains the `name`, `publicId`, and `systemId` attributes.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For example, in the following DOCTYPE node, <code>name</code> is <code>HTML</code>; <code>publicId</code> is <code>-//W3C//DTD HTML 4.01 Transitional//EN</code>; <code>systemId</code> is <code>https://www.w3.org/TR/html4/loose.dtd</code>.</div>


<div data-tips="true" data-tips-type="tip">```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "https://www.w3.org/TR/html4/loose.dtd">
```
</div>


<span id="name"></span>
### name

A [String object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) that represents the name of the DOCTYPE node.

<span id="publicid"></span>
### publicId

A [String object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) that represents the public id of the DOCTYPE node.

<span id="systemid"></span>
### systemId

A [String object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) that represents the system id of the DOCTYPE node.

<span id="htmldocend"></span>
## HtmlDocend

Represents the end of HTML document parsing. Contains the following method:

<span id="append-string-contentoption"></span>
### append(String, ContentOption)

Inserts a footer into the HTML document.


* The first parameter is a [String object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) that represents the content to be inserted.

* The second parameter is a `ContentOption` object. This object contains the unique attribute `isHtml`. This attribute is a [Boolean object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean) that indicates whether the content type of the first parameter is HTML:

   * true: Indicates that the content type of the first parameter is HTML. The content of the first parameter will not be HTML\-escaped.

   * false: Indicates that the content type of the first parameter is not HTML. The content of the first parameter will be HTML\-escaped before being inserted into the HTML document.


For example:

```JavaScript
append("not html", {isHtml: false});
```


<span id="htmlcomment"></span>
## HtmlComment

Represents the parsed Comment node. Contains the following methods and attributes:

<span id="set-string"></span>
### set(String)

Changes the content of the comment.

<span id="before-string-contentoption"></span>
### before(String, ContentOption)

Inserts content before the Comment node.

<span id="parameters"></span>
#### Parameters


* The first parameter is a [String object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) that represents the content to be inserted.

* The second parameter is a `ContentOption` object. This object contains the unique attribute `isHtml`. This attribute is a [Boolean object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean) that indicates whether the content type of the first parameter is HTML:

   * true: Indicates that the content type of the first parameter is HTML. The content of the first parameter will not be HTML\-escaped.

   * false: Indicates that the content type of the first parameter is not HTML. The content of the first parameter will be HTML\-escaped before being inserted into the HTML document.


<span id="after-string-contentoption"></span>
### after(String, ContentOption)

Inserts content after the Comment node.

<span id="parameters"></span>
#### Parameters


* The first parameter is a [String object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) that represents the content to be inserted.

* The second parameter is a `ContentOption` object. This object contains the unique attribute `isHtml`. This attribute is a [Boolean object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean) that indicates whether the content type of the first parameter is HTML:

   * true: Indicates that the content type of the first parameter is HTML. The content of the first parameter will not be HTML\-escaped.

   * false: Indicates that the content type of the first parameter is not HTML. The content of the first parameter will be HTML\-escaped before being inserted into the HTML document.


<span id="replace-string-contentoption"></span>
### replace(String, ContentOption)

Replaces the Comment node.

<span id="parameters"></span>
#### Parameters


* The first parameter is a [String object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) used to replace the node. This String will replace the entire node.

* The second parameter is a `ContentOption` object. This object contains the unique attribute `isHtml`. This attribute is a [Boolean object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean) that indicates whether the content type of the first parameter is HTML:

   * true: Indicates that the content of the first parameter is HTML. The content of the first parameter will not be HTML\-escaped.

   * false: Indicates that the content of the first parameter is not HTML. The content of the first parameter will be HTML\-escaped before being inserted into the HTML document.


<span id="remove"></span>
### remove()

Deletes the Comment node.

<span id="removed"></span>
### removed

A [Boolean object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean) that indicates whether the tag has been deleted.


* true: The tag is deleted.

* false: The tag is not deleted.


<span id="value"></span>
### value

A [String object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) that represents the content of the Comment node.

<span id="htmltext"></span>
## HtmlText

Represents a Text node. Contains the following methods and attributes:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In streaming parsing, the content of the same Text node may be divided into multiple chunks. You need to use the <a href="https://docs.byteplus.com/en/docs/18/36364#lastInTextNode">lastInTextNode</a> attribute to determine whether the content of the entire Text node has been completely parsed.</div>


<span id="before-string-contentoption"></span>
### before(String, ContentOption)

Inserts content before the Text node.

<span id="parameters"></span>
#### Parameters


* The first parameter is a [String object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) that represents the content to be inserted.

* The second parameter is a `ContentOption` object. This object contains the unique attribute `isHtml`. This attribute is a [Boolean object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean) that indicates whether the content type of the first parameter is HTML:

   * true: Indicates that the content type of the first parameter is HTML. The content of the first parameter will not be HTML\-escaped.

   * false: Indicates that the content type of the first parameter is not HTML. The content of the first parameter will be HTML\-escaped before being inserted into the HTML document.


<span id="after-string-contentoption"></span>
### after(String, ContentOption)

Inserts content after the Text node.

<span id="parameters"></span>
#### Parameters


* The first parameter is a [String object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) that represents the content to be inserted.

* The second parameter is a `ContentOption` object. This object contains the unique attribute `isHtml`. This attribute is a [Boolean object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean) that indicates whether the content type of the first parameter is HTML:

   * true: Indicates that the content type of the first parameter is HTML. The content of the first parameter will not be HTML\-escaped.

   * false: Indicates that the content type of the first parameter is not HTML. The content of the first parameter will be HTML\-escaped before being inserted into the HTML document.


<span id="replace-string-contentoption"></span>
### replace(String, ContentOption)

Replaces the Text node.

<span id="parameters"></span>
#### Parameters


* The first parameter is a [String object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) used to replace the node. This String object will replace the entire node.

* The second parameter is a `ContentOption` object. This object contains the unique attribute `isHtml`. This attribute is a [Boolean object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean) that indicates whether the content type of the first parameter is HTML:

   * true: Indicates that the content of the first parameter is HTML. The content of the first parameter will not be HTML\-escaped.

   * false: Indicates that the content of the first parameter is not HTML. The content of the first parameter will be HTML\-escaped before being inserted into the HTML document.


<span id="remove"></span>
### remove()

Deletes the Text node.

<span id="value"></span>
### value

A [String object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) that represents the content of the Text node. If the chunk contained in the current `HtmlText` object is the last chunk of the Text node, this attribute returns an empty string.

<span id="removed"></span>
### removed

A [Boolean object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean) that indicates whether the Text node has been deleted.


* true: The Text node is deleted.

* false: The Text node is not deleted.


<span id="lastintextnode"></span>
### lastInTextNode

A [Boolean object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean) that indicates whether the chunk contained in the current `HtmlText` object is the last chunk of the Text node.


* true: The chunk contained in the current `HtmlText` object is the last chunk of the Text node.

* false: The chunk contained in the current `HtmlText` object is not the last chunk of the Text node.


The `onText()` callback may be triggered multiple times for the same Text node. If you need to get the content of the entire Text node, you can buffer the content until the `lastInTextNode` attribute of the Text node is true.

<span id="example"></span>
### Example

The following example demonstrates how to use the `onText` callback to capture and transform text content within an HTML document. In this example, the content of all text nodes is converted to uppercase.

```javascript
addEventListener('fetch', (event) => {
  event.respondWith(handle(event));
});

async function handle(event) {
  // Fetch the original HTML page.
  const req = await fetch(event.request);

  // Create a buffer to concatenate text chunks in the onText event.
  // onText may be triggered multiple times on a single text node, so concatenation is necessary.
  let buffer = [];
  const htmlStream = createHtmlStream(
      req.body,  // Parameter 1: Pass in the ReadableStream, i.e., the body of the original response.
      undefined, // Parameter 2: DocumentHandler, document-level events are not processed here.
      [[         // Parameter 3: An array of ElementHandlers to process specific elements.
        '*',   // Use the CSS selector '*' to match all elements.
        {
          // onText handler: Triggered when a text node is parsed.
          onText(text) {
            // Store the current text chunk in the buffer.
            buffer.push(text.value);
            // lastInTextNode being true indicates this is the last text chunk for the current text node.
            if (text.lastInTextNode) {
              // Concatenate all text chunks to form the complete text.
              const data = buffer.join("");
              // Convert the text to uppercase and replace the original text.
              text.replace(data.toUpperCase());
              // Reset the buffer to prepare for processing the next text node.
              buffer = [];
            }
          }
        }
      ]]);

  // Return the modified ReadableStream object as the response to the client.
  return htmlStream;
}
```


<span id="htmlelement"></span>
## HtmlElement

Represents the HTML element corresponding to the tag selected by the CSS selector. Contains the following methods and attributes:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Assuming the current HTML element is a div node, the content insertion positions of <code>after()</code>, <code>before()</code>, <code>append()</code>, <code>prepend()</code>, and <code>setInnerContent()</code> are as shown in the figure below.</div>


<div data-tips="true" data-tips-type="tip"><img src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_86b8dec24c73c57a2a3731e077b30a1e.jpeg" width="500px" /></div>


<span id="setattribute-string-string"></span>
### setAttribute(String, String)

Sets the value of an attribute of an HTML element.

<span id="parameters"></span>
#### Parameters


* The first parameter is the attribute name.

* The second parameter is the attribute value.


<span id="after-string-contentoption"></span>
### after(String, ContentOption)

Inserts content after this tag.

<span id="parameters"></span>
#### Parameters


* The first parameter is a [String object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) that represents the content to be inserted.

* The second parameter is a `ContentOption` object. This object contains the unique attribute `isHtml`. This attribute is a [Boolean object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean) that indicates whether the content type of the first parameter is HTML:

   * true: Indicates that the content type of the first parameter is HTML. The content of the first parameter will not be HTML\-escaped.

   * false: Indicates that the content type of the first parameter is not HTML. The content of the first parameter will be HTML\-escaped before being inserted into the HTML document.


<span id="append-string-contentoption"></span>
### append(String, ContentOption)

Inserts content after the content within this tag.

<span id="parameters"></span>
#### Parameters


* The first parameter is a [String object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) that represents the content to be inserted.

* The second parameter is a `ContentOption` object. This object contains the unique attribute `isHtml`. This attribute is a [Boolean object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean) that indicates whether the content type of the first parameter is HTML:

   * true: Indicates that the content type of the first parameter is HTML. The content of the first parameter will not be HTML\-escaped.

   * false: Indicates that the content type of the first parameter is not HTML. The content of the first parameter will be HTML\-escaped before being inserted into the HTML document.


<span id="prepend-string-contentoption"></span>
### prepend(String, ContentOption)

Inserts content before the content within this tag.

<span id="parameters"></span>
#### Parameters


* The first parameter is a [String object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) that represents the content to be inserted.

* The second parameter is a `ContentOption` object. This object contains the unique attribute `isHtml`. This attribute is a [Boolean object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean) that indicates whether the content type of the first parameter is HTML:

   * true: Indicates that the content type of the first parameter is HTML. The content of the first parameter will not be HTML\-escaped.

   * false: Indicates that the content type of the first parameter is not HTML. The content of the first parameter will be HTML\-escaped before being inserted into the HTML document.


<span id="setinnercontent-string-contentoption"></span>
### setInnerContent(String, ContentOption)

Modifies the content within the tag.

<span id="parameters"></span>
#### Parameters


* The first parameter is a [String object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) that represents the content to be set.

* The second parameter is a `ContentOption` object. This object contains the unique attribute `isHtml`. This attribute is a [Boolean object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean) that indicates whether the content type of the first parameter is HTML:

   * true: Indicates that the content type of the first parameter is HTML. The content of the first parameter will not be HTML\-escaped.

   * false: Indicates that the content type of the first parameter is not HTML. The content of the first parameter will be HTML\-escaped before being inserted into the HTML document.


<span id="removeandkeepcontent"></span>
### removeAndKeepContent()

Deletes the tag but keeps its child node content.

<span id="replace-string-contentoption"></span>
### replace(String, ContentOption)

Replaces the tag.

<span id="parameters"></span>
#### Parameters


* The first parameter is a [String object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) used to replace the node. This String will replace the entire node.

* The second parameter is a `ContentOption` object. This object contains the unique attribute `isHtml`. This attribute is a [Boolean object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean) that indicates whether the content type of the first parameter is HTML:

   * true: Indicates that the content of the first parameter is HTML. The content of the first parameter will not be HTML\-escaped.

   * false: Indicates that the content of the first parameter is not HTML. The content of the first parameter will be HTML\-escaped before being inserted into the HTML document.


<span id="remove"></span>
### remove()

Deletes the node.

<span id="hasattribute-string"></span>
### hasAttribute(String)

Checks if an attribute exists and returns a [Boolean object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean).


* true: The attribute exists.

* false: The attribute does not exist.


The parameter is a [String object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) that represents the name of the attribute.

<span id="getattribute-string"></span>
### getAttribute(String)

Returns a [String object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) that represents the value of the attribute, or null if the attribute does not exist.

The parameter is a [String object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) that represents the name of the attribute.

<span id="removeattribute-string"></span>
### removeAttribute(String)

Deletes an attribute.

The parameter is a [String object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) that represents the name of the attribute.

<span id="iterator"></span>
### [@iterator]

Used to iterate over the properties of an [HtmlElement](https://docs.byteplus.com/en/docs/18/36364#htmlelement) object. For each property of the [HtmlElement](https://docs.byteplus.com/en/docs/18/36364#htmlelement) object, the iterator returns an Array object containing 2 elements, where `[0]` represents the property name and `[1]` represents the property value.

```JavaScript
for (const attribute of element) {
    console.log(attribute[0]);
    console.log(attribute[1]);
}

// If the above example iterates over the <a attr='1', attr2='2'> tag
// It will print
// attr
// 1
// attr2
// 2
```


<span id="tagname"></span>
### tagName

A [String object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String). Gets or sets the current tag name.

<span id="namespaceuri"></span>
### namespaceUri

A [String object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String). Gets the XML namespace of the tag.

<span id="removed"></span>
### removed

A [Boolean object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean) that indicates whether the tag has been deleted.


* true: The tag is deleted.

* false: The tag is not deleted.


<span id="how-to-use-css-selectors"></span>
# How to use CSS selectors

&nbsp;

CSS selectors are used to match HTML elements. Common usage is as follows:

<span id="select-all-tags-of-a-specified-type"></span>
### Select all tags of a specified type

`"a"` selects all a tags.

<span id="select-child-nodes-under-a-specific-tag"></span>
### Select child nodes under a specific tag

`"a div"` selects div tags under a tags.

<span id="select-all-tags"></span>
### Select all tags

`"*"`

<span id="select-child-nodes-under-a-certain-tag"></span>
### Select child nodes under a certain tag

`"a > b"`: Selects the b tag. The b tag has a parent node named a.

<span id="select-all-tags-with-the-specified-attribute-and-type"></span>
### Select all tags with the specified attribute and type

`"a[x]"`: Selects all a tags with the attribute x.

<span id="select-all-tags-with-the-specified-class-and-type"></span>
### Select all tags with the specified class and type

`"a.u"`: Selects all a tags with the class attribute u.

<span id="select-all-tags-with-the-specified-id-and-type"></span>
### Select all tags with the specified id and type

`"a#u"`: Selects all a tags with the id u.

<span id="select-all-tags-with-the-specified-attribute-name-attribute-value-and-type"></span>
### Select all tags with the specified attribute name, attribute value, and type

`"a[y=\"z\"]"`: Selects all a tags where the attribute name is y and the attribute value is z.

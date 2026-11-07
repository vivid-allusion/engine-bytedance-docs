---
title: "Configure custom block response policies"
product: "LLM Application Firewall"
product_code: "LLM-Application-Firewall"
source: "https://docs.byteplus.com/en/docs/LLM-Application-Firewall/Configure_custom_block_response_policies"
---

A custom block response replaces the default error page or response body returned when the LLM Application Firewall blocks a request. You can use custom responses to explain why a request was blocked, provide further instructions, or return data in a format that your application can process.

You can configure separate responses for non\-streaming and streaming scenarios.

<span id="6e4349e7"></span>
## Response modes

You can configure response information separately based on the response mode (non\-streaming response and streaming response). The following describes the differences between the two:


|Aspect |Non\-streaming block response |Streaming block response |
|---|---|---|
|Applies to |User prompts and non\-streaming model responses for which the triggered protection rule uses the `Block` action. |Streaming model responses for which the triggered protection rule uses the `Block` action. |
|Response behavior |Returns the complete custom response in a single response. |Returns the configured replacement text as part of the response stream. |
|Configuration |Response status code, page template, page type, page content, or redirect path.<br><br>Supported page types are `text/html`, `text/xml`, `application/json`, and `text/event-stream`. |Replacement text returned when content in the response stream triggers a protection rule. |
|Result |Returns a complete HTML page, XML document, JSON object, SSE event stream, or redirect response. |Forwards compliant chunks normally. If a chunk triggers a protection rule, the system replaces the detected content with the configured text and returns it as the final content in the stream. |


<span id="24201d40"></span>
## Prerequisites

Configure and enable at least one protection rule that uses the **Block** action. Supported rules include:


* Access control rules

* Prompt injection protection rules

* Model abuse prevention rules

* Sensitive data leakage prevention rules


For an overview of the available protection capabilities, see [Introduction to protection policies](https://docs.byteplus.com/docs/LLM-Application-Firewall/introduction_to_protection_policy).

<span id="fd59f69c"></span>
## Configure a response rule


1. Log in to the [LLM Application Firewall console](https://console.byteplus.com/omni-shield/llm-shield).

2. Select the region where the instance resides in the top navigation bar.

3. In the left navigation pane, select **Protection \> Custom Block Response**.

4. Click **Add Rule** to configure custom block response parameters.

   
   |Parameter |Description |
   |---|---|
   |**Rule Name** |Enter a name that identifies the rule.<br><br>The name must begin with a letter or digit. It can contain letters, digits, periods (`.`), underscores (`_`), and hyphens (`-`). The length must be between 1 and 128 characters. |
   |**Asset** |Select the asset or request path to which the rule applies. To apply the rule to every configured path under a domain, select the domain itself.<br><br>Path\-based matching is not currently supported for assets integrated through the SDK. |
   |**Response Code** |Enter the HTTP status code returned when a request is blocked. For example, use `403` to indicate that access is forbidden. |
   |**Page Template** |Select **System Default**, **Custom**, or **Redirect**. For a system or custom template, select a page type and configure the response content. |
   |**Streaming Response** |Enable this option to return replacement text when content in a streaming model response is blocked. |
   |**Text Content** |Enter the replacement text returned in the response stream. The text can contain up to 500 characters. |
   |**Rule Toggle** |Enable or disable the rule. |
   

5. Click **OK**.


<span id="caa3340e"></span>
## Page template options

<span id="8bb3df88"></span>
### System default

Use a system\-provided response template. The following page types are supported:


|Page type |Description |
|---|---|
|`text/html` |Returns an HTML page that a browser can render. |
|`text/xml` |Returns structured XML data. |
|`application/json` |Returns a JSON object for processing by an application or Web API. |
|`text/event-stream` |Returns the response as a Server\-Sent Events stream. Use this type when the client expects an SSE response. |


Examples of the corresponding response formats are shown below.


<Tabs>
<Tab zoneid="tMeycKNhqe" title="HTML">
<TabTitle>HTML</TabTitle>

```HTML
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>Access denied</title>
</head>
<body>
  <p>Access denied by the system.</p>
</body>
</html>
```



</Tab>
<Tab zoneid="v3nAyrl2cE" title="XML">
<TabTitle>XML</TabTitle>

```XML
<?xml version="1.0" encoding="UTF-8"?>
<body>
  <message>Access denied by the system.</message>
</body>
```



</Tab>
<Tab zoneid="H9wtItnb2r" title="JSON">
<TabTitle>JSON</TabTitle>

```JSON
{
  "Content": "Access denied by the system."
}
```



</Tab>
<Tab zoneid="WTSuYBFEWA" title="Server-Sent Events">
<TabTitle>Server-Sent Events</TabTitle>

Content returned as `text/event-stream` must follow the SSE format. Each event must begin with an SSE field such as `data:`, and consecutive events must be separated by a blank line. Ensure that the response structure matches the format expected by your client.

```Plain Text
data: {"id":"1","object":"chat.completion.chunk","choices":[{"index":0,"delta":{"role":"assistant","content":"Sorry, I cannot answer this question."},"finish_reason":null}]}

data: {"id":"2","object":"chat.completion.chunk","choices":[{"index":0,"delta":{},"finish_reason":"stop"}]}

data: [DONE]
```



</Tab>
</Tabs>


<span id="9b35bb9b"></span>
### Custom

Select **Custom** to provide your own response body. Custom templates support the following page types:


* `text/html`

* `text/xml`

* `application/json`

* `text/event-stream`


The response body must be valid for the selected page type. For `text/event-stream`, include the required SSE fields, such as `data:`, and separate events with blank lines.

For example, you can configure the following HTML response:

```HTML
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>Access denied</title>
</head>
<body>
  <p>
    You do not have permission to access this page.
    Obtain the required authorization and try again.
  </p>
</body>
</html>
```


<span id="e39a4432"></span>
### Redirect

Select **Redirect** to redirect the client to another path under the protected domain when a request is blocked.

Enter a relative path, such as:

```Plain Text
/common/info/redirect
```


The redirect path must belong to the protected domain associated with the rule.

<span id="614dd7c1"></span>
## Response behavior

The response returned by the LLM Application Firewall depends on whether a custom rule exists and whether streaming response replacement is enabled.


|Configuration |Non\-streaming request or response blocked |Streaming response blocked |
|---|---|---|
|No rule exists, or the rule is disabled |Returns the default block response. |Returns the default block response. |
|A rule exists, but **Streaming Response** is disabled |Returns the configured page or data response, or redirects the client to the configured path. |Returns the configured page or data response, or redirects the client to the configured path. |
|A rule exists and **Streaming Response** is enabled |Returns the configured page or data response, or redirects the client to the configured path. |Returns the configured replacement text in the response stream. |

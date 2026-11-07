---
title: "Optimize content crawling for AI agents with HTML to Markdown"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/html-md-best-practice_en-us"
---

HTML to Markdown converts HTML web pages into Markdown. Compared with raw HTML, Markdown uses a simpler, text\-oriented structure while preserving headings, paragraphs, lists, links, and other key information. This makes web content easier for AI agents, AI search crawlers, and LLM\-powered Q&A systems to read and process.

After you enable HTML to Markdown in CDN, the conversion is completed at edge nodes. AI clients can receive Markdown by sending the `Accept: text/markdown` request header, while regular browsers still receive the original HTML. This gives AI clients a lighter\-weight way to consume content without requiring you to develop and maintain a separate conversion service at the origin.

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260708060237-886905902319.png) </span>

<span id="1c89793d"></span>
# Use cases

If your site has a large number of public content pages, and the page content is already present in the HTML returned by the origin, we recommend starting with HTML to Markdown. This feature is especially suitable for websites that want AI agents, AI search crawlers, and LLM\-powered Q&A systems to read their content more easily.


* Your site already has many public content pages, such as help center articles, documentation pages, news articles, blog posts, knowledge base articles, and product detail pages.

* You want regular browsers to keep receiving the original HTML while AI clients can receive a lighter\-weight Markdown version of the same content.

* You do not want to develop and maintain an HTML\-to\-Markdown conversion service at the origin.


<span id="7d9595c9"></span>
# Benefits

For websites with a large number of public content pages, the main value of HTML to Markdown is that AI agents can read the same content more easily while regular browsers continue to receive the original HTML. Actual benefits depend on the structure of each page. Before enabling the feature on more pages, test a few representative pages and compare the Markdown output with the original HTML.


|Benefit |Description |
|---|---|
|Reduce non\-content noise |Markdown is more compact than raw HTML and can reduce interference from elements unrelated to the main page content. |
|Reduce response size |After HTML is converted to Markdown, the response usually contains less page structure, style, and script information, which can reduce the amount of data transferred. For example, a 5 MB HTML page that contains a large amount of navigation, styles, scripts, and other non\-content information may be converted into about 3 MB of Markdown, reducing the size by more than 40%. The more non\-content information a page contains, the more noticeable the size reduction usually is. |
|Improve content readability |Markdown preserves structures such as headings, paragraphs, lists, and links, making it easier for AI agents, search crawlers, and LLM\-powered Q&A systems to read. |
|Reduce origin\-side development work |The conversion is completed at CDN edge nodes, so the origin does not need to build a separate HTML\-to\-Markdown service. |
|Continue returning HTML to browsers |When a browser request does not include the Markdown request header, CDN still returns the original HTML page. |


<span id="250cf4d6"></span>
# Recommended usage

We recommend first enabling and verifying the feature on 3 to 5 typical content pages, such as help center articles, documentation pages, news articles, or product detail pages. Access the same URL twice: once in a browser without the Markdown request header, and once with the `Accept: text/markdown` request header. Compare whether the browser request still returns the original HTML, whether the Markdown output includes the expected headings and page text, and whether lists and links are preserved.

After the results meet expectations, gradually expand the feature to similar pages. Before expanding usage, evaluate the conversion result for pages that load content dynamically in the browser, have complex content structures, or depend heavily on user interaction.

<span id="1a474c4d"></span>
# How the feature works

HTML to Markdown is a configuration option in CDN domain settings. After it is enabled, CDN identifies the request type based on the request header: AI clients that request Markdown receive Markdown, while regular browsers still receive the original HTML.

<span id="8ed52ccc"></span>
## Processing flow


1. Clients such as AI agents and AI search crawlers request a page and include `Accept: text/markdown` in the request header.

2. The CDN edge node receives the request, confirms that HTML to Markdown is enabled for the target domain, and checks whether the request includes `Accept: text/markdown`.

3. If the condition is met, CDN fetches the original HTML page from the origin and converts the HTML to Markdown at the edge node.

4. CDN returns the Markdown response to the client. If a browser request does not include this request header, CDN still returns the original HTML.



|Item |Description |
|---|---|
|Trigger |Conversion is triggered only when the request header includes `Accept: text/markdown`. |
|Origin response content type |The origin response `Content-Type` must be `text/html`. |
|Conversion result |Markdown content is returned. |
|Response header |After successful conversion, the response includes the header `content-type: text/markdown; charset=utf-8`. |
|Cache policy |CDN does not cache converted Markdown responses. Each request is converted in real time. |


<span id="f3b7516c"></span>
# Limitations

Before using this feature, review the following limits. HTML to Markdown helps AI clients read existing HTML content more easily, but it does not change the original web page content.


* **Trigger condition:**  Conversion is triggered only when the request header includes `Accept: text/markdown`. If a browser request does not include this request header, CDN still returns the original HTML.

* **Origin response content type:**  The origin response `Content-Type` must be `text/html`.

* **File extension:**  The requested file must use the `.html` or `.htm` extension. Files with other extensions do not trigger HTML to Markdown.

* **Applicable pages:**  This feature applies to pages where the page content is already present in the HTML returned by the origin, such as help center articles, documentation pages, news articles, blog posts, knowledge base articles, and product detail pages.

* **Pages not recommended:**  If the HTML returned by the origin contains only the page shell and does not include the page content, we do not recommend enabling this feature. Client\-side rendered (CSR/SPA) pages usually fall into this category. These pages typically display their content only after JavaScript runs in the browser. For requests that include `Accept: text/markdown`, the converted Markdown may be almost empty. If a browser or debugging tool sends `Accept: text/markdown`, the returned response is displayed as Markdown instead of being rendered as the original HTML page.

* **Content processing:**  This feature does not extract main content, generate summaries, or remove noise. CDN converts the full HTML returned by the origin without extracting the main content or removing non\-content elements.

* **Caching:**  CDN does not cache converted Markdown responses. Each request that matches the conversion condition is converted in real time.

* **Content quality:**  This feature does not replace content quality optimization. Heading hierarchy, page structure, link text, and unrelated content should still be managed at the origin.


<span id="0b5b2b2d"></span>
# View configuration steps

For instructions on where to find this setting in the console and how to configure it, see [HTML to Markdown configuration documentation](https://docs.byteplus.com/en/docs/byteplus-cdn/html-to-md_zh-cn).

In the CDN console, go to the configuration page for the target domain, locate HTML to Markdown, enable the feature, and submit the configuration. After the configuration takes effect, only requests that include the `Accept: text/markdown` request header trigger conversion. Requests without this header still receive the original HTML.

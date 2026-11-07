---
title: "URL Blocking and Unblocking"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/url-block_en-us"
---

BytePlus Content Delivery Network (CDN) provides a URL blocking and unblocking feature that allows you to specify and block external access to certain URLs under your accelerated domains, or restore access to previously blocked URLs. This feature helps you quickly respond to security incidents or flexibly manage content access based on your business needs.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Behavior when accessing a blocked URL</div>


<div data-tips="true" data-tips-type="tip">If a user attempts to access a blocked URL, the CDN will respond with a <code>403</code> status code, and the response header will contain <code>Byte-Error-Code: 007</code>.</div>


<span id="overview"></span>
## Overview

On the **URL Blocking and Unblocking** page of the BytePlus CDN Console, you can perform the following operations:


* **URL Blocking**: Proactively block external access to specific URLs.

* **URL Unblocking**: Restore normal access to blocked URLs.

* **Operation Records**: Query the historical status and execution results of your block and unblock operations.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Wildcard Domain Restrictions</div>


<div data-tips="true" data-tips-type="tip">You cannot directly block or unblock files and directories under a wildcard domain. To perform these operations, see <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/purge-prefetch-faq_en-us?lang=en#purging-prefetching-blocking-and-unblocking-under-a-wildcard-domain">How to perform operations on wildcard domains</a>.</div>


<span id="block-urls"></span>
## Block URLs

If you want to prevent users from accessing specific files on your domain, you can specify the URLs to be blocked on this page. When a user requests a matched blocked URL, the CDN will reject the request.


* **Quota**: Your primary account can block up to 3,000 URLs per day.

* **Requirements**:

   * Must start with `http://` or `https://`.

   * A single task can contain up to 100 URLs.

* **Methods**:

   1. **Enter URLs**: Directly enter the URLs you want to block in the text box (one URL per line).

   2. **Upload File**: Upload a `.txt` file containing the URLs you want to block (one URL per line).


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260330140708-739097416649.png) </span>

<span id="unblock-urls"></span>
## Unblock URLs

Use this feature to unblock previously intercepted URLs and restore normal access for users.


* **Quota**: Your primary account can unblock up to 3,000 URLs per day.

* **Requirements**: Same as the block requirements, must include the `http/https` prefix, and a single task can contain up to 100 URLs.

* **Methods**: Supports **Enter URLs** and **Upload File**.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">You cannot unblock URLs penalized by the platform</div>


<div data-tips="true" data-tips-type="warning">For businesses involving the Chinese mainland, BytePlus CDN will inspect whether the content you distribute complies with relevant laws and regulations of the Chinese mainland (such as the Cybersecurity Law, Administrative Measures on Internet Information Services, etc.). For URLs proactively blocked by BytePlus due to content violations, you cannot perform a self\-service unblock on this page; such tasks will indicate <strong>unblock failed</strong>. To unblock them, please <a href="https://console.byteplus.com/ticket/createTicketV2/">submit a ticket</a> to apply.</div>


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260330140727-718643813512.png) </span>

<span id="view-operation-records"></span>
## View Operation Records

On the **Operation Records** tab of the "URL Blocking and Unblocking" page, you can track the execution results of each URL block and unblock task.

The system allows you to query records from the past **92 days**. You can precisely filter using the following conditions:


* **Operation Time**: Customize a time period within the past 92 days (default is "Today").

* **Task Type**: URL Blocking / URL Unblocking.

* **Task Status**: Completed / In Progress / Failed (default includes all statuses).

* **Reason**: The reason why the URL was blocked.

* **URL**: Precisely query the execution status of a specific URL.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The system only retains queryable records for 92 days. For URLs blocked more than 92 days ago, you can only determine their status by checking for a <code>403</code> HTTP status code and the <code>Byte-Error-Code: 007</code> response header.</div>


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260330140744-1258955821078.png) </span>

---
title: "Origin Retry"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/origin_retry-en"
---

This document describes the **Origin Retry** feature in BytePlus.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To use this feature, <a href="https://console.byteplus.com/workorder/create">submit a ticket</a>.</div>


<span id="overview"></span>
## Overview

By default, when CDN fetches content from an origin and the origin returns a 5xx status code, CDN retries the origin request. The **Origin Retry** feature allows you to specify the origin response status codes that trigger an origin retry.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">CDN retries an eligible origin request only when the client request uses the <code>POST</code>, <code>HEAD</code>, or <code>GET</code> method and meets the <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/origin-retry-logic_en-us?#origin-request-failure-criteria">origin request failure criteria</a>.</div>


The status codes configured for this feature replace the default 5xx status codes that trigger origin retries. For example, if you configure `404;408`, a 504 response does not trigger an origin retry.

<span id="procedure"></span>
## Procedure


1. Open the **Origin Retry** configuration page. For instructions, see [Domain configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

2. Set **Status** to **On**.

3. In **Status Code**, enter one or more status codes from 400 through 599. Separate multiple status codes with semicolons (`;`). You can enter `4xx` or `5xx` to represent all 4xx or 5xx status codes, respectively. For example: `404;408;5xx`.

4. Click **Save**.


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260818033332-171471810199.png) </span>

---
title: "WebSocket"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/websocket_en"
---

This topic describes how to enable WebSocket and configure WebSocket Timeout in BytePlus CDN.

<span id="overview"></span>
## Overview

WebSocket is a full\-duplex communication protocol that uses a single TCP connection. It is suitable for scenarios that require bidirectional communication, such as real\-time chat, online games, and real\-time data updates.

WebSocket is disabled by default in CDN. After you enable it, CDN establishes a WebSocket connection with the origin server when a client initiates a WebSocket request. CDN then forwards WebSocket messages among the client, CDN point of presence (POP), and origin server.

<span id="websocket-timeout"></span>
## WebSocket Timeout

WebSocket Timeout controls how long a WebSocket connection between a CDN POP and an origin server can remain idle. The default value is 60 seconds. CDN closes the connection if no data is sent or received during the configured period.

Configure WebSocket Timeout based on the interval at which your application sends messages. The unit is seconds, the valid range is 1–900, and the default value is 60.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Set <strong>WebSocket Timeout</strong> to a value greater than or equal to <strong>HTTP Read Timeout</strong> under <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/docs-request-time-out">Origin Fetch Timeout</a>. Otherwise, WebSocket messages sent by the origin server may not be delivered correctly.</div>


<span id="steps"></span>
## Steps


1. Open the **WebSocket** configuration page. For instructions, see [Domain configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

2. Set **Status** to **Enabled**.

3. Configure **WebSocket Timeout**.

4. Click **Save**.


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260806105230-1190898735942.png) </span>

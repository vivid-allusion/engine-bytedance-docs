---
title: "Media transmission keepalive mechanism"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-rtm-keepalive-mechanism"
---

WebRTC's default Ping\-Pong mechanism is used to maintain the connection status once the [ICE](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-rtm-terminology#ice) connection is successfully established. The following points should be noted:


* Sessions must be kept alive for each ICE channel.

* Use the STUN binding request or STUN binding indication message types.

* If no response is received, it will be retransmitted up to the maximum number of retransmissions.

* When no data is sent, the Keep\-Alive packet transmission interval should not exceed 5 seconds.

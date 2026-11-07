---
title: "Ending the media transmission"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-rtm-ending-transmission"
---

RTM supports the following two options to end the transmission.


* Recommended option: End RTM media by sending a notification message to the server via [RTCP](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-rtm-terminology#rtcp);

* Custom extension: End RTM media by sending a proprietary custom notification message to the media server via a separate signaling channel; the server then interrupts the media transmission after receiving the command.


<span id="755e328e"></span>
## RTCP/BYE

A sample Goodbye RTCP packet is shown below.

```Plain
0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|V=2|P|    SC   |  PT=BYE=203  |             length             |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                           SSRC/CSRC                           |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
:                              ...                              :
+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+
|     length    |          reason for leaving           ... (opt)
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```



* There is an EOS/EOF mark in the media stream once the RTM push\-stream ends, and the server sends an RTCP/BYE package.

* The client sends an RTCP/BYE packet to the server once the RTM pull\-stream ends, and the server stops forwarding the stream (5 seconds) and ends charging.

* Goodbye RTCP packets are a special form of low\-latency RTCP control commands. Please see [RTCP](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-rtm-terminology#rtcp) for details.

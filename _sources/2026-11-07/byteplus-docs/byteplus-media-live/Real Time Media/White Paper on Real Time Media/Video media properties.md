---
title: "Video media properties"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-rtm-video-media-properties"
---

RTM coding technology supports a variety of codec technologies, including VP8, VP9, H.264, and H.265. B\-frame compression is supported for video sequences encoded in H.264 and H.265. B\-frame offers better compression efficiency than P\-frame.

Therefore, this white paper recommends that the specification be described using H.264 and H.265 [RTP](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-rtm-terminology#rtp) encoded video (MPEG\-4 Visual RTP encoding).

<span id="1edef838"></span>
## Payload type encoding

MPEG\-4 visual RTP payload format encoding is shown below.

```Plain
0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|V=2|P|X|  CC   |M|     PT      |       sequence number         | RTP
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                           timestamp                           | Header
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|           synchronization source (SSRC) identifier            |
+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+
|            contributing source (CSRC) identifiers             |
|                             ....                              |
+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+
|                                                               | RTP
|              MPEG-4 Visual stream (byte aligned)              | Pay-
|                                                               | load
|                               +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                               :...OPTIONAL RTP padding        |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```


The RTP data header contains the payload type (PT). The [RFC 3551](https://www.rfc-editor.org/rfc/rfc3551.html#page-6) standard specifies and recommends PTs for audio & video encodings in the section Registering Additional Encodings. Some values are reserved in RFC 3551, while other PT recommendations used for unlisted encodings are determined via negotiation within the range of 96 to 127, for example, via SDP protocol negotiations:


* Use PT=96 to represent H.264;

* Use PT=98 to represent H.265.


<span id="9836558d"></span>
## H.264 codec support

RFC specification reference: [RTP Payload Format for H.264 Video](https://datatracker.ietf.org/doc/html/rfc6184)

H.264 encoding is represented by payload type (PT)=96, and an example of SDP negotiation is shown below.

```Plain
... 
a=rtpmap:96 H264/90000
a=fmtp:96 BFrame-enabled=1;
...
```


<span id="006f876a"></span>
## H.265 codec support

RFC specification reference: [RTP Payload Format for High Efficiency Video Coding (HEVC)](https://datatracker.ietf.org/doc/html/rfc7798)

H.265 encoding is represented by payload type (PT)=98, and an example of SDP negotiation is shown below.

```Plain
...
a=rtpmap:98 H265/90000
a=fmtp:98 BFrame-enabled=1;
...
```


<span id="ed57cc06"></span>
## Video B\-frame support

<span id="ed7e5f98"></span>
#### SDP video B\-frame negotiations

The client needs to add B\-frame related information to the Offer SDP to realize the non\-monotonically increasing processing logic in the B\-frame timestamp, and the back end needs to implement the corresponding B\-frame timestamp encoding logic. An example of SDP B\-frame negotiation is shown below.

```Plain
...
a=rtpmap:96 H264/90000
a=fmtp:96 BFrame-enabled=1;level-asymmetry-allowed=1;packetization-mode=1;profile-level-id=42e01f
...
```


In SDP, **BFrame\-enabled** indicates whether or not the client supports B\-frame decoding. It does not indicate whether the server supports sending B\-frames.

The result processing logic for whether the client supports decoding B\-frames and whether the source stream contains B\-frames is as follows:


1. Where BFrame\-enabled=0 in the Offer SDP and the source stream contains B\-frames, the server removes the source stream B\-frames and then forwards it to the client.

2. Where BFrame\-enabled=0 in the Offer SDP and the source stream contains B\-frames, the server forwards the source stream directly to the client.

3. Where BFrame\-enabled=1 in the Offer SDP and the source stream contains B\-frames, the server forwards the source stream directly to the client.

4. Where BFrame\-enabled=1 in the Offer SDP and the source stream does not contain B\-frames, the server forwards the source stream directly to the client.


<span id="2eef99ae"></span>
#### Video B\-frame timestamp calculation

There are two recommended specifications for calculating video B\-frame timestamps:


* **Specification 1:**  The RTP timestamp of each RTP packet carries the sampling time (PTS) of the current frame data, and the decoding order depends on the SequenceNumber. Under this specification, the client side cannot directly calculate the value of the DTS, which is not conducive to fast decoding and frame output when B\-frames are present.

* **Specification 2**: With the RTP private extension header used to carry the CTS value, the RTP timestamp of each RTP packet carries the sampling time (PTS) of the current frame data, while the first RTP packet and VPS/SPS/PPS packet of each frame carry the CTS value of the frame through the RFC5285\-Header\-Extension, and the decoding time of the current frame is calculated using the formula DTS = PTS \- CTS \* 90.


An example of SDP with a=extmap is shown below.

```Plain
...
a=rtpmap:96 H264/90000
a=fmtp:96 BFrame-enabled=1;
a=extmap:7 rtp-hrdext:video:CompositionTime
...
```


The above two methods are compatible. Specification 2 is used when the Offer SDP has corresponding extmap and rtp\-hrdext fields, otherwise Specification 1 is used.

See [RTP extension headers](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-rtm-appendix#rtp-extension-headers) for a detailed explanation of RTP Extension Headers.

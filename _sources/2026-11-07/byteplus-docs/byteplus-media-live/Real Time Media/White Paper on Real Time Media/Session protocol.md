---
title: "Session protocol"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-rtm-session-protocol"
---

This section explains the SDP and MiniSDP protocols used in media negotiation.

<span id="d0ac70ba"></span>
## SDP

**About**: SDP (Session Description Protocol) is a text\-based format (similar to JSON/XML) with special conventions. It is used to describe media information during the transmission process.

**Structure**: The SDP follows the format of `<type>=<value>`, where both `<type>` and `<value>` are case\-sensitive and there can be no spaces around `=`. The SDP consists of a session\-level description followed by zero or multiple media\-level descriptions. The session level begins at `v=` and continues until the first line containing the media level `m=`. Each media level description begins with `m=` and continues until the next `m=` or the end of the SDP.

Some fields in the SDP are mandatory (REQUIRED) while some fields are optional (OPTIONAL). Optional fields are marked with `*` in the following example. All fields must be arranged in the order shown in the example in order to facilitate error detection and parser implementation.

The following is an example of the format and fields used in an SDP description document:

**Session description**

```Plain
v= (protocol version)
o= (originator and session identifier)
s= (session name)
i=* (session information)
u=* (URI of description)
e=* (email address)
p=* (phone number)
c=* (connection information -- not required if included in all media descriptions)
b=* (zero or more bandwidth information lines)
One or more time descriptions:
("t=", "r=" and "z=" lines; see below)
k=* (obsolete)
a=* (zero or more session attribute lines)
Zero or more media descriptions
```


**Time description**

```Plain
t= (time the session is active)
r=* (zero or more repeat times)
z=* (optional time zone offset line)
```


**Media description, if present**

```Plain
m= (media name and transport address)
i=* (media title)
c=* (connection information -- optional if included at session level)
b=* (zero or more bandwidth information lines)
k=* (obsolete)
a=* (zero or more media attribute lines)
```


RFC specification reference: [SDP](https://datatracker.ietf.org/doc/html/rfc8866)

<span id="256ee842"></span>
## MiniSDP

**About**: MiniSDP protocol is a binary encoding compression protocol used to compress the standard SDP.

**Features**: Standard SDP is relatively long (around 5\-10KB), which is not conducive to fast and efficient transmission. In a live streaming scenario, this impacts the time to first frame. MiniSDP facilitates compression of the standard SDP text protocol by converting the native SDP into a smaller binary format that can be transmitted over a UDP packet.

**Advantages**:


* Faster signaling interaction and more efficient network transmission.

* Faster rendering time for the first frame of the live stream pull\-stream.

* Increases the pull\-stream instant loading rate, success rate and other QoS metrics.


**Structure**

The figure below shows the structure of the MiniSDP protocol.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6f25f0f9ecec49a7a6004f1de083fff7~tplv-goo7wpa0wc-image.image) </span>

The structure is described in the table below.


|**Structure** |Description |
|---|---|
|mini_sdp header |MiniSDP headers mainly define the type of SDP and some auxiliary information required for MiniSDP transmission. |
|session header |Mainly defines information about the session dimensions, such as whether to encrypt, candidates, the number of media contained in the session, and the session extension etc. |
|media |Describes the properties of each media type in the session, such as media type, codec, tracks, RTP extensions, etc. |

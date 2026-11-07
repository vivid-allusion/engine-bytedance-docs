---
title: "Appendix"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-rtm-appendix"
---

<span id="590188ad"></span>
## SDP and RTP

The figure below shows the correlations between SDP and RTP.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/748567d0f59b4651b2975bacc52418fe~tplv-goo7wpa0wc-image.image) </span>

Key mapping relationships are shown below.

```Plain
rtpmap  <-->  PT(payload type)
extmap  <-->  Extension ID
SSRC    <-->  SSRC
```


There are two types of profile for extension: **0XBEDE** and **0x1000**.


* **0XBEDE**

   0XBEDE has only 4 bits to specify the `Extension ID` and so supports up to 14 kinds, of which 0 and 0xFF are special IDs.

   ```Plain
   0 1 2 3 4 5 6 7
   +-+-+-+-+-+-+-+-+
   |  ID   |  len  |
   +-+-+-+-+-+-+-+-+
   ```
   

   * Len=0: indicates that it is followed by 1 byte of data;

   * Len=1: indicates that it is followed by 2 bytes of data.

      An example is shown below.

   ```Plain
   0                   1                   2                   3
    0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |      0xBE     |     0xDE      |          length=3             |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |  ID   | L=0   |     data      |  ID   |  L=1  |   data...
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
         ...data   |    0 (pad)    |    0 (pad)    |  ID   | L=3   |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |                             data                              |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   ```
   

* **0x1000**

   255 kinds can be supported when using 8 bits (i.e., 1 byte) to specify the `Extension ID`.

   ```Plain
   0                   1
    0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |       ID      |     length    |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   ```
   

   * length=0: indicates that it is followed by 0 bytes of data;

   * length=1: indicates that it is followed by 1 byte of data.

      An example is shown below.

   ```Plain
   0                   1                   2                   3
    0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |      0x10     |     0x00      |          length=3             |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |      ID       |     L=0       |     ID        |     L=1       |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |       data    |    0 (pad)    |       ID      |     L=4       |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |                          data                                 |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   ```
   

   Here are some common extensions:

   * Audio Level: indicates the volume;

   * TCC: used for bandwidth estimation.

   * Video Orientation: rotates the video.


<span id="bfae3406"></span>
## QoS control FEC/NACK selection

RTC mainly uses FEC and NACK to counter network packet loss. The usage scenarios for the two options are as follows.


* It is recommended to turn off the FEC function when RTT < 20ms (recommended reference average);

* It is recommended to turn on the FEC function when RTT \>=20ms (recommended reference average);


WebRTC maintains a one\-dimensional redundancy table for FEC Rate, which actually resembles a two\-dimensional table (kFecRateTable[rate_i][loss_j]). The rows represent the single frame bit rate, and the columns represent the packet loss rate loss_ratio \* 256. Theoretically, the packet loss rate is 50% of the maximum supported value.

The use of NACK will introduce a delay when the RTT is too large (e.g., the arrival time of retransmission packets is too long, causing stuttering and deterioration). If FEC is used, lost packets can be recovered via redundant packets and source data packets.

<span id="4b4d6e95"></span>
## STUN protocol

RFC specification reference: [Session Traversal Utilities for NAT (STUN)](https://tools.ietf.org/html/rfc8489).

STUN (Session Traversal Utilities for NAT) is a session transmission tool in the NAT environment. It is a protocol that handles NAT transmission, but is mainly used as a tool to serve other protocols. The STUN protocol is used to obtain the NAT traversal and the extranet address corresponding to the intranet address on the NAT. STUN is a C/S mode protocol: the client sends a STUN request, and the STUN service responds with the IP address and port number assigned to the host by the NAT.

<span id="ec7f1e51"></span>
## TURN protocol

RFC specification reference: [Traversal Using Relays around NAT (TURN)](https://tools.ietf.org/html/rfc5766).

ICE uses the TURN (RFC 5766) protocol to support STUN; in the event of point\-to\-point traversal failure, interconnectivity can be achieved by leveraging the forwarding function of the TURN protocol. The ports are the same as those for STUN.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Except ChannelData messages, all other TURN messages follow the STUN message format.</div>


<span id="c98cdd83"></span>
## AAC packaging

There are usually two ways for AAC to be packaged into network transmissions: ADTS and LATM.

Each ADTS frame has a frame header. If the information in each frame header is the same, there will be greater redundancy.

The LATM format offers excellent flexibility; the audio configuration unit of each frame can be transmitted either in\-band or out\-of\-band. As such, LATM is suitable for both streaming and RTP transmission.

During RTP transmission, if the configuration information for the audio data remains unchanged, StreamMuxConfig (AudioSpecificConfig) information can be transmitted first through the SDP session. This is because a LATM stream consists of a sequence of audioMuxElements containing one or more audio frames.

A complete or partially complete audioMuxElement can be directly mapped to an RTP payload.

<span id="8d298e01"></span>
### Converting ADTS raw frames to LATM frames

Read the ADTS header information, then obtain the sampling rate, channel number, AAC algorithm parameters, frame length and other information to generate the audio specific configuration unit AudioSpecficConfig.


* Extract and save the original frame data;

* The PayloadLengthInfo is generated according to the original frame length information, then the LATM audio payload is generated by the PayloadLengthInfo and the original frame data, and finally the LATM frame is assembled with the AudioSpecficConfig.


<span id="af78ebb0"></span>
## Private codec support

In order to expand the private codec capabilities of different vendors, the client and server need to follow the same codec implementation rules and clarify the expansion of codec types in SDP; the following is an example of the BytePlus ByteVC1 encoder (in the SDP text description, ByteVC1 is used as a placeholder for the private video codec format). The sample SDP is as follows:

```Plain
a=rtpmap:98 ByteVC1/90000
a=fmtp:98 BFrame-enabled=1;
```


<span id="a7a772e4"></span>
## RTP timestamp

In low\-latency (WebRTC) live broadcast systems, timestamps packaged and transmitted based on the RTP protocol are different from those in traditional live stream technologies. For each bit of data packaged into an RTP, a timestamp is placed on the head of the current RTP, and the unit of measurement depends on the sampling rate of the audio & video data itself (unlike standard RTMP, FLV, and HLS live stream protocols, where a 32\-bit unsigned integer is usually used to represent the timestamp unit of each individual audio & video data packet, generally in milliseconds).

The unit used for video timestamps is 1/90,000 seconds, and 90,000 (90k clock ticks per second) is the TimeScale used for video synchronization. 90k is used because current video frame rates are mainly 25fps, 29.97fps, 30fps, etc. and 90k is a multiple of these figures. The frame rate is the sampling rate of the video source; different video streams have different timestamps (e.g., H.264 and H.265).


* Single Nalu: If a video frame contains 1 NALU, it can be packaged into an RTP package separately; the RTP timestamp then corresponds to the acquisition time of this frame.

* FU\-A: If the NALU of a video frame is too large (exceeds MTU) and needs to be split into multiple packets, you can use the FU\-A method to split it into several RTP packets, each with the same timestamp.

* STAP\-A: If a frame is too large to be packaged separately but the individual NALUs within the frame are relatively small, multiple NALUs can be packaged and sent using STAP\-A. However, the timestamps of these NALUs must match and so must the packaged RTP timestamps.


The audio timestamp unit is the inverse of the sampling rate. For example, if the sampling rate is 48,000, then there are 48,000 samples per second, each sample is 1/48ms, and each sample corresponds to a timestamp. RTP audio packets typically pack 20ms of data corresponding to 48,000 \* 20/1000 = 960 samples, which means that each audio packet carries 960 audio samples. Since one sample corresponds to one timestamp, the difference between the timestamps of two adjacent audio RTP packets is 960.

<span id="2779209f"></span>
### RTP extension headers

RFC specification reference: [A General Mechanism for RTP Header Extensions](https://tools.ietf.org/html/rfc5285).

A generic RTP header structure in the [RTP](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-rtm-terminology#rtp) definition is as follows.

```Plain
0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|V=2|P|X|  CC   |M|     PT      |       sequence number         |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                           timestamp                           |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|           synchronization source (SSRC) identifier            |
+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+
|            contributing source (CSRC) identifiers             |
|                             ....                              |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```


If the X bit is 1, this indicates that there are some additional RTP extension headers behind the CSRC, which will take the following form.

```Plain
0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|      defined by profile       |           length              |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                       header extension                        |
|                             ....                               |
```


However, this form can only append a single extension header, and RFC5285 is extended as defined by profile to support multiple extension headers.

<span id="8816aa66"></span>
#### One\-byte extension (one\-byte header)

```Plain
0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|      0xBE     |    0xDE   |            length =3              |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|  ID   |  L=0  |   data    |   ID  |  L=1  |    data...
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
     ...data    |  0 (pad)  |    0 (pad)    |   ID   |   L=3    |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                              data                             |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```


The first 16 bits after the RTP header are fixed as the **0XBEDE** flag, which means that this is a one\-byte extension. **length = 3** indicates that there are three extension headers after it. Each extension header starts with a single byte. The first 4 bits are the ID of the extension header, and the last four bits are the length of the data minus one (\-1). For example, **L=0** means that there is 1 byte of data after it. Similarly, **L=1** in the second extension header indicates that there are 2 bytes of data after it. However, note that the third extension header does not follow immediately; instead, 2 bytes of zeros are added in order to pad for 32 bits.

<span id="e9db43d2"></span>
#### Double\-byte extension

In the case of a one\-byte extension header, the first 16 bits after the RTP header are as follows (**0x100 + appbit**). The appbits can be used to populate data at the application level.

```Plain
0                   1
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|         0x100         |appbits|
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```


In the following example, the extension starts with **0x100 + 0x0**, followed by **length = 3** to indicate that there are three headers. This is then followed by the extension header and data. The extension header now has 8 bits compared with 4 bits for the one\-byte header (except for the ID and L), and the remaining data is unchanged.

```Plain
0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|      0x10     |      0x00     |           length=3            |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|       ID      |      L=0      |      ID      |      L=1       |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|      data     |    0 (pad)    |      ID      |      L=4       |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                             data                              |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```


<span id="e6ea4207"></span>
### SSRC

SSRC is equivalent to the ID of an RTP transfer session. The ID of each session is an independent and non\-repeating identifier (i.e., each RTP transfer has a name). This number is randomly generated and must be unique. When the RTP session changes (e.g., IP address, etc.), this ID also needs to be changed.

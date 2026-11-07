---
title: "Audio media properties"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-rtm-audio-media-properties"
---

RTM audio coding technology supports Opus coding and AAC coding.

<span id="fa8b27ff"></span>
## Opus codec support

The Google reference code for the WebRTC standard natively supports built\-in implementations.

The following definitions are required in the SDP to use Opus encoding.

```Plain
a=rtpmap:111 opus/48000/2 
a=rtcp-fb:111 transport-cc 
a=fmtp:111 minptime=10;useinbandfec=1
```


Opus supports 8000Hz, 12000Hz, 16000Hz, 24000Hz, and 48000Hz sampling rates. Different sampling rates are defined differently in SDP, and can be defined by modifying `maxplaybackrate` parameters. The following examples show the SDP settings for 8000Hz and 16000Hz sampling rates.


* The SDP settings for an 8000Hz sample rate would be as follows:

   ```Plain
   a=rtpmap:111 opus/48000/2 
   a=rtcp-fb:111 transport-cc 
   a=fmtp:111 minptime=10;useinbandfec=1;maxplaybackrate=8000
   ```
   

* The SDP settings for a 16000Hz sample rate would be as follows:

   ```Plain
   a=rtpmap:111 opus/48000/2 
   a=rtcp-fb:111 transport-cc 
   a=fmtp:111 minptime=10;useinbandfec=1;maxplaybackrate=16000
   ```
   


<span id="20679553"></span>
## AAC codec support

RTM audio coding technology supports AAC\-LC, AAC\-HE, and AAC\-HE2 coding.


* See [RFC 3640 Opinions](https://datatracker.ietf.org/doc/html/rfc3640) for RTP encapsulation of MPEG4 elementary streams;

* See [RFC 6416 Opinions](https://datatracker.ietf.org/doc/html/rfc6416) for RTP encapsulation of MPEG4 audio/video streams.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The AAC codec does not support the RFC 3640 method when the AAC audio config differs, and RFC 6416 can write the config information to RTP.</div>


<span id="8bda5be9"></span>
### LATM(MP4A\-LATM)

LATM (Low\-overhead MPEG\-4 Audio Transport Multiplex) is a high\-efficiency streaming method developed using MPEG\-4 AAC. The LATM format is expressed in frames and is mainly composed of AudioSpecificConfig (Audio Specific Configuration Unit) and audio payload. See [ACC packaging](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-rtm-appendix#aac-packaging).

<span id="515acdc9"></span>
#### RTP encapsulation instructions for MP4A\-LATM

The RTP container format for MP4A\-LATM is shown below.

```Plain
0                   1                   2                   3
0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|V=2|P|X|  CC |M|      PT     |       sequence number           |RTP
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                           timestamp                           |Header
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|          synchronization source (SSRC) identifier             |
+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+
|             contributing source (CSRC) identifiers            |
|                             ....                              |
+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+
|                                                               |RTP
:                   audioMuxElement (byte aligned)              :Payload
|                                                               |
|                               +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                               :...OPTIONAL RTP padding        |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```


RFC 3640 describes the RTP encapsulation instructions for MP4A\-Generic (AU_header_size+AU_header+AudioData); audio\-specific configurations can use in\-band transmission (i.e. where each frame is attached) or out\-of\-band transmission (i.e. where each frame is passed to the decoder via SDP). The audio payload consists of several subframes, each composed of PayloadLengthInfo and PayloadMux.

The LATM format is expressed in frames and consists of audio\-specific configuration StreamMuxConfig and audio payload PayloadLengthInfo+PayloadMux.

The structure of AudioMuxElement is shown in the figure below.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/185cf59653e143e2930a4b1c5bea2dd3~tplv-goo7wpa0wc-image.image) </span>

AudioSpecificConfig describes the information contained in a LATM frame. The audio payload is mainly composed of the payload length information PayloadLengthInfo and the payload net load PayloadMux. AudioSpecificConfig information can be in\-band or out\-of\-band transmission.


* In\-band transmission: Each LATM frame contains AudioSpecificConfig information;

* Out\-of\-band transmission: Each LATM frame does not contain AudioSpecificConfig information, and AudioSpecificConfig information is sent to the decoder by other means. Since the AudioSpecificConfig information is generally unchanged, it only needs to be sent once.


As such, in the case of in\-band transmission, the AudioSpecificConfig information can adapt to the constantly changing audio coding information, while out\-of\-band transmission saves on bit rate.

In\-band and out\-of\-band transmission is determined by the muxconfigPresent flag. For example, in streaming media applications, muxconfigPresent can be set to 0 so that no AudioSpecificConfig information is contained in each LATM frame. In this case, LATM frames are sent through the RTP packet, and the AudioSpecificConfig can be sent to the decoder all at once through the SDP file.

<span id="cc0dceff"></span>
#### SDP request and response example

<span id="3110e24a"></span>
##### **Sample SDP request:** 

```Plain
...
a=rtpmap:111 opus/48000/2
a=rtcp-fb:111 transport-cc
a=fmtp:111 minptime=10;useinbandfec=1
a=rtpmap:120 MP4A-LATM/48000/2
a=rtcp-fb:120 transport-cc
a=rtpmap:121 MP4A-LATM/44100/2
a=rtcp-fb:121 transport-cc
...
```


<span id="83834418"></span>
##### **Sample SDP response**

`a=fmtp` with detailed AAC information.

```Plain
...
a=rtpmap:121 MP4A-LATM/44100/2
a=rtcp-fb:121 nack
a=rtcp-fb:121 transport-cc
a=fmtp:121 SBR-enabled=1;config=40005724101fe0;cpresent=0;object=2;profile-level-id=1
...
```


The values and meanings of some AAC\-HE (SBR\-enabled=1) and AAC\-HE2 (SBR\-enabled=1;PS\-enabled = 1;) `objects` are shown below.


* Object = 2 indicates AAC\-LC (Advanced Audio Coding \- Low Complexity);

* Object = 5 indicates SBR (Spectral Band Replication);

* Object = 29 indicates PS (Parametric Stereo);


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Where there are multiple sampling rates in the AAC supported by the playback client, priority should be given to the sampling rate of the media source stream.</div>

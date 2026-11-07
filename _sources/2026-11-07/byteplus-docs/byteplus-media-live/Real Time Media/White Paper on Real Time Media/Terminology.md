---
title: "Terminology"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-rtm-terminology"
---

<span id="96e45991"></span>
## FEC

FEC (Forward Error Correction) is a forward error correction technique. The sender sends payload data together with a redundant error correction code, and the receiver then performs error detection on the data. If an error is found, the error correction code is used to correct the error. FEC uses a redundant transmission mechanism. FEC can achieve the desired effect when bandwidth allows; however, it may cause undesirable side effects where severe bandwidth limitations apply.

Commonly used low latency (WebRTC) live stream FEC solutions include **ULPFec** and **RSFec**. For example, **ULPFec** can be enabled for live streams or video calls in Chrome or Firefox, while clients and servers can also separately implement **RSFec**. Specific FEC steps are implemented according to the SDP negotiation between the two parties.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/26b057f33b7f413b887441943cc617b1~tplv-goo7wpa0wc-image.image) </span>


* RFC specification reference for ULPFec: [https://datatracker.ietf.org/doc/html/rfc5109](https://datatracker.ietf.org/doc/html/rfc5109)

* RFC specification reference for RSFec: [https://datatracker.ietf.org/doc/html/rfc5510](https://datatracker.ietf.org/doc/html/rfc5510)


<span id="3c654fbf"></span>
## ICE

RFC specification reference for ICE: [Interactive Connectivity Establishment (ICE)](https://tools.ietf.org/html/rfc5245).

ICE stands for Interactive Connectivity Establishment. P2P (Peer to Peer) transmission paths between the client and server are realized with a set of protocol families that use the offer/answer format to solve the NAT traversal problem. Please refer to [STUN protocol](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-rtm-appendix#stun-protocol) for more details on NAT traversal. Makes comprehensive use of existing STUN, [TURN protocol](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-rtm-appendix#turn-protocol) and other protocols to establish sessions in a more effective manner.

ICE does not know the location and NAT type of the network, and can dynamically discover the optimal transmission path via ICE. In the following figure, L and R are ICE agents, referred to as L and R. L and R have their own transport addresses, including the host's network interface card address, the extranet address on the NAT, and the TURN service address. ICE finds the candidate address pairs of L and R from these addresses to enable efficient connectivity between the two ends. ICE can exchange SDP information from both ends via the signaling server. ICE uses protocols such as STUN and TURN to establish sessions.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/234752ea01474b01b88e59e3a0e66cea~tplv-goo7wpa0wc-image.image) </span>

There are two types of ICE: Full ICE and Lite ICE.


* Full ICE: Each party must perform connectivity checks.

* Lite ICE: When Full ICE and Lite ICE communicate, only the Full ICE side needs to check the connectivity while the Lite side only needs to respond to the response message. This model is often used in scenarios that require deployment on public network facilities.


ICE has the following five states.


* Waiting: A connectivity check has not yet been performed; the highest\-priority candidate pair on the checklist is selected and a connectivity check is performed on that pair.

* In\-Progress: A check has been initiated for this pair, but the check's transaction is still in progress.

* Succeeded: A check for this pair has been completed successfully.

* Failed: A check for this pair has been performed but failed.

* Frozen: No check has been performed yet for this candidate pair.


<span id="0e705729"></span>
## NACK

Retransmission of lost packets (NACK) is an important countermeasure against network errors. NACK detects data packet loss at the receiving end and sends a NACK packet to the sending end; the sending end then locates the corresponding data packet in the sending buffer according to the sequence number in the NACK packet and re\-transmits it to the receiving end. NACK requires the support of the sender and the send buffer.

<span id="ec389933"></span>
## RTCP

RFC specification reference: [RTP: A Transport Protocol for Real-Time Applications](https://tools.ietf.org/html/rfc3550)

The RTCP protocol is responsible for assuring the quality of media streams and provides services such as flow control. During RTP transmission, participants periodically send RTCP packets containing various statistical information, according to which audio & video quality can be dynamically adjusted.

```Plain
0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|V=2|P|  RC/FMT |      PT      |             length             |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```


The main RTCP types are shown in the table below.


|Name |PT |RC/FMT |Sender |Information contained and purpose |
|---|---|---|---|---|
|SR (Sender Report) |200 |*  |RTP sender |Primarily time information and the number of packets sent. |
|RR (Receiver Report) |201 |*  |RTP Receiver |Primarily the number of packages, package loss rate, jitter, and time information |
|NACK |205 |1 |RTP Receiver |Sends a NACK to the publisher when the sequence number is not received by the receiver |
|TCC |205 |15 |RTP Receiver |Reflects time information from when the receiver received the RTP packet, and the bandwidth calculated by the sender according to the TCC |
|PLI (Picture loss Indication) |206 |1 |RTP Receiver |Requests sender to encode key frames |
|FIR (Full Intra Request) |206 |4 |RTP Receiver |Requests sender to encode key frames |
|REMB |206 |15 |RTP Receiver |Contains the bandwidth calculated by the receiver |
|XR (eXtended Report) |207 |*  |RTP Sender/Receiver |*  |
|APP (Application defined) |204 |1 ||*  |


<span id="d17b1845"></span>
## RTP

RFC specification reference: [RTP: A Transport Protocol for Real-Time Applications](https://tools.ietf.org/html/rfc3550)

RTP is a data packet format for audio & video streaming; it is used to provide end\-to\-end real\-time transmission services for voice, image, fax and other multimedia data that require real\-time transmission over the internet. RTP provides time information and stream synchronization for end\-to\-end real\-time transmission, but it does not guarantee the quality of service, which is provided by [RTCP](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-rtm-terminology#rtcp).

```Plain
0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|V=2|P|X|  CC   |M|     PT      |       sequence number         |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                           timestamp                           |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|          synchronization source (SSRC) identifier             |
+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+
|           contributing source (CSRC) identifiers              |
|                             ....                              |
+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+
|       extension profile      |            length              |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                        header extension                       |
|                             ....                              |
```


The meanings of standard RTP header fields are shown in the following table.


|Field |Meaning |
|---|---|
|V |Version, fixed value is 2 |
|P |Padding bit, indicates whether there is padding data after the RTP packet |
|X |eXtension, [RTP extension headers](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-rtm-appendix#rtp-extension-headers) flag, 1 indicates extension present |
|CC |CSRC Count |
|M |Marker, generally used to mark the end of audiovisual frames. |
|PT |Payload Type, specifies the payload type |
|Sequence Number |Packet sequence number, records the order of packets |
|Timestamp |Timestamp for video and audio synchronization |
|SSRC |RTP source identifier, different to SSRC for different streams but Payload Type may be the same. See [SSRC](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-rtm-appendix#ssrc). |
|CSRC |Shared source label, usually used when mixing sounds or mixing screens. For example, if an RTP packet is composed of multiple voices mixed together, then each person is one CSRC. |


<span id="1ae53ecb"></span>
## RTX

RFC specification reference: [RTP Retransmission Payload Format](https://tools.ietf.org/html/rfc4588).

NACK and RTX are both **packet retransmission** strategies in WebRTC.


* NACK: The receiver notifies the sender of the serial number of the lost packet via RTCP and asks the sender to retransmit the packet;

* RTX: The sender sends NACK retransmission packets or FEC redundant packets over the new SSRC.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/809119f18bdd4f569c73109d7b414ed8~tplv-goo7wpa0wc-image.image) </span>

In RTX mode, there are the following two types of data packets.


1. NACK retransmission packet;

2. Redundant packets sent by the sender.


<span id="8fc32f05"></span>
## SDP

SDP (Session Description Protocol) is a general session description protocol mainly used to describe multimedia sessions; its uses include session declaration, session invitation, and session initialization. Low Latency (WebRTC) live streaming is expanded on the basis of RFC 8866, such as ICE and DTLS.


* offer: initiator's SDP;

* answer: responder's SDP;

* localSDP: local SDP;

* remoteSDP: peer SDP.

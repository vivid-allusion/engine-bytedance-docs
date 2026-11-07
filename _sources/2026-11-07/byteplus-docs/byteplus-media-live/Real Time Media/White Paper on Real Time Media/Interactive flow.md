---
title: "Interactive flow"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-rtm-Interactive-flow"
---

RTM is based on WebRTC technology, and establishing point\-to\-point transmission based on the WebRTC standard typically involves the following three steps:


1. Media Negotiation: Communicating parties interact with the Session Description Protocol (SDP). This step is designed to confirm the media types, encoding methods, resolutions, and other parameters supported by both parties in order to ensure that subsequent media transmissions can proceed smoothly.

2. Network Address Negotiation: In this step, both parties engage in interactive network address negotiation to obtain the true IP address of the peer. This step prepares for the construction of media transmission channels and ensures that data can be accurately transmitted between each party.

3. Point\-to\-point transmission of media data: Both parties can now engage in point\-to\-point transmission of media data. In this step, the media data is transmitted in real time via the previously negotiated transmission channels, thus realizing RTM.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/20b9198390434d809b95cf0993742fcb~tplv-goo7wpa0wc-image.image) </span>

<span id="52c0016e"></span>
## Signaling interaction

Prior to the transmission of media data, the client and server need to verify their ability to transmit and process audiovisual media (e.g., supported formats, codec processing details, quality assurance methods, etc.). RTM uses the SDP to communicate shared media capabilities and ensure compatibility.

Media negotiation is conducted over the network in a process called signaling interaction. Signaling interaction primarily uses the SDP. During signaling interaction, different network transport protocols can be, including TCP/UDP and HTTP/QUIC.

<span id="f5840039"></span>
## Media transmission

Once the negotiation step is complete, the transmission of media data (including livestream push/pull audiovisual data) begins. Audiovisual data can be transmitted and delivered via UDP in combination with QoS methods such as congestion control, packet loss detection and recovery to realize WebRTC\-based media streaming.

The complete process of signaling interaction, media negotiation and media transmission constitutes a single effective RTM session.

Stream pushing (where the live streaming host sends audio & video data to the server) and stream pulling (where the audience requests audio & video data from the server) both constitute one\-way transmission, which differs from the full\-duplex two\-way transmission of audiovisual data in video call mode.

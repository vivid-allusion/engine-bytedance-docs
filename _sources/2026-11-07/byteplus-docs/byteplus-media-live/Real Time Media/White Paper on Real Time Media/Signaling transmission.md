---
title: "Signaling transmission"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-rtm-signaling-transmission"
---

This chapter describes signaling interactions based on the HTTP, UDP, and QUIC protocols.

<span id="685b18b6"></span>
## HTTP signaling interactions

**Advantages**: Excellent compatibility, supports browser/client\-side intercommunication; high reliability.

**Disadvantages**:


* Success rates are poor in weak connection environments where there are long round\-trip times (RTT) or unstable network signals;

* Responses to playback requests may be slow or time out, mainly due to the large size of signaling data packets and TCP retransmission.


**Transmission method**: In the case of standard SDP signaling based on the HTTP protocol, data is transmitted between the client and the server.

The figure below shows the interaction flow for SDP signaling based on the HTTP protocol.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a43c049e72374f6aaaf28b188b5b2ac1~tplv-goo7wpa0wc-image.image) </span>

<span id="99cb380c"></span>
### **Signaling request flow**


1. Client generates description information (Offer SDP);

2. Client transmits the description information (Offer SDP) by sending a data request (offer request) to the signal server using the HTTP protocol;

3. Server receives the Offer SDP request, performs a redirect to origin servers on the specified media data source, queries the audiovisual media information, and generates a standard answer SDP;

4. Server replies by sending a response to the client that initiated the request (answer response);

5. Once the SDP parties have completed the negotiation, an [ICE](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-rtm-terminology#ice) connection is established; the client will query the network address from the server and then finish communications with the server to complete the handshake;

6. RTP transmission starts and playback begins according to the traditional P2P connection process.


<span id="9c81a2b3"></span>
### Stop playback flow

There are two options for stopping the playback process. For more information, see [Ending the media transmission](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-rtm-ending-transmission).


* Recommended Option: Send a RTCP Bye Message to the media server using the RTCP media feedback channel;

* Back\-up Option: Use UDP Socket to send a stop command to the signaling server, which controls the media server and stops transmitting data;


<span id="1b02ad57"></span>
## UDP signaling interaction

There are two types of UDP signaling interaction: **UDP standard path** and **UDP fast path**.

<span id="d1deb45f"></span>
### UDP standard path


* **Advantages**: Faster first frame rendering time and higher instant load and success rates.

* **Disadvantages**: Creates security\-related compliance issues in areas where authenticated encryption is mandatory, and web browser support is unavailable.

* **Transmission means**: Transmits over UDP network via MiniSDP protocol; a single UDP data packet request is able to transmit complete SDP compression information.


The figure below shows the interaction flow for MiniSDP signaling under the UDP protocol.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bd4be5472b094b48a5211afa65faade1~tplv-goo7wpa0wc-image.image) </span>

<span id="2ed5f750"></span>
#### **Signaling request flow**


1. Client generates offer SDP;

2. Client compresses the standard SDP into MiniSDP according to the specified protocol;

3. Client makes MiniSDP (offer SDP) send a request (offer request) to the signal server through the UDP socket;

4. Server receives the MiniSDP request and extracts and restores the request to the standard SDP according to the specified protocol;

5. Server performs a redirect to origin servers on the FLV data according to the standard SDP, queries the audiovisual media information, and generates the standard SDP;

6. Server compresses the standard SDP into MiniSDP according to the specified protocol;

7. Server replies so that the MiniSDP (answer SDP) sends a response (answer response) to the client that initiated the request through the UDP socket;

8. Client receives the MiniSDP request and extracts and restores the request to the standard SDP according to the specified protocol;

9. RTP transmission starts and playback begins according to the traditional P2P connection process.


<span id="8064ac92"></span>
#### **Stop playback flow**

The process for stopping playback is the same as for HTTP signalling. For details, see [Ending the media transmission](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-rtm-ending-transmission).

<span id="ec7392aa"></span>
### UDP fast path

The UDP fast path uses multiplexing signaling and media data transmission channels to remove ICE setup time from first frame overhead rendering.

<span id="5276804a"></span>
#### Signaling request flow

Unlike the UDP standard path, when using the fast path, the process for establishing the interactive connection runs in parallel with the transmission and decoding of media data. This means that the server sends media data to the client for decoding and rendering while the ICE connection is being established.


* **UDP standard path**: The server sends media data (RTP packet) to the client once the ICE connection is established;

* **UDP fast path**: UDP signaling channels are multiplexed. The server sends the media data (RTP packet) via the signaling channel once signaling is successful but before the ICE connection is established. Once the ICE connection is established, the server switches to the new socket media channel and continues to send the RTP packet.


The figure below shows a flowchart of signaling requests for the UDP fast path.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1e263a715486429b84b80e09e5288d0a~tplv-goo7wpa0wc-image.image) </span>


1. Client establishes a signaling channel with the server through MiniSDP;

2. The server passes the remote answer to the client;

3. The client establishes the ICE connection while, simultaneously, the server sends the RTP data packet containing audiovisual data to the signaling socket.

4. The client activates WebRTC and the video receiving engine (video_recv_pipeline) inside the client (PeerConnection) enables RTP data packets to access the transport module;

5. Once the ICE connection has been established, the server sends the RTP data packet to the transmission module socket.


<span id="08aa990c"></span>
#### Stop playback flow

The process for stopping playback is the same as for HTTP signalling. For details, see [Ending the media transmission](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-rtm-ending-transmission).

<span id="601e00ad"></span>
## QUIC signaling interaction

QUIC signaling interaction is a security\-supplementing interaction solution. QUIC signaling interaction differs from HTTP/UDP signaling interaction in the following ways:


1. Standardized SDP signaling is ideally transmitted through HTTP/HTTPS with CDN support, but this results in the longest signaling connection time, as well as a relatively low success rate in weak connection environments.

2. The best results are obtained when existing MiniSDP signaling is transmitted via bare UDP channels. This improves the success rate in weak connection environments, but creates potential security issues.

3. MiniSDP over QUIC is expected to offer excellent security with a signaling connection time between HTTP and UDP metrics and no significant adverse impact on success rates in weak connection environments compared to UDP.

4. The ultimate advantage of QUIC is enhanced security. All content transmitted by QUIC is encrypted by default, thus protecting people's privacy.


<span id="1e3b4eba"></span>
### QUIC standard transport

The figure below shows a signaling interaction flowchart for MiniSDP Over QUIC.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b7b4d52c622349299f9bf3bbb9ffb454~tplv-goo7wpa0wc-image.image) </span>

**Initial QUIC connection**


1. Client generates offer SDP.

2. Client compresses the standard SDP into MiniSDP according to the specified protocol.

3. Client sends inchoate hello to the server and requests the server public key.

4. Server returns a rejection with the server's public key, certificate, and random number.

5. Client verifies the certificate, calculates the symmetric key K1 and sends a full hello with the client's public key, random number, and the MiniSDP offer encrypted by the symmetric key K1, and uses the HTTP/1.1 POST method to send the MiniSDP data buffer (MiniSDP over QUIC) over the established QUIC channel.

6. Server receives the client reply again, and extracts and restores the received MiniSDP to standard SDP according to the specified protocol.

7. Server performs a redirect to origin servers on the media data according to the standard SDP, queries the audiovisual media information, and generates the answer SDP.

8. Server compresses the standard SDP into MiniSDP according to the specified protocol.

9. Server generates the temporary server public key 2, computes the forward\-secure symmetric key K2, and returns server hello and the MiniSDP answer encrypted with the symmetric key K2.

10. Client receives the MiniSDP request and extracts and restores the request to the standard SDP according to the specified protocol.

11. RTP transmission starts and playback begins according to the traditional P2P connection process.


**Subsequent QUIC connection**


1. Client generates offer SDP.

2. Client compresses the standard SDP into MiniSDP according to the specified protocol.

3. Client sends full hello with the client's public key, random number, and a MiniSDP offer (MiniSDP over QUIC) encrypted with the symmetric key K1 calculated with the saved server config (including the server public key).

4. Server receives the client reply again, and extracts and restores the received MiniSDP to standard SDP according to the specified protocol.

5. Server performs a redirect to origin servers on the media data according to the standard SDP, queries the audiovisual media information, and generates the answer SDP.

6. Server compresses the standard SDP into MiniSDP according to the specified protocol.

7. Server generates the temporary server public key 2, computes the forward\-secure symmetric key K2, and returns server hello and the MiniSDP answer encrypted with the symmetric key K2.

8. Client receives the MiniSDP request and extracts and restores the request to the standard SDP according to the specified protocol.

9. RTP transmission starts and playback begins according to the traditional P2P connection process.


**QUIC failed downgrade**

The client sets the timeout waiting time when establishing a QUIC connection with the server. If the connection times out, reconnection attempts are initiated according to the set number of retries. Once several attempts fail, the connection is downgraded to other streaming methods such as HTTP\-FLV or HLS.


* **Initial Connection (1\-RTT\-signaling)** : The client saves the server public key, and the server also saves its own server public key. The server public key stored by the server expires after one week, while the server public key stored by the client does not expire.

* **Subsequent connections (0\-RTT\-signaling)** : When the client is 0\-RTT connected, the 0\-RTT connection is successful if the server hello is returned; the 1\-RTT connection process is restarted if a rejection is returned.

* **QUIC data sending (MiniSDP)** : The server opens a port that supports the QUIC protocol, the client accesses a QUIC server that is listening to a UDP port via the domain name, and MiniSDP data is sent to the peer over the QUIC channel via the HTTP/1.1 POST method (HTTP/HTTPS type wrapping).


<span id="89497b30"></span>
### QUIC fast transport

QUIC fast transport uses multiplex signaling and media data transmission channels to remove ICE setup time from first frame overhead rendering.

**Signaling request flow**

Unlike with QUIC standard transport, when using the fast path, the process for establishing the interactive connection runs in parallel with the transmission and decoding of media data. This means that the server sends media data to the client for decoding and rendering while the ICE connection is being established.


* **QUIC standard transport**: The server sends media data (RTP packet) to the client once the ICE connection is established;

* **QUIC fast transport**: UDP (quic\-minisdp) signaling channels are multiplexed. The server sends the media data (RTP packet) via the signaling channel once signaling is successful but before the ICE connection is established. Once the ICE connection is established, the server switches to the new socket media channel and continues to send the RTP packet.


The figure below shows a flowchart of signalling requests for QUIC fast transport.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2302100ef57f400f901d738f93fd9efc~tplv-goo7wpa0wc-image.image) </span>


1. Client establishes a signaling channel with the server through the QUIC protocol;

2. The server passes the remote answer to the client;

3. The client establishes the ICE connection while, simultaneously, the server sends the RTP data packet to the signaling socket QUIC.

4. The client activates the WebRTC video receiving engine inside the client (video_recv_pipeline), enabling RTP data packets to access the QUIC\-transport module;

5. Once the ICE connection has been established, the server sends the RTP data packet to the transmission module transport socket.


<span id="25ecc607"></span>
### QUIC specification

QUIC\-based MiniSDP signaling interactions use the [gQUIC](https://www.chromium.org/quic) protocol (an earlier version of the QUIC protocol) and will continue to evolve to support the IETF QUIC (QUIC protocol standardized by the Internet Engineering Task Force IETF).


* [QUIC Wire Layout Specification](https://docs.google.com/document/d/1WJvyZflAO2pq77yOLbp9NsGjC1CHetAXV8I0fQe-B_U/edit#heading=h.o9jvitkc5d2g)

* The QUIC specification is compatible with gQUIC Q043.

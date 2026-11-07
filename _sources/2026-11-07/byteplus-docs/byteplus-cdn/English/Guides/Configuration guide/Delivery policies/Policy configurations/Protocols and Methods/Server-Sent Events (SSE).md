---
title: "Server-Sent Events (SSE)"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/sse_en-us"
---

This document describes how BytePlus CDN supports Server\-Sent Events (SSE), including request identification, streaming behavior, and configuration steps.

<span id="e5eee699"></span>
## SSE overview

Server\-Sent Events (SSE) is an HTTP\-based technology that allows a server to push updates to a client over a persistent, one\-way connection. SSE is suitable for scenarios where the server needs to continuously send text\-based event data to the client.

<span id="de85d6a9"></span>
### Key benefits


* Lightweight integration: SSE uses the existing HTTP protocol stack. Clients can connect by using the native `EventSource` API, which reduces development effort and is supported by major browsers.

* Automatic reconnection: The client\-side `EventSource` API supports automatic reconnection. During reconnection, the client can send the last received event ID by using `Last-Event-ID`, providing the foundation for resumable event delivery.


<span id="121d7c22"></span>
### Use cases


* Real\-time notifications, such as social messages, order updates, and operational alerts. Real\-time data monitoring, such as financial quotes and sensor data.

* LLM streaming output, where generated text is sent to the client incrementally to create a typewriter\-style experience, reduce time to first token, and improve interactivity.


<span id="febd2412"></span>
## How CDN supports SSE

After SSE is enabled, CDN treats requests that meet the SSE identification requirement as long\-lived requests. The edge node maintains the client connection, forwards the request to the origin, and streams the origin response back to the client.

<span id="f4d2c8a1"></span>
### Request identification

In the current version, CDN identifies a request as an SSE request when the client request includes the `Accept: text/event-stream` header. To produce an SSE streaming response, the origin response must include the `Content-Type: text/event-stream` header and continuously output data in SSE format.

If the client request does not include `Accept: text/event-stream`, CDN processes the request as a regular HTTP request, even if the origin response includes `Content-Type: text/event-stream`. In this case, the client may not receive the response as a real\-time event stream.

<span id="6b9c6511"></span>
### Long\-lived connection bridging

After the client request is routed to the nearest CDN edge node, the client and edge node maintain a long\-lived connection. The edge node forwards the request to the origin and maintains a separate connection with the origin. Together, these connections allow the edge node to fetch the event stream from the origin and forward it to the client.

<span id="84f98c37"></span>
### Event stream forwarding

After SSE\-formatted data reaches the edge node, CDN forwards the stream to the client without caching or modifying the event data.

<span id="275ec1c5"></span>
### Connection reuse

If you enable SSE, we also recommend enabling HTTP/2. When HTTP/2 origin fetch is available and enabled, HTTP/2 multiplexing allows the edge node and origin to reuse a single TCP connection for multiple streams. These streams can carry SSE data for multiple clients, reducing the number of origin connections.

<span id="connection-interruption-and-recovery"></span>
### Connection interruption and recovery

CDN does not store historical SSE events and does not replay missed events after a client reconnects. Resuming or replaying events after a disconnection depends on the client\-side reconnection mechanism and the origin's ability to return subsequent events based on `Last-Event-ID`.

If the origin does not send data for an extended period, the connection may be interrupted because of the origin request timeout. The default origin request timeout for BytePlus CDN is 60 seconds, and the configurable range is 5 to 60 seconds. We recommend that the origin send heartbeat messages at an interval shorter than the timeout and that the client support reconnection.

<span id="71503458"></span>
## Steps


1. Open the **Server\-Sent Events** configuration page. For instructions, see [Domain Name Configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

2. Set **Status** to Enabled.

3. When you are finished, click **Save**.

4. After the configuration takes effect, use a client program or command\-line tool to access the SSE test URL. Verify that the request includes the `Accept: text/event-stream` header, the origin response includes the `Content-Type: text/event-stream` header, and the client can continuously receive the event stream. Example command:


```shell
curl -N -H "Accept: text/event-stream" "https://example.com/sse"
```


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260806080535-1212605370597.png) </span>

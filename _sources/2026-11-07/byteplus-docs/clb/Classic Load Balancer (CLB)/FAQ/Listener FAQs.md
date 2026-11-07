---
title: "Listener FAQs"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Listener-faq"
---

<span id=".VURQ5Y2P6K6u5LiOVENQ5Y2P6K6u5pyJ5LuA5LmI5Yy65Yir77yf"></span>
## Concept introduction

<span id=".VURQ5Y2P6K6u5LiOVENQ5Y2P6K6u5pyJ5LuA5LmI5Yy65Yir77yf"></span>
### What is the difference between UDP and TCP?

TCP is connection\-oriented, requiring a reliable connection to be established with the peer before data transmission. It is mainly suitable for scenarios that emphasize reliability and high data accuracy, with relatively lower speed requirements, such as file transfer, email sending/receiving, and remote login.

UDP is connectionless; data is sent directly without a three\-way handshake. It is mainly suitable for scenarios that emphasize real‑time performance and have relatively lower reliability requirements, such as video chat and real‑time financial market data push.

<span id=".55uR5ZCs5Zmo55qE6buY6K6k6LaF5pe25pe26Ze05piv5aSa5bCR77yf"></span>
### What is the default timeout of a listener?


* The default timeout for a TCP listener is 900 seconds, with an allowable range of 10\-900 seconds.

* The default timeout for a UDP listener is 90 seconds, with an allowable range of 1\-300 seconds.

* For HTTP and HTTPS listeners, the timeout can be customized. For details, see [Creating an HTTP listener](https://docs.byteplus.com/en/docs/clb/Creating-an-HTTP-listener) and [Creating an HTTPS listener](https://docs.byteplus.com/en/docs/clb/Creating-an-HTTPS-listener).


<span id=".6LSf6L295Z2H6KGh5rWB6YeP57uf6K6h5ZKM5YWs572RSVDmtYHph4_nu5_orqHmnInku4DkuYjkuI3lkIzvvJ8="></span>
### What is the difference between CLB traffic statistics and EIP traffic statistics?

Elastic IP traffic is measured at the public network ingress/egress and includes all traffic that reaches the EIP after rate limiting. CLB traffic statistics are the sum of traffic for all listeners (all listening ports) under the CLB instance. In addition to public traffic, it also includes traffic that accesses the CLB from within the BytePlus data center. Besides traffic statistics, CLB also provides statistics on metrics such as new connection count and active connection count.

<span id=".5pON5L2c5L2_55So"></span>
## Actions

<span id=".Q0xC55uR5ZCs56uv5Y-j5LiO5ZCO56uv5pyN5Yqh5Zmo56uv5Y-j5piv5ZCm5Y-v5Lul5LiN5LiA6Ie077yf"></span>
### Can the CLB listening port and the backend server port be different?

Yes. The CLB listening port and the backend server port have no necessary relationship. The CLB listening port is used by external clients to access the CLB instance, while the backend server port is used by the server to provide services. You can customize both as needed.

<span id=".Q0xC5a-55LiK5Lyg5paH5Lu255qE6YCf5bqm5ZKM5aSn5bCP5piv5ZCm5pyJ6ZmQ5Yi277yf"></span>
### Does CLB have any limits on the speed or size of uploaded files?


* Layer‑4 listeners themselves do not limit the speed of client file uploads, but the upload speed is limited by the VPC bandwidth defined for the CLB instance.

* Layer‑7 listeners limit the client upload file size to 1 GB and also limit the upload speed according to the VPC bandwidth upper limit of the CLB instance.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For both layer‑4 and layer‑7 listeners, if the CLB instance is associated with an EIP (e.g., a public CLB instance or a private CLB instance bound to an EIP), the upload speed is also affected by the internet bandwidth cap.</div>


<span id=".55uR5ZCs5Zmo5Yig6Zmk5LmL5ZCO77yMQ0xC5piv5ZCm5Lya56uL5Y2z5YGc5q2i6L2s5Y-R5Lia5Yqh5rWB6YeP77yf"></span>
### After a listener is deleted, does the CLB immediately stop forwarding traffic?


* If the connection between the client and the CLB is a short connection, deleting a layer‑4 listener causes the CLB to immediately stop forwarding traffic.

* If a persistent connection is maintained between the client and the CLB, when a layer‑7 listener is deleted, new connections are no longer established, but existing TCP persistent connections are not affected by the listener deletion. The CLB will disconnect these persistent connections and stop forwarding traffic only after the system‑default listener timeout is reached.


<span id=".5bCG5Zub5bGC55uR5ZCs5Zmo5YWz6IGU55qE5ZCO56uv5pyN5Yqh5Zmo5p2D6YeN5L-u5pS55Li6MO-8jOWOn-i_nuaOpeS8muiHquWKqOWFs-mXreWQl--8nw=="></span>
### If the weight of a backend server associated with a layer‑4 listener is changed to 0, are the original connections automatically closed?

For a layer‑4 TCP listener, if the connection between the client and the backend server is a persistent connection, changing the backend server weight to 0 does not immediately close the original connection. You need to manually close it or wait for the keep‑alive timeout to expire, after which it will close automatically.

<span id=".SFRUUFPljY_orq7nmoTnm5HlkKzlmajorr_pl67lkI7nq6_mnI3liqHlmajnmoTor7fmsYLpgJrov4fku4DkuYjljY_orq7kvKDovpPvvJ8="></span>
### Through which protocol does an HTTPS listener forward requests to the backend server?

An HTTPS listener encrypts only the requests between the client and the CLB. The requests from the CLB to the backend server are still transmitted over HTTP.

<span id=".5LiD5bGC55uR5ZCs5Zmo6K6_6Zeu5ZCO56uv5pyN5Yqh5Zmo55qE5Y2P6K6u54mI5pys5piv5LuA5LmI77yf"></span>
### What protocol version does a layer‑7 listener use to access the backend server?

The default protocol version used by a layer‑7 listener to access the backend server is HTTP 1.1, independent of the client and server protocol versions.

After HTTP/2.0 is enabled on an HTTPS listener, the protocol version used between the client and the CLB is HTTP 2.0, but the protocol version between the CLB and the backend server remains HTTP 1.1.

<span id=".6LSf6L295Z2H6KGhQ0xC5piv5ZCm5pSv5oyBSFRUUCAyLjDljY_orq7vvJ8="></span>
### Does CLB support the HTTP/2.0 protocol?

The CLB layer‑7 HTTPS listener supports HTTP/2.0. For detailed configuration, see [Creating an HTTPS listener](https://docs.byteplus.com/en/docs/clb/Creating-an-HTTPS-listener).

<span id=".5Y2V5LiqVURQ5oql5paH6LaF6L-HTVRV5pe2Q0xC5piv5ZCm5pSv5oyB77yf"></span>
### Does CLB support a single UDP packet larger than the MTU?

Unsupported. CLB does not support UDP fragmentation. A single UDP packet larger than the MTU will be discarded.

<span id=".55uR5ZCs5Zmo5piv5ZCm5pSv5oyBR3ppcOaVsOaNruWOi-e8qe-8nw=="></span>
### Does a listener support Gzip data compression?

Layer‑7 listeners support Gzip compression. HTTP/HTTPS listeners enable Gzip data compression by default. When a client request carries the `accept-encoding: gzip` header, if the backend server returns a file of a specific type (including text/plain, text/css, text/xml, application/xml, text/javascript, application/x‑javascript, application/json, application/javascript, application/x‑protobuf) to the client, the CLB compresses it before returning it to the client.

<span id=".6LCD5bqm566X5rOV55u45YWz"></span>
## Scheduling algorithm related

<span id=".55uR5ZCs5Zmo5pSv5oyB55qE6LCD5bqm566X5rOV77yf"></span>
### What scheduling algorithms are supported by listeners?

Weighted Round Robin (WRR), Weighted Least Connections (WLC), and Source IP Hash (SH).


* Weighted Round Robin (WRR): Higher weights values receive more frequent polling attempts (higher probability).

* Weighted Least Connections (WLC): Distributes requests to the backend server with the smallest "current connection/weight" ratio.

* Source Address Hash (SH): A consistency hash based on the Source IP address, allowing the same source to be scheduled to the same backend server.


<span id=".5Li65LuA5LmI55So5rWP6KeI5Zmo5ZCR5Zub5bGC55uR5ZCs5Zmo5Y-R6LW35aSa5qyh6K-35rGC5pe277yM6K-35rGC5oC75piv5Lya6LCD5bqm5Yiw5ZCM5LiA5Y-w5ZCO56uv5pyN5Yqh5Zmo5LiK77yf"></span>
### Why do requests always get dispatched to the same backend server when multiple requests are made to a layer‑4 listener from a browser?


* If you are using the Source Hash (SH) algorithm, requests from the same source address will be dispatched to the same backend server.

* If you are using Weighted Round Robin (WRR) or Weighted Least Connections (WLC), note whether the browser uses HTTP/1.1. HTTP/1.1 enables keep\-alive by default, which causes multiple requests from the same client in a short period to reuse the same TCP connection. The connection from the client to the layer‑4 listener will be maintained.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you wish to disable HTTP/1.1 keep\-alive, specify <code>Connection: Close</code> in the request header.   </div>
   

<span id=".5L-u5pS555uR5ZCs5Zmo55qE6LCD5bqm566X5rOV5Lya5a-86Ie05Lia5Yqh5Lit5pat5ZCX77yf"></span>
### Does modifying the listener scheduling algorithm cause service interruption?

No. Modifying the scheduling algorithm only affects subsequent request forwarding and does not impact existing connections, so it does not cause service interruption.

<span id=".6L2s5Y-R6KeE5YiZ55u45YWz"></span>
## Forwarding rule related

<span id=".5aaC5L2V5Li65LiD5bGC55uR5ZCs5Zmo6YWN572u5Z-f5ZCN5oiWVVJM77yf"></span>
### How to configure a domain name or URL for a layer‑7 listener?

You can configure a domain name or URL by setting forwarding rules for the layer‑7 listener. For detailed steps, see [Adding a forwarding rule](https://docs.byteplus.com/en/docs/clb/Adding-a-forwarding-rule).

<span id=".5Li65LuA5LmI5Zyo5o6n5Yi25Y-w55WM6Z2i5om-5LiN5Yiw6YWN572u6L2s5Y-R6KeE5YiZ55qE5YWl5Y-j77yf"></span>
### Why can't I find the entry for configuring forwarding rules in the console?

Only listeners using HTTP or HTTPS protocols support forwarding rules. Please check whether your listener protocol is TCP or UDP.

<span id=".6L2s5Y-R6KeE5YiZ5pSv5oyB5aSn5bCP5YaZ5qih57OK5Yy56YWN5ZCX77yf"></span>
### Do forwarding rules support case‑insensitive matching?

Yes, supported. Forwarding rules are case‑insensitive when matching domain names, but case‑sensitive when matching URLs. Therefore, when configuring forwarding rules for a layer‑7 listener, ensure they are correctly set according to the actual case of the URL.

&nbsp;

<span id=".V1MvV1NT5Y2P6K6u55u45YWz"></span>
## WS/WSS protocol related

<span id=".5LuA5LmI5pivV1MvV1NT77yf"></span>
### What is WS/WSS?

WebSocket (WS) is a communication protocol in HTML5 that enables simpler and faster bidirectional data transfer between a client and a server. WS is built on top of TCP and establishes a persistent connection after a single TCP handshake. Once the connection is established, both the client and the server can actively send or receive data.

WebSocket Secure (WSS) is the encrypted version of WS.

<span id=".5Li65LuA5LmI6KaB5L2_55SoV1MvV1NT77yf"></span>
### Why use WS/WSS?

Before WS/WSS, clients had to pull data from the server via polling. This data exchange method was inefficient, and the server could not actively push data to the client.

The new WebSocket protocol introduced with HTML5 solved these issues and enabled bidirectional data transfer between client and server.

Compared to HTTP, WS also offers the following advantages:


* Lower control overhead.

* Better real\-time performance.

* Longer‑lasting connection state.


<span id=".5ZOq5Lqb5Zyw5Z-f5pSv5oyBV1MvV1NT77yf"></span>
### Which regions support WS/WSS?

All regions currently supported by CLB support WS/WSS.

<span id=".5aaC5L2V5ZCv55SoV1MvV1NT77yf"></span>
### How to enable WS/WSS?

The CLB layer‑7 listener supports them by default, with no additional configuration required.

HTTP listeners support WS by default.

HTTPS listeners support WSS by default.

<span id=".V1MvV1NT5Y2P6K6u5piv5ZCm5pS26LS577yf"></span>
### Are WS/WSS protocols charged?

WS and WSS are free by default, and you do not need to pay any fees.

<span id=".5Lya6K-d5L-d5oyB55u45YWz"></span>
## Session persistence related

<span id=".6LSf6L295Z2H6KGh5pSv5oyB5ZOq5Lqb57G75Z6L55qE5Lya6K-d5L-d5oyB77yf"></span>
### What types of session persistence does CLB support?

CLB supports two types: source IP‑based and cookie‑based.


* Layer‑4 listeners (TCP and UDP) support source IP‑based session persistence.

* Layer‑7 listeners (HTTP and HTTPS) support cookie‑based session persistence when the scheduling algorithm is Weighted Round Robin (WRR). Two cookie handling methods are available: Implant Cookie and Rewrite Cookie.


<span id=".5Lya6K-d5L-d5oyB6LaF5pe25pe26Ze05piv5ZCm5pSv5oyB5L-u5pS577yf"></span>
### Can the session persistence timeout be modified?

Yes, supported.


* For layer‑4 listeners (TCP/UDP) and for layer‑7 listeners using the Implant Cookie method, the timeout can be directly modified on the listener configuration page.

* For layer‑7 listeners using the Rewrite Cookie method, the timeout defaults to the value configured on the backend server cookie and must be modified in the backend server cookie configuration.


<span id=".55uR5ZCs5Zmo55qE6LCD5bqm566X5rOV5LiO5Lya6K-d5L-d5oyB5pyJ5LuA5LmI5YWz57O777yf"></span>
### What is the relationship between listener scheduling algorithms and session persistence?


* Scheduling algorithm is a basic, mandatory function of a listener – it is the policy for forwarding requests and applies to all requests reaching the CLB.

* Session persistence is an optional advanced feature that forwards requests from the same user to the same backend server.


Layer‑7 listeners (HTTP/HTTPS) support session persistence only when the scheduling algorithm is WRR. Layer‑4 listeners (TCP/UDP) support session persistence for all scheduling algorithm types.

<span id=".5Lya6K-d5L-d5oyB5LiO6ZW_6L-e5o6l5pyJ5LuA5LmI5LiN5ZCM77yf"></span>
### What is the difference between session persistence and persistent connections?

Session persistence and persistent connections are two different concepts with no necessary relationship.


* Session persistence means the CLB forwards requests from the same session to the same backend server for processing.

* It is a persistent connection established between a client and a server, allowing continuous data transfer after the connection is established.


<span id=".5aaC5L2V5p-l55yL5Lya6K-d5L-d5oyB5a2X56ym5Liy77yf"></span>
### How to view the session persistence string?


* Using a browser, press `F12` and look at the `Set-Cookie` field in the response header.

* Using the command line, run `curl -v` and look at the `Set-Cookie` field in the response header.


<span id=".5LiD5bGC55uR5ZCs5Zmo5aaC5L2V6YWN572u6YeN5YaZQ29va2ll55qE5Lya6K-d5L-d5oyB77yf"></span>
### How to configure rewrite‑cookie session persistence for a layer‑7 listener?

Configuring rewrite‑cookie session persistence for a layer‑7 listener requires two steps: 1) Configure the cookie on the backend server; 2) Enable session persistence on the listener. For detailed configuration steps, see [Configuring Cookie‑based session persistence for a Layer‑7 listener](https://docs.byteplus.com/en/docs/clb/Configuring-cookie-based-sticky-session-for-a-Layer-7-listener).

---
title: "Basic concepts"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/docs-basic-concepts"
---

<span id="421f5934"></span>
## Web application

Web applications refer to applications that users can access through a web browser. Web applications usually run on web servers and provide services over the Internet or a local network, offering various functionalities such as e\-commerce, social networking, online gaming, etc.

<span id="b06ae258"></span>
## Origin server

The origin server refers to the actual server that provides services to end users. As an intermediate layer between the origin server and the user, WAF can detect and filter requests from users and forward valid requests to the origin server for processing. Therefore, all traffic is forwarded through WAF to the origin server and then returned as a response to the user.

<span id="bb60941e"></span>
## BytePlus CDN

BytePlus CDN (Content Delivery Network) comprises a geographically distributed network of edge servers linked to the origin server. It stores cached content on edge servers in point\-of\-presence (POP) locations that are close to end users and delivers web and mobile content to them. Since edge servers are geographically closer to the user, this will also minimize latency as well as improve website performance and, ultimately, the user’s experience.

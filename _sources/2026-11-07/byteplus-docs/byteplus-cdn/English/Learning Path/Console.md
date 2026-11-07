---
title: "Console"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/learning_path_console_en"
---

## First\-time use of BytePlus CDN (Must\-read)

If you are using the CDN for the first time, you need to create and publish a delivery policy first, and then add your domain name.

We have prepared a CDN Quick Start guide to instruct you on how to connect your domain name with the CDN. You can click the links in the steps to view the relevant operations in the Quick Start guide.

**Steps**

1.

   [Create a delivery policy](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-set-up-distribution-policy-and-origin).

2.

   [Publish the delivery policy](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-set-up-distribution-policy-and-origin).

3.

   [Add your domain name and bind the policy to it](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-add-your-domain-name).

4.

   [Test the CDN-assigned CNAME](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-test-domain-name-with-hosts).

5.

   [Create a CNAME record to route requests to the CDN](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-set-up-cname).

> **说明**

*

   > When creating a delivery policy, you need to specify your site as the origin.

*

   > The domain name you add to the CDN cannot be the same as the origin you specified. This is because, in step 5, you need to resolve the domain name you added to the CDN to the CNAME assigned by the CDN. If the origin is also that domain name, the requests sent by the CDN to the origin will be received by the CDN itself, causing a request loop. Therefore, if your origin is indeed the domain name you want to add to the CDN, you can specify the IP address of your domain name as the origin.

*

   > Step 5 is performed at your domain name resolution service provider.

## Enable HTTPS Encryption Service (Recommended)

After you enable HTTPS Encryption Service for your domain name, users can access your domain name using the HTTPS protocol to encrypt communication between users and the CDN.

To enable HTTPS Encryption Service, you need to upload a certificate issued for your domain name to the CDN. The certificate you upload to the CDN is hosted in the BytePlus Certificate Center. Since CDN and BytePlus Certificate Center are different BytePlus services, you need to authorize CDN to access the Certificate Center before uploading the certificate.

**Steps**

1.

   [Authorize CDN access to BytePlus Certificate Center](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-authorize-byteplus-cdn-to-access-byteplus-certificate-center).

2.

   [Upload a certificate for your domain name](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-upload-certificates-certfiicate-center).

3.

   [Enable HTTPS Encryption Service for your domain name](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-add-domain-name_1).

4.

   [Associate your domain name with the certificate](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-associate-domain-name-with-certificate).

> **说明**

> Only after enabling HTTPS can the domain name be bound to an encryption policy, allowing you to configure [HTTPS\-related CDN features](https://docs.byteplus.com/en/docs/18/29939#https-related-cdn-features) for the domain name.

## Modify CDN feature configurations (Optional)

Policies contain the configurations for various CDN features. By binding a policy to your domain name, the CDN features you configured will take effect on the domain name, becoming the domain name's configuration.

In the CDN, there are the following types of policies:

*

   Delivery policy: Used to configure [regular CDN features](https://docs.byteplus.com/en/docs/18/29939#regular-cdn-features).

*

   Encryption policy: Used to configure [HTTPS-related CDN features](https://docs.byteplus.com/en/docs/18/29939#https-related-cdn-features).

> **说明**

*

   > Only published policies can be bound to a domain name.

*

   > If a policy is published, you cannot modify the policy's configuration.

*

   > To bind with an encryption policy, the domain name must have HTTPS Encryption Service enabled.

**Steps**

Since policies cannot be changed after being published, you can create a policy by duplicating a bound policy. In the new policy, you can change the configuration of CDN features. After publishing the new policy, you bind the new policy to your domain name.

1.

   [Duplicate the policy bound to your domain name](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-policy#duplicate-policies).

   > **说明**

   *

   > To modify regular CDN features, you need to duplicate the bound delivery policy.

   *

   > To modify HTTPS\-related CDN features, you need to duplicate the bound encryption policy.

   *

   > If you want to set HTTPS\-related CDN features for the domain name but the domain name is not yet bound to an encryption policy, step 1 is to create an encryption policy instead of duplicating a policy.

2.

   Add or remove the CDN features to be configured in the new policy. Refer to the [Feature List](https://docs.byteplus.com/en/docs/byteplus-cdn/learning_path_console_en#complete-cdn-feature-list).

3.

   Configure CDN features in the new policy. Click the links in the [Feature List](https://docs.byteplus.com/en/docs/byteplus-cdn/learning_path_console_en#complete-cdn-feature-list) to learn how to configure the features.

4.

   [Publish the policy](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-policy#step-3-publish-policy).

5.

   [Bind the new policy with your domain name](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-policy#step-4-bind-domain-names).

## Use Edge Functions (Optional)

With Edge Functions, you can create and publish functions to handle requests that meet specific conditions. The language supported by Edge Functions is JavaScript.

When receiving user requests:

*

   If the request meets the conditions you specified, the CDN will pass the request to the function for processing. This processing can include responding with specific content or forwarding the request to other services.

*

   If the request does not meet the conditions you specified, the CDN will handle the request.

**Steps**

1.

   [Authorize CDN access to Edge Functions](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-authorize-byteplus-cdn-to-access-byteplus-certificate-center).

2.

   [Enable Edge Functions for your domain name](https://docs.byteplus.com/zh-CN/docs/byteplus-cdn/docs-Configure-Edge-Function-Forwarding-Rules).

3.

   [Create a function](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-create-function).

4.

   [Publish the function](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-create-function).

5.

   [Associate your domain name with the function](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-domain-triggers).

6.

   [Create a forwarding rule for the function](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Configure-Edge-Function-Forwarding-Rules).

Edge Functions also provides Edge KV. You can create key\-value pairs in Edge KV in advance, and then use runtime APIs in your function code to read values using the keys. When the value of a key\-value pair is updated, the value read in the function code is also the updated value. You don't need to republish the function.

The steps to create a key\-value pair are as follows:

1.

   [Create a namespace](https://docs.byteplus.com/en/docs/byteplus-cdn/doc-manage-namespace).

2.

   [Create a key-value pair in the namespace](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-manage-data).

## Use Tools (Optional)

CDN provides the following tools:

*

   Purge and prefetch

   *

      [Cache purge](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-purge): CDN deletes or marks the specified files as expired to ensure users get the latest version of the files from the origin.

   *

      [Origin prefetch](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-prefetch): CDN pre\-caches the specified files to edge nodes so that the first access to these files can also benefit from data transfer acceleration.

*

   Diagnostic Tools:

   *

      [IP detection](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-diagnostic-tools#ip-detection): Check whether one or more IP addresses are IP addresses of CDN edge nodes.

   *

      [Domain name comparison](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-diagnostic-tools#domain-name-comparison): Compare the configuration differences between two domain names. The compared configurations cover:

      *

         The configuration of CDN features in the policies bound to the domain names.

      *

         Basic domain attributes, such as creation time, CNAME, and HTTPS Encryption Service status.

   *

      [Policy comparison](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-diagnostic-tools#policy-comparison): Compare the configuration differences of CDN features in two policies.

## View Metrics (Recommended)

CDN provides the following pages to display metric data, allowing you to monitor the usage of CDN.

*

   [Edge report](https://docs.byteplus.com/en/docs/byteplus-cdn/bWlzDn): Based on user requests, this page displays the aggregate data and data trends of the following metrics:

   * Bandwidth, traffic, number of requests, QPS, status codes, response time, average speed

*

   [Origin report](https://docs.byteplus.com/en/docs/byteplus-cdn/xdlhZY): Based on origin requests, this page displays the aggregate data and data trends of the following metrics:

   * Bandwidth, traffic, number of requests, QPS, status codes, response time

*

   [Traffic hit ratio](https://docs.byteplus.com/en/docs/byteplus-cdn/17GTty): Based on user requests, this page displays the metric data of the traffic hit ratio.

*

   [Popular objects](https://docs.byteplus.com/en/docs/byteplus-cdn/og-CdZ): Based on user requests, this page displays the following popular objects and their metric data:

   * Popular request URLs, popular Referer domain names, popular access devices, popular operating systems, popular browsers, client IP addresses that frequently access your domain name, popular regions

*

   [Insights](https://docs.byteplus.com/en/docs/byteplus-cdn/6a4Gqa):

   *

      Based on user requests, this page displays several insights: aggregate data for various metrics by country and region, trends in unique visitor IP addresses, and domain name rankings based on aggregate metrics.

   *

      Based on origin requests, this page displays the ranking of domain names based on the aggregate data of various metrics.

## Complete CDN Feature List

When processing user requests, if the requested file is not cached or has expired in the cache, the CDN will go through the following stages:

* Receive user request \> Request file from origin \> Receive origin response \> Cache requested file \> Respond to user request

![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_5b2668936c71c67a704f4b01fa8a5b18.png)

> **说明**

> If the requested file has not expired in the cache, the stages the CDN goes through are:

* > Receive user request \> Respond to user request

Each CDN feature corresponds to a request processing stage. The configuration of the feature affects how CDN handles user requests at a specific stage.

### Regular CDN Features

The following features are configured in delivery policies.

|**Stage** |**Category** |**CDN Feature** |**Feature Description** |
|---|---|---|---|
|Receive user request |Protocols and Methods |[IPv6](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-ipv6) |Configure whether to allow clients using IPv6 addresses to access CDN. |
|||[Disabled HTTP Methods](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-disallowed-http-method) |Configure the request methods not supported by CDN. |
|||[WebSocket](https://docs.byteplus.com/en/docs/byteplus-cdn/websocket_en) |Enable support for WebSocket in CDN. |
|||[Server-Sent Events (SSE)](https://docs.byteplus.com/en/docs/byteplus-cdn/sse_en-us) |Configure CDN to handle Server\-Sent Events (SSE) requests that meet the identification conditions as persistent connection requests and pass through the data stream from the origin. |
|||[PROXY Protocol](https://docs.byteplus.com/en/docs/byteplus-cdn/proxy-protocol_en-us) |Enable support for PROXY Protocol in CDN. |
||Access Restrictions |[Geographic Restrictions](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-geographical-restrictions) |Configure to allow or deny user requests from specific countries and regions. |
|||[IP Restrictions](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-ip-restrictions) |Configure to allow or deny client IP addresses from accessing CDN. |
|||[UA Restrictions](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-ua-restrictions) |Based on the User\-Agent header value in the request, configure to allow or deny requests to access CDN. |
|||[Referer Restrictions](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-referer-restrictions) |Based on the Referer header value in the request, configure to allow or deny requests to access CDN. |
|||[Origin Restrictions](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-origin-restrictions) |Based on the Origin header value in the request, configure to allow or deny requests to access CDN. |
|||[Remote Authentication](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-remote-authentication_1) |If you have set up a dedicated authentication server, you can use this configuration to forward requests to your authentication server for authentication. |
|||[Signed URL Authentication](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-overview) |Configure CDN to use a pre\-agreed authentication algorithm to authenticate user requests by verifying the signature in the user request. |
|||[Custom Restrictions](https://docs.byteplus.com/en/docs/byteplus-cdn/custom-restrictions_en) |Configure matching conditions based on request paths, query parameters, and client IP addresses, and specify how CDN handles matching requests. |
||Rate Limiting |[Data Rate Limiting](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-data-rate-throttling) |Configure the maximum data transfer rate for user requests based on specified conditions. |
|||[Request Rate Limiting](https://docs.byteplus.com/en/docs/byteplus-cdn/rate-limiting_en-us) |Configure the QPS threshold for client IP addresses. When the threshold is exceeded, CDN rejects new requests and returns a 403 status code. |
||CDN Responses |[URL Normalization](https://docs.byteplus.com/en/docs/byteplus-cdn/url-normalization_en-us) |Configure CDN to normalize non\-standard content in request URLs to reduce the risk of request failures caused by non\-standard URLs. |
|Request file from origin |Origins |[Standard Origins](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-origin-configurations) (Must\-read) |Configure the origins. |
|||[Conditional Origins](https://docs.byteplus.com/en/docs/byteplus-cdn/conditional_origins_en) |Specify the origin server that the CDN needs to access during origin fetch when the user request meets the specified conditions. |
||Origin Fetch |[Origin Fetch Timeouts](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-request-time-out) |Configure the TCP connection and HTTP connection timeout for origin requests. |
|||[Origin Request Headers](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-origin-request-headers) |Configure the headers included in the origin request. |
|||[Range Origin Fetch](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-range-get) |Configure CDN to use Range requests when fetching content from the origin. |
|||[Redirect Follow](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-redirect-follow) |Configure the CDN to access the redirect address to obtain the target file when the origin server returns a 301/302, instead of returning the 301/302 response to the client. |
|||[Origin Retry](https://docs.byteplus.com/en/docs/byteplus-cdn/origin_retry-en) |Configure the origin response status codes that trigger CDN origin retries. |
|||[Origin Request Parameters](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-query-parameters_1) |Configure the query parameters included in the origin request URL. |
|||[Origin SNI](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-origin-sni_1) |Configure the SNI header in origin requests. |
||Performance Optimization |[Smart Routing](https://docs.byteplus.com/en/docs/byteplus-cdn/smart-routing_en-us) |Configure CDN to dynamically select the path with better network quality from available origin fetch paths to improve origin fetch latency and stability. |
|||[Origin Keep-Alive](https://docs.byteplus.com/en/docs/byteplus-cdn/origin-preconnection_en-us) |Configure CDN nodes to maintain and reuse persistent TCP connections with the origin to reduce origin connection establishment time and TLS handshake time for HTTPS origin fetches. |
|Receive origin response |Origin Fetch |[Origin Response Headers](https://docs.byteplus.com/en/docs/byteplus-cdn/origin-response-headers_en-us) |Configure CDN to update response headers after receiving an origin response before performing the corresponding operations based on the updated response headers. |
|Cache requested file |Cache Rule |[Caching Rules](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-caching-rules) |Configure how CDN caches the requested files. |
|||[Cache Key](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-cache-keys) |Configure how CDN matches the requested files in the cache. |
|||[Negative Caching](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-negative-caching) |Configures the CDN to cache error status codes for a specified duration. During this time, subsequent requests for the same file receive the cached error code directly, without contacting the origin. |
|||[URL Redirect](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-url-redirect) |Configure CDN to return a 301 or 302 status code when a user request matches a rule, directing the client to request a new URL. |
|||[Browser Caching](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-browser-caching) |Configure CDN to instruct client browsers on how to cache the requested files. |
|||[Serve Stale](https://docs.byteplus.com/en/docs/byteplus-cdn/always-online_en-us) |Configure CDN to use cached files to respond to user requests when the origin fails or an unknown error occurs during origin fetch. |
|Respond to user request |Content Optimization |[File Compression](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-file-compression) |Configure how CDN compresses files when returning requested files. |
|||[Video Seeking](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-video-seeking) |Enables users to seek to different time points in a video by dragging the player's progress bar. |
|||[File Minification](https://docs.byteplus.com/en/docs/byteplus-cdn/qJ-Dp4) |Configure CDN to remove comments and redundant whitespace characters in HTML, JavaScript, and CSS files before returning them to reduce file size and improve distribution efficiency. |
||CDN Responses |[Client Response Headers](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-cdn-response-headers) |Configure the headers included in the CDN response to user requests. |
|||[Custom Error Pages](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-custom-error-pages_1) |For CDN response status codes indicating errors, configure CDN to return a user\-friendly error page. |
||AI Traffic Management |[Convert HTML to Markdown](https://docs.byteplus.com/en/docs/byteplus-cdn/html-to-md_en-us) |Configure CDN to convert responses to requests that contain the `Accept: text/markdown` header and access HTML resources into Markdown format. |

### HTTPS\-related CDN Features

The following features are configured in encryption policies.

|**Stage** |**Category** |**CDN Feature** |**Feature Description** |
|---|---|---|---|
|Receive user request |Protocols |[HTTP/3 (QUIC)](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-quic_1) |Configure the CDN to support the QUIC protocol. After you enable QUIC, the CDN also supports HTTP/3. |
|||[HTTP/2](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-http-2) |Configure the CDN to support HTTP/2. |
|||[Protocol Redirect](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-protocol-redirect_1) |Configure CDN to redirect user HTTP requests to HTTPS requests or redirect HTTPS requests to HTTP requests. |
||SSL/TLS |[OCSP Stapling](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-ocsp-stapling-1) |Configure the CDN to send the OCSP response of the server certificate to the client during the TLS handshake phase, thereby reducing the TLS handshake time. |
|||[HSTS](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-hsts_1) |Configure the CDN to include the `Strict-Transport-Security` header in the response to instruct client browsers to always send HTTPS requests to the CDN. |
|||[TLS Versions](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-allowed-tls-versions) |Configure the TLS versions supported by the CDN. If a request uses an unsupported TLS version, the CDN will reject the request. |
|||[Mutual TLS](https://docs.byteplus.com/en/docs/byteplus-cdn/mtls_en-us) |Configure CDN to validate client certificates during the TLS handshake to authenticate clients. |

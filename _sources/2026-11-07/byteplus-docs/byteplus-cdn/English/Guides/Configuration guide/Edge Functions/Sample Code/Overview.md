---
title: "Overview"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/functions-overview-en"
---

Edge Functions provide sample code for the following scenarios.

<span id="generate-content"></span>
## Generate content


|Scenario |Description |
|---|---|
|[Return an HTML Page](https://docs.byteplus.com/docs/byteplus-cdn/docs-Return-an-HTML-page) |Generate an HTML page containing static and dynamic content, and return it as a response to the client. |
|[Return JSON](https://docs.byteplus.com/docs/byteplus-cdn/docs-Return-JSON) |Generate data in JSON format and return it as a response to the client. |


<span id="retrieve-and-process-data"></span>
## Retrieve and process data


|Scenario |Description |
|---|---|
|[Retrieve and Process JSON](https://docs.byteplus.com/docs/byteplus-cdn/docs-JSON-processing) |Retrieve and process JSON data. |


<span id="authenticate"></span>
## Authenticate


|Scenario |Description |
|---|---|
|[Verify HMAC-SHA256 Signature of a Token](https://docs.byteplus.com/docs/byteplus-cdn/Verify_HMAC-SHA256_Signature_of_a_Token) |Verify the HMAC\-SHA256 signature of the Token embedded in the URL of the user request. |
|[JWT Authentication](https://docs.byteplus.com/docs/byteplus-cdn/functions_JWT_Authentication) |Verify JWT. |


<span id="modify-request-headers-or-response-headers"></span>
## Modify request headers or response headers


|Scenario |Description |
|---|---|
|[Modify HTTP Request Headers or Response Headers](https://docs.byteplus.com/docs/byteplus-cdn/docs-Reverse-proxy) |Modify HTTP request headers in user requests and response headers in responses returned to users. |
|[Add Custom Request Headers Based on User-Agent](https://docs.byteplus.com/docs/byteplus-cdn/doc-Adding-Request-Headers-Based-on-User-Agent) |Determine the client device type based on the User\-Agent request header in the user request, and add custom request headers and custom query parameters to identify the client device type. BytePlus CDN can differentiate caches based on different query parameters, thus enabling caching based on client device type. |


<span id="redirect"></span>
## Redirect


|Title |Title |
|---|---|
|[Redirect URLs](https://docs.byteplus.com/docs/byteplus-cdn/docs-Redirect) |Redirect user requests to a specified URL. |
|[Redirect HTTP to HTTPS](https://docs.byteplus.com/docs/byteplus-cdn/Redirect_HTTP_Requests_to_HTTPS_Requests) |Redirect the HTTP protocol used in user requests to HTTPS protocol. |


<span id="geolocation-information"></span>
## Geolocation information


|Scenario |Description |
|---|---|
|[Retrieve Weather Data Based on User Geolocation](https://docs.byteplus.com/docs/byteplus-cdn/Weather_forcasting_based_on_geolocation) |Retrieve weather data based on the user's geolocation information. |


<span id="stream-requests-and-responses"></span>
## Stream requests and responses


|Scenario |Description |
|---|---|
|[Stream a Rewritten HTML Page as Response](https://docs.byteplus.com/docs/byteplus-cdn/docs-Modify-the-footer-header) |Write the retrieved HTML page into a writable stream, rewrite the HTML page in the writable stream, and return the rewritten HTML page as a response stream to the client. |
|[Stream Aggregated Requests and Responses](https://docs.byteplus.com/docs/byteplus-cdn/docs-Aggregate-requests) |Aggregate multiple different requests into one streaming request, and aggregate the responses of these requests into one streaming response to return to the user. |
|[Stream Multiple Files as a Single Response](https://docs.byteplus.com/docs/byteplus-cdn/Stream_Multiple_Files_as_a_Single_Response) |Request multiple files in a single request and return these files as a stream. |


<span id="custom-error-pages"></span>
## Custom error pages


|Scenario |Description |
|---|---|
|[Return a Custom Error Page](https://docs.byteplus.com/docs/byteplus-cdn/docs-HTML-rendering) |Generate a custom error page based on the HTTP status code returned by the origin server and return this page to the user. |


<span id="a-b-testing"></span>
## A/B testing


|Scenario |Description |
|---|---|
|[Cookie-based AB Testing](https://docs.byteplus.com/docs/byteplus-cdn/docs-AB-Testing) |Determine whether the user belongs to the test group or control group based on the Cookie request header in the user request, and conduct A/B testing. |


<span id="cors-proxy"></span>
## CORS proxy


|Scenario |Description |
|---|---|
|[CORS Proxy](https://docs.byteplus.com/docs/byteplus-cdn/docs-CORS) |Add CORS response headers to responses from third\-party APIs. |


<span id="manage-cdn-cache"></span>
## Manage CDN cache


|Scenario |Description |
|---|---|
|[Bypass CDN Cache Based on Cookie](https://docs.byteplus.com/docs/byteplus-cdn/Bypass_CDN_Cache_Based_on_Cookie) |Bypass CDN cache based on Cookie. |
|[Cookie-based caching](https://docs.byteplus.com/docs/byteplus-cdn/Cookie-based_Caching) |Add custom query parameters to user requests based on Cookie to implement cookie\-based caching. |
|[Add Custom Request Headers Based on User-Agent](https://docs.byteplus.com/docs/byteplus-cdn/doc-Adding-Request-Headers-Based-on-User-Agent) |Determine the client device type based on the User\-Agent request header in the user request, and add custom request headers and custom query parameters to identify the client device type. BytePlus CDN can differentiate caches based on different query parameters, thus enabling caching based on client device type. |


<span id="website-fallback"></span>
## Website fallback


|Scenario |Description |
|---|---|
|[Website Fallback By Caching Static Pages](https://docs.byteplus.com/docs/byteplus-cdn/Implement_Website_Fallback_By_Caching_Static_Pages) |Implement fallback by caching static pages of the website. If the origin server fails, the cached static pages can be returned to users as a fallback. |


<span id="accelerate-web-pages"></span>
## Accelerate web pages


|Scenario |Description |
|---|---|
|[Accelerate Website by Deferring JavaScript Loading](https://docs.byteplus.com/docs/byteplus-cdn/accelerate-by-defer-js) |Demonstrates how to accelerate a website by deferring JavaScript loading. |

---
title: "Log Configuration (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Log-configuration-java-sdk"
---

The TOS Java SDK provides a logging feature that allows you to view request\-related information by enabling logging.

<span id=".5pel5b-X6K-05piO"></span>
## Log Description

The TOS Java SDK uses the `slf4j` logging framework and prints logs at the following locations.


* When calculating the request signature, print the `canonical request` log at the `DEBUG` log level.

* When calculating the request signature, print the `string to sign` log with a log level of `DEBUG`.

* When a request is successful, log the HTTP status code, requestId, total request duration, and other relevant information. The log level is `INFO`.

* When a client request fails (excluding cases where the server returns TosServerException), print the failure information with the log level set to `INFO`.

* When a request succeeds or fails, print the request chain timing information, including DNS resolution, connection establishment, sending/receiving requests, etc. The log level is set to `DEBUG`.


<span id=".5byA5ZCv5pel5b-X5pa55byP"></span>
## Method for Enabling Logging

The TOS Java SDK utilizes the `slf4j` logging framework. Users may bind and customize log4j, log4j2, JUL, or other logging frameworks according to specific business requirements.

<span id=".5pel5b-X5YaF5a6556S65L6L"></span>
## Sample Log Content

An example of log content is provided below.

```java
18:11:35.627 [main] DEBUG com.volcengine.tos.auth.SignV4 - canonical request:
GET
/
list-type=2&prefix=example_dir%2F
date:20221209T101135Z
host:bucket-example.your endpoint
x-tos-date:20221209T101135Z

date;host;x-tos-date
e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
18:11:35.629 [main] DEBUG com.volcengine.tos.auth.SignV4 - string to sign:
 TOS4-HMAC-SHA256
20221209T101135Z
20221209/your region/tos/request
74ce8b173574bcb5dcd50cad3c35d1900121dd44e720ce62473756b69e44e1a3

18:22:55.046 [main] INFO  com.volcengine.tos.internal.RequestTransport - tos: status code:404, request id:1cc948930c7f7d0463930c7f-ac1811f3-1p3aWt-GO-cgb-tos, request cost 512 ms, request 1 times

18:22:55.048 [main] DEBUG com.volcengine.tos.internal.RequestTransport - requestId: 1cc948930c7f7d0463930c7f-ac1811f3-1p3aWt-GO-cgb-tos, method: GET, host: bucket.tos-cn-beijing.volces.com, request uri: /example_dir%2Fexample_object.txt, dns cost: 112 ms, connect cost: 323 ms, tls handshake cost: 275 ms, send headers and body cost: 1 ms, wait response cost: 3 ms, request cost: 508 ms
```

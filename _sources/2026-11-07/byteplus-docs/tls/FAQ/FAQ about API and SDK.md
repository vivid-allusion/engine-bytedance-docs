---
title: "FAQ about API and SDK"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/consultation_faq_api_and_sdk"
---

<span id="sdk-中的-searchlogs-和-searchlogsv2-接口有什么区别？"></span>
## What are the differences between SearchLogs and SearchLogsV2 in an SDK?

After the query features of Torch Log Service are upgraded in the back end, you must call SearchLogsV2 to use the upgraded query capabilities. Compared with SearchLogs, the X\-Tls\-Apiversion in the request header of SearchLogsV2 is fixed to 0.3.0. You can use the latest SQL functions and syntax after query features such as estimation functions are upgraded.

<span id="java-sdk-中的-putlogs-和-putlogsv2-接口有什么区别？"></span>
## What are the differences between PutLogs and PutLogsV2 in the Java SDK?

PutLogsV2 is easier to use in Torch Log Service SDK for Java. The two API actions have the same parameters. However, when you use PutLogsV2, you do not need to use the Protobuf format to upload logs, making it easier to use. We recommend that you use the latest version of the Java SDK to call PutLogsV2.

---
title: "Common parameters"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/common-parameters"
---

The common parameters in BytePlus API requests are as follows:

<span id="request-header-parameters"></span>
## Request header parameters


|Parameter Name |Type |Required |Meaning |
|---|---|---|---|
|Content\-Length |Integer |Optional |The request content defined in RFC2616, excluding the length of the message header. |
|Content\-Type |String |Optional |Specifies the structured format of the request message body. The Content\-Type of the log service is fixed as **application/json**. |
|Host |String |Optional |This is the service address, also known as the Endpoint. The service addresses of logs in different regions are different. See Service Address for details. |
|X\-Tls\-Apiversion |String |Optional |The version of the API being operated. The default is 0.3.0, and it can be set to 0.2.0 or 0.3.0. |
|X\-Date |String |Required |This is the date and time when you send the request. Specifying the date in the request helps prevent third parties from intercepting your request and resubmitting it later. The date uses UTC time and is formatted as **YYYYMMDD'T'HHMMSS'Z'**  , for example, 20201103T104027Z. |
|Authorization |String |Required |The standard HTTP authentication header field.<br><br>Format: `HMAC-SHA256 Credential={AccessKeyId}/{ShortDate}/{Region}/{Service}/request, SignedHeaders={SignedHeaders}, Signature={Signature}`. |


Parameters for generating `Authorization` are as follows:


|**Name** |**Data type** |**Description** |
|---|---|---|
|AccessKeyId |String |The access key of the BytePlus user account. Go to **BytePlus Console** \> **User Profile** \> **IAM** \> **Key Management** to obtain it. |
|ShortDate |String |The date of the API request. Format: `YYYYMMDD`. For example, `20180201`. |
|Region |String |The region of the API service. For example, `ap-singapore-1`. |
|Service |String |The name of the API service. For example, `TLS`. |
|SignedHeaders |String |The headers that are included in generating the signature. Separate them by semicolon. |
|Signature |String |The calculated signature. |

---
title: "Exception Handling (PHP SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Exception-handling-php-sdk"
---

This article introduces exception handling when using the TOS SDK.

<span id=".5byC5bi46K-05piO"></span>
## Exception Description

Exceptions are categorized as client\-side exceptions and server\-side exceptions, corresponding to TosClientError and TosServerError, respectively. A server\-side exception must include the HTTP status code and response headers returned by the server. The struct definition for exceptions is as follows:

The TOS server complies with HTTP standards and defines detailed HTTP status codes and business error codes for scenarios involving request failures. For details on error codes, please refer to [ TOS Server-Side Status and Error Code Definitions](https://docs.byteplus.com/en/docs/tos/reference-codes-in-response).

<span id=".c2RrLeiHquWumuS5ieW8guW4uA=="></span>
## SDK Custom Exceptions

The TOS PHP SDK encapsulates two types of custom exceptions based on TOS server\-side errors: Tos\Exception\TosClientException and Tos\Exception\TosServerException. The former typically indicates a request parameter error, in which case the request is not sent to the server. The latter represents errors returned by the server after a request has been sent; this exception provides access to detailed error information returned from the server.

For general methods of handling exceptions with TosClient, please refer to the [General Client Example](https://docs.byteplus.com/docs/tos/Quick-start-php-sdk#%E5%AE%A2%E6%88%B7%E7%AB%AF%E9%80%9A%E7%94%A8%E7%A4%BA%E4%BE%8B).

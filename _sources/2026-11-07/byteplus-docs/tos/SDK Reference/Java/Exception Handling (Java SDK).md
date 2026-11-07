---
title: "Exception Handling (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Exception-handling-java-sdk"
---

This document introduces exception handling when using the TOS SDK.

<span id=".dG9zLeacjeWKoeerr-mUmeivrw=="></span>
## TOS Server\-Side Error

The TOS server complies with HTTP specifications and defines detailed HTTP status codes and business error codes for scenarios involving request failures. For detailed information, please refer to [TOS Server-side Status Codes and Error Codes Definition](https://docs.byteplus.com/en/docs/tos/reference-codes-in-response).

<span id=".c2RrLeiHquWumuS5ieW8guW4uA=="></span>
## SDK Custom Exception

The TOS Java SDK defines two types of exceptions: TosClientException for client\-side errors and TosServerException for server\-side errors. Both exception classes inherit from TosException, which in turn extends RuntimeException.

<span id=".5a6i5oi356uv5byC5bi4LXRvc2NsaWVudGV4Y2VwdGlvbg=="></span>
### Client\-Side Exception: TosClientException

A TosClientException is typically thrown before the SDK sends a request to the TOS server. The following are scenarios in which this exception may be raised.


* Parameter validation failed. For example, when the parameters of the XXInput class are empty or the bucket name is non\-compliant (such as when the bucket name exceeds 63 characters), etc.

* Transmission failures may occur during upload or download processes due to network anomalies, program interruptions, and other similar issues.


If a TosClientException occurs, it is recommended to first verify that the input parameters comply with the specifications. The TosClientException records the cause of the exception in its message, which can be obtained and analyzed using the TosClientException.getMessage() method.

<span id=".5pyN5Yqh56uv5byC5bi4LXRvc3NlcnZlcmV4Y2VwdGlvbg=="></span>
### Server\-Side Exception: TosServerException

TosServerException is an exception parsed and thrown by the SDK based on the response returned from the TOS server, including information such as HTTP status codes and exception reasons. If a TosServerException occurs, refer to [the definition of TOS server-side status codes and error codes](https://docs.byteplus.com/docs/6349/74874) to handle it.

<span id=".5byC5bi45aSE55CG56S65L6L"></span>
### Exception Handling Examples

For handling TosClientException and TosServerException thrown by the SDK, please refer to the [Client General Example](https://docs.byteplus.com/docs/tos/Quick-start-java-sdk#%E5%AE%A2%E6%88%B7%E7%AB%AF%E9%80%9A%E7%94%A8%E7%A4%BA%E4%BE%8B) for details.

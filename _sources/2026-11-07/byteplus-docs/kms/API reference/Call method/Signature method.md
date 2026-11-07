---
title: "Signature method"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/Signature_method"
---

To ensure that the identity of the requester is valid and the request is not tampered with during transmission, the BytePlus signature mechanism requires the requester to perform hash calculation on request parameters, encrypt them, and send them with the API request to the server. The server will use the same mechanism to calculate a signature based on the received request and compare the result with the signature sent by the requester. If the signature fails to pass verification, the request is rejected.

<span id="constructing-a-signature"></span>
## Constructing a signature

BytePlus provides a signature function or method in the SDK. You only need to provide information such as an access key in a request. The SDK automatically calculates the request signature and adds the signature to the request. This method simplifies both the signature and development processes, and is especially friendly to developers who are unfamiliar with signature algorithms.


* [Java SDK](https://github.com/volcengine/volcengine-java-sdk)

* [Go SDK](https://github.com/volcengine/volcengine-go-sdk)

* [Python SDK](https://github.com/volcengine/volcengine-python-sdk)

* [PHP SDK](https://github.com/volcengine/volcengine-php-sdk)


Alternatively, you can use the BytePlus developer tool API Explorer to initiate an API call online to instantly obtain the call result.


* [API Explorer](https://api.volcengine.com/api-explorer?action=DescribeSecrets&groupName=%E5%87%AD%E6%8D%AE%E7%AE%A1%E7%90%86&serviceCode=kms&version=2021-02-18%EF%BC%9F%EF%BC%9F%EF%BC%9F)


When you cannot avoid writing code to construct a signature, refer to the following signature mechanism. A signature demo is provided for your reference.


* [Calculating a signature](https://docs.byteplus.com/en/docs/byteplus-platform/reference-how-to-calculate-a-signature)

* [Example](https://docs.byteplus.com/en/docs/byteplus-platform/reference-example)


<span id="signature-mechanism"></span>
## Signature mechanism

For more information on the signature mechanism, refer to [Signature method](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-signature).

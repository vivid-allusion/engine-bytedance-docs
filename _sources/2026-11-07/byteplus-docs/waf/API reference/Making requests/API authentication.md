---
title: "API authentication"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/API_authentication"
---

When calling an interface, you can authenticate your identity in two ways before initiating an interface call.


* AK / SK Authentication: Encrypt the call request using your Access Key ID and Secret Access Key. AK / SK Authentication is recommended as it is more secure than Token Authentication.

* Token Authentication: Authenticate generic requests using a Token.


<span id="99ae453d"></span>
## **AK / SK Authentication**

AK / SK Authentication involves signing your requests with the Access Key ID and Secret Access Key and adding the signature information to the request parameters.

To ensure the legitimacy of the requester's identity and that the request is not maliciously tampered with during transmission, BytePlus's signature mechanism requires the requester to calculate the hash value of the request parameters. After encryption, it is sent to the server along with the API request. The server will perform signature calculation on the received request using the same mechanism and compare it with the signature sent by the requester. If the signature fails to validate, the request will be denied. For information on how to calculate signatures, please refer to [Calculating a signature](https://docs.byteplus.com/en/docs/byteplus-platform/reference-how-to-calculate-a-signature).

<span id="43a84372"></span>
## **Token Authentication**

Token authentication involves adding the Token to the request header when calling an API, thereby passing identity verification and gaining permission to operate the API.

Token can be obtained by calling the [AssumeRole](https://docs.byteplus.com/en/docs/byteplus-platform/reference-assumerole) interface.

---
title: "Vision AI FAQ"
product: "Vision AI"
product_code: "byteplus-vision"
source: "https://docs.byteplus.com/en/docs/byteplus-vision/FAQ"
---

<span id="jqYbz5uw"></span>
# Vision AI

<span id="dCjr4hYh"></span>
## 1. How to obtain the AK/SK required for integrating the API?

APIs already listed on the console can be directly obtained via the [BytePlus Console](https://console.byteplus.com/iam/keymanage).

For capabilities not yet listed on the console, please contact the business team to apply for authorization.

<span id="APYxQgU7"></span>
## 2. How to integrate the API?

You can call the API via the SDK.


* The SDK encapsulates the signature of the TOP gateway layer, eliminating the need for cumbersome manual calculations.

* It also encapsulates API calls (including requests and responses) and provides corresponding examples.


Currently, we offer SDKs for the following languages. If you require SDKs for other languages, please contact us, and we will assist you with the integration.

**Python**


* Code repository: [byteplus-sdk-python](https://github.com/byteplus-sdk/byteplus-sdk-python)

* Calling examples: see [Examples](https://github.com/byteplus-sdk/byteplus-sdk-python/tree/master/byteplus_sdk/example/visual)


**Golang**


* Code repository: [byteplus-sdk-golang](https://github.com/byteplus-sdk/byteplus-sdk-golang)

* Calling examples: see [Examples](https://github.com/byteplus-sdk/byteplus-sdk-golang/tree/master/example/visual)


Currently, SDKs for some languages have not been developed, or the capabilities supported by the SDKs are insufficient. Signature code examples are provided for your reference during integration. Please refer to [HTTP Request Sample](https://docs.byteplus.com/en/docs/byteplus-vision/http_request_sample).

<span id="VjeDuzAv"></span>
## 3. What is the expiration time of the returned image URLs/video URLs?

Image URLs are valid for 24 hours and must be regenerated after they expire.

Video URLs are valid for 1 hour and must be regenerated after they expire.

<span id="YTLk1fCj"></span>
## 4. What are the requirements for the image URLs/video URLs provided to the API service?

The image URLs/video URLs must be publicly accessible via the Internet.

The image URLs/video URLs should not require human verification.

The provided images/videos must comply with the requirements specified in the API documentation (e.g., size, length, resolution, etc.).

<span id="mUrpupHg"></span>
## 5. What do the returned error codes mean?

Error codes fall into two categories: common error codes and business error codes.


* Common error codes can be found in [Common Response and Error Codes](https://docs.byteplus.com/en/docs/byteplus-vision/docs-common-responses-and-error-codes).

* Business error codes can be found in the interface documentation for the respective capability.


<span id="bj7myVnJ"></span>
## 6. Support sub\-accounts?

Each main account can create multiple sub\-accounts with differentiated permissions.

Applicable scenarios:


1. Set up separate sub\-accounts for diverse businesses to manage resources independently.

2. Generate dedicated sub\-account AK/SK for OpenAPI calls, preventing security risks from primary account credential leakage.


&nbsp;

A. Creation steps:


1. Create sub\-account


Log in to the console, access [Access Control - User Management](https://console.byteplus.com/iam/identitymanage/user) via the personal center icon at the top right corner.


2. Click New User to start creation. Each user corresponds to one sub\-account.

3. Select creation method, such as username or mobile phone number.

4. Fill in basic information according to the chosen method.

5. Permission settings: Associate policies and roles. Create and manage policies and roles in Role Management and Policy Management on the left. Current policies of AI Open Platform are as follows:

   
   |**Policy name** |**Description** |
   |---|---|
   |[CVFullAccess](https://console.byteplus.com/iam/policymanage/System/CVFullAccess) |Provides full access to CV. |
   


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260522035847-1304744299501.png) </span>

B. Obtain sub\-account AK/SK

It is recommended to use sub\-account AK/SK for OpenAPI and server SDK access to prevent primary account credential leakage.

Locate the sub\-account in Access Control \> User Management and click Manage.

Manage sub\-account AK/SK under AccessKey Management.

<span id="3aNWHob8"></span>
## 7. Service activation failed. 

Please verify whether your account has completed enterprise verification. An enterprise\-verified account is required to activate the service.

<span id="jqYbz5uw"></span>
# BytePlus Console

<span id="dTxhfOJh"></span>
## 1. BytePlus Console IP Blocking

BytePlus Console IP Blocking [https://console.byteplus.com/ai](https://console.byteplus.com/ai)


* The process for users to access the BytePlus Console follows the following rules:


Only whitelisted regions support access to the Console's features; IP addresses from other regions will be blocked. Access is determined as follows:

a. First, check if the account registration address is in the whitelist. If yes, access is granted.

b. Second, verify if the source IP address is in the whitelist. If yes, access is granted.

c. In all other cases, access will be blocked.

If you encounter issues accessing the BytePlus Console, please contact technical support for assistance.

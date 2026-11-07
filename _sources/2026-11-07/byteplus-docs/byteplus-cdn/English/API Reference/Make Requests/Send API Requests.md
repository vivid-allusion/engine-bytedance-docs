---
title: "Send API Requests"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-send-api-requests"
---

This document describes how to call the BytePlus CDN API.

Before sending API requests, you need to understand the following:


* [Request Structure](https://docs.byteplus.com/en/docs/18/6813#request-structure).

* [Common Parameters](https://docs.byteplus.com/en/docs/18/6813#common-parameters).

* [Request Authentication](https://docs.byteplus.com/en/docs/18/6813#request-authentication).

* [Signature Calculation Method](https://docs.byteplus.com/en/docs/18/6813#signature-calculation-method).


<span id="request-structure"></span>
## Request Structure

The structure of an API request includes the following:


* API service address.

* Communication protocol.

* Request method.

* Request parameters.


<span id="api-service-address"></span>
### API Service Address

The API service address for the BytePlus CDN is `cdn.byteplusapi.com`.

<span id="communication-protocol"></span>
### Communication Protocol

You can use either the `HTTP` or `HTTPS` protocol to send requests. It is recommended to use the `HTTPS` protocol for higher security.

<span id="request-method"></span>
### Request Method

Unless otherwise specified, use the `POST` method to send requests. Additionally, you must specify `Content-Type: application/json` in the request header.

<span id="request-parameters"></span>
### Request Parameters

Request parameters include common parameters and parameters specific to each API.

<span id="common-parameters"></span>
## Common Parameters

Common parameters are required for every API request. If a common parameter is missing in an API request, the request will fail. The following table lists the common parameters that must be included in the query string.


|Parameter Name |Data Type |Required |Description |Example |
|---|---|---|---|---|
|Action |string |Yes |Represents the API name. The name follows the regular expression format [a\-zA\-Z]+. |`DescribeCdnData` |
|Version |string |Yes |Represents the API version. The value of this parameter is `2021-03-01`. |`2021-03-01` |
|X\-Expires |int |No |Represents the validity period of the signature included in the authentication information, in seconds. The default value is `900`. |`900` |


<span id="request-authentication"></span>
## Request Authentication

Every request must include authentication information to verify the identity of the requester. You can provide authentication information using either of the following methods. Method 1 is recommended.

<span id="recommended-method-1-include-authentication-information-in-the-request-header"></span>
### (Recommended) Method 1: Include Authentication Information in the Request Header

You need to include the following parameters in the request header:


|**Parameter Name** |**Data Type** |**Required** |**Description** |**Example** |
|---|---|---|---|---|
|X\-Date |string |Yes |Represents the time of signature calculation in UTC. The time precision is in seconds.<br><br>Regarding this parameter, please note the following: When the request arrives, the CDN calculates the difference between the arrival time and X\-Date. If the difference exceeds the time range specified by X\-Expires, the CDN considers the request invalid. Therefore, it is recommended to calibrate the system time before calculating the signature. |`20210913T081805Z` |
|Authorization |string |Yes |This parameter represents the authentication string. The pseudocode for this parameter is as follows:<br><br>`HMAC-SHA256 Credential = {AccessKey}/{ShortDate}/{Region}/{Service}/{Request}, SignedHeaders={SignedHeaders}, Signature={Signature}`<br><br>The explanation of this pseudocode is as follows:<br><br><br>* The `Signature` parameter in the pseudocode represents a calculated signature. For the calculation method of the signature, refer to [Signature Calculation Method](https://docs.byteplus.com/en/docs/18/6813#signature-calculation-method).<br><br>* For the explanation of other parameters in the pseudocode, refer to [Pseudo Code Parameter Explanation](https://docs.byteplus.com/en/docs/18/6813#pseudo-code-parameter-explanation). | |


<span id="method-2-including-authentication-information-in-the-query-string"></span>
### Method 2: Including Authentication Information in the Query String

You need to include the following query parameters in the query string.


|**Parameter Name** |**Data Type** |**Parameter Description** |**Example** |
|---|---|---|---|
|X\-Date |string |Represents the time of signature calculation in UTC. The time precision is in seconds. Regarding this parameter, please note the following:<br><br><br>* When the request arrives, the CDN calculates the time difference between the request arrival time and `X-Date`. If the difference exceeds the time range specified by `X-Expires`, the CDN considers the request invalid. Therefore, it is recommended to calibrate the system time before calculating the signature. |`20210913T081805Z` |
|X\-Algorithm |string |Represents the algorithm used for signature calculation. The value of this parameter is `HMAC-SHA256`. |`HMAC-SHA256` |
|X\-Credential |string |The pseudocode for the parameter value is as follows:<br><br>`{AccessKey}/{ShortDate}/{Region}/{Service}/{Request}`<br><br>For the explanation of the parameters in the pseudocode of `X-Credential`, refer to [Pseudo Code Parameter Explanation](https://docs.byteplus.com/en/docs/18/6813#pseudo-code-parameter-explanation). |`AKLTMjI2ODVlYzI3ZGY1NGU4ZjhjYWRjMTlmNTM5OTZkYzE/20210913/singapore/CDN/request` |
|X\-SignedHeaders |string |The explanation of this parameter is the same as the `SignedHeaders` parameter in the [Pseudo Code Parameter Explanation](https://docs.byteplus.com/en/docs/18/6813#pseudo-code-parameter-explanation). |`host;x-content-sha256;x-date` |
|X\-Signature |string |Represents a calculated signature. For the calculation method of the signature, refer to [Signature Calculation Method](https://docs.byteplus.com/en/docs/18/6813#signature-calculation-method). | |


<span id="signature-calculation-method"></span>
## Signature Calculation Method

This section mainly describes how the signature is calculated. The [Pseudo Code Parameter Explanation](https://docs.byteplus.com/en/docs/18/6813#pseudo-code-parameter-explanation) is provided at the end of the document.


* Signature calculation is a complex process. We recommend using [BytePlus SDK](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-byteplus-sdk) to interact with CDN, which eliminates the need for signature calculation.

* The `HMAC` method used in the pseudo code in this section uses the HMAC\-SHA256 algorithm.

* The `HexEncode` method used in the pseudo code in this section converts a string to a string in hexadecimal encoding format.


The signature parameter `Signature` is calculated based on the `kSigning` and `StringToSign` parameters. The pseudo code for `Signature` is as follows:

```Plain
Signature = HexEncode(HMAC(kSigning, StringToSign))
```


<span id="ksigning"></span>
### kSigning

`kSigning` represents the key used to calculate the signature. To calculate `kSigning`, you must first [obtain the Access Key Secret of your account](https://console.byteplus.com/iam/keymanage), and then use the following pseudo code to generate `kSigning`.

```Plain
kSecret = <Your Access Key Secret>
kDate = HMAC(kSecret, ShortDate)
kRegion = HMAC(kDate, Region)
kService = HMAC(kRegion, Service)
kSigning = HMAC(kService, "request")
```


For the explanation of the parameters in the pseudo code of `kSigning`, see [Pseudo Code Parameter Explanation](https://docs.byteplus.com/en/docs/18/6813#pseudo-code-parameter-explanation).

<span id="stringtosign"></span>
### StringToSign

`StringToSign` represents the signature string used to calculate the signature. The pseudo code for `StringToSign` is as follows:

```Plain
// The Hash function uses the SHA256 algorithm
StringToSign = Algorithm + '\n' + RequestDate + '\n' + CredentialScope + '\n' + HexEncode(Hash(CanonicalRequest))
```


For the explanation of the `Algorithm` and `RequestDate` parameters in the pseudo code of `StringToSign`, see the explanation of the parameters in the pseudo code. The explanation of other parameters in the pseudo code of `StringToSign` is as follows.

**CredentialScope**

`CredentialScope` represents the scope of the credentials. The pseudo code for `CredentialScope` is as follows:

```Plain
{ShortDate}/{Region}/{Service}/{Request}
```


For the explanation of the parameters in the pseudo code of `CredentialScope`, see [Pseudo Code Parameter Explanation](https://docs.byteplus.com/en/docs/18/6813#pseudo-code-parameter-explanation).

**CanonicalRequest**

`CanonicalRequest` represents the canonical request. The pseudo code for `CanonicalRequest` is as follows:

```Plain
HTTPRequestMethod + '\n' + CanonicalURI + '\n' + CanonicalQueryString + '\n' + CanonicalHeaders + '\n' + SignedHeaders + '\n' + HexEncode(Hash(RequestPayload))
```


The explanation of the parameters in the pseudo code of `CanonicalRequest` is as follows:


* `HTTPRequestMethod`: Represents the request method. For the CDN, the value of this parameter is `POST`.

* `CanonicalURI`: Represents the URI of the request.

* `CanonicalQueryString`: Represents the canonical query string. The value of `CanonicalQueryString` is generated according to the following rules:

   * Sort the query parameters in ascending order by parameter name.

* `CanonicalHeaders`: Represents the canonical request headers. `CanonicalHeaders` is generated through the following steps:

   1. Convert the names of the request header parameters involved in signature calculation to lowercase letters.

   2. Sort these names in ascending order at the character level.

   3. Concatenate these request header parameters in the key\-value format. The key is the name of the request header parameter, and the value is the value of the request header parameter.

   4. Add a line break (`\n`) after each request header parameter.

* `SignedHeaders`: See [Pseudo Code Parameter Explanation](https://docs.byteplus.com/en/docs/18/6813#pseudo-code-parameter-explanation).

* `HexEncode(Hash(RequestPayload))`: Represents a calculated value. This value is obtained by applying the SHA256 hash algorithm to the value of the `payload` in the request body.


<span id="pseudo-code-parameter-explanation"></span>
## Pseudo Code Parameter Explanation

The following table contains explanations of the parameters used in the pseudo code in this document.


|Parameter Name |Data Type |Parameter Description |Example |
|---|---|---|---|
|AccessKey |string |Represents the Access Key ID of your account. Refer to [Get Access Key](https://console.byteplus.com/iam/keymanage). |`AKLTMjI2ODVlYzI3ZGY1NGU4ZjhjYWRjMTlmNTM5OTZkYzE` |
|RequestDate |string |This parameter is the same as the definition of `X-Date` in the [Request Authentication](https://docs.byteplus.com/en/docs/18/6813#request-authentication) section. |`20210913T081805Z` |
|ShortDate |string |This parameter is the same as the definition of `RequestDate`, but with a daily time precision. |`20210913` |
|Region |string |This parameter is used for signature calculation. The parameter value is recommended to be `singapore`, but it can also be any non\-empty string. |`singapore` |
|Service |string |Represents the service name of the CDN. The value of this parameter is `CDN`. |`CDN` |
|SignedHeaders |string |Represents the request header parameters involved in the signature calculation. Multiple request header parameters are separated by semicolons (;). These request header parameters are sorted in ascending order based on the parameter name.<br><br>In general, the value of `SignedHeaders` is `host;x-content-sha256;x-date`. You can also specify any request header parameter as the value of `SignedHeaders`. |`host;x-content-sha256;x-date` |
|Algorithm |string |Represents the algorithm used for the signature calculation. The value of this parameter is `HMAC-SHA256`. |`HMAC-SHA256` |
|Request |string |This parameter is a constant with the value `request`. |`request` |


<span id="request-example"></span>
## Request Example

```Plain
POST https://cdn.byteplusapi.com/?Action=DescribeCdnConfig&Version=2021-03-01

// Request Headers
X-Date: 20230116T073702Z
Authorization: HMAC-SHA256 Credential=AKLTMjYxYTZmYWU4ZWYzNGI2NDg8NTUxODE1ZGVhNmIxZmQ/20230116/singapore/CDN/request, SignedHeaders=x-content-sha256;x-date, Signature=5a394ce80456c7cdf989c28bd638807c8ead386eb15dd36e39952f405380aef2
Content-Type: application/json

//Request Body
{
    "Domain": "www.example.com"
}
```

---
title: "Calculating a signature"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/reference-how-to-calculate-a-signature"
---

The process of calculating a signature is as follows:


1. Creating a canonical request.

2. Extracting a signature string.

3. Calculating the signing key.

4. Calculating the signature.


<span id="3698d1e4"></span>
## Before you start

The following preparations are required before calling BytePlus OpenAPI:


1. Sign up for a BytePlus account (click [here](https://docs.byteplus.com/en/byteplus-platform/docs/signing-up-your-account) for details) to get the AccessKey ID and AccessKey Secret (AK/SK), which are used for API request authentication. The AK/SK can be retrieved through **BytePlus Console** \> **User Profile** \> **IAM** \> **Key Management**.

2. Purchase or request the access to BytePlus products or services and ensure that your account has the permission to access the resources of the target product.

3. (Recommended) Download the [Open Platform SDK](https://github.com/byteplus-sdk) for calling BytePlus OpenAPI. The SDK is integrated with the signature mechanism.

4. Read the API reference documentation of the target BytePlus product for details about its API operations.


<span id="0015cb62"></span>
## Creating a canonical request

Create a canonical request to normalize the process of signature calculation. The pseudocode is as follows:

```text
CanonicalRequest = HTTPRequestMethod + '\n' + CanonicalURI + '\n' + CanonicalQueryString + '\n' + CanonicalHeaders + '\n' + SignedHeaders + '\n' + HexEncode(Hash(RequestPayload))
```


In the pseudocode above:


* `Hash` represents SHA256 algorithm.

* `HexEncode` represents the conversion to hexadecimal encoding.

* `Hmac` represents Hmac_SHA256 algorithm.


The descriptions of related fields are as follows:


|**Field name** |**Description** |
|---|---|
|HTTPRequestMethod |The method of an HTTP request, such as GET and POST. |
|CanonicalURI |The canonical URI of an API request.<br><br>If the URI is a null value, use / as absolute path. The URIs of most BytePlus OpenAPI operations are / . For complex path, follow [RFC3986](https://tools.ietf.org/html/rfc3986) specification for encoding. |
|CanonicalQueryString |The canonical query string of an API request. The process of generating the canonical query string is as follows:<br><br>**1.**  urlencode each parameter and its value (using [RFC3986](https://tools.ietf.org/html/rfc3986)).<br><br>**2.**  Sort all the parameters of the API request by ASCII order, and different values of the same parameter are sorted by the original requesting sequence.<br><br>**3.**  Connect the sorted parameters and their values with `=`, and concatenate the parameter pairs into a string with `&`. For example: `CanonicalQueryString = Action=ListUsers&Version=2018-01-01` . |
|CanonicalHeaders |The canonical headers of an API request. The pseudocode is: `CanonicalHeaders = CanonicalHeadersEntry0 + CanonicalHeadersEntry1 + ... + CanonicalHeadersEntryN`.<br><br>In `CanonicalHeadersEntry = Lowercase(HeaderName) + ':' + Trimall(HeaderValue) + '\n'`:<br><br>`Lowercase` means converting all the header names to lowercase.<br><br>`Trimall` means removing the extra spaces before and after the header value.<br><br>**Note:**  A "\n" character must be added in the end, and headers are sorted by the lowercase header name in ASCII order. |
|SignedHeaders |The headers that are included in generating the signature, which correspond to the canonical headers one by one. The purpose is to specify the headers that are included in the signature calculation, so as to ignore the additional headers added by the proxy.<br><br>The `host` and `x-date` are required if they are included in the request header.<br><br>The pseudocode is: `SignedHeaders = Lowercase(HeaderName0) + ';' + Lowercase(HeaderName1) + ; + ... + Lowercase(HeaderNameN)`. |
|RequestPayload |The complete request body. |


<span id="210b5aee"></span>
## Extracting a signature string

A signature string consists of the request's metadata and the canonical request, including the signing algorithm, request date, credential scope, and hash value of the canonical request. The pseudocode is as follows:

```text
StringToSign = Algorithm + '\n' + RequestDate + '\n' + CredentialScope + '\n' + HexEncode(Hash(CanonicalRequest))
```


The descriptions of related fields are as follows:


|**Field name** |**Description** |
|---|---|
|Algorithm |The signing algorithm. BytePlus OpenAPI supports the `HMAC-SHA256` algorithm only. |
|RequestDate |The time when the API request is sent (the value of `X-Date` in the request header). Format: UTC (`YYYYMMDD'T'HHMMSS'Z'`). For example, `20201103T104027Z`. |
|CredentialScope |The credential scope. Format: `{``YYYYMMDD}/{region}/{service}/request`. For example, `20201230/ap-singapore-1/livesaas/request`. |
|CanonicalRequest |The result of the canonical request described above. |


<span id="fae450fc"></span>
## Calculating the signing key

Derive the signing key from the private access key (AccessKey Secret) instead of directly using the private access key. The process of calculating the signing key is as follows:

```text
kSecret = *Your AccessKey Secret*
kDate = HMAC(kSecret, Date)
kRegion = HMAC(kDate, Region)
kService = HMAC(kRegion, Service)
kSigning = HMAC(kService, "request")
```


The format of `Date` is `YYYYMMDD`. Its value is the same as the `YYYYMMDD` part in `RequestDate`.

<span id="9531c35c"></span>
## Calculating the signature

The following pseudocode shows how to calculate the signature.

```text
Signature = HexEncode(HMAC(kSigning, StringToSign))
```


The following pseudocode shows how to construct the `Authorization` header.

```text
Authorization: HMAC-SHA256 Credential={AccessKeyId}/{CredentialScope}, SignedHeaders={SignedHeaders}, Signature={Signature}
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The expressions enclosed by {} represent the intermediate values that are calculated in the above steps.</div>

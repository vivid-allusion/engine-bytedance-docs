---
title: "Signature mechanism"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Signature_mechanism"
---

The AI Native Database Platform services authenticate every access request, so you need to include signature information in the request. This topic introduces the API signature mechanism of the AI Native Database Platform.

<span id=".5Yib5bu65LiA5Liq5q2j6KeE5YyW6K-35rGC"></span>
## Create a canonical request

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Hash refers to the SHA256 algorithm.</div>


* <div data-tips="true" data-tips-type="tip">HexEncode refers to hexadecimal encoding.</div>



You need to sign your request using the following method:

```Plain Text
CanonicalRequest = HTTPRequestMethod + '\n' + CanonicalURI + '\n' + CanonicalQueryString + '\n' + CanonicalHeaders + '\n' + SignedHeaders + '\n' + HexEncode(Hash(RequestPayload))
```



* **HTTPRequestMethod**

   Refers to the HTTP request method, for example: GET or POST.

* **CanonicalURI**:

   CanonicalURI refers to the normalized URI. If URI is empty, a forward slash ( / ) is used as the absolute path. The URI of most APIs in BytePlus is represented as ( / ).

* **CanonicalQueryString**

   Refers to the normalized Query String. For example:

   ```Plain Text
   CanonicalQueryString = "Action=ListUsers&Version=2018-01-01"
   ```
   

   The general process for normalizing the query string is as follows:

   * URI encode each querystring parameter name and value.

   * Parameter names are strictly sorted according to ASCII byte order, and different parameter values ​​with the same parameter name must maintain the original order of the request.

   * Concatenate sorted parameter names and values with equal signs ( = ) and the **parameter pairs** with ampersands ( & ) according to the sorting result.

* **CanonicalHeaders**

   CanonicalHeaders refers to the canonicalized Header. The pseudo code is as follows:

   ```Plain Text
   CanonicalHeaders =
   CanonicalHeadersEntry0 +
   CanonicalHeadersEntry1 + ... +
   CanonicalHeadersEntryN
   ```
   

   Among them

   ```Plain Text
   CanonicalHeadersEntry = Lowercase(HeaderName) + ':' + Trimall(HeaderValue) + '\n'
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Lowcase means converting the entire header name to lowercase.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Trimall removes extra spaces before and after the value in the header.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Finally, add the newline character <code>\n</code>.   </div>
   

* **SignedHeaders**

   Refers to the names of Headers involved in the signature. SignedHeaders is a list of header names from the canonicalized headers. It specifies which headers are part of the signature calculation, which allows for ignoring any extra headers added by a proxy. If the `host` and `x\-date` headers exist, they must be included. The pseudo code is as follows:

   ```Plain Text
   SignedHeaders = Lowercase(HeaderName0) + ';' + Lowercase(HeaderName1) + ";" + ... + Lowercase(HeaderNameN)
   ```
   

* **RequestPayload**

   Refers to the complete request body. Note the following points:

   * URI encoding (Note: same as [RFC3986](https://tools.ietf.org/html/rfc3986) method) of each querystring parameter name and parameter value (Note: GET method requires all parameters such as hash algorithm, letter of trust, signature date and signature header).

   * Sort parameter names strictly in ASCII byte order.

   * Concatenate sorted parameter names and values with equal signs ( = ) and the **parameter pairs** with ampersands ( & ) according to the sorting result.


<span id=".5Yib5bu6562-5ZCN5a2X56ym5Liy"></span>
## Create a string to sign

A string to sign contains the metadata information of the request and request canonicalization and concatenates the signature algorithm, request date, credential, and canonical request hash value. The pseudocode is as follows:

```Plain Text
StringToSign = Algorithm + '\n' + RequestDate + '\n' + CredentialScope + '\n' + HexEncode(Hash(CanonicalRequest))
```



* **Algorithm**

   Refers to the signature algorithm. Currently, BytePlus only supports the HMAC\-SHA256 signature algorithm.

* **RequestDate**

   Refers to the requested UTC time. Use the following format: YYYYMMDD'T'HHMMSS'Z'.

* **CredentialScope**

   Refers to the credential in the format of:  * YYYYMMDD/region/ service/request*.

* **CanonicalRequest**

   Refers to the result of the canonicalized request in the previous section.


<span id=".6K6h566X562-5ZCN56eY6ZKl77yILXNpZ25pbmcta2V5Le-8iQ=="></span>
## Calculate the signing key (signing\-key)

Calculate the signing key before calculating the signature, first derive the signing key from the Secret Access Key, instead of directly using the private access key. The specific calculation process is as follows:

```Plain Text
kSecret = *Your Secret Access Key*
kDate = HMAC(kSecret, Date)
kRegion = HMAC(kDate, Region)
kService = HMAC(kRegion, Service)
kSigning = HMAC(kService, "request")
```



1. Calculate signature

   ```Plain Text
   Signature = HexEncode(HMAC(kSigning, StringToSign))
   ```
   

2. Build header

   ```Plain Text
   Authorization: HMAC-SHA256 Credential={AccessKeyId}/{CredentialScope}, SignedHeaders={SignedHeaders}, Signature={Signature}
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the expression, the content enclosed in {} represents intermediate results calculated from the previous steps.   </div>
   

<span id=".562-5ZCN56S65L6L"></span>
## Signature example

For more information, refer to [Signature example](https://docs.byteplus.com/en/docs/byteplus-platform/reference-how-to-calculate-a-signature).

---
title: "Signature mechanism"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/signature-mechanism"
---

Document Database for MongoDB authenticates each access request, so you need to include signature information in the request. This topic introduces the signature mechanism used by Document Database for MongoDB APIs.

<span id=".5Yib5bu65LiA5Liq5q2j6KeE5YyW6K-35rGC"></span>
## Create a canonical request

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Hash refers to the SHA256 algorithm.</div>


* <div data-tips="true" data-tips-type="tip">HexEncode refers to hexadecimal encoding.</div>



When accessing, you need to sign the request according to the following method:

```json
CanonicalRequest = HTTPRequestMethod + '\n' + CanonicalURI + '\n' + CanonicalQueryString + '\n' + CanonicalHeaders + '\n' + SignedHeaders + '\n' + HexEncode(Hash(RequestPayload))
```



* **HTTPRequestMethod**

   Refers to the HTTP request method, for example: GET or POST.

* **CanonicalURI**:

   Refers to the normalized URI. If the URI is empty, use `/` as the absolute path. The URI of most APIs in BytePlus is represented as `/`.

* **CanonicalQueryString**

   Refers to the normalized Query String. For example:

   ```Plain Text
   CanonicalQueryString = "Action=ListUsers&Version=2018-01-01"
   ```
   

   The general process for normalizing the Query String is as follows:

   * URI\-encode each querystring parameter name and parameter value.

   * Sort parameter names strictly in ASCII byte order. Different parameter values with the same parameter name must maintain the original order of the request.

   * Connect the sorted parameter name and parameter value with `=`, and connect `parameter pairs` with an ampersand ( `&`) according to the sorting result.

* **CanonicalHeaders**

   Refers to the canonical Header. The pseudo code is as follows:

   ```json
   CanonicalHeaders =
   CanonicalHeadersEntry0 +
   CanonicalHeadersEntry1 + ... +
   CanonicalHeadersEntryN
   ```
   

   Among them,

   ```json
   CanonicalHeadersEntry = Lowercase(HeaderName) + ':' + Trimall(HeaderValue) + '\n'
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Lowcase converts all Header names to lowercase.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Trimall removes extra spaces before and after the Header value.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The <code>\n</code> newline character must be added at the end.   </div>
   

* **SignedHeaders**

   Refers to the names of the Headers included in the signature. Signature Header is the list of names included in the normalized Headers, which indicates which Headers participate in signature calculation, so any additional Headers added by a proxy can be ignored. If Host and X\-Date headers exist, they must be added. The pseudo code is as follows:

   ```json
   SignedHeaders = Lowercase(HeaderName0) + ';' + Lowercase(HeaderName1) + ";" + ... + Lowercase(HeaderNameN)
   ```
   

* **RequestPayload**

   Refers to the complete request body. Focus on the key points below:

   * URI\-encode (same as [RFC3986](https://tools.ietf.org/html/rfc3986)) each Query String parameter name and parameter value (note: the GET method needs to include all parameters such as hash algorithm, credential, signature date, and signature Header).

   * Sort parameter names strictly in ASCII byte order.

   * Connect the sorted parameter name and parameter value with `=`, and connect `parameter pairs` with an ampersand ( `&`) according to the sorting result.


<span id=".5Yib5bu6562-5ZCN5a2X56ym5Liy"></span>
## Create a signature string

The signature string primarily contains the request and metadata information of the canonical request. It is formed by concatenating the signature algorithm, request date, credential, and the hash value of the canonical request. The pseudo code is as follows:

```json
StringToSign = Algorithm + '\n' + RequestDate + '\n' + CredentialScope + '\n' + HexEncode(Hash(CanonicalRequest))
```



* **Algorithm**

   Algorithm refers to the signature algorithm. Currently, BytePlus supports the HMAC\-SHA256 signature algorithm only.

* **RequestDate**

   Refers to the requested UTC time. Use the following format `YYYYMMDD'T'HHMMSS'Z'`.

* **CredentialScope**

   Refers to the credential in the format of `YYYYMMDD/region/ service/request`.

* **CanonicalRequest**

   Refers to the result of the canonicalized request in the previous section.


<span id=".6K6h566X562-5ZCN56eY6ZKl77yIc2lnbmluZy1rZXnvvIk="></span>
## Calculate the signing\-key

Before calculating the signature, first derive the signing key from the Secret Access Key, instead of directly using the Secret Access Key. The calculation process is as follows:

```json
kSecret = *Your Secret Access Key*
kDate = HMAC(kSecret, Date)
kRegion = HMAC(kDate, Region)
kService = HMAC(kRegion, Service)
kSigning = HMAC(kService, "request")
```



1. Calculate signature

   ```json
   Signature = HexEncode(HMAC(kSigning, StringToSign))
   ```
   

2. Build Header

   ```json
   Authorization: HMAC-SHA256 Credential={AccessKeyId}/{CredentialScope}, SignedHeaders={SignedHeaders}, Signature={Signature}
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Content enclosed in braces ({})<code>{}</code> in the expressions represents intermediary processes calculated earlier.   </div>
   

<span id=".562-5ZCN56S65L6L"></span>
## Signature example

For more details, refer to [Signature example](https://docs.byteplus.com/en/docs/byteplus-platform/reference-example).

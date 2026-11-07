---
title: "Signature mechanism"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/signature-mechanism"
---

The Database Workshop (DBW) service authenticates each access request. Therefore, you must include signature information in the request. This topic describes the API signature mechanism of Database Workshop (DBW).

<span id=".5Yib5bu65LiA5Liq5q2j6KeE5YyW6K-35rGC"></span>
## Create a canonical request

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Hash refers to the SHA256 algorithm.</div>


* <div data-tips="true" data-tips-type="tip">HexEncode refers to hexadecimal encoding.</div>



When accessing, you need to sign the request according to the following method:

```json
CanonicalRequest = HTTPRequestMethod + '\n' + CanonicalURI + '\n' + CanonicalQueryString + '\n' + CanonicalHeaders + '\n' + SignedHeaders + '\n' + HexEncode(Hash(RequestPayload))
```



* **HTTPRequestMethod** refers to the HTTP request method, for example, GET or POST.

* **CanonicalURI** refers to the canonicalized URI. If the URI is empty, use "/" as the absolute path. The URI of most APIs in BytePlus is represented as "/".

* **CanonicalQueryString** refers to the canonicalized Query String. For example:

   ```json
   CanonicalQueryString = "Action=ListUsers&Version=2022-01-01"
   ```
   


The general process for normalizing the Query String is as follows:


* URI\-encode each querystring parameter name and parameter value.

* Sort parameter names strictly in ASCII byte order. Different parameter values with the same parameter name must maintain the original order of the request.

* Connect the sorted parameter names and parameter values using`=`. Connect the "parameter pairs" by sorting results using `&`.

* **CanonicalHeaders** refers to the canonicalized Header. The pseudo code is as follows:

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


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Lowcase converts all Header names to lowercase.</div>


* <div data-tips="true" data-tips-type="tip">Trimall removes extra spaces before and after the Header value.</div>


* <div data-tips="true" data-tips-type="tip">Be sure to add the <code>\n</code> newline character at the end.</div>


* **SignedHeaders** refers to the Header names that participate in the signature. Signature Header is the list of names included in the normalized Headers, which indicates which Headers participate in signature calculation, so any additional Headers added by a proxy can be ignored. If Host and X\-Date headers exist, they must be added. The pseudo code is as follows:

   ```json
   SignedHeaders = Lowercase(HeaderName0) + ';' + Lowercase(HeaderName1) + ";" + ... + Lowercase(HeaderNameN)
   ```
   

* **RequestPayload** refers to the complete request Body. Note the following:

   * URI\-encode (note: same as [RFC3986](https://tools.ietf.org/html/rfc3986) method) each Query String parameter name and parameter value (note: the GET method needs to include all parameters such as hash algorithm, credential, signature date, and signature Header).

   * Sort parameter names strictly in ASCII byte order.

   * Connect the sorted parameter names and parameter values using `=`. Connect the "parameter pairs" by sorting results using `&`.


<span id=".5Yib5bu6562-5ZCN5a2X56ym5Liy"></span>
## Create a signature string

The signature string primarily contains the request and metadata information of the canonical request. It is formed by concatenating the signature algorithm, request date, credential, and the hash value of the canonical request. The pseudo code is as follows:

```json
StringToSign = Algorithm + '\n' + RequestDate + '\n' + CredentialScope + '\n' + HexEncode(Hash(CanonicalRequest))
```



* **Algorithm** refers to the signature algorithm. Currently, BytePlus supports the HMAC\-SHA256 signature algorithm only.

* **RequestDate** refers to the request UTC time in the format of `YYYYMMDD'T'HHMMSS'Z'`.

* **CredentialScope** refers to credentials in the format of `YYYYMMDD/region/ service/request`.

* **CanonicalRequest** refers to the canonical request result in the last section.


<span id=".6K6h566X562-5ZCN56eY6ZKl77yIc2lnbmluZy1rZXnvvIk="></span>
## Calculate the signing\-key

Before calculating the signature, first derive the signing key from the SecretAccess Key, instead of directly using the SecretAccess Key. The calculation process is as follows:

```json
kSecret = *Your Secret Access Key*
kDate = HMAC(kSecret, Date)
kRegion = HMAC(kDate, Region)
kService = HMAC(kRegion, Service)
kSigning = HMAC(kService, "request")
```



1. Calculate the signature


```json
Signature = HexEncode(HMAC(kSigning, StringToSign))
```



2. Build the Header


```json
Authorization: HMAC-SHA256 Credential={AccessKeyId}/{CredentialScope}, SignedHeaders={SignedHeaders}, Signature={Signature}
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In the expression, the content enclosed in <code>{}</code> represents intermediate results calculated from the previous steps.</div>


<span id=".562-5ZCN56S65L6L"></span>
## Signature example

For more information, refer to [Signature example](https://docs.byteplus.com/en/docs/DBW/signature-mechanism?type=preview&lang=en).

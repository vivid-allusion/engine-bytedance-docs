---
title: "Signature mechanism"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Signature_mechanism"
---

Table Storage for HBase services authenticate every access request, so you need to include signature information in the request. This article describes the API signature mechanism for Table Storage for HBase.

<span id=".5Yib5bu65LiA5Liq5q2j6KeE5YyW6K-35rGC"></span>
## Create a canonical request

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Hash refers to the SHA256 algorithm.</div>


* <div data-tips="true" data-tips-type="tip">HexEncode refers to hexadecimal encoding.</div>



When accessing, you need to sign the request according to the following method:

```Plain Text
CanonicalRequest = HTTPRequestMethod + '\n' + CanonicalURI + '\n' + CanonicalQueryString + '\n' + CanonicalHeaders + '\n' + SignedHeaders + '\n' + HexEncode(Hash(RequestPayload))
```



* `HTTPRequestMethod` refers to the HTTP request method, for example, GET or POST.

* `CanonicalURI` refers to the canonicalized URI. If the URI is empty, use `/` as the absolute path. The URI of most APIs in BytePlus is represented as `/`.

* `CanonicalQueryString` refers to the canonicalized Query String. For example:

   ```Plain Text
   CanonicalQueryString = "Action=ListUsers&Version=2018-01-01"
   ```
   

   The general process for normalizing the Query String is as follows:

   * URI\-encode each querystring parameter name and parameter value.

   * Sort parameter names strictly in ASCII byte order. Different parameter values with the same parameter name must maintain the original order of the request.

   * Connect the sorted parameter names and values with `=`, and then connect the resulting `parameter pairs` with `&`.

* `CanonicalHeaders` refers to the canonicalized Header. The pseudo code is as follows:

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
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Trimall removes extra spaces before and after the header value.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Add a newline character <code>\n</code> at the end.   </div>
   

* `SignedHeaders` refers to the Header names that participate in the signature. SignedHeaders is a list of header names from the canonicalized headers. It specifies which headers are part of the signature calculation, which allows for ignoring any extra headers added by a proxy. If the `host` and `x\-date` headers exist, they must be included. The pseudo code is as follows:

   ```json
   SignedHeaders = Lowercase(HeaderName0) + ';' + Lowercase(HeaderName1) + ";" + ... + Lowercase(HeaderNameN)
   ```
   

* `RequestPayload` refers to the complete request body. Note the following:

   * URI\-encode (note: same as the [RFC3986](https://tools.ietf.org/html/rfc3986) method) each querystring parameter name and parameter value (note: the GET method needs to include all parameters such as hash algorithm, credential, signature date, and signature header).

   * Sort parameter names strictly in ASCII byte order.

   * Connect the sorted parameter names and values with `=`, and then connect the resulting **parameter pairs** with `&`.


<span id=".5Yib5bu6562-5ZCN5a2X56ym5Liy"></span>
## Create a signature string

The signature string primarily contains the request and metadata information of the canonical request. It is formed by concatenating the signature algorithm, request date, credential, and the hash value of the canonical request. The pseudo code is as follows:

```json
StringToSign = Algorithm + '\n' + RequestDate + '\n' + CredentialScope + '\n' + HexEncode(Hash(CanonicalRequest))
```



* `Algorithm` refers to the signature algorithm. Currently, BytePlus supports the HMAC\-SHA256 signature algorithm only.

* `RequestDate` refers to the request UTC time in the `YYYYMMDD'T'HHMMSS'Z'` format.

* `CredentialScope` refers to the credential in the format of `YYYYMMDD/region/ service/request`.

* `CanonicalRequest` refers to the result of the canonical request from the previous section.


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
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the expression, the parts enclosed in<code>{}</code> represent the intermediate processes calculated above.   </div>
   

<span id=".562-5ZCN56S65L6L"></span>
## Example

For more information, refer to [Signature example](https://docs.byteplus.com/en/docs/byteplus-platform/reference-how-to-calculate-a-signature).

&nbsp;

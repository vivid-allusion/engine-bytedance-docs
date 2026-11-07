---
title: "Signature method"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/signature-method"
---

Cloud Search performs identity verification for every incoming request. You must include signature information in each request. This topic introduces the signature method of the Cloud Search API.

<span id="创建一个正规化请求"></span>
## Creating a canonical request

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Hash refers to the SHA256 algorithm.</div>


* <div data-tips="true" data-tips-type="tip">HexEncode is a function that encodes values in Base16.</div>



When making a request, you must sign it according to the following method:

```undefined
CanonicalRequest = HTTPRequestMethod + '\n' + CanonicalURI + '\n' + CanonicalQueryString + '\n' + CanonicalHeaders + '\n' + SignedHeaders + '\n' + HexEncode(Hash(RequestPayload))
```



* **HTTPRequestMethod**

   Refers to the method of the HTTP request, such as GET or POST.

* **CanonicalURI**

   Refers to the normalized URI. If the URI is empty, a forward slash ( / ) is used as the absolute path.

* **CanonicalQueryString**

   Refers to the normalized query string. Example:

   ```undefined
    CanonicalQueryString = "Action=ListUsers&Version=2018-01-01"
   ```
   

   The general process for the normalization of the query string is as follows:

   * Apply URI encoding to the name and value of each query string parameter.

   * Strictly sort the parameter names according to the ASCII character order. For parameters with the same name but different values, maintain the order in which they appear in the original request.

   * Connect each sorted parameter name and the corresponding value with an equal sign ( = ), then concatenate these parameter pairs with ampersands ( & ) in the sorted order to form the final query string.

* **CanonicalHeaders**

   Refers to the normalized headers. The pseudocode for constructing the canonical headers is as follows:

   ```undefined
    CanonicalHeaders =
    CanonicalHeadersEntry0 +
    CanonicalHeadersEntry1 + ... +
    CanonicalHeadersEntryN
   ```
   

   Where:

   ```undefined
   CanonicalHeadersEntry = Lowercase(HeaderName) + ':' + Trimall(HeaderValue) + '\n'
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Lowercase means converting the header name to all lowercase letters.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Trimall means removing any extra spaces before and after the header value.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The newline character <code>\n</code> must be added at the end.   </div>
   

* **SignedHeaders**

   Refers to the names of the headers that are used to calculate the signature. The SignedHeaders is a list of header names included in the canonical headers. It indicates which headers are part of the signature calculation, thus excluding any additional headers added by proxies. If the host and x\-date headers are present, they must be included in the SignedHeaders list. The pseudocode for constructing SignedHeaders is as follows:

   ```undefined
   SignedHeaders = Lowercase(HeaderName0) + ';' + Lowercase(HeaderName1) + ";" + ... + Lowercase(HeaderNameN)
   ```
   

* **RequestPayload**

   Refers to the complete request body. You must follow the following process to format the request payload:

   * Apply URI encoding as per the [RFC3986](https://tools.ietf.org/html/rfc3986) standard to the name and value of each query string parameter. For requests using the GET method, all relevant parameters, such as hash algorithms, credential scope, signature date, and signature headers, must be included.

   * Strictly sort the parameter names according to the ASCII character order.

   * Connect each sorted parameter name and the corresponding value with an equal sign ( = ), then concatenate these parameter pairs with ampersands ( & ) in the sorted order to form the final query string.


<span id="创建签名字符串"></span>
## Creating a signature string

The signature string contains the request and the metadata information of the canonical request. It consists of the signature algorithm, request date, credential scope, and the Base16\-encoded hash of the canonical request. The pseudocode for constructing the signature string is as follows:

```undefined
StringToSign = Algorithm + '\n' + RequestDate + '\n' + CredentialScope + '\n' + HexEncode(Hash(CanonicalRequest))
```



* **Algorithm**

   Refers to the signing algorithm. Currently, only HMAC\-SHA256 is supported.

* **RequestDate**

   Refers to the request time in UTC. Format: YYYYMMDD'T'HHMMSS'Z'.

* **CredentialScope**

   Refers to the credential scope. Format: *YYYYMMDD/region/ service/request*.

* **CanonicalRequest**

   Refers to the result of request normalization from the previous section.


<span id="计算签名秘钥（signing-key）"></span>
## Calculating a signing key

Before calculating the signature, derive the signing key from the private AccessKey pair (secret AccessKey) instead of using the private AccessKey pair directly. The calculation process is as follows:

```undefined
kSecret = *Your Secret Access Key*
kDate = HMAC(kSecret, Date)
kRegion = HMAC(kDate, Region)
kService = HMAC(kRegion, Service)
kSigning = HMAC(kService, "request")
```



1. Calculate the signature.

   ```undefined
    Signature = HexEncode(HMAC(kSigning, StringToSign))
   ```
   

2. Construct the header.

   ```undefined
    Authorization: HMAC-SHA256 Credential={AccessKeyId}/{CredentialScope}, SignedHeaders={SignedHeaders}, Signature={Signature}
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The items enclosed in <code>{}</code> are derived from the calculation processes detailed above.   </div>

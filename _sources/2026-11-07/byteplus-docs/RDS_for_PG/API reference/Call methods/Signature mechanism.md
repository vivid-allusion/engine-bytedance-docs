---
title: "Signature mechanism"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/signature_mechanism"
---

This topic introduces the signature mechanism for calling the RDS for PostgreSQL Open API. Signature encrypts request parameters to ensure requests are not tampered with during transmission.

<span id=".562-5ZCN5py65Yi2"></span>
## Signature example

The BytePlus manual signature mechanism requires the requester to perform hash calculation for the request parameters, encrypt the request parameters, and send them with the API request to the server.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_954668bec90d5bec0446f7aa9b44b488.png) </span>

<span id=".6I635Y-W6K6_6Zeu5a-G6ZKlQWNjZXNzIEtlee-8iQ=="></span>
### Getting the access key

The access key is the security credential for requesting the BytePlus OpenAPI. Refer to [Managing an access key ](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey)to retrieve the account's Access Key ID and Secret Access Key.

<span id=".5p6E5bu66KeE6IyD6K-35rGC5a2X56ym5Liy77yIQ2Fub25pY2FsUmVxdWVzdO-8iQ=="></span>
### Constructing canonical request strings (CanonicalRequest)

Before applying a signature, it is important to canonicalize the request to avoid objections during the signature calculation process. Construct the canonical request string. The specific process and pseudocode are as follows:

```plain
CanonicalRequest = 
    HTTPRequestMethod + '\n' + 
    CanonicalURI + '\n' + 
    CanonicalQueryString + '\n' + 、
    CanonicalHeaders + '\n' + 
    SignedHeaders + '\n' + 
    HexEncode(Hash(RequestPayload))
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>Hash</code> refers to <code>the SHA256 algorithm</code>, <code>HexEncode</code> refers to <code>hexadecimal encoding</code>, and <code>HMAC</code> refers to <code>HMAC_SHA256</code>.</div>



* **HTTPRequestMethod**

   HTTPRequestMethod refers to the HTTP request method, for example: GET or POST.

* **CanonicalURI**

   CanonicalURI refers to the normalized URI. If URI is empty, a forward slash ( / ) is used as the absolute path. The URI of most APIs in BytePlus is represented as ( / ).

* **CanonicalQueryString**

   Refers to the normalized Query String. For example:

   ```Plain Text
   CanonicalQueryString = "Action=ListUsers&Version=2018-01-01"
   ```
   

   The general process for normalizing the Query String is as follows:

   * URI\-encode each querystring parameter name and parameter value.

   * Sort parameter names strictly in ASCII byte order.

   * Concatenate sorted parameter names and values with equal signs ( = ) and the parameter pairs with ampersands ( & ) according to the sorting result.

* **CanonicalHeaders**

   CanonicalHeaders refers to the canonicalized Header. The pseudo code is as follows:

   ```Plain Text
   CanonicalHeaders =
   CanonicalHeadersEntry0 +
   CanonicalHeadersEntry1 + ... +
   CanonicalHeadersEntryN
   ```
   

   Among them,

   ```Plain Text
   CanonicalHeadersEntry = Lowercase(HeaderName) + ':' + Trimall(HeaderValue) + '\n'
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Lowcase converts all Header names to lowercase.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Trimall removes extra spaces before and after the header value.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Be sure to add the <code>\n</code> newline character at the end.   </div>
   

* **SignedHeaders**

   Refers to the names of Headers involved in the signature. Signature Header is the list of names included in the normalized Headers, which indicates which Headers participate in signature calculation, so any additional Headers added by a proxy can be ignored. If Host and X\-Date headers exist, they must be added. The pseudo code is as follows:

   ```Plain Text
   SignedHeaders = Lowercase(HeaderName0) + ';' + Lowercase(HeaderName1) + ";" + ... + Lowercase(HeaderNameN)
   ```
   

* **RequestPayload**

   Refers to the complete request body. Note the following:

   * URI\-encode (note: same as [RFC3986](https://tools.ietf.org/html/rfc3986) method) each querystring parameter name and parameter value.<|diff_marker|\>

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The GET method needs to include all parameters such as hash algorithm, credential, signature date, and signature header.<|diff_marker|\>      </div>
      

   * Sort parameter names strictly in ASCII byte order.

   * Concatenate sorted parameter names and values with equal signs ( = ) and the parameter pairs with ampersands ( & ) according to the sorting result.


<span id=".5p6E5bu65b6F562-5ZCN5a2X56ym5Liy77yIU3RyaW5nVG9TaWdu77yJ"></span>
### Constructing the string to sign (StringToSign)

A string to sign contains the metadata information of the request and request canonicalization and concatenates the signature algorithm, request date, credential, and canonical request hash value. The pseudocode is as follows:

```plain
StringToSign = Algorithm + '\n' + RequestDate + '\n' + CredentialScope + '\n' + HexEncode(Hash(CanonicalRequest))
```



* **Algorithm** refers to the signature algorithm. Currently, BytePlus supports the HMAC\-SHA256 signature algorithm only.

* **RequestDate** refers to the request UTC time in the following format: YYYYMMDD'T'HHMMSS'Z'.

* **CredentialScope** refers to credentials in the following format: *YYYYMMDD/region/ service/request*.

* **CanonicalRequest** refers to the canonical request result in the last section.


<span id=".6K6h566X562-5ZCN5a-G6ZKl77yIa1NpZ25pbmfvvIk="></span>
### Calculating the signing key (kSigning)

Before signature calculation, you must first use the secret access key of the access key to derive a signing key (kSigning). Access Key is the security credential for requesting BytePlus OpenAPI. Refer to [Managing an access key ](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey) to retrieve the account’s Access Key ID and Secret Access Key.

calculate the derived signing key, the calculation process and pseudocode are as follows:

```plain
kSecret = *Your Secret Access Key*
kDate = HMAC(kSecret, Date)
kRegion = HMAC(kDate, Region)
kService = HMAC(kRegion, Service)
kSigning = HMAC(kService, "request")
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">where Date is accurate to the day and is the same as the YYYYMMDD part in RequestDate.</div>


<span id=".6K6h566X562-5ZCN77yIU2lnbmF0dXJl77yJ"></span>
### Calculating the signature (Signature)

The pseudocode for calculating a signature is as follows:

```plain
Signature = HexEncode(HMAC(kSigning, StringToSign))
```


<span id=".5p6E5bu6IEF1dGhvcml6YXRpb24="></span>
### Constructing the Authorization parameter

The Authorization parameter of the header is constructed in the following format:

```plain
Authorization: HMAC-SHA256 Credential={AccessKeyId}/{CredentialScope}, SignedHeaders={SignedHeaders}, Signature={Signature}
```


<span id=".562-5ZCN56S65L6L"></span>
## Signature example

For more details, refer to [Signature example](https://docs.byteplus.com/en/docs/byteplus-platform/reference-example).

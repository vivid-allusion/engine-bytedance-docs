---
title: "Signature Mechanism"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/reference-signature-mechanism_1"
---

Each request to TOS is verified and needs to contain a signature. This topic describes the signature mechanism of TOS APIs.

<span id="f03951ec"></span>
## **Signature verification**

TOS verifies the signature to check the request sender's identity if the request is signed using the Access Key ID (AK) and Secret Access Key (SK).


* AK: It is the access key ID to identify a user.

* SK: It works with the AK to encrypt a signature.


To send a request to TOS as an individual, you need to construct a StringToSign in TOS format and encrypt it using your SK. Upon receiving the request, TOS calculates the signature using the same method. If the calculated signature matches the signature you provide, the request is valid; otherwise, TOS returns an HTTP 403 error.

You can include the signature in the request header or URL query parameters as needed.

<span id="5f4dacc8"></span>
## **Functions required to calculate signatures**


|**Function** |**Description** |
|---|---|
|UriEncode() |Encodes a string with the following restraints:<br><br><br>* All characters except `A`–`Z`, `a`–`z`, `0`–`9`, `-`, `.`, `_`, and `~` must be encoded.<br><br>* Spaces must be encoded as `%20` (not `+`).<br><br>* Each URI\-encoded byte is converted to a `%` + two hexadecimal digits. The hexadecimal representation must use uppercase letters.<br><br>* `/` must be encoded unless it is in an object name. |
|Lowercase() |Converts a string to lowercase. |
|Hex() |Performs hexadecimal encoding on a string. |
|SHA256Hash() |Implements the SHA\-256 algorithm. |
|HMAC\-SHA256() |Implements the HMAC\-SHA256 algorithm. |
|Trim() |Removes whitespaces from both sides of a string. |


<span id="8900fe34"></span>
## **Including a signature in the Authorization header**

You can include a signature in the Authorization header of an HTTP request.

The Authorization header value is derived as follows:

<span id="4593fdaa"></span>
### **Constructing a CanonicalRequest**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Hash() uses the SHA\-256 algorithm.</div>


* <div data-tips="true" data-tips-type="tip">HexEncode() converts text into hexadecimal encoding.</div>



```Plain
CanonicalRequest = 
    HTTPMethod + '\n' + 
    CanonicalURI + '\n' + 
    CanonicalQueryString + '\n' + 
    CanonicalHeaders + '\n' + 
    SignedHeaders + '\n' + 
    HashedPayload
```


Below are the parameters.


|**Parameter** |**Description** |
|---|---|
|HTTPMethod |The method used by the HTTP request, for example, PUT, GET, HEAD, or DELETE. |
|CanonicalURI |UriEncode(` *<PATH>* `)<br><br><br>* If `PATH` in the URL is empty, CanonicalURI is `/`.<br><br>* For example, if the complete URL is `[https://bucketname.tos-ap-southeast-1.bytepluses.com/object](https://bucketname.tos-ap-southeast-1.bytepluses.com/object)`, CanonicalURI is `/object`. |
|CanonicalQueryString |The request query parameters are concatenated as follows:<br><br>UriEncode(` *<QueryParam1>* `) + '=' + UriEncode(` *<value>* `) + '&' + UriEncode(` *<QueryParam2>* `) + '=' + UriEncode(` *<value>* `) + '&' +<br><br>...<br><br>UriEncode(` *<QueryParamN>* `) + '=' + UriEncode(` *<value>* `).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Sort the encoded query parameters as per ASCII values of the characters.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">All query parameters must be included.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If there are no query parameters, CanonicalQueryString is an empty string.</div><br> |
|CanonicalHeaders |The request headers are concatenated as follows:<br><br>Lowercase(` *<HeaderName1>* `) + ':' + Trim(` *<value>* `) + '\n'<br><br>Lowercase(` *<HeaderName2>* `) + ':' + Trim(` *<value>* `) + '\n'<br><br>...<br><br>Lowercase(` *<HeaderNameN>* `) +' :' + Trim(` *<value>* `) + '\n'.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Sort the HeaderNames in lexicographic order.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">CanonicalHeaders does not have to contain all header fields.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If the request contains the <code>Content-Type</code> header, it must be included in CanonicalHeaders.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The host header must be included in CanonicalHeaders.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When using the temporary AK/SK for authentication, the header <code>x-tos-security-token</code> must be present and included in CanonicalHeaders.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">All <code>x-tos-*</code> headers must be included in CanonicalHeaders.</div><br> |
|SignedHeaders |Indicates the headers involved in signing:<br><br>Lowercase (` *<HeaderName1>* `) + ';' + Lowercase (` *<HeaderName2>* `) + ... + Lowercase(` *<HeaderNameN>* `)<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Sort the HeaderNames in CanonicalHeaders in lexicographic order.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">HeaderNames in SignedHeaders must be present in the request header.</div><br> |
|HashedPayload |Hex(SHA256Hash(` *<payload>* `)<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This is the SHA\-256 hash of the request payload represented in hexadecimal.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If the request has no payload, calculate Hex(SHA256Hash("")) (using an empty string). The resultant value is e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">In presigning scenarios, you can use UNSIGNED\-PAYLOAD instead of calculating the payload.</div><br> |


<span id="e523599b"></span>
### **Constructing a StringToSign**

A StringToSign contains metadata of the request and canonical request. It is a concatenation of the signing algorithm, request date, credential scope, and hashed canonical request, as shown below:

```Plain
StringToSign = Algorithm + '\n' + RequestDate + '\n' + CredentialScope + '\n' + HexEncode(Hash(CanonicalRequest))
```


Below are the parameters:


|**Parameter** |**Description** |
|---|---|
|Algorithm |The signing algorithm. Currently, only the HMAC\-SHA256 algorithm is supported. |
|RequestDate |The UTC timestamp of the request in the format of `yyyyMMddTHHmmssZ`. |
|CredentialScope |The scope of your credentials in the format of `yyyyMMdd/region/tos/request`. |
|CanonicalRequest |The canonical request obtained in the previous section. |


<span id="48ec0548"></span>
## **Calculating SigningKey**

Before calculating the signature, derive SigningKey from the SK instead of using the latter directly. The calculation process is as follows:

```Plain
kSecret = *Your Secret Access Key*
kDate = HMAC-SHA256(kSecret, Date)
kRegion = HMAC-SHA256(kDate, Region)
kService = HMAC-SHA256(kRegion, "tos")
kSigning = HMAC-SHA256(kService, "request")
```


<span id="ba6837cb"></span>
## **Calculating the signature**

```Plain
Signature = HexEncode(HMAC-SHA256(kSigning, StringToSign))
```


Then, construct the header.

```Plain
Authorization: TOS4-HMAC-SHA256 Credential={AccessKeyId}/{CredentialScope}, SignedHeaders={SignedHeaders}, Signature={Signature}
```


The `{}` parts in the expression represent the intermediate values calculated above.

<span id="c977db1b"></span>
## **Sample case**

In this example, an object is downloaded from TOS. The relevant information is as follows.


|**Parameter** |**Value** |
|---|---|
|Bucket name |examplebucket |
|Object name |exampleobject |
|Region |ap\-southeast\-1 |
|Time |Sat, 1 Jan 2022 00:00:00 GMT |
|AccessKeyId |testAK |
|SecretAccessKey |testSK |


<span id="4b9a5428"></span>
### **CanonicalRequest**

```Plain
GET
/exampleobject

host:examplebucket.tos-ap-southeast-1.bytepluses.com
x-tos-content-sha256:e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
x-tos-date:20220101T000000Z

host;x-tos-content-sha256;x-tos-date
e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
```


<span id="22c18f3e"></span>
### **StringToSign**

```Plain
TOS4-HMAC-SHA256
20220101T000000Z
20220101/tos-ap-southeast-1/tos/request
c5b4f2fac36f0a3351d91753998bd811d1c446c186a2b3fb2b9e420630f13534
```


<span id="0cb3919e"></span>
### **SigningKey**

```Plain
HMAC-SHA256(HMAC-SHA256(HMAC-SHA256(HMAC-SHA256("testSK", "20220101"), "tos-ap-southeast-1"), "tos"), "request")
```


<span id="ca88ebe2"></span>
### **Signature**

```Plain
d40b66cf0054d1642843670d10fa095e1609c7896f25df217770b0abe717693b
```


<span id="73da2c49"></span>
### **Authorization header**

```Plain
TOS4-HMAC-SHA256 Credential=testAK/20220322/tos-ap-southeast-1/tos/request, SignedHeaders=host;x-tos-content-sha256;x-tos-date, Signature=d40b66cf0054d1642843670d10fa095e1609c7896f25df217770b0abe717693b
```

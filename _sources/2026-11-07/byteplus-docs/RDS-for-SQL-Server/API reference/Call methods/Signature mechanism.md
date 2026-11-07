---
title: "Signature mechanism"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/signature-mechanism"
---

The RDS for SQL Server service authenticates each request for access, so you need to include signature information in the request. This article describes the API signing mechanism for RDS for SQL Server.

<span id="create-a-regularization-request"></span>
## **Create a regularization request**

When accessing, the request needs to be signed as follows:

```plain
CanonicalRequest = HTTPRequestMethod + '\n' + CanonicalURI + '\n' + CanonicalQueryString + '\n' + CanonicalHeaders + '\n' + SignedHeaders + '\n' + HexEncode(Hash(RequestPayload))
```



* **HTTPRequestMethod** refers to the method of HTTP request, such as GET, POST, etc.

* **CanonicalURI** : Refers to the normalized URI. If the URI is empty, use (/) as the absolute path. In the Byteplus, the URI of most interfaces is (/).

* **CanonicalQueryString** Refers to the normalized Query String. For example:

   ```plain
   CanonicalQueryString = "Action=ListUsers&Version=2018-01-01"
   ```
   

   The process of normalizing a Query String is as follows:

   The URI encodes the parameter names and values of each querystring.

   * Strict ordering of parameter names in ASCII byte order, with different parameter values of the same parameter name maintaining the original order of the request.

   * Connect the sorted parameter names and parameter values with (=), and connect the **parameter pairs** with (&) according to the sorted results.

* **CanonicalHeaders** refer to normalized headers. The pseudocode is as follows:

   ```plain
   CanonicalHeaders = 
   CanonicalHeadersEntry0 + 
   CanonicalHeadersEntry1 + ... + 
   CanonicalHeadersEntryN
   ```
   

   * Of which,

      ```plain
      CanonicalHeadersEntry = Lowercase(HeaderName) + ':' + Trimall(HeaderValue) + '\n'
      ```
      

      * Lowcase stands for converting all header names to lowercase.

      * Trimall means to remove the extra spaces before and after the value of the Header.

      * Finally, you need to add a newline character `n`.

* **SignedHeaders** refers to the name of the header participating in the signature. The signature header is a list of names contained in the normalized headers. Its purpose is to specify which headers participate in the signature calculation, thus ignoring the additional headers added by the proxy. If the host and x\-date headers exist, they must be added. The pseudo\-code is as follows:

   ```plain
   SignedHeaders = Lowercase(HeaderName0) + ';' + Lowercase(HeaderName1) + ";" + ... + Lowercase(HeaderNameN)
   ```
   

* **RequestPayload** refers to the body of the complete request. The following points need to be noted:

   * URI encoding (Note: same as [RFC3986](https://tools.ietf.org/html/rfc3986) method) The parameter name and parameter value of each querystring.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The GET method needs to include all parameters such as the hash algorithm, certificate of trust, signature date, and signature header).   </div>
   

   * Strict ordering of parameter names in ASCII byte order.

   * Connect the sorted parameter names and parameter values with (=), and connect the **parameter pairs** with (&) according to the sorted results.

* Hash refers to the SHA256 algorithm.

* HexEncode proxy to hexadecimal encoding.


<span id="create-signature-string"></span>
## **Create signature string**

The signature string mainly contains the metadata information of the request and the regularization request. It consists of the signature algorithm, the request date, the trust certificate, and the regularization request hash value connection. The pseudo\-code is as follows:

```plain
StringToSign = Algorithm + '\n' + RequestDate + '\n' + CredentialScope + '\n' + HexEncode(Hash(CanonicalRequest))
```



* **Algorithm** refers to the signature algorithm. Currently, Byteplus only supports the signature algorithm of HMAC\-SHA256.

* **RequestDate** refers to the request UTC time, please use the following format: YYYYMMDD T'HHMMSS'Z '.

* **CredentialScope** refers to a certificate of trust in the format: \*YYYYMMDD/region/service/request \*.

* **CanonicalRequest** refers to the result of the regularization request in the previous section.


<span id="calculate-the-signing-key"></span>
## **Calculate the signing key**

Before computing the signature, first derive the signing key from the private access key, rather than using the private access key directly. The specific calculation process is as follows:

```plain
kSecret = Your Secret Access Key 
kDate = HMAC(kSecret, Date) 
kRegion = HMAC(kDate, Region) 
kService = HMAC(kRegion, Service) 
kSigning = HMAC(kService, "request")
```



1. Calculate the signature.

   ```plain
   Signature = HexEncode(HMAC(kSigning, StringToSign))
   ```
   

2. Build the Header.

   ```plain
   Authorization: HMAC-SHA256 Credential={AccessKeyId}/{CredentialScope}, SignedHeaders={SignedHeaders}, Signature={Signature}
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The contents of the expression enclosed in ({}) represent the intermediate process computed above.   </div>
   

<span id="signature-example"></span>
## **Signature example**

For more details, see [Signature Examples](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-signature).

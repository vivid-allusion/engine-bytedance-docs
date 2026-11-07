---
title: "API authentication"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-API-authentication"
---

To authenticate your API requests to BytePlus Live, you must create a valid signature and include it in your HTTP or HTTPS request. This guide provides a detailed, step\-by\-step procedure for generating this signature, ensuring your requests are successfully verified by the server.

<span id="background"></span>
## Background

When you send API requests to BytePlus Live, to verify the identity of the requester and to protect the API requests from being maliciously tampered during transmission, the BytePlus signature mechanism requires requesters to calculate a signature for request parameters and then transmit the signature to the API server together with the API request for authentication.

When BytePlus Live receives the request, it uses the same information to calculate the signature and matches it against the one in your request. If the values fail to match, the request is denied.

<span id="prerequisites"></span>
## Prerequisites


* Sign up for a BytePlus account. For more information, see [Signing up for a BytePlus account](https://docs.byteplus.com/en/byteplus-platform/docs/signing-up-your-account).

* Go to [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/) \> **User Profile** \> **IAM** \> **Key management** to get the AccessKey ID (AK) and Secret Access Key (SK) for API request authentication.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/c0c5750-Obtain_the_AccessKey_ID_and_AccessKey_secret.JPEG) </span>


<span id="process"></span>
## Process

The following process shows how to create a signed request.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/dac1414-Process.JPEG) </span>

<span id="procedure"></span>
## Procedure

This section takes `GetActivityAPI` as an example and explains how to sign a BytePlus Live API request.

The original request of `GetActivityAPI` before being signed is as follows.

```Plain
Get http://livesaas.byteplusapi.com/?Action=GetActivityAPI&Version=2020-06-01&ActivityId=1231231231
Host: livesaas.byteplusapi.com
Content-Type: application/x-www-form-urlencoded; charset=utf-8
X-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
X-Date: 20201230T081805Z
```


<span id="step-1-create-a-canonical-request"></span>
### Step 1: Create a canonical request

To start the signing process, create a request in a canonical format. This ensures that the signature calculated by BytePlus Live matches the one you calculate. If they are not the same, the request will be denied.

The following pseudocode shows how to create a canonical request:

```Plain
CanonicalRequest = HTTPRequestMethod + '\n' + CanonicalURI + '\n' + CanonicalQueryString + '\n' + CanonicalHeaders + '\n' + SignedHeaders + '\n' + HexEncode(Hash(RequestPayload))
```


Complete the following steps to create a canonical request:


1. Start with the HTTP request method (`HTTPRequestMethod`), such as `GET` and `POST`. In this example, the HTTP request method of `GetActivityAPI` is `GET`.

   ```Plain
   GET
   ```
   

2. Add the canonical URI (`CanonicalURI`) of an API request. The canonical URI is the URI\-encoded version of the absolute path component of the URI, which is after the host and before the question mark (`?`) that begins the query string parameters (if any).

   Normalize URI paths according to [RFC 3986](https://tools.ietf.org/html/rfc3986). Remove redundant and relative path components. Add a forward slash (`/`) at the end if the absolute path does not end with one.

   If the absolute path is empty, use a forward slash (`/`). In this example, nothing follows the host in the URI of `GetActivityAPI`, so the absolute path is empty, with the canonical URI as follows:

   ```Plain
   /
   ```
   

3. Add the canonical query string (`CanonicalQueryString`) of an API request. In this example, the query string of `GetActivityAPI` is as follows:

   ```Plain
   Action=GetActivityAPI&Version=2020-06-01&ActivityId=1231231231
   ```
   

   To construct the canonical query string, complete the following steps:

   1. URL\-encode each parameter name and value according to [RFC 3986](https://tools.ietf.org/html/rfc3986).

   2. Sort parameter names in ASCII order. For different values of the same parameter name, keep the original order in the request.

   3. Connect the sorted parameter names and their values with equal signs (`=`), and concatenate the parameter pairs into a string with ampersands (`&`).

      In this example, `GetActivityAPI` has the following canonical query string.

   ```Plain
   Action=GetActivityAPI&ActivityId=1231231231&Version=2020-06-01
   ```
   

4. Add the canonical headers (`CanonicalHeaders`), which consist of all the HTTP headers contained in the signed request.

   The following pseudocode shows how to add the canonical headers:

   ```Plain
   CanonicalHeaders = CanonicalHeadersEntry0 + CanonicalHeadersEntry1 + ... + CanonicalHeadersEntryN
   CanonicalHeadersEntry = Lowercase(HeaderName) + ':' + Trimall(HeaderValue) + '\n'
   ```
   

   Here,

   * `Lowercase`: Converts all the header names to lowercase.

   * `Trimall`: Removes extra spaces before and after header values.

      You must sort lowercase header names in ASCII order and add a line break (`\n`) at the end of each header.

      In this example, the canonical headers are as follows:

   ```Plain
   content-type:application/x-www-form-urlencoded; charset=utf-8\n
   host:livesaas.byteplusapi.com\n
   x-content-sha256:e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855\n
   x-date:20201230T081805Z\n
   ```
   

5. Add the signed headers (`SignedHeaders`). The value of `SignedHeaders` is the list of headers included in the canonical headers. By adding signed headers, you specify which headers in the request are used in the signing process to ignore additional headers added by a proxy.

   The `host` and `x-date` headers must be included as signed headers if they are included as HTTP headers.

   The following pseudocode shows how to add the signed headers:

   ```Plain
   SignedHeaders = Lowercase(HeaderName0) + ';' + Lowercase(HeaderName1) + ";" + ... + Lowercase(HeaderNameN)
   ```
   

   Convert all header names to lowercase, sort them in ASCII order, and separate them with semicolons (`;`).

   In this example, the signed headers are as follows:

   ```Plain
   content-type;host;x-content-sha256;x-date
   ```
   

6. Use SHA256 algorithm to create a hashed value from the payload, which is a byte array, in the body of the HTTP or HTTPS request. The hashed payload must be represented as a lowercase hexadecimal string.

   ```Plain
   HashedPayload = HexEncode(Hash(RequestPayload))
   ```
   

   Here,

   * `Hash` represents the SHA256 algorithm.

   * `HexEncode` represents the conversion to hexadecimal encoding in lowercase characters. For example, `HexEncode("z")` returns the value `7a` instead of `7A`.

      Both GET and POST requests have `RequestPayload`. In this example, the payload is empty. It is therefore appropriate to use an empty string as the input to the hash function. The hashed payload is `e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855`.

7. To construct the canonical request (`CanonicalRequest`), combine all the components from steps 1 to 6 as a single string, with each component ending with a newline character.

   In this example, the resulting canonical request is as follows:

   ```Plain
   GET
   /
   Action=GetActivityAPI&ActivityId=1231231231&Version=2020-06-01
   content-type:application/x-www-form-urlencoded; charset=utf-8
   host:livesaas.byteplusapi.com
   x-content-sha256:e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
   x-date:20201230T081805Z
   
   content-type;host;x-content-sha256;x-date
   e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
   ```
   

   An extra line must always remain between canonical headers and signed headers.


<span id="step-2-create-a-string-to-sign"></span>
### Step 2: Create a string to sign

The string to sign includes meta information about your request and the canonical request created in **Step 1: Create a canonical request**.

The following pseudocode shows how to create the string to sign:

```Plain
StringToSign = Algorithm + '\n' + RequestDate + '\n' + CredentialScope + '\n' + HexEncode(Hash(CanonicalRequest))
```


Here,


* `Algorithm`: The signing algorithm. Currently, only `HMAC-SHA256` is supported.

* `RequestDate`: UTC time when the API request is sent, which is the value of `X-Date` in the request header. Format: `YYYYMMDD'T'HHMMSS'Z'`. Example: `20201230T081805Z`.

* `CredentialScope`: The credential scope in the format `{YYYYMMDD}/{region}/{service}/request`. In this case, the value of `YYYYMMDD` must be the same as that of `YYYYMMDD` in `RequestDate`. For BytePlus Live, always use `ap-singapore-1` as the `region` and `livesaas` as the `service`. Example: `20201230/ap-singapore-1/livesaas/request`.

* `HexEncode(Hash(CanonicalRequest))`: Use the SHA256 algorithm to calculate the hash of the canonical request created in **Step 1: Create a canonical request**. Then, convert the result to be a lowercase hexadecimal string. Example: `ba542a51d36e6c5ba0901612efe1c86c5e6502ce5c842e77975dc7acc2503a1e`.


Separate fields with line breaks (`\n)`.

In this example, the resulting string to sign is as follows:

```Plain
HMAC-SHA256
20201230T081805Z
20201230/ap-singapore-1/livesaas/request
ba542a51d36e6c5ba0901612efe1c86c5e6502ce5c842e77975dc7acc2503a1e
```


<span id="step-3-calculate-a-signing-key"></span>
### Step 3: Calculate a signing key

Before calculating the signature, you must first calculate a signing key based on your Secret Access Key. The signing key is specific to the date, region, and service, which is more secure than your Secret Access Key.

Use your Secret Access Key to create a series of hash\-based message authentication codes (HMACs). The following pseudocode shows how to calculate the signing key:

```Plain
kSecret = *Your Secret Access Key*
kDate = HMAC(kSecret, Date)
kRegion = HMAC(kDate, Region)
kService = HMAC(kRegion, Service)
kSigning = HMAC(kService, "request")
```


Here,


* `HMAC(key, data)` represents an HMAC\-SHA256 function that returns output in binary format. The result of each hash function is the `key` for the next one.

* `Date` is in the format `YYYYMMDD`, and its value is the same as that of `YYYYMMDD` in `RequestDate` used in **Step 2: Create a string to sign**.

* Use `ap-singapore-1` as the `Region` and `livesaas` as the `Service`.


In some programming languages, the `key` and `data` may be in a different order.

In this example, the inputs to calculate a signing key are shown below. The `kSecret` is `TkdKbE1qSmpOVFJrTUdGbE5ABCDZbUV5Wm1RelpUQXlPR1ExTURsa01qVQ==`, though only for demonstration purposes. Replace with your own Secret Access Key when calculating the signing key.

```Plain
HMAC(HMAC(HMAC(HMAC(kSecret,"20201230"),"ap-singapore-1"),"livesaas"),"request")
```


The signing key resulting from the preceding HMAC hash operations is then provided as below. Note that it shows the hexadecimal representation of each byte in the binary signing key.

```Plain
1e952b8ff47aaee5d7cf0b43aa295d6820ef5a0940bfaf59d4623c3d50d41e3
```


<span id="step-4-calculate-the-signature"></span>
### Step 4: Calculate the signature

Use the preceding signing key created in **Step 3: Calculate a signing key** and the string to sign created in **Step 2: Create a string to sign** as inputs to the HMAC\-SHA256 function and then convert the binary value to a hexadecimal representation in lowercase characters.

The following pseudocode shows how to calculate the signature:

```Plain
Signature = HexEncode(HMAC(Signingkey, StringToSign))
```


In some programming languages, the `Signingkey` and `StringToSign` may be in a different order.

In this example, the resulting signature is as follows:

```Plain
11a2e7bb9db7ee7ea2e4d7f3d6989a65dc3bb5feedf3aae50ba1b3313fe0093a
```


<span id="step-5-add-the-signature-to-the-http-or-https-request"></span>
### Step 5: Add the signature to the HTTP or HTTPS request

After calculating the signature, add it to the HTTP or HTTPS request in one of the following ways to authenticate who sent the request:


* The HTTP header `Authorization`.

* The query string.


<span id="adding-signing-information-to-the-authorization-header"></span>
#### Adding signing information to the `Authorization` header

The following pseudocode shows how to construct the `Authorization` header:

```Plain
Authorization: Algorithm Credential={AccessKeyId}/{CredentialScope}, SignedHeaders={SignedHeaders}, Signature={Signature}
```


Here,


* `Algorithm`: The signing algorithm `HMAC-SHA256`.

* `AccessKeyId`: Your AccessKey ID. For more information, see **Prerequisites**.

* `CredentialScope`: The credential scope. For more information, see **Step 2: Create a string to sign**.

* `SignedHeaders`: The signed headers. For more information, see **Step 1: Create a canonical request**.

* `Signature`: The calculated signature. The signature confirms your identity to BytePlus Live. For more information, see **Step 4: Calculate the signature**.


The `Authorization` header is constructed after you calculate the signature, so it is not included in the signed headers.

In this example, the `Authorization` header is as follows:

```Plain
Authorization: HMAC-SHA256 Credential=AKAPY2RhYmQzODhhYTg4NGZmNTk3ZGUxODk3ODgzYTA****/20201230/ap-singapore-1/livesaas/request, SignedHeaders=content-type;host;x-content-sha256;x-date, Signature=11a2e7bb9db7ee7ea2e4d7f3d6989a65dc3bb5feedf3aae50ba1b3313fe0093a
```


Then, the signed request of `GetActivityAPI` is as follows:

```Plain
Get http://livesaas.byteplusapi.com/?Action=GetActivityAPI&Version=2020-06-01&ActivityId=1231231231
Authorization: HMAC-SHA256 Credential=AKAPY2RhYmQzODhhYTg4NGZmNTk3ZGUxODk3ODgzYTA****/20201230/ap-singapore-1/livesaas/request, SignedHeaders=content-type;host;x-content-sha256;x-date, Signature=11a2e7bb9db7ee7ea2e4d7f3d6989a65dc3bb5feedf3aae50ba1b3313fe0093a
Host: livesaas.byteplusapi.com
Content-Type: application/x-www-form-urlencoded; charset=utf-8
X-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
X-Date: 20201230T081805Z
```


<span id="adding-signing-information-to-the-query-string"></span>
#### Adding signing information to the query string

The following pseudocode shows how to construct the query string that includes the signing information and then add it to the end of your original query string:

```Plain
X-Algorithm=algorithm&X-Credential=credential&X-Date=date&X-Expires=time&X-SignedHeaders=signedheaders&X-Signature=signature
```


Here,


* `Algorithm`: The signing algorithm `HMAC-SHA256`.

* Credential: A combination of your AccessKey ID and the credential scope, in the format `AccessKeyId/CredentialScope`. For more information about the AccessKey ID and credential scope, see Prerequisites and Step 2: Create a string to sign.

* `X-Date`: UTC time when the API request was sent. You can find the parameter value in the request. In this example, the value is `20201230T081805Z`.

* X\-Expires: The validity period of your signature, in seconds. This is an optional parameter with a default value of 900. If you want to set the parameter value, we recommend a small value to be safe, since the resulting query string contains everything required to make a successful call to BytePlus Live.

* `SignedHeaders`: The signed headers. For more information, see **Step 1: Create a canonical request**.

* `Signature`: The calculated signature. The signature confirms your identity to BytePlus Live. For more information, see **Step 4: Calculate the signature**.


Use an equal sign (=) to connect a parameter and its value and separate parameter\-value pairs with ampersands (&). URL\-encode each parameter name and value according to RFC 3986. In this example, you must URL\-encode the forward slash (/) in the Credential value (AccessKeyId/CredentialScope) to %2F, and the semicolons (;) in the SignedHeaders value to %3B.

In this example, the resulting query string is as follows:

```Plain
Action=GetActivityAPI&Version=2020-06-01&ActivityId=1231231231&X-Algorithm=HMAC-SHA256&X-Credential=AKAPY2RhYmQzODhhYTg4NGZmNTk3ZGUxODk3ODgzYTA****%2F20201230%2Fap-singapore-1%2Flivesaas%2Frequest&X-Date=20201230T081805Z&X-Expires=60&X-SignedHeaders=content-type%3Bhost%3Bx-content-sha256%3Bx-date&X-Signature=11a2e7bb9db7ee7ea2e4d7f3d6989a65dc3bb5feedf3aae50ba1b3313fe0093a
```


Then, the signed request of `GetActivityAPI` is as follows:

```Plain
Get http://livesaas.byteplusapi.com/?Action=GetActivityAPI&Version=2020-06-01&ActivityId=1231231231&X-Algorithm=HMAC-SHA256&X-Credential=AKAPY2RhYmQzODhhYTg4NGZmNTk3ZGUxODk3ODgzYTA****%2F20201230%2Fap-singapore-1%2Flivesaas%2Frequest&X-Date=20201230T081805Z&X-Expires=60&X-SignedHeaders=content-type%3Bhost%3Bx-content-sha256%3Bx-date&X-Signature=11a2e7bb9db7ee7ea2e4d7f3d6989a65dc3bb5feedf3aae50ba1b3313fe0093a
Host: livesaas.byteplusapi.com
Content-Type: application/x-www-form-urlencoded; charset=utf-8
X-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
```

---
title: "Signing BytePlus MediaLive requests"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-signing-byteplus-medialive-requests"
---

This topic describes how to create a signature and add it to an HTTP or HTTPS request sent to BytePlus MediaLive.

<span id="Background"></span>
## Background

When you send API requests to BytePlus MediaLive to verify the identity of the requester and protect the API requests from tampering during transmission, the BytePlus signature mechanism requires requesters to calculate a signature for request parameters, and then transmit the signature to the API server together with the API request for authentication. When BytePlus MediaLive receives the request, it uses the same information to calculate the signature and matches it against the one in your request. If the values don't match, the request is denied.

<span id="Preparation"></span>
## Preparation


1. Sign up for a BytePlus account. For more information, see [Signing up for a BytePlus account](https://docs.byteplus.com/byteplus-platform/docs/signing-up-your-account).

2. Log in to the [BytePlus console](https://console.byteplus.com/home).

3. Click your username in the upper\-right corner of the page and select **IAM**.

4. On the left navigation pane, click **Key management**.

5. Obtain the AccessKey ID and AccessKey secret, which are used for API request authentication.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/5ddc848-accesskey.png) </span>

<span id="Process"></span>
## Process

The following process shows how to create a signed request.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/dac1414-Process.JPEG) </span>

<span id="Procedure"></span>
## Procedure

This section takes `DescribeLiveDomainLog` as an example and explains how to sign a BytePlus MediaLive API request.

The original request of `DescribeLiveDomainLog` before being signed is as follows.

```plain
GET http://open.byteplusapi.com/?Action=DescribeLiveDomainLog&Version=2020-08-01
Host: open.byteplusapi.com
Content-Type: application/x-www-form-urlencoded; charset=utf-8
X-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
X-Date: 20201230T081805Z
```


<span id="Step 1: Create a canonical request"></span>
### Step 1: Create a canonical request

To start the signing process, create a request in a canonical format. In this way, the signature calculated by BytePlus MediaLive is the same as the one calculated by you. If they are not the same, the request will be denied.

The following pseudocode shows how to create a canonical request:

```plain
CanonicalRequest = HTTPRequestMethod + '\n' + CanonicalURI + '\n' + CanonicalQueryString + '\n' + CanonicalHeaders + '\n' + SignedHeaders + '\n' + HexEncode(Hash(RequestPayload))
```


Complete the following steps to create a canonical request:


1. Start with the HTTP request method (`HTTPRequestMethod`), such as `GET` and `POST`. In this example, the HTTP request method of `DescribeLiveDomainLog` is `GET`.

   ```plain
   GET
   ```
   

2. Add the canonical URI (`CanonicalURI`) of an API request. The canonical URI is the URI\-encoded version of the absolute path component of the URI, which is after the host and before the question mark (`?`) that precedes the query string parameters (if any).

   Normalize URI paths according to [RFC 3986](https://tools.ietf.org/html/rfc3986). Remove redundant and relative path components. Add a forward slash (`/`) at the end if the absolute path does not end with one.

   If the absolute path is empty, use a forward slash (`/`). In this example, nothing follows the host in the URI of `DescribeLiveDomainLog`, so the absolute path is empty and the canonical URI is as follows:

   ```plain
   /
   ```
   

3. Add the canonical query string (`CanonicalQueryString`) of an API request. In this example, the query string of `DescribeLiveDomainLog` is as follows:

   ```plain
   Action=DescribeLiveDomainLog&Version=2020-08-01
   ```
   

   To construct the canonical query string, complete the following steps:

   1. URL\-encode each parameter name and value according to [RFC 3986](https://tools.ietf.org/html/rfc3986).

   2. Sort parameter names in ASCII order. For different values of the same parameter name, keep the original order in the request.

   3. Connect the sorted parameter names and their values with equal signs (`=`), and concatenate the parameter pairs into a string with ampersands (`&`).

      In this example, `DescribeLiveDomainLog` has the following canonical query string.

   ```plain
   Action=DescribeLiveDomainLog&Version=2020-08-01
   ```
   

4. Add the canonical headers (`CanonicalHeaders`). The canonical headers consist of all the HTTP headers contained in the signed request.

   The following pseudocode shows how to add the canonical headers:

   ```plain
   CanonicalHeaders = CanonicalHeadersEntry0 + CanonicalHeadersEntry1 + ... + CanonicalHeadersEntryN
   CanonicalHeadersEntry = Lowercase(HeaderName) + ':' + Trimall(HeaderValue) + '\n'
   ```
   

   Where,

   * `Lowercase`: Converts all the header names to lowercase.

   * `Trimall`: Removes extra spaces before and after header values.

      **Warning**: You must sort lowercase header names in ASCII order and add a line break (`\n`) at the end of each header.

      In this example, the canonical headers are as follows:

   ```plain
   content-type:application/x-www-form-urlencoded; charset=utf-8\n
   host:open.byteplusapi.com\n
   x-content-sha256:e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855\n
   x-date:20201230T081805Z\n
   ```
   

5. Add the signed headers (`SignedHeaders`). The value of `SignedHeaders` is the list of headers included in the canonical headers. By adding signed headers, you specify which headers in the request are used in the signing process to ignore additional headers added by a proxy.

   The `host` and `x-date` headers must be included as signed headers if they are included as HTTP headers.

   The following pseudocode shows how to add the signed headers:

   ```plain
   SignedHeaders = Lowercase(HeaderName0) + ';' + Lowercase(HeaderName1) + ";" + ... + Lowercase(HeaderNameN)
   ```
   

   Convert all header names to lowercase, sort them in ASCII order, and separate them with semicolons (`;`).

   In this example, the signed headers are as follows:

   ```plain
   content-type;host;x-content-sha256;x-date
   ```
   

6. Use SHA256 algorithm to create a hashed value from the payload, which is a byte array, in the body of the HTTP or HTTPS request. The hashed payload must be represented as a lowercase hexadecimal string.

   ```plain
   HashedPayload = HexEncode(Hash(RequestPayload))
   ```
   

   Where,

   * `Hash` represents the SHA256 algorithm.

   * `HexEncode` represents the conversion to hexadecimal encoding in lowercase characters. For example, `HexEncode("z")` returns the value `7a` instead of `7A`.

      Both GET and POST requests have `RequestPayload`. In this example, the payload is empty. Therefore, use an empty string as the input to the hash function. The hashed payload is `e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855`.

7. To construct the canonical request (`CanonicalRequest`), combine all the components from steps 1 to 6 as a single string, with each component ending with a newline character.

   In this example, the resulting canonical request is as follows:

   ```plain
   GET
   /
   Action=DescribeLiveDomainLog&Version=2020-08-01
   content-type:application/x-www-form-urlencoded; charset=utf-8
   host:open.byteplusapi.com
   x-content-sha256:e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
   x-date:20201230T081805Z
   
   content-type;host;x-content-sha256;x-date
   e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
   ```
   

   **Warning**: An extra line exists between canonical headers and signed headers.


<span id="Step 2: Create a string to sign"></span>
### Step 2: Create a string to sign

The string to sign includes meta information about your request and about the canonical request created in [Step 1: Create a canonical request](/docs/byteplus\-media\-live/docs\-signing\-byteplus\-medialive\-requests#Step 1: Create a canonical request).

The following pseudocode shows how to create the string to sign:

```plain
StringToSign = Algorithm + '\n' + RequestDate + '\n' + CredentialScope + '\n' + HexEncode(Hash(CanonicalRequest))
```


Where,


* `Algorithm`: The signing algorithm. Currently, only `HMAC-SHA256` is supported.

* `RequestDate`: UTC time when the API request is sent, which is the value of `X-Date` in the request header. Format: `YYYYMMDD'T'HHMMSS'Z'` Example: `20201230T081805Z`

* `CredentialScope`: The credential scope in the format `YYYYMMDD/region/service/request`. Here, the value of `YYYYMMDD` must be the same as that of `YYYYMMDD` in `RequestDate`. For BytePlus MediaLive, always use `ap-singapore-1` as the `region` and `live` as the `service`. Example: `20201230/ap-singapore-1/live/request`.

* `HexEncode(Hash(CanonicalRequest))`: Use SHA256 algorithm to calculate the hash of the canonical request created in [Step 1: Create a canonical request](/docs/byteplus\-media\-live/docs\-signing\-byteplus\-medialive\-requests#Step 1: Create a canonical request), and convert the result to be a lowercase hexadecimal string. Example: `ba542a51d36e6c5ba0901612efe1c86c5e6502ce5c842e77975dc7acc2503a1e`


**Warning**: Separate fields with line breaks (`\n)`.

In this example, the resulting string to sign is as follows:

```plain
HMAC-SHA256
20201230T081805Z
20201230/ap-singapore-1/live/request
ba542a51d36e6c5ba0901612efe1c86c5e6502ce5c842e77975dc7acc2503a1e
```


<span id="Step 3: Calculate a signing key"></span>
### Step 3: Calculate a signing key

Before calculating the signature, you must calculate a signing key based on your AccessKey secret. The signing key is specific to the date, region, and service, which is more secure than your AccessKey secret.

Use your AccessKey secret to create a series of hash\-based message authentication codes (HMACs). The following pseudocode shows how to calculate the signing key:

```plain
kSecret = *Your AccessKey Secret*
kDate = HMAC(kSecret, Date)
kRegion = HMAC(kDate, Region)
kService = HMAC(kRegion, Service)
kSigning = HMAC(kService, "request")
```


Where,


* `HMAC(key, data)` represents an HMAC\-SHA256 function that returns output in binary format. The result of each hash function is the `key` for the next one.

* `Date` is in the format `YYYYMMDD`, and its value is the same as that of `YYYYMMDD` in `RequestDate` used in [Step 2: Create a string to sign](/docs/byteplus\-media\-live/docs\-signing\-byteplus\-medialive\-requests#Step 2: Create a string to sign).

* Use `ap-singapore-1` as the `Region` and `live` as the `Service`.


**Note**: For some programming languages, the `key` and `data` might be in a different order.

In this example, the inputs to calculate a signing key are as follows and the `kSecret` is `TkdKbE1qSmpOVFJrTUdGbE5ABCDZbUV5Wm1RelpUQXlPR1ExTURsa01qVQ==`. The `kSecret` here is only for demonstration purposes. Replace with your own AccessKey secret when calculating the signing key.

```plain
HMAC(HMAC(HMAC(HMAC(kSecret,"20201230"),"ap-singapore-1"),"live"),"request")
```


The signing key resulting from the preceding HMAC hash operations is as follows, which shows the hexadecimal representation of each byte in the binary signing key.

```plain
1e952b8ff47aaee5d7cf0b43aa295d6820ef5a0940bfaf59d4623c3d50d41e3
```


<span id="Step 4: Calculate the signature"></span>
### Step 4: Calculate the signature

Use the preceding signing key created in [Step 3: Calculate a signing key](/docs/byteplus\-media\-live/docs\-signing\-byteplus\-medialive\-requests#Step 3: Calculate a signing key) and the string to sign created in [Step 2: Create a string to sign](/docs/byteplus\-media\-live/docs\-signing\-byteplus\-medialive\-requests#Step 2: Create a string to sign) as inputs to the HMAC\-SHA256 function, and then convert the binary value to a hexadecimal representation in lowercase characters.

The following pseudocode shows how to calculate the signature:

```plain
Signature = HexEncode(HMAC(Signingkey, StringToSign))
```


**Note**: For some programming languages, the `Signingkey` and `StringToSign` might be in a different order.

In this example, the resulting signature is as follows:

```plain
11a2e7bb9db7ee7ea2e4d7f3d6989a65dc3bb5feedf3aae50ba1b3313fe0093a
```


<span id="Step 5: Add the signature to the HTTP or HTTPS request"></span>
### Step 5: Add the signature to the HTTP or HTTPS request

After calculating the signature, add it to the HTTP or HTTPS request in one of the following ways to authenticate who sent the request:


* The HTTP header `Authorization`

* The query string


<span id="Adding signing information to the Authorization header"></span>
#### Adding signing information to the `Authorization` header

The following pseudocode shows how to construct the `Authorization` header:

```plain
Authorization: Algorithm Credential={AccessKeyId}/{CredentialScope}, SignedHeaders={SignedHeaders}, Signature={Signature}
```


Where,


* `Algorithm`: The signing algorithm `HMAC-SHA256`.

* `AccessKeyId`: Your AccessKey ID. For more information, see [Preparation](https://docs.byteplus.com/docs/byteplus-media-live/docs-signing-byteplus-medialive-requests#Preparation).

* `CredentialScope`: The credential scope. For more information, see [Step 2: Create a string to sign](/docs/byteplus\-media\-live/docs\-signing\-byteplus\-medialive\-requests#Step 2: Create a string to sign).

* `SignedHeaders`: The signed headers. For more information, see [Step 1: Create a canonical request](/docs/byteplus\-media\-live/docs\-signing\-byteplus\-medialive\-requests#Step 1: Create a canonical request).

* `Signature`: The calculated signature. The signature confirms your identity to BytePlus MediaLive. For more information, see [Step 4: Calculate the signature](/docs/byteplus\-media\-live/docs\-signing\-byteplus\-medialive\-requests#Step 4: Calculate the signature).


**Note**: The `Authorization` header is constructed after you calculate the signature, so it is not included in the signed headers.

In this example, the `Authorization` header is as follows:

```plain
Authorization: HMAC-SHA256 Credential=AKAPY2RhYmQzODhhYTg4NGZmNTk3ZGUxODk3ODgzYTA****/20201230/ap-singapore-1/live/request, SignedHeaders=content-type;host;x-content-sha256;x-date, Signature=11a2e7bb9db7ee7ea2e4d7f3d6989a65dc3bb5feedf3aae50ba1b3313fe0093a
```


Then, the signed request of `DescribeLiveDomainLog` is as follows:

```plain
GET http://open.byteplusapi.com/?Action=DescribeLiveDomainLog&Version=2020-08-01
Authorization: HMAC-SHA256 Credential=AKAPY2RhYmQzODhhYTg4NGZmNTk3ZGUxODk3ODgzYTA****/20201230/ap-singapore-1/live/request, SignedHeaders=content-type;host;x-content-sha256;x-date, Signature=11a2e7bb9db7ee7ea2e4d7f3d6989a65dc3bb5feedf3aae50ba1b3313fe0093a
Host: open.byteplusapi.com
Content-Type: application/x-www-form-urlencoded; charset=utf-8
X-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
X-Date: 20201230T081805Z
```


<span id="Adding signing information to the query string"></span>
#### Adding signing information to the query string

The following pseudocode shows how to construct the query string that includes the signing information and then add it to the end of your original query string:

```plain
X-Algorithm=algorithm&X-Credential=credential&X-Date=date&X-Expires=time&X-SignedHeaders=signedheaders&X-Signature=signature
```


Where,


* `Algorithm`: The signing algorithm `HMAC-SHA256`.

* `Credential` *:*  A combination of your AccessKey ID and the credential scope, that is, `AccessKeyId/CredentialScope`. For more information about the AccessKey ID and credential scope, see [Preparation](https://docs.byteplus.com/docs/byteplus-media-live/docs-signing-byteplus-medialive-requests#Preparation) and [Step 2: Create a string to sign](/docs/byteplus\-media\-live/docs\-signing\-byteplus\-medialive\-requests#Step 2: Create a string to sign).

* `X-Date`: UTC time when the API request was sent. You can find the parameter value in the request. In this example, the value is `20201230T081805Z`.

* `X-Expires`: The validity period of your signature. This is an optional parameter, with the default value 900 (unit: seconds). If you want to set the parameter value, we recommend a small value for security, since the resulting query string contains everything required to make a successful call to BytePlus MediaLive.

* `SignedHeaders`: The signed headers. For more information, see [Step 1: Create a canonical request](/docs/byteplus\-media\-live/docs\-signing\-byteplus\-medialive\-requests#Step 1: Create a canonical request).

* `Signature`: The calculated signature. The signature confirms your identity to BytePlus MediaLive. For more information, see [Step 4: Calculate the signature](/docs/byteplus\-media\-live/docs\-signing\-byteplus\-medialive\-requests#Step 4: Calculate the signature).


Use an equal sign (=) to connect a parameter and its value and separate parameter\-value pairs with ampersands (&). URL\-encode each parameter name and value according to [RFC 3986](https://tools.ietf.org/html/rfc3986). In this example, you only need to convert the forward slash (`/`) into `%2F` in `AccessKeyId/CredentialScope`, the value of `Credential`, and convert the semicolon (`;`) into `%3B` in the signed headers, the value of `SignedHeaders`.

In this example, the resulting query string is as follows:

```plain
Action=DescribeLiveDomainLog&Version=2020-08-01&X-Algorithm=HMAC-SHA256&X-Credential=AKAPY2RhYmQzODhhYTg4NGZmNTk3ZGUxODk3ODgzYTA****%2F20201230%2Fap-singapore-1%2Flive%2Frequest&X-Date=20201230T081805Z&X-Expires=60&X-SignedHeaders=content-type%3Bhost%3Bx-content-sha256%3Bx-date&X-Signature=11a2e7bb9db7ee7ea2e4d7f3d6989a65dc3bb5feedf3aae50ba1b3313fe0093a
```


Then, the signed request of `DescribeLiveDomainLog` is as follows:

```plain
GET http://open.byteplusapi.com/?Action=DescribeLiveDomainLog&Version=2020-08-01&X-Algorithm=HMAC-SHA256&X-Credential=AKAPY2RhYmQzODhhYTg4NGZmNTk3ZGUxODk3ODgzYTA****%2F20201230%2Fap-singapore-1%2Flive%2Frequest&X-Date=20201230T081805Z&X-Expires=60&X-SignedHeaders=content-type%3Bhost%3Bx-content-sha256%3Bx-date&X-Signature=11a2e7bb9db7ee7ea2e4d7f3d6989a65dc3bb5feedf3aae50ba1b3313fe0093a
Host: open.byteplusapi.com
Content-Type: application/x-www-form-urlencoded; charset=utf-8
X-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
```


<span id="Additional resources"></span>
## Additional resources

You do not need to manually complete the signing process if you can find the SDK for your programming language [here](https://docs.byteplus.com/byteplus-media-live/docs/server-sdk) as these SDKs are integrated with the signature mechanism.

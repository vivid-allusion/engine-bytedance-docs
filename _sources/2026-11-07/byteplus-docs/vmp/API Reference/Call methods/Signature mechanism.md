---
title: "Signature mechanism"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Signature-mechanism"
---

BytePlus verifies the identity of each request initiator based on the access key, including the Access Key ID and Secret Access Key, in the signature information of each HTTPS request.

<span id=".6I635Y-W6K6_6Zeu5a-G6ZKl"></span>
## Getting a secret key

Accounts and authorized users can create an access key by performing the following steps:


1. Log in to the [Identity and Access Management console](https://console.byteplus.com/iam) as a root user or an IAM user who has access to the Access Key Management.

2. Select **Access Key Management** in the left navigation bar.

3. View the list of access keys for your account.

   * Each account can have up to 2 access keys.

   * Click **Create Access Key** to create a new access key. After the new key is created, click **View AccessKey** to see the details.


<span id=".5Yib5bu65LiA5Liq5q2j6KeE5YyW6K-35rGC"></span>
## Creating a canonical request

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Hash refers to the SHA256 algorithm.</div>


* <div data-tips="true" data-tips-type="tip">HexEncode refers to hexadecimal encoding.</div>



```Plain Text
CanonicalRequest = HTTPRequestMethod + '\n' + CanonicalURI + '\n' + CanonicalQueryString + '\n' + CanonicalHeaders + '\n' + SignedHeaders + '\n' + HexEncode(Hash(RequestPayload))

```


Before applying a signature, the request needs to be canonicalized first. The following table contains the fields and pseudocodes used for canonicalization:


|Field |Descriptions |
|---|---|
|HTTPRequestMethod |HTTP request method, e.g., POST. |
|CanonicalURI |Canonicalized URI. If the URI is empty, use `/` as the absolute path. |
|CanonicalQueryString |Canonicalized query string. The steps to canonicalize query strings:<br><br><br>1. Each query parameter name and value needs to be converted using URL encoding (UrlEncode)<br><br>2. Sort the parameter names in ASCII byte order.<br><br>3. Connect each sorted parameter name and value with `=`, and connect the sorted parameter pairs with `&`.<br><br>   ```Plain Text```<br>```   CanonicalQueryString = "Action=ListUsers&Version=2018-01-01"```<br>```   ```<br>    |
|CanonicalHeaders |Canonicalized header. The pseudocode is as follows:<br><br>```Plain Text```<br>```CanonicalHeaders = CanonicalHeadersEntry0 + CanonicalHeadersEntry1 + ... + CanonicalHeadersEntryN```<br><br><br>```Plain Text```<br>```CanonicalHeadersEntry = Lowercase(HeaderName) + ':' + Trimall(HeaderValue) + '\n'```<br><br><br>In the above pseudocodes, `Lowercase` means converting the header names to lowercase, and `Trimall` means removing extra spaces before and after header values.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">A line break <code>\\n</code> is required at the end.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The order of headers is sorted by lowercase ASCII characters of <code>headerName</code>.</div><br> |
|SignedHeaders |The names of the headers involved in the signature.<br><br>The headers involved in signature generation must be included during canonicalization, with the purpose of ignoring those headers added by proxies. The headers `host` and `x-date`,  if exist, need to be included anyway.<br><br>The pseudocode is as follows:<br><br>```Plain Text```<br>```SignedHeaders = Lowercase(HeaderName0) + ';' + Lowercase(HeaderName1) + ";" + ... + Lowercase(HeaderNameN)```<br> |
|RequestPayload |The complete request body.<br><br><br>* Each query parameter name and value needs to be converted using URL encoding (same as the [RFC3986](https://tools.ietf.org/html/rfc3986) method)<br><br>   For the GET method, all parameters, such as the hash algorithm, credential, signing date, and signed headers, must be included.<br><br>* Sort the parameter names in ASCII byte order.<br><br>* Connect each sorted parameter name and value with `=`, and connect the sorted parameter pairs with `&`. |


<span id=".5Yib5bu6562-5ZCN5a2X56ym5Liy"></span>
## Creating a signature string

A signature string is generally made up of a request and the related metadata. In detail, it includes a signature algorithm, request date, credential, and a hash value of the canonicalized request. The pseudocode is as follows:

```Plain Text
StringToSign = Algorithm + '\n' + RequestDate + '\n' + CredentialScope + '\n' + HexEncode(Hash(CanonicalRequest))
```


The following table shows the fields used above.


|Field |Descriptions |
|---|---|
|Algorithm |The signature algorithm. Currently, BytePlus only supports the HMAC\-SHA256 signature algorithm. |
|RequestDate |Request UTC time. Please use the `YYYYMMDD'T'HHMMSS'Z'` format. |
|CredentialScope |Credential scope. The format is `YYYYMMDD/region/service/request`. |
|CanonicalRequest |The canonicalized request produced previously. |


<span id=".6K6h566X562-5ZCN56eY6ZKl"></span>
## Calculating a signing key


1. A signing key needs to be calculated first by using the Secret Access Key before getting the signature. The calculation steps are shown below:

   ```Plain Text
   kSecret = *Your Secret Access Key*
   kDate = HMAC(kSecret, Date)
   kRegion = HMAC(kDate, Region)
   kService = HMAC(kRegion, Service)
   kSigning = HMAC(kService, "request")
   ```
   

2. Calculate the signature.

   ```Plain Text
   Signature = HexEncode(HMAC(kSigning, StringToSign))
   ```
   

3. Construct the headers.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the pseudocode,<code>{}</code>\-enclosed content represents the intermediate results calculated in the preceding steps.   </div>
   

   ```Plain Text
   Authorization: HMAC-SHA256 Credential={AccessKeyId}/{CredentialScope}, SignedHeaders={SignedHeaders}, Signature={Signature}
   ```
   


<span id=".562-5ZCN56S65L6L5ZKMIFNESw=="></span>
## Signature examples and SDKs

<span id=".562-5ZCN56S65L6L"></span>
### Signature examples

The preceding pseudocode examples help you understand how signatures are calculated. We also provide a Signature Process Demo for your reference.

<span id=".U0RLIOWPguiAgw=="></span>
### SDK reference

BytePlus OpenAPI provides SDKs in different languages, such as Java, Golang, PHP, Python, and Node.js. You can use the SDKs to call product OpenAPIs or use only the signature method provided by the SDKs to avoid manually coding the signature logic.

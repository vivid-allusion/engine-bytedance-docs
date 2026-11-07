---
title: "Signature mechanism"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Signature_mechanism"
---

For each HTTPS protocol access request, system verifies the identity of the requester using the access keys in the access signature information, including Access Key ID and Secret Access Key.

<span id=".6I635Y-W6K6_6Zeu5a-G6ZKl"></span>
## Obtain access keys

Accounts and authorized users can create new access keys. The actions are as follows:


1. Log in to the [Access control console](https://console.byteplus.com/iam) using the main account or an IAM user with key management permissions.

2. In the left navigation bar, select **Resource management \> Key management**.

3. View the list of access keys for your account.

   * Each account can have up to 2 access keys at the same time.

   * If the current account has not reached the maximum number of access keys, you can click **Create Key** to create a new access key. After creation is complete, click **View AccessKey details** to view the new access key information.


<span id=".5Yib5bu65LiA5Liq5q2j6KeE5YyW6K-35rGC"></span>
## Create a normalization request

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Hash refers to the SHA256 algorithm.</div>


* <div data-tips="true" data-tips-type="tip">"HexEncode" refers to hexadecimal encoding.</div>



```Plain Text
CanonicalRequest = HTTPRequestMethod + '\n' + CanonicalURI + '\n' + CanonicalQueryString + '\n' + CanonicalHeaders + '\n' + SignedHeaders + '\n' + HexEncode(Hash(RequestPayload))
```


Before signing, the request must be normalized to ensure that the signature calculation process is unambiguous. The main process and pseudocode are as follows:


|field |Descriptions |
|---|---|
|HTTPRequestMethod |HTTP request methods, for example, POST. |
|CanonicalURI |Normalized URI. If the URI is empty, then use`/`As an absolute path. |
|CanonicalQueryString |The normalized QueryString. QueryString normalization process:<br><br><br>1. URL encode (UrlEncode) each QueryString parameter name and parameter value.<br><br>2. Strictly sort parameter names in ASCII byte order.<br><br>3. Use the sorted parameter names and parameter values`=`Connect; match parameters according to the sorting results`&`Connect.<br><br><br>```Plain Text```<br>```CanonicalQueryString = "Action=ListPipelines&Version=2023-05-01"```<br> |
|CanonicalHeaders |The standardized header. The pseudocode is as follows:<br><br>```Plain Text```<br>```CanonicalHeaders = CanonicalHeadersEntry0 + CanonicalHeadersEntry1 + ... + CanonicalHeadersEntryN```<br><br><br>```Plain Text```<br>```CanonicalHeadersEntry = Lowercase(HeaderName) + ':' + Trimall(HeaderValue) + '\n'```<br><br><br>Among them, `Lowercase` means converting all Header names to lowercase, while `Trimall` means removing any extra spaces from the beginning and end of the Header Value.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Add a line break character at the end: `\n`.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Headers are sorted by the ASCII values of <code>headerName</code> after converting to lowercase.</div><br> |
|SignedHeaders |Header names included in the signature<br><br>Headers to be signed must be included in the list of normalized header names to specify which headers are involved in the signature calculation, so that any additional headers added to the request by a proxy are ignored. If both `host` and `x-date` headers are present, add them to the list of normalized header names.<br><br>The pseudocode is as follows:<br><br>```Plain Text```<br>```SignedHeaders = Lowercase(HeaderName0) + ';' + Lowercase(HeaderName1) + ";" + ... + Lowercase(HeaderNameN)```<br> |
|RequestPayload |The complete body of the request.<br><br><br>* URL encode (using the [RFC3986](https://tools.ietf.org/html/rfc3986) method) each QueryString parameter name and value.<br><br>   The GET method must include all parameters: hash algorithm, credential, signature date, and signature header.<br><br>* Strictly sort parameter names in ASCII byte order.<br><br>* Use the sorted parameter names and parameter values`=`Connect; pair the parameters according to the sorting result.`&`Connection. |


<span id=".5Yib5bu6562-5ZCN5a2X56ym5Liy"></span>
## Create a signature string

The signature string contains the request and the metadata of the normalized request, and is constructed by concatenating the signature algorithm, request date, credential, and normalized request hash value. The pseudocode is as follows:

```Plain Text
StringToSign = Algorithm + '\n' + RequestDate + '\n' + CredentialScope + '\n' + HexEncode(Hash(CanonicalRequest))
```


The field descriptions are as follows.


|field |Descriptions |
|---|---|
|Algorithm |Signature algorithms. Currently, only supports the HMAC\-SHA256 signature algorithm. |
|RequestDate |Request UTC time. Use the `YYYYMMDD'T'HHMMSS'Z'` format, for example: `20201103T104027Z`. |
|CredentialScope |Scope of vouchers. The format is `YYYYMMDD/region/service/request`. |
|CanonicalRequest |The results of the preorder normalization request. |


<span id=".6K6h566X562-5ZCN56eY6ZKl"></span>
## Calculate the signature key


1. Before calculating the signature, first derive a signing key (Signing Key) from the Secret Access Key, rather than using the Secret Access Key directly. The specific calculation process is as follows:

   ```Plain Text
   kSecret = *Your Secret Access Key*
   kDate = HMAC(kSecret, Date)
   kRegion = HMAC(kDate, Region)
   kService = HMAC(kRegion, Service)
   kSigning = HMAC(kService, "request")
   ```
   

2. Calculate a signature.

   ```Plain Text
   Signature = HexEncode(HMAC(kSigning, StringToSign))
   ```
   

3. Build a header.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In expressions, use<code>{}</code>The content inside represents the intermediate result calculated above.   </div>
   

   ```Plain Text
   Authorization: HMAC-SHA256 Credential={AccessKeyId}/{CredentialScope}, SignedHeaders={SignedHeaders}, Signature={Signature}
   ```

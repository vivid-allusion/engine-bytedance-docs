---
title: "Sign API Request"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69859"
---

In order to ensure safely calling OpenAPI, BytePlus will authenticate each OpenAPI request by signing.

<span id="signing-sdk"></span>
## Signing SDK

RTC provides signature SDKs in multiple languages. You can call them directly to sign, and you can refer to the signature SDK to implement your own OpenAPI.


|Development language |SDK with Encapsulated signature mechanism |
|---|---|
|PHP SDK |[Byteplus-sdk-php](https://github.com/byteplus-sdk/byteplus-sdk-php/tree/master/examples/Rtc/rtc-openapi-demo) |
|Golang SDK |[Byteplus-sdk-golang](https://github.com/byteplus-sdk/byteplus-sdk-golang) |
|Java SDK |[Byteplus-sdk-java](https://github.com/byteplus-sdk/byteplus-sdk-java) |
|Python SDK |[Byteplus-sdk-python](https://github.com/byteplus-sdk/byteplus-sdk-python) |


<span id="example"></span>
## Example

If you want to build the signature yourself, please refer to [Calculating a signature](https://docs.byteplus.com/byteplus-platform/reference/how-to-calculate-a-signature#calculating-the-signing-key). RTC uses the `GetRecordTask` interface as an example to provide a signature example to help you understand the whole process of signing.

The `Access Key` and `Secret Access Key` in the example do not have real permission, and are only used for demo demonstration. Please use the real `Access Key` and `Secret Access Key` for actual requests.

> **Access Key ID:** 

> AKLTMjI2ODVlYzI3ZGY1NGU4ZjhjYWRjMTlmNTM5OTZkYzE

> **Secret Access Key:** 

> TnpCak5XWXpZV1U0WkRaaE5ERmxaR0ZpTmpjeVkyUXlZek0wTWpJMU1qWQ==


The request parameters of the `GetRecordTask` interface are as follows:


|**Parameter** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`GetRecordTask` |Interface name. This value takes: `GetRecordTask` |
|Version |String |Yes |`2022-06-01` |Interface version. This value takes: `2022-06-01` |
|AppId |String |Yes |`Your_AppId` |The only identifier for your audio & video app |
|RoomId |String |Yes |`Your_RoomId` |The ID of the room. It's the only identifier of a room |
|TaskId |String |Yes |`Your_TaskId` |Task ID of cloud recording. You must set the TaskId for each cloud recording task. |


So the original request is:

```Plain Text
GET https://open.byteplusapi.com?Action=GetRecordTask&Version=2022-06-01&AppId=Your_AppId&RoomId=Your_RoomId&TaskId=Your_TaskId HTTP/1.1
Host: open.byteplusapi.com
Content-Type: application/x-www-form-urlencoded; charset=utf-8
X-Content-Sha256:e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
X-Date:20201230T081805Z
```


> For detailed explanation of each field, please refer to [Common Parameters](https://docs.byteplus.com/byteplus-rtc/doc/69828#common-parameters).


The signing process is as follows:

<span id="step-1-creating-a-canonical-request"></span>
#### Step 1: Creating a canonical request

Create a canonical request to normalize the process of signature calculation. The pseudocode is as follows:

```Plain Text
CanonicalRequest = HTTPRequestMethod + '\n' + CanonicalURI + '\n' + CanonicalQueryString + '\n' + CanonicalHeaders + '\n' + SignedHeaders + '\n' + HexEncode(Hash(RequestPayload))
```


In the pseudocode above:


* Hash represents SHA256 algorithm.

* HexEncode represents the conversion to hexadecimal encoding.

* Hmac represents Hmac_SHA256 algorithm


**HTTPRequestMethod**

```Plain Text
GET
```


**Canonical URI**

```Plain Text
/
```


**CanonicalQueryString**

```Plain Text
Action=GetRecordTask&AppId=Your_AppId&RoomId=Your_RoomId&TaskId=Your_TaskId&Version=2022-06-01
```


**Canonical Headers**

Headers are sorted by the lowercase header name in ASCII order.

```Plain Text
content-type:application/x-www-form-urlencoded; charset=utf-8
host:open.byteplusapi.com
x-content-sha256:e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
x-date:20201230T081805Z
// A "\n" character must be added in the end
```


**SignedHeaders**

```Plain Text
content-type;host;x-content-sha256;x-date
```


**HexEncode(Hash(RequestPayload))** 

Both GET and POST requests have a RequestPayload , where RequestPayload in this request is an empty string.

The hash algorithm here refers to: sha256 []byte

```Plain Text
e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
```


**Canonical Request**

```Plain Text
GET
/
Action=GetRecordTask&AppId=Your_AppId&RoomId=Your_RoomId&TaskId=Your_TaskId&Version=2022-06-01
content-type:application/x-www-form-urlencoded; charset=utf-8
host:open.byteplusapi.com
x-content-sha256:e3b0c44298fc1c149afbf4zc8996fb92427ae41e4649b934ca495991b7852b855
x-date:20201230T081805Z

content-type;host;x-content-sha256;x-date
e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
```


<span id="step-2-extracting-a-signature-string"></span>
#### Step 2: Extracting a signature string

```Plain Text
StringToSign = Algorithm + '\n' + RequestDate + '\n' + CredentialScope + '\n' + HexEncode(Hash(CanonicalRequest))
```


**Algorithm**

The signing algorithm

For this request:

```Plain Text
HMAC-SHA256
```


**RequestDate**

The time when the API request is sent (the value of X\-Date in the request header). Format: UTC (YYYYMMDD'T'HHMMSS'Z'). For example, `20201103T104027Z`.

For this request:

```Plain Text
20201230T081805Z
```


**CredentialScope**

The credential scope. Format: {``YYYYMMDD}/{region}/{service}/request.

For this request:

```Plain Text
20201230/ap-singapore-1/rtc/request
```


**HexEncode(Hash(CanonicalRequest))** 

```Plain Text
347e7f5324998a2c7984370c3c50dc75bf9e6b449ea498a6bf8864d94cbd84b9
```


**StringToSign**

```Plain Text
HMAC-SHA256
20201230T081805Z
20201230/ap-singapore-1/rtc/request
347e7f5324998a2c7984370c3c50dc75bf9e6b449ea498a6bf8864d94cbd84b9
```


<span id="step-3-calculating-the-signature"></span>
#### Step 3: Calculating the signature

> Hmac represents Hmac_SHA256 algorithm


**Signing key**

> Before calculating the signature, deriving the signing key from the private access key (AccessKey Secret) instead of directly using the private access key.


```Plain Text
Signingkey=HMAC(HMAC(HMAC(HMAC("Your Secret Access Key","20201230"),"ap-singapore-1"),"rtc"),"request")
```


The following example shows the derived signing key produced by this sequence of HMAC hash operations. This shows the hexadecimal representation of each byte in this binary signing key.

```Plain Text
aa6c033b312f2984f152589a7b015852909f850a150ba517ae8dea394126af08
```


**Signature example**

```Plain Text
signature = HexEncode(HMAC(Signingkey, StringToSign))
```


The final result is as follows:

```Plain Text
0d7e689b7d7949fa8b0132f5718b8f3b0d25cf7ea6c46eea33d91efd79f1e973
```


<span id="step-4-add-the-signature-to-the-request"></span>
#### Step 4: Add the signature to the request

Add the Authorization header to the request as follows:

```Plain Text
Authorization: HMAC-SHA256 Credential={AccessKeyId}/{CredentialScope}, SignedHeaders={SignedHeaders}, Signature={Signature}
```


The full result is as follows:

```Plain Text
HMAC-SHA256 Credential=AKLTMjI2ODVlYzI3ZGY1NGU4ZjhjYWRjMTlmNTM5OTZkYzE/20201230/ap-singapore-1/rtc/request, SignedHeaders=content-type;host;x-content-sha256;x-date, Signature=0d7e689b7d7949fa8b0132f5718b8f3b0d25cf7ea6c46eea33d91efd79f1e973
```

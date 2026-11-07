---
title: "API 认证"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-API-authentication-zh-CN"
---

要对发送至 BytePlus Live 的 API 请求进行认证，您必须创建一个有效的签名，并将其包含在您的 HTTP 或 HTTPS 请求中。本指南提供了生成该签名的详细分步流程，确保您的请求能够被服务器成功验证。

<span id="background"></span>
## 背景

当您向 BytePlus Live 发送 API 请求时，为了验证请求者身份并防止 API 请求在传输过程中被恶意篡改，BytePlus 的签名机制要求请求者对请求参数进行签名计算，并将签名与 API 请求一同传递至 API 服务器进行认证。

当 BytePlus Live 接收到请求后，会使用相同的信息计算签名，并与您的请求中的签名进行比对。如果签名值不匹配，请求将被拒绝。

<span id="prerequisites"></span>
## 前提条件


* 注册 BytePlus 账号。更多信息，请参见[注册 BytePlus 账号](https://docs.byteplus.com/en/byteplus-platform/docs/signing-up-your-account)。

* 前往[BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/) \> **用户信息** \> **IAM** \> **密钥管理**，获取用于 API 请求认证的 AccessKey ID（AK）和 Secret Access Key（SK）。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/c0c5750-Obtain_the_AccessKey_ID_and_AccessKey_secret.JPEG) </span>


<span id="process"></span>
## 流程

以下流程展示如何创建一个已签名的请求。

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/dac1414-Process.JPEG) </span>

<span id="procedure"></span>
## 操作步骤

本节以`GetActivityAPI`为例，说明如何对 BytePlus Live API 请求进行签名。

`GetActivityAPI` 的原始请求（未签名）如下。

```Plain
Get http://livesaas.byteplusapi.com/?Action=GetActivityAPI&Version=2020-06-01&ActivityId=1231231231
Host: livesaas.byteplusapi.com
Content-Type: application/x-www-form-urlencoded; charset=utf-8
X-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
X-Date: 20201230T081805Z
```


<span id="step-1-create-a-canonical-request"></span>
### Step 1: 创建规范化请求

要开始签名流程，请以规范化格式创建请求。这样可以确保 BytePlus Live 计算的签名与您计算的签名一致。如果两者不一致，请求将被拒绝。

以下伪代码展示如何创建规范化请求：

```Plain
CanonicalRequest = HTTPRequestMethod + '\n' + CanonicalURI + '\n' + CanonicalQueryString + '\n' + CanonicalHeaders + '\n' + SignedHeaders + '\n' + HexEncode(Hash(RequestPayload))
```


完成以下步骤以创建规范化请求：


1. 以 HTTP 请求方式（`HTTPRequestMethod`）开始，例如 `GET` 和 `POST`。在本例中，`GetActivityAPI` 的 HTTP 请求方式为 `GET`。

   ```Plain
   GET
   ```
   

2. 添加 API 请求的规范化 URI（`CanonicalURI`）。规范化 URI 是 URI 的绝对路径部分经过 URI 编码后的版本，该部分位于 host 之后、问号（`?`）之前（如果有），问号用于开始查询字符串参数。

   根据[RFC 3986](https://tools.ietf.org/html/rfc3986)规范化 URI 路径。移除冗余和相对路径部分。如果绝对路径未以斜杠（`/`）结尾，则在末尾添加一个斜杠。

   如果绝对路径为空，则使用斜杠（`/`）。在本例中，`GetActivityAPI` 的 URI 中 host 之后没有任何内容，因此绝对路径为空，规范化 URI 如下：

   ```Plain
   /
   ```
   

3. 添加 API 请求的规范化查询字符串（`CanonicalQueryString`）。在本例中，`GetActivityAPI` 的查询字符串如下：

   ```Plain
   Action=GetActivityAPI&Version=2020-06-01&ActivityId=1231231231
   ```
   

   要构建规范化查询字符串，请完成以下步骤：

   1. 根据[RFC 3986](https://tools.ietf.org/html/rfc3986)对每个参数名称和值进行 URL 编码。

   2. 按 ASCII 顺序对参数名称进行排序。对于同一参数名称的不同值，保持请求中的原始顺序。

   3. 将排序后的参数名称和值用等号（`=`）连接，并用和号（`&`）将参数对串联成字符串。

      在本示例中，`GetActivityAPI`具有如下规范化查询字符串。

   ```Plain
   Action=GetActivityAPI&ActivityId=1231231231&Version=2020-06-01
   ```
   

4. 添加规范化头部（`CanonicalHeaders`），其包含签名请求中的所有 HTTP 头部。

   以下伪代码展示了如何添加规范化头部：

   ```Plain
   CanonicalHeaders = CanonicalHeadersEntry0 + CanonicalHeadersEntry1 + ... + CanonicalHeadersEntryN
   CanonicalHeadersEntry = Lowercase(HeaderName) + ':' + Trimall(HeaderValue) + '\n'
   ```
   

   其中，

   * `Lowercase`：将所有头部名称转换为小写。

   * `Trimall`：移除头部值前后的多余空格。

      必须按照 ASCII 顺序对小写头部名称进行排序，并在每个头部末尾添加换行符（``


）。

在本示例中，规范化头部如下：

```Plain
content-type:application/x-www-form-urlencoded; charset=utf-8\n
host:livesaas.byteplusapi.com\n
x-content-sha256:e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855\n
x-date:20201230T081805Z\n
```



5. 添加签名头部（`SignedHeaders`）。`SignedHeaders` 的值为包含在规范化头部中的头部列表。通过添加签名头部，可以指定请求中哪些头部参与签名过程，从而忽略代理添加的额外头部。

   如果 `Host` 和 `x-date` 头部作为 HTTP 头部包含，则必须作为签名头部包含。

   以下伪代码展示了如何添加签名头部：

   ```Plain
   SignedHeaders = Lowercase(HeaderName0) + ';' + Lowercase(HeaderName1) + ";" + ... + Lowercase(HeaderNameN)
   ```
   

   将所有头部名称转换为小写，按 ASCII 顺序排序，并用分号（`;`）分隔。

   在本示例中，签名头部如下：

   ```Plain
   content-type;host;x-content-sha256;x-date
   ```
   

6. 使用 SHA256 算法对 HTTP 或 HTTPS 请求正文中的 payload（字节数组）进行哈希处理。哈希后的 payload 必须以小写十六进制字符串表示。

   ```Plain
   HashedPayload = HexEncode(Hash(RequestPayload))
   ```
   

   其中，

   * `Hash` 表示 SHA256 算法。

   * `HexEncode` 表示转换为小写字符的十六进制编码。例如，`HexEncode("z")` 返回值为 `7a`，而不是 `7A`。

      GET 和 POST 请求均有 `RequestPayload`。在本示例中，payload 为空。因此，使用空字符串作为哈希函数的输入是合适的。哈希后的 payload 为 `e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855`。

7. 要构建规范化请求（`CanonicalRequest`），需将第 1 步到第 6 步的所有组件合并为一个字符串，每个组件以换行符结尾。

   在本示例中，生成的规范化请求如下：

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
   

   规范化头部与签名头部之间必须始终保留一个空行。


<span id="step-2-create-a-string-to-sign"></span>
### Step 2: Create a string to sign

待签名字符串包含请求的元信息和规范化请求，这些规范化请求是在 **Step 1: Create a canonical request** 中生成的。

以下伪代码展示了如何创建待签名字符串：

```Plain
StringToSign = Algorithm + '\n' + RequestDate + '\n' + CredentialScope + '\n' + HexEncode(Hash(CanonicalRequest))
```


其中，


* `Algorithm`：签名算法。当前仅支持 `HMAC-SHA256`。

* `RequestDate`：API 请求发送时的 UTC 时间，即请求头中的 `X-Date` 的值。格式：`YYYYMMDD'T'HHMMSS'Z'`。示例：`20201230T081805Z`。

* `CredentialScope`：凭证作用域，格式为 `{YYYYMMDD}/{region}/{service}/request`。在本例中，`YYYYMMDD` 的值必须与 `RequestDate` 中的 `YYYYMMDD` 相同。对于 BytePlus Live，`region` 始终使用 `ap-singapore-1`，`service` 始终使用 `livesaas`。示例：`20201230/ap-singapore-1/livesaas/request`。

* `HexEncode(Hash(CanonicalRequest))`：使用 SHA256 算法计算在 **Step 1: Create a canonical request** 中生成的规范化请求的哈希值。然后，将结果转换为小写十六进制字符串。示例：`ba542a51d36e6c5ba0901612efe1c86c5e6502ce5c842e77975dc7acc2503a1e`。


各字段之间用换行符（``

）分隔。

在本示例中，生成的待签名字符串如下：

```Plain
HMAC-SHA256
20201230T081805Z
20201230/ap-singapore-1/livesaas/request
ba542a51d36e6c5ba0901612efe1c86c5e6502ce5c842e77975dc7acc2503a1e
```


<span id="step-3-calculate-a-signing-key"></span>
### Step 3: Calculate a signing key

在计算签名之前，必须先根据您的 Secret Access Key 计算一个签名密钥。签名密钥与日期、区域和服务相关，因此比您的 Secret Access Key 更安全。

使用您的 Secret Access Key 创建一系列基于哈希的消息认证码（HMAC）。以下伪代码展示了如何计算签名密钥：

```Plain
kSecret = *Your Secret Access Key*
kDate = HMAC(kSecret, Date)
kRegion = HMAC(kDate, Region)
kService = HMAC(kRegion, Service)
kSigning = HMAC(kService, "request")
```


在此，


* `HMAC(key, data)` 表示一个 HMAC\-SHA256 函数，返回二进制格式的输出。每个哈希函数的结果都是下一个的 `key`。

* `Date` 的格式为 `YYYYMMDD`，其值与 `RequestDate` 中 `YYYYMMDD` 的值相同，该值用于 **Step 2: Create a string to sign**。

* 使用 `ap-singapore-1` 作为 `Region`，使用 `livesaas` 作为 `Service`。


在某些编程语言中，`key` 和 `data` 的顺序可能不同。

在本示例中，计算签名密钥的输入如下所示。`kSecret` 的值为 `TkdKbE1qSmpOVFJrTUdGbE5ABCDZbUV5Wm1RelpUQXlPR1ExTURsa01qVQ==`，仅用于演示目的。在计算签名密钥时，请替换为您自己的 Secret Access Key。

```Plain
HMAC(HMAC(HMAC(HMAC(kSecret,"20201230"),"ap-singapore-1"),"livesaas"),"request")
```


前述 HMAC 哈希操作得到的签名密钥如下所示。注意，此处展示的是二进制签名密钥每个字节的十六进制表示。

```Plain
1e952b8ff47aaee5d7cf0b43aa295d6820ef5a0940bfaf59d4623c3d50d41e3
```


<span id="step-4-calculate-the-signature"></span>
### Step 4: Calculate the signature

使用在 **Step 3: Calculate a signing key** 中创建的签名密钥，以及在 **Step 2: Create a string to sign** 中创建的待签字符串作为 HMAC\-SHA256 函数的输入，然后将二进制值转换为小写字符的十六进制表示。

以下伪代码展示了如何计算签名：

```Plain
Signature = HexEncode(HMAC(Signingkey, StringToSign))
```


在某些编程语言中，`Signingkey` 和 `StringToSign` 的顺序可能不同。

在本示例中，生成的签名如下：

```Plain
11a2e7bb9db7ee7ea2e4d7f3d6989a65dc3bb5feedf3aae50ba1b3313fe0093a
```


<span id="step-5-add-the-signature-to-the-http-or-https-request"></span>
### Step 5: Add the signature to the HTTP or HTTPS request

计算签名后，将其添加到 HTTP 或 HTTPS 请求中，通过以下方式之一认证请求发送者：


* HTTP 头部 `Authorization`。

* 查询字符串。


<span id="adding-signing-information-to-the-authorization-header"></span>
#### 将签名信息添加到 `Authorization` 头部

以下伪代码展示了如何构造 `Authorization` 头部：

```Plain
Authorization: Algorithm Credential={AccessKeyId}/{CredentialScope}, SignedHeaders={SignedHeaders}, Signature={Signature}
```


在此，


* `Algorithm`：签名算法 `HMAC-SHA256`。

* `AccessKeyId`：您的 AccessKey ID。更多信息，请参见 **Prerequisites**。

* `CredentialScope`：凭证范围。更多信息，请参见 **Step 2: Create a string to sign**。

* `SignedHeaders`：已签名的头部。更多信息，请参见 **Step 1: Create a canonical request**。

* `Signature`：计算得到的签名。签名用于向 BytePlus Live 证明您的身份。更多信息，请参见 **Step 4: Calculate the signature**。


`Authorization` 头部是在计算签名后构造的，因此不会包含在已签名的头部中。

在本示例中，`Authorization` 头部如下：

```Plain
Authorization: HMAC-SHA256 Credential=AKAPY2RhYmQzODhhYTg4NGZmNTk3ZGUxODk3ODgzYTA****/20201230/ap-singapore-1/livesaas/request, SignedHeaders=content-type;host;x-content-sha256;x-date, Signature=11a2e7bb9db7ee7ea2e4d7f3d6989a65dc3bb5feedf3aae50ba1b3313fe0093a
```


随后，`GetActivityAPI` 的已签名请求如下：

```Plain
Get http://livesaas.byteplusapi.com/?Action=GetActivityAPI&Version=2020-06-01&ActivityId=1231231231
Authorization: HMAC-SHA256 Credential=AKAPY2RhYmQzODhhYTg4NGZmNTk3ZGUxODk3ODgzYTA****/20201230/ap-singapore-1/livesaas/request, SignedHeaders=content-type;host;x-content-sha256;x-date, Signature=11a2e7bb9db7ee7ea2e4d7f3d6989a65dc3bb5feedf3aae50ba1b3313fe0093a
Host: livesaas.byteplusapi.com
Content-Type: application/x-www-form-urlencoded; charset=utf-8
X-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
X-Date: 20201230T081805Z
```


<span id="adding-signing-information-to-the-query-string"></span>
#### 将签名信息添加到查询字符串

以下伪代码展示了如何构造包含签名信息的查询字符串，并将其添加到原始查询字符串末尾：

```Plain
X-Algorithm=algorithm&X-Credential=credential&X-Date=date&X-Expires=time&X-SignedHeaders=signedheaders&X-Signature=signature
```


在此，


* `Algorithm`：签名算法 `HMAC-SHA256`。

* Credential：由您的 AccessKey ID 和 credential scope 组合而成，格式为 `AccessKeyId/CredentialScope`。有关 AccessKey ID 和 credential scope 的更多信息，请参见“前提条件”和“Step 2: Create a string to sign”。

* `X-Date`：API 请求发送时的 UTC 时间。您可以在请求中找到该参数值。在本示例中，该值为 `20201230T081805Z`。

* X\-Expires：签名的有效期（单位：秒）。这是一个可选参数，默认值为 900。若需设置参数值，建议使用较小的值以确保安全，因为生成的查询字符串包含发起 BytePlus Live 成功调用所需的全部内容。

* `SignedHeaders`：已签名的请求头。更多信息请参见 **Step 1: Create a canonical request**。

* `Signature`：计算得到的签名。签名用于确认您在 BytePlus Live 的身份。更多信息请参见 **Step 4: Calculate the signature**。


使用等号（=）连接参数及其值，并用与号（&）分隔参数值对。请根据 RFC 3986 对每个参数名称和值进行 URL 编码。在本示例中，您需将 Credential 值（AccessKeyId/CredentialScope）中的斜杠（/）编码为 %2F，将 SignedHeaders 值中的分号（;）编码为 %3B。

在本示例中，生成的查询字符串如下：

```Plain
Action=GetActivityAPI&Version=2020-06-01&ActivityId=1231231231&X-Algorithm=HMAC-SHA256&X-Credential=AKAPY2RhYmQzODhhYTg4NGZmNTk3ZGUxODk3ODgzYTA****%2F20201230%2Fap-singapore-1%2Flivesaas%2Frequest&X-Date=20201230T081805Z&X-Expires=60&X-SignedHeaders=content-type%3Bhost%3Bx-content-sha256%3Bx-date&X-Signature=11a2e7bb9db7ee7ea2e4d7f3d6989a65dc3bb5feedf3aae50ba1b3313fe0093a
```


随后，`GetActivityAPI` 的签名请求如下：

```Plain
Get http://livesaas.byteplusapi.com/?Action=GetActivityAPI&Version=2020-06-01&ActivityId=1231231231&X-Algorithm=HMAC-SHA256&X-Credential=AKAPY2RhYmQzODhhYTg4NGZmNTk3ZGUxODk3ODgzYTA****%2F20201230%2Fap-singapore-1%2Flivesaas%2Frequest&X-Date=20201230T081805Z&X-Expires=60&X-SignedHeaders=content-type%3Bhost%3Bx-content-sha256%3Bx-date&X-Signature=11a2e7bb9db7ee7ea2e4d7f3d6989a65dc3bb5feedf3aae50ba1b3313fe0093a
Host: livesaas.byteplusapi.com
Content-Type: application/x-www-form-urlencoded; charset=utf-8
X-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
```

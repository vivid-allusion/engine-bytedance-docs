---
title: "签署 BytePlus MediaLive 请求"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-signing-byteplus-medialive-requests-zh-CN"
---

为确保您对 BytePlus MediaLive 的 API 调用的安全性和完整性，您必须对请求进行签名。本主题提供详细的分步说明，指导您如何手动创建签名并将其添加到您的 HTTP 或 HTTPS 请求中。按照此流程操作，可以验证您的身份，并防止请求在传输过程中被篡改。

<span id="Background"></span>
## 背景

当您向 BytePlus MediaLive 发送 API 请求时，为验证请求者身份并防止 API 请求在传输过程中被恶意篡改，BytePlus 的签名机制要求请求者对请求参数进行签名计算，并将签名与 API 请求一同传递至 API 服务器进行认证。当 BytePlus MediaLive 接收到请求后，会使用相同的信息计算签名，并与您的请求中的签名进行比对。如果值不匹配，则请求将被拒绝。

<span id="Preparation"></span>
## 准备工作


1. 注册 BytePlus 账号。更多信息，请参见[注册 BytePlus 账号](https://docs.byteplus.com/byteplus-platform/docs/signing-up-your-account)。

2. 登录[BytePlus 控制台](https://console.byteplus.com/home)。

3. 点击页面右上角的用户名，选择**IAM**。

4. 在左侧导航栏，点击**密钥管理**。

5. 获取 AccessKey ID 和 AccessKey Secret，这些用于 API 请求认证。


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/5ddc848-accesskey.png) </span>

<span id="Process"></span>
## 流程

以下流程展示如何创建已签名的请求。

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/dac1414-Process.JPEG) </span>

<span id="Procedure"></span>
## 操作步骤

本节以`DescribeLiveDomainLog`为例，说明如何对 BytePlus MediaLive API 请求进行签名。

`DescribeLiveDomainLog`未签名的原始请求如下。

```plain
GET http://open.byteplusapi.com/?Action=DescribeLiveDomainLog&Version=2020-08-01
Host: open.byteplusapi.com
Content-Type: application/x-www-form-urlencoded; charset=utf-8
X-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
X-Date: 20201230T081805Z
```


<span id="Step 1: Create a canonical request"></span>
### Step 1: 创建规范化请求

要开始签名流程，需创建一个规范化格式的请求。这样可以确保 BytePlus MediaLive 计算的签名与您计算的签名一致。如果两者不一致，请求将被拒绝。

以下伪代码展示如何创建规范化请求：

```plain
CanonicalRequest = HTTPRequestMethod + '\n' + CanonicalURI + '\n' + CanonicalQueryString + '\n' + CanonicalHeaders + '\n' + SignedHeaders + '\n' + HexEncode(Hash(RequestPayload))
```


完成以下步骤以创建规范化请求：


1. 以 HTTP 请求方式（`HTTPRequestMethod`）开始，例如`GET`和`POST`。在本例中，`DescribeLiveDomainLog`的 HTTP 请求方式为`GET`。

   ```plain
   GET
   ```
   

2. 添加 API 请求的规范化 URI（`CanonicalURI`）。规范化 URI 是 URI 的绝对路径部分的 URI 编码版本，该部分位于 host 之后、问号（`?`）之前（如果有查询字符串参数）。

   根据[RFC 3986](https://tools.ietf.org/html/rfc3986)规范化 URI 路径，移除冗余和相对路径部分。如果绝对路径未以斜杠（`/`）结尾，则在末尾添加斜杠。

   如果绝对路径为空，则使用斜杠（`/`）。在本例中，`DescribeLiveDomainLog`的 URI 中 host 后无内容，因此绝对路径为空，规范化 URI 如下：

   ```plain
   /
   ```
   

3. 添加 API 请求的规范化查询字符串（`CanonicalQueryString`）。在本例中，`DescribeLiveDomainLog`的查询字符串如下：

   ```plain
   Action=DescribeLiveDomainLog&Version=2020-08-01
   ```
   

   要构建规范化查询字符串，请完成以下步骤：

   1. 根据[RFC 3986](https://tools.ietf.org/html/rfc3986)对每个参数名称和值进行 URL 编码。

   2. 按 ASCII 顺序对参数名称进行排序。对于同一参数名称的不同值，在请求中保持其原有顺序。

   3. 将已排序的参数名称及其值用等号（`=`）连接，并使用与符号（`&`）将参数对拼接为一个字符串。

      在本例中，`DescribeLiveDomainLog` 的规范化查询字符串如下。

   ```plain
   Action=DescribeLiveDomainLog&Version=2020-08-01
   ```
   

4. 添加规范化头部（`CanonicalHeaders`）。规范化头部包含签名请求中的所有 HTTP 头部。

   以下伪代码展示了如何添加规范化头部：

   ```plain
   CanonicalHeaders = CanonicalHeadersEntry0 + CanonicalHeadersEntry1 + ... + CanonicalHeadersEntryN
   CanonicalHeadersEntry = Lowercase(HeaderName) + ':' + Trimall(HeaderValue) + '\n'
   ```
   

   说明：

   * `Lowercase`：将所有头部名称转换为小写。

   * `Trimall`：移除头部值前后的多余空格。

      **Warning**：必须按 ASCII 顺序对小写头部名称进行排序，并在每个头部末尾添加换行符（``


）。

```Plain Text
  在本例中，规范化头部如下：
```


```plain
content-type:application/x-www-form-urlencoded; charset=utf-8\n
host:open.byteplusapi.com\n
x-content-sha256:e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855\n
x-date:20201230T081805Z\n
```



5. 添加签名头部（`SignedHeaders`）。`SignedHeaders` 的值为包含在规范化头部中的头部列表。通过添加签名头部，可以指定请求中哪些头部参与签名过程，以忽略代理添加的额外头部。

   如果 `主播` 和 `x-date` 头部作为 HTTP 头部包含在请求中，则必须将其作为签名头部。

   以下伪代码展示了如何添加签名头部：

   ```plain
   SignedHeaders = Lowercase(HeaderName0) + ';' + Lowercase(HeaderName1) + ";" + ... + Lowercase(HeaderNameN)
   ```
   

   将所有头部名称转换为小写，按 ASCII 顺序排序，并用分号（`;`）分隔。

   在本例中，签名头部如下：

   ```plain
   content-type;host;x-content-sha256;x-date
   ```
   

6. 使用 SHA256 算法对请求体中的 payload（字节数组）进行哈希处理。哈希后的 payload 必须以小写十六进制字符串表示。

   ```plain
   HashedPayload = HexEncode(Hash(RequestPayload))
   ```
   

   说明：

   * `Hash` 表示 SHA256 算法。

   * `HexEncode` 表示转换为小写字符的十六进制编码。例如，`HexEncode("z")` 返回值为 `7a`，而不是 `7A`。

      GET 和 POST 请求均有 `RequestPayload`。在本例中，payload 为空。因此，使用空字符串作为哈希函数的输入。哈希后的 payload 为 `e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855`。

7. 要构建规范化请求（`CanonicalRequest`），需将第 1 步到第 6 步的所有组件合并为一个字符串，每个组件以换行符结尾。

   在本例中，生成的规范化请求如下：

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">在以下示例中，由于<code>CanonicalHeaders</code>必须以换行符（<code>\n</code>）结尾，并且与<code>SignedHeaders</code>通过另一个换行符（<code>\n</code>）连接，因此两个连续的换行符（<code>\n\n</code>）自然形成一个空行。   </div>
   

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
   


<span id="Step 2: Create a string to sign"></span>
### Step 2: Create a string to sign

待签名字符串包含关于您的请求的元数据，以及在 [Step 1: 创建规范化请求](/docs/byteplus\-media\-live/docs\-signing\-byteplus\-medialive\-requests\-zh\-CN#Step 1: Create a canonical request) 中创建的规范化请求的相关信息。

以下伪代码展示了如何创建待签名字符串：

```plain
StringToSign = Algorithm + '\n' + RequestDate + '\n' + CredentialScope + '\n' + HexEncode(Hash(CanonicalRequest))
```


说明：


* `Algorithm`：签名算法。当前仅支持 `HMAC-SHA256`。

* `RequestDate`：API 请求发送时的 UTC 时间，即请求头中的 `X-Date` 的值。格式：`YYYYMMDD'T'HHMMSS'Z'` 示例：`20201230T081805Z`

* `CredentialScope`：凭证范围，格式为 `YYYYMMDD/region/service/request`。此处，`YYYYMMDD` 的值必须与 `RequestDate` 中的 `YYYYMMDD` 相同。对于 BytePlus MediaLive，`ap-singapore-1` 作为 `region`，`live` 作为 `service`，始终使用该值。示例：`20201230/ap-singapore-1/live/request`。

* `HexEncode(Hash(CanonicalRequest))`：使用 SHA256 算法计算在 [Step 1: Create a canonical request](/docs/byteplus\-media\-live/docs\-signing\-byteplus\-medialive\-requests#Step 1: Create a canonical request) 中创建的规范化请求的哈希值，并将结果转换为小写十六进制字符串。示例：`ba542a51d36e6c5ba0901612efe1c86c5e6502ce5c842e77975dc7acc2503a1e`


**警告**：请使用换行符（`\n`）分隔各字段。

在本示例中，生成的待签名字符串如下：

```plain
HMAC-SHA256
20201230T081805Z
20201230/ap-singapore-1/live/request
ba542a51d36e6c5ba0901612efe1c86c5e6502ce5c842e77975dc7acc2503a1e
```


<span id="Step 3: Calculate a signing key"></span>
### Step 3: 计算签名密钥

在计算签名之前，必须根据你的 AccessKey 密钥计算签名密钥。签名密钥与日期、区域和服务相关，比你的 AccessKey 密钥更安全。

使用你的 AccessKey 密钥创建一系列基于哈希的消息认证码（HMAC）。以下伪代码展示了如何计算签名密钥：

```plain
kSecret = *Your AccessKey Secret*
kDate = HMAC(kSecret, Date)
kRegion = HMAC(kDate, Region)
kService = HMAC(kRegion, Service)
kSigning = HMAC(kService, "request")
```


其中：


* `HMAC(key, data)` 表示 HMAC\-SHA256 函数，输出为二进制格式。每个哈希函数的结果作为下一个的 `key`。

* `Date` 的格式为 `YYYYMMDD`，其值与 [Step 2: Create a string to sign](/docs/byteplus\-media\-live/docs\-signing\-byteplus\-medialive\-requests#Step 2: Create a string to sign) 中 `RequestDate` 的 `YYYYMMDD` 相同。

* 使用 `ap-singapore-1` 作为 `Region`，`live` 作为 `Service`。


**说明**：对于某些编程语言，`key` 和 `data` 的顺序可能不同。

在本示例中，计算签名密钥的输入如下，`kSecret` 为 `TkdKbE1qSmpOVFJrTUdGbE5ABCDZbUV5Wm1RelpUQXlPR1ExTURsa01qVQ==`。此处的 `kSecret` 仅用于演示。实际计算签名密钥时，请替换为你自己的 AccessKey 密钥。

```plain
HMAC(HMAC(HMAC(HMAC(kSecret,"20201230"),"ap-singapore-1"),"live"),"request")
```


前述 HMAC 哈希操作生成的签名密钥如下，展示了二进制签名密钥每个字节的十六进制表示。

```plain
1e952b8ff47aaee5d7cf0b43aa295d6820ef5a0940bfaf59d4623c3d50d41e3
```


<span id="Step 4: Calculate the signature"></span>
### Step 4: 计算签名

使用在 [Step 3: Calculate a signing key](/docs/byteplus\-media\-live/docs\-signing\-byteplus\-medialive\-requests#Step 3: Calculate a signing key) 中生成的签名密钥和在 [Step 2: Create a string to sign](/docs/byteplus\-media\-live/docs\-signing\-byteplus\-medialive\-requests#Step 2: Create a string to sign) 中生成的待签名字符串作为 HMAC\-SHA256 函数的输入，然后将二进制值转换为小写字符的十六进制表示。

以下伪代码展示了如何计算签名：

```plain
Signature = HexEncode(HMAC(Signingkey, StringToSign))
```


**说明**：对于某些编程语言，`Signingkey` 和 `StringToSign` 的顺序可能不同。

在本示例中，生成的签名如下：

```plain
11a2e7bb9db7ee7ea2e4d7f3d6989a65dc3bb5feedf3aae50ba1b3313fe0093a
```


<span id="Step 5: Add the signature to the HTTP or HTTPS request"></span>
### Step 5: 将签名添加到 HTTP 或 HTTPS 请求中

计算签名后，可通过以下方式之一将签名添加到 HTTP 或 HTTPS 请求中，以验证请求：


* HTTP 头部 `Authorization`

* 查询字符串


<span id="Adding signing information to the Authorization header"></span>
#### 将签名信息添加到 `Authorization` 头部

以下伪代码展示了如何构造 `Authorization` 头部：

```plain
Authorization: Algorithm Credential={AccessKeyId}/{CredentialScope}, SignedHeaders={SignedHeaders}, Signature={Signature}
```


其中：


* `Algorithm`：签名算法 `HMAC-SHA256`。

* `AccessKeyId`：你的 AccessKey ID。更多信息，请参见 [Preparation](https://docs.byteplus.com/docs/byteplus-media-live/docs-signing-byteplus-medialive-requests#Preparation)。

* `CredentialScope`：凭证范围。更多信息，请参见 [Step 2: Create a string to sign](/docs/byteplus\-media\-live/docs\-signing\-byteplus\-medialive\-requests#Step 2: Create a string to sign)。

* `SignedHeaders`：已签名头部。更多信息，请参见 [Step 1: Create a canonical request](/docs/byteplus\-media\-live/docs\-signing\-byteplus\-medialive\-requests#Step 1: Create a canonical request)。

* `Signature`：已计算的签名，用于向 BytePlus MediaLive 验证你的身份。更多信息，请参见 [Step 4: Calculate the signature](/docs/byteplus\-media\-live/docs\-signing\-byteplus\-medialive\-requests#Step 4: Calculate the signature)。


**说明**：`Authorization` 头部是在计算签名后构造的，因此不包含在已签名头部中。

在本示例中，`Authorization` 头部如下：

```plain
Authorization: HMAC-SHA256 Credential=AKAPY2RhYmQzODhhYTg4NGZmNTk3ZGUxODk3ODgzYTA****/20201230/ap-singapore-1/live/request, SignedHeaders=content-type;host;x-content-sha256;x-date, Signature=11a2e7bb9db7ee7ea2e4d7f3d6989a65dc3bb5feedf3aae50ba1b3313fe0093a
```


随后，`DescribeLiveDomainLog` 的签名请求如下：

```plain
GET http://open.byteplusapi.com/?Action=DescribeLiveDomainLog&Version=2020-08-01
Authorization: HMAC-SHA256 Credential=AKAPY2RhYmQzODhhYTg4NGZmNTk3ZGUxODk3ODgzYTA****/20201230/ap-singapore-1/live/request, SignedHeaders=content-type;host;x-content-sha256;x-date, Signature=11a2e7bb9db7ee7ea2e4d7f3d6989a65dc3bb5feedf3aae50ba1b3313fe0093a
Host: open.byteplusapi.com
Content-Type: application/x-www-form-urlencoded; charset=utf-8
X-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
X-Date: 20201230T081805Z
```


<span id="Adding signing information to the query string"></span>
#### 将签名信息添加到查询字符串

以下伪代码展示了如何构建包含签名信息的查询字符串，并将其添加到原始查询字符串的末尾：

```plain
X-Algorithm=algorithm&X-Credential=credential&X-Date=date&X-Expires=time&X-SignedHeaders=signedheaders&X-Signature=signature
```


其中：


* `Algorithm`：签名算法`HMAC-SHA256`。

* `Credential` *:*  由您的 AccessKey ID 和凭证范围组合而成，即`AccessKeyId/CredentialScope`。有关 AccessKey ID 和凭证范围的更多信息，请参见[Preparation](https://docs.byteplus.com/docs/byteplus-media-live/docs-signing-byteplus-medialive-requests#Preparation)以及[Step 2: Create a string to sign](/docs/byteplus\-media\-live/docs\-signing\-byteplus\-medialive\-requests#Step 2: Create a string to sign)。

* `X-Date`：API 请求发送时的 UTC 时间。您可以在请求中找到该参数的值。在本例中，该值为`20201230T081805Z`。

* `X-Expires`：签名的有效期。这是一个可选参数，默认值为 900（单位：秒）。若需设置参数值，建议出于安全考虑选择较小的值，因为生成的查询字符串包含发起 BytePlus MediaLive 成功请求所需的全部内容。

* `SignedHeaders`：已签名的请求头。更多信息请参见[Step 1: Create a canonical request](/docs/byteplus\-media\-live/docs\-signing\-byteplus\-medialive\-requests#Step 1: Create a canonical request)。

* `Signature`：计算所得的签名。签名用于向 BytePlus MediaLive 验证您的身份。更多信息请参见[Step 4: Calculate the signature](/docs/byteplus\-media\-live/docs\-signing\-byteplus\-medialive\-requests#Step 4: Calculate the signature)。


使用等号（=）连接参数及其值，并用与号（&）分隔参数值对。根据[RFC 3986](https://tools.ietf.org/html/rfc3986)对每个参数名称和值进行 URL 编码。在本例中，您只需将`Credential`值中的斜杠（`/`）转换为`%2F`，以及将`SignedHeaders`值中的分号（`;`）转换为`%3B`。

在本例中，生成的查询字符串如下：

```plain
Action=DescribeLiveDomainLog&Version=2020-08-01&X-Algorithm=HMAC-SHA256&X-Credential=AKAPY2RhYmQzODhhYTg4NGZmNTk3ZGUxODk3ODgzYTA****%2F20201230%2Fap-singapore-1%2Flive%2Frequest&X-Date=20201230T081805Z&X-Expires=60&X-SignedHeaders=content-type%3Bhost%3Bx-content-sha256%3Bx-date&X-Signature=11a2e7bb9db7ee7ea2e4d7f3d6989a65dc3bb5feedf3aae50ba1b3313fe0093a
```


随后，`DescribeLiveDomainLog`的签名请求如下：

```plain
GET http://open.byteplusapi.com/?Action=DescribeLiveDomainLog&Version=2020-08-01&X-Algorithm=HMAC-SHA256&X-Credential=AKAPY2RhYmQzODhhYTg4NGZmNTk3ZGUxODk3ODgzYTA****%2F20201230%2Fap-singapore-1%2Flive%2Frequest&X-Date=20201230T081805Z&X-Expires=60&X-SignedHeaders=content-type%3Bhost%3Bx-content-sha256%3Bx-date&X-Signature=11a2e7bb9db7ee7ea2e4d7f3d6989a65dc3bb5feedf3aae50ba1b3313fe0093a
Host: open.byteplusapi.com
Content-Type: application/x-www-form-urlencoded; charset=utf-8
X-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
```


<span id="Additional resources"></span>
## 更多资源

如果您能在[here](https://docs.byteplus.com/byteplus-media-live/docs/server-sdk)找到适用于您的编程语言的 SDK，则无需手动完成签名流程，因为这些 SDK 会自动处理签名。

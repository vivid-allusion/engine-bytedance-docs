---
title: "配置URL鉴权"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-url-authentication-zh-CN"
---

为防止直播流资源被未经授权使用，可以启用URL鉴权。该功能会为推流地址和拉流地址添加鉴权参数，确保只有经过验证的请求才能被服务。本主题将介绍鉴权流程，并提供通过BytePlus MediaLive控制台配置A、B、C三种类型URL鉴权的分步操作说明。

<span id="4ef0cf9e"></span>
# 适用范围

URL鉴权适用于推流域名和拉流域名。


* 为推流域名配置URL鉴权：控制哪些URL可以推流，防止未经授权的推流，保护内容源。目前，推流域名仅支持配置B类型URL鉴权。

* 为拉流域名配置URL鉴权：控制哪些URL可以拉流，确保观众只能通过指定URL观看。拉流域名支持配置A、B、C三种类型URL鉴权。


<span id="882ce378"></span>
# 前提条件

你已添加域名。更多信息，请参见[添加域名](https://docs.byteplus.com/docs/byteplus-media-live/docs-domain-zh-CN)。

<span id="f9dd2d8d"></span>
# URL鉴权流程

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ebd6ea56ff424d2e8dc7334085832fd5~tplv-goo7wpa0wc-image.image) </span>


1. 你的服务器生成鉴权URL，并将这些URL提供给用户。

2. 用户使用鉴权URL向BytePlus MediaLive服务器发送推流或拉流请求。

3. BytePlus MediaLive服务器通过比对URL中的鉴权参数与请求中的参数，验证请求是否有效。

   * 若请求有效，BytePlus MediaLive服务器会响应，允许用户成功推流或拉流。

   * 若请求无效，服务器返回403错误并拒绝请求。这样可防止用户推流或拉流，保护直播流资源。


<span id="e7e3f739"></span>
# 操作步骤


1. 登录[BytePlus MediaLive控制台](https://console.byteplus.com/live)。

2. 在左侧导航栏，点击**域名**。

3. 在**域名**页面，找到需要配置推流或拉流的域名，在**操作**列点击**设置**，进入域名设置页面。

4. 点击**访问控制**标签页。

5. 打开**URL鉴权**开关，或在**URL鉴权**区域点击**编辑**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b89826da54b947279e3aa61e56ecab5e~tplv-goo7wpa0wc-image.image) </span>

6. 在弹出的**编辑URL鉴权**对话框中，根据业务需求选择以下任意一种鉴权类型，并完成相应配置。

   * [A类型URL鉴权](https://docs.byteplus.com/docs/byteplus-media-live/docs-url-authentication-zh-CN#1747184f)

   * [B 类型 URL 认证](https://docs.byteplus.com/docs/byteplus-media-live/docs-url-authentication-zh-CN#1c5d686d)

   * [C 类型 URL 认证](https://docs.byteplus.com/docs/byteplus-media-live/docs-url-authentication-zh-CN#a4f520fc)

      所有鉴权类型均采用MD5加密算法。

      完成URL鉴权配置约5分钟后，用户只能通过鉴权URL推流或拉流，原始URL将无法使用。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">默认情况下，推流域名已开启 URL 认证。   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">目前，推流域名仅支持 B 类型 URL 认证。   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">如上述认证类型无法满足您的业务需求，可<a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980">提交工单</a>联系技术支持，完成自定义 URL 认证配置。   </div>
   

7. 获取鉴权URL。

   你可以根据各鉴权类型的说明手动构造鉴权URL，也可按以下步骤使用地址生成器。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">对于已配置自定义 URL 认证的域名，获取认证 URL 时，您可以根据自定义认证规则自行拼接 URL，或<a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980">提交工单</a>联系技术支持。   </div>
   

   1. 在左侧导航栏，点击**地址生成器**。

   2. 选择**推流地址**或**拉流地址**。

   3. 选择域名，并配置**AppName**、**StreamName**和过期时间。更多信息，请参见[Generating stream addresses](https://docs.byteplus.com/docs/byteplus-media-live/docs-address-generator)。

   4. 点击**生成推流地址**或**生成拉流地址**。

   5. 在页面右侧获取鉴权URL。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b484ff0075ff494d885701d5665904fe~tplv-goo7wpa0wc-image.image) </span>


<span id="1747184f"></span>
## A类型URL鉴权

<span id="8f01aaf5"></span>
### 工作原理

鉴权URL格式：

```Plain
OriginalURL?auth_key={timestamp}-{rand}-{uid}-{md5hash}
```



|字段 |接口行为 |示例值 |
|---|---|---|
|auth_key |签名参数的名称。您可以在控制台的**编辑 URL 认证**对话框中配置名称。 |`auth_key` |
|timestamp |Unix 时间戳，单位为秒。支持十进制或十六进制，且必须在控制台的**编辑 URL 认证**对话框中选择相同的时间格式。<br><br>该字段与控制台**编辑 URL 认证**对话框中配置的有效期配合使用，用于计算实际签名失效时间。签名失效后，用户无法通过认证 URL 拉流。<br><br>签名失效时间 = `timestamp` + 有效期。例如，若 `timestamp` 的值为 `1758296819`（2025\-09\-19 23:46:59），有效期为 600 秒，则签名失效时间为 `1758297419`（2025\-09\-19 23:56:59）。 |`1758296819` |
|rand |一个随机数。可以使用 UUID（通用唯一标识符）格式，且该字段不能包含连字符（\-）。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">当你在控制台使用地址生成器生成鉴权 URL 时，该字段的值始终为<code>0</code>。</div><br> |`123e4567` |
|uid |用户 ID。保留参数，目前未使用。将该值设置为 `0`。 |`0` |
|md5hash |使用 MD5 加密算法计算得到的 32 位小写字符串。<br><br>计算公式如下。<br><br>```Plain```<br>```sstring = "{URI}-{timestamp}-{rand}-{uid}-{key}"```<br>```md5hash = md5sum(sstring)```<br><br><br><br>* `URI`：原始 URL 的路径部分，即域名后的内容。例如，原始 URL 为 `http://pull.example.com/live/test.flv`，则 URI 的值为 `/live/test.flv`。<br><br>* `key`：主 KEY 或副 KEY，可在控制台的**Edit URL authentication**对话框中进行配置。例如，`123abc`。<br><br><br>在此示例中，`{URI}-{timestamp}-{rand}-{uid}-{key}`的值为`/live/test.flv-1758296819-123e4567-0-123abc`。对该值生成 MD5 哈希后，会得到一个 32 位小写字符串，此时`md5hash`的值为`fbe5e26c0b7abe1431c3c897f7bdc278`。 |`fbe5e26c0b7abe1431c3c897f7bdc278` |


鉴权URL示例：

```Plain
http://pull.example.com/live/test.flv?auth_key=1758296819-123e4567-0-fbe5e26c0b7abe1431c3c897f7bdc278
```


<span id="7cb9e341"></span>
### 认证流程


1. BytePlus MediaLive 服务器收到用户的认证 URL 请求后，会对`{URI}-{timestamp}-{rand}-{uid}-{key}`的值进行 MD5 哈希，生成一个 32 位小写字符串。在本主题示例中，最终生成的字符串为`fbe5e26c0b7abe1431c3c897f7bdc278`。

2. BytePlus MediaLive 服务器会校验认证 URL 中的认证参数。只有同时满足以下两项校验，认证才会通过。

   * 判断服务器计算出的签名值是否与请求中的签名值一致。如果一致，则认证通过。在本主题示例中，签名值为`auth_key=1758296819-123e4567-0-fbe5e26c0b7abe1431c3c897f7bdc278`。

   * 判断签名是否有效。服务器会将当前时间与签名失效时间（`timestamp` + 有效期）进行比较。如果签名失效时间晚于当前时间，则判定签名有效，认证通过。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">对于用于拉取长时长流的 RTMP 和 FLV 等协议，当用户发起拉流请求时，BytePlus MediaLive 服务器会校验认证参数。校验通过后，用户可以持续拉流，不受签名失效时间影响。因此，只要请求在签名失效前发起，拉流不会因签名失效而中断。只有新发起的拉流请求会因签名失效而失败。   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">HLS 协议用于分段视频回放，用户会持续发起新的拉流请求以获取视频分段。每次用户发起拉流请求时，BytePlus MediaLive 服务器都会校验认证参数。因此，一旦签名失效，请求将被拒绝，导致回放中断。由于直播流回放过程中会频繁请求新分段，建议设置较长的签名失效时间，以避免直播流回放失败。   </div>
   

3. 根据认证结果判断请求是否有效。

   * 认证通过：请求有效，服务器响应请求。用户可以成功拉流。

   * 认证失败：请求无效。返回 403 错误，拒绝请求。用户无法拉流，从而保护直播流资源。


<span id="8ad6a89e"></span>
### 控制台配置

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/18d57f989cc14a7cb9a4f454b6bee9b7~tplv-goo7wpa0wc-image.image) </span>


|配置项 |接口行为 |
|---|---|
|主 KEY |主 KEY。<br><br>值长度必须为 1\-100 个字符，可包含数字（0–9）、小写字母（a–z）和大写字母（A–Z）。<br><br>也可点击输入框右侧的图标，随机生成包含数字、小写和大写字母的 24 位 KEY。 |
|副 KEY |副 KEY，用于无缝更新主 KEY。<br><br>值长度必须为 1\-100 个字符，可包含数字（0–9）、小写字母（a–z）和大写字母（A–Z）。<br><br>也可点击输入框右侧的图标，随机生成包含数字、小写和大写字母的 24 位 KEY。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">为防止在更换主 KEY 时出现在线服务中断，可以使用副 KEY 生成认证 URL，实现平滑过渡。在过渡期间，可以将认证 URL 替换为副 KEY 生成的版本。主 KEY 更换后，逐步将认证 URL 替换为新主 KEY 生成的认证 URL。</div><br> |
|签名参数 |签名参数的名称。默认值为`auth_key`。<br><br>值长度必须为 1\-100 个字符，可包含：<br><br><br>* 数字（0\-9）<br><br>* 小写字母（a\-z）<br><br>* 大写字母（A\-Z）<br><br>* 下划线（_）<br><br>* 连字符（\-）<br><br>* 点（.）<br><br>* 逗号（,）<br><br>* 感叹号（!）<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">该值必须包含至少一个字母。</div><br> |
|有效期 |签名的有效期。单位：秒。默认值为`600`。取值范围：[0, 2592000]。<br><br>该参数与认证 URL 中的`timestamp`参数配合使用，可用于计算实际签名失效时间。签名失效后，用户无法通过认证 URL 拉流。<br><br>签名失效时间 = `timestamp` + 有效期。例如，若`timestamp`的值为`1758296819`（2025\-09\-19 23:46:59），有效期为 600 秒，则签名失效时间为`1758297419`（2025\-09\-19 23:56:59）。 |
|时间戳基准 |`timestamp`的时间格式。默认值为**Decimal**。有效值：<br><br><br>* **Decimal**<br><br>* **Hexadecimal** |


<span id="1c5d686d"></span>
## B 类型 URL 认证

<span id="28f7c6dd"></span>
### 工作原理

认证 URL 格式：

```Plain
OriginalURL?sign=md5(/{AppName}/{StreamName}{key}{timestamp})&expire=timestamp
```



|字段 |接口行为 |示例值 |
|---|---|---|
|sign |签名参数的名称。你可以在控制台的**编辑 URL 鉴权**对话框中配置该名称。 |`sign` |
|AppName |`AppName`字段在直播流地址中的取值。<br><br>取值长度为 1\-30 个字符，可包含：<br><br><br>* 数字（0\-9）<br><br>* 小写字母（a\-z）<br><br>* 大写字母（A\-Z）<br><br>* 下划线（_）<br><br>* 连字符（\-）<br><br>* 点号（.）<br><br><br>例如，若原始 URL 为`http://pull.example.com/live/test.flv`，则`AppName`的取值为`live`。 |`live` |
|StreamName |`StreamName`字段在直播流地址中的取值。<br><br>取值长度为 1\-100 个字符，可包含：<br><br><br>* 数字（0\-9）<br><br>* 小写字母（a\-z）<br><br>* 大写字母（A\-Z）<br><br>* 下划线（_）<br><br>* 连字符（\-）<br><br><br>例如，若原始 URL 为`http://pull.example.com/live/test.flv`，则`StreamName`的取值为`test`。 |`test` |
|key |主 KEY 或副 KEY，可在控制台的**编辑 URL 鉴权**对话框中配置。 |`123abc` |
|timestamp |Unix 时间戳，单位为秒。支持十进制或十六进制，且需在控制台的**编辑 URL 鉴权**对话框中选择相同的时间格式。<br><br>该字段与在控制台**编辑 URL 鉴权**对话框中配置的有效期共同用于计算实际签名失效时间。签名失效后，用户无法通过已鉴权的 URL 进行推流或拉流。<br><br>签名失效时间 = `timestamp` + 有效期。例如，若`timestamp`取值为`1758296819`（2025\-09\-19 23:46:59），有效期为 600 秒，则签名失效时间为`1758297419`（2025\-09\-19 23:56:59）。 |`1758296819` |
|expire |时间戳参数的名称。你可以在控制台的**编辑 URL 鉴权**对话框中配置该名称。 |`expire` |


根据`md5(/{AppName}/{StreamName}{key}{timestamp})`计算签名值。在本主题示例中，`/{AppName}/{StreamName}{key}{timestamp}`的值为`/live/test123abc1758296819`。对该值进行 MD5 哈希，生成一个 32 位小写字符串，结果为`1e2ea5d60de5adcf5e4b7688ccd76915`。

认证 URL 示例：

```Plain
http://pull.example.com/live/test.flv?sign=1e2ea5d60de5adcf5e4b7688ccd76915&expire=1758296819
```


<span id="a83c35b7"></span>
### 认证流程


1. BytePlus MediaLive 服务器收到用户的认证 URL 请求后，会对`/{AppName}/{StreamName}{key}{timestamp}`的值进行 MD5 哈希，生成一个 32 位小写字符串。在本主题示例中，最终生成的字符串为`1e2ea5d60de5adcf5e4b7688ccd76915`。

2. BytePlus MediaLive 服务器会校验认证 URL 中的认证参数。只有同时满足以下两项校验，认证才会通过。

   * 判断服务器计算出的签名值是否与请求中的签名值一致。如果一致，则认证通过。在本主题示例中，签名值为`sign=1e2ea5d60de5adcf5e4b7688ccd76915& expire=175829681 9`。

   * 判断签名是否有效。服务器会将当前时间与签名失效时间（`timestamp` + 有效期）进行比较。如果签名失效时间晚于当前时间，则判定签名有效，认证通过。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">对于 RTMP、FLV 等用于推流或拉流长时长流的协议，当用户发起推流或拉流请求时，BytePlus MediaLive 服务器会校验鉴权参数。校验通过后，用户可持续推流或拉流，不受签名失效时间影响。因此，只要在签名失效前发起请求，推流或拉流不会因签名失效而中断。只有新发起的推流或拉流请求会因签名失效而失败。   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">HLS 协议用于分片视频回放，用户会持续发起新的拉流请求以获取视频分片。每次用户发起拉流请求时，BytePlus MediaLive 服务器都会校验鉴权参数。因此，一旦签名失效，请求将被拒绝，导致回放中断。由于直播流回放过程中会频繁请求新分片，建议你设置较长的签名失效时间，以防止直播过程中回放失败。   </div>
   

3. 根据认证结果判断请求是否有效。

   * 认证通过：请求有效，服务器响应请求。用户可以成功推流或拉流。

   * 认证失败：请求无效。返回 403 错误，拒绝请求。用户无法推流或拉流，从而保护直播流资源。


<span id="3f8e2d6e"></span>
### 控制台配置

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d6fd24ca2a51482a9de27eacf1ace271~tplv-goo7wpa0wc-image.image) </span>


|配置项 |接口行为 |
|---|---|
|主 KEY |主 KEY。<br><br>取值长度为 1\-100 个字符，可包含数字（0–9）、小写字母（a–z）、大写字母（A–Z）。<br><br>你也可以点击输入框右侧的图标，随机生成包含数字、小写和大写字母的 24 位 KEY。 |
|副 KEY |副 KEY，用于无缝更新主 KEY。<br><br>取值长度需为 1\-100 个字符，可包含数字（0–9）、小写字母（a–z）和大写字母（A–Z）。<br><br>你也可以点击输入框右侧的图标，随机生成一个包含数字、小写字母和大写字母的 24 位 KEY。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">为防止在更换主 KEY 时出现在线服务中断，可以使用副 KEY 生成认证 URL，实现平滑过渡。在过渡期间，可以将认证 URL 替换为副 KEY 生成的版本。主 KEY 更换后，逐步将认证 URL 替换为新主 KEY 生成的认证 URL。</div><br> |
|签名参数 |签名参数的名称。默认值为`sign`。<br><br>取值长度需为 1\-100 个字符，可包含：<br><br><br>* 数字（0\-9）<br><br>* 小写字母（a\-z）<br><br>* 大写字母（A\-Z）<br><br>* 下划线（_）<br><br>* 连字符（\-）<br><br>* 点（.）<br><br>* 逗号（,）<br><br>* 感叹号（!）<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">该值必须包含至少一个字母。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">签名参数和时间戳参数不能使用相同的名称。</div><br> |
|时间戳参数 |时间戳参数的名称。默认值为`expire`。<br><br>取值长度需为 1\-100 个字符，可包含：<br><br><br>* 数字（0\-9）<br><br>* 小写字母（a\-z）<br><br>* 大写字母（A\-Z）<br><br>* 下划线（_）<br><br>* 连字符（\-）<br><br>* 点（.）<br><br>* 逗号（,）<br><br>* 感叹号（!）<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">该值必须包含至少一个字母。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">签名参数和时间戳参数不能使用相同的名称。</div><br> |
|有效期 |签名的有效期。单位：秒。默认值为`600`。取值范围：[0, 2592000]。<br><br>该参数与认证 URL 中的`timestamp`参数配合使用，可用于计算实际签名失效时间。签名失效后，用户无法通过认证 URL 推流或拉流。<br><br>签名失效时间 = `timestamp` + 有效期。例如，若`timestamp`的值为`1758296819`（2025\-09\-19 23:46:59），有效期为 600 秒，则签名失效时间为`1758297419`（2025\-09\-19 23:56:59）。 |
|时间戳基数 |`timestamp`的时间格式。默认值为**Decimal**。可选值：<br><br><br>* **Decimal**<br><br>* **Hexadecimal**<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">用于流推送的域名仅支持十进制时间格式。</div><br> |


<span id="a4f520fc"></span>
## C 类型 URL 认证

<span id="b10ab2b8"></span>
### 工作原理

认证 URL 格式：

```SQL
OriginalURL?txSecret=md5({key}{StreamName}{timestamp})&txTime=timestamp
```



|字段 |接口行为 |示例值 |
|---|---|---|
|txSecret |签名参数的名称。你可以在控制台的**Edit URL authentication**对话框中配置名称。 |`txSecret` |
|key |主 KEY 或副 KEY，可在控制台的**Edit URL authentication**对话框中进行配置。 |`123abc` |
|StreamName |直播流地址中`StreamName`字段的值。<br><br>取值长度需为 1\-100 个字符，可包含：<br><br><br>* 数字（0\-9）<br><br>* 小写字母（a\-z）<br><br>* 大写字母（A\-Z）<br><br>* 下划线（_）<br><br>* 连字符（\-）<br><br><br>例如，原始 URL 为`http://pull.example.com/live/test.flv`，则`StreamName`的值为`test`。 |`test` |
|timestamp |Unix 时间戳，单位为秒。支持十进制或十六进制，且需在控制台的**Edit URL authentication**对话框中选择相同的时间格式。<br><br>该字段与控制台**Edit URL authentication**对话框中配置的有效期配合使用，用于计算实际签名失效时间。签名失效后，用户无法通过认证 URL 拉流。<br><br>签名失效时间 = `timestamp` + 有效期。例如，若`timestamp`的值为`68cd7af3`（2025\-09\-19 23:46:59），有效期为 600 秒，则签名失效时间为`68cd7d4b`（2025\-09\-19 23:56:59）。 |`68cd7af3` |
|txTime |时间戳参数的名称。你可以在控制台的**Edit URL authentication**对话框中配置名称。 |`txTime` |


根据`md5({key}{StreamName}{timestamp})`计算签名值。在本主题示例中，`{key}{StreamName}{timestamp}`的值为`123abctest68cd7af3`。对该值进行 MD5 哈希，生成一个 32 位小写字符串，结果为`73af6af9c874d9d4cc50f8490325cd7b`。

认证 URL 示例：

```Plain
http://pull.example.com/live/test.flv?txSecret=73af6af9c874d9d4cc50f8490325cd7b&txTime=68cd7af3
```


<span id="cdbc1626"></span>
### 认证流程


1. BytePlus MediaLive 服务器收到用户的认证 URL 请求后，会对 `{key}{StreamName}{timestamp}` 的值进行 MD5 哈希，生成一个 32 位小写字符串。在本主题的示例中，最终生成的字符串为 `73af6af9c874d9d4cc50f8490325cd7b`。

2. BytePlus MediaLive 服务器会校验认证 URL 中的认证参数。只有同时满足以下两项校验，验证才会通过。

   * 判断服务器计算出的签名值是否与请求中的签名值一致。若一致，则验证通过。在本主题的示例中，签名值为 `txSecret=73af6af9c874d9d4cc50f8490325cd7b&txTime=68cd7af3`。

   * 判断签名是否有效。服务器会将当前时间与签名失效时间（`timestamp` + 有效期）进行比较。如果签名失效时间晚于当前时间，则认为签名有效，验证通过。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">对于 RTMP 和 FLV 等用于拉取长时长流的协议，当用户发起拉流请求时，BytePlus MediaLive 服务器会校验鉴权参数。校验通过后，用户可以持续拉流，不受签名失效时间影响。因此，只要请求在签名失效前发起，拉流不会因签名失效而中断。只有新发起的拉流请求会因签名失效而失败。   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">HLS 协议用于分片视频回放，用户会持续发起新的拉流请求以获取视频分片。每次用户发起拉流请求时，BytePlus MediaLive 服务器都会校验鉴权参数。因此，一旦签名失效，请求将被拒绝，导致回放中断。由于在直播流回放过程中会频繁请求新分片，建议将签名失效时间设置得更长，以防止直播流回放失败。   </div>
   

3. 根据验证结果判断请求是否有效。

   * 验证通过：请求有效，服务器响应请求。用户可以成功拉流。

   * 验证失败：请求无效。返回 403 错误，拒绝请求。用户无法拉流，从而保护直播流资源。


<span id="4c04cb54"></span>
### 控制台配置

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7060192fc9b5436b87d30286b0d8e4a4~tplv-goo7wpa0wc-image.image) </span>


|配置项 |接口行为 |
|---|---|
|主 KEY |主 KEY。<br><br>取值长度为 1\-100 个字符，可包含数字（0–9）、小写字母（a–z）和大写字母（A–Z）。<br><br>你也可以点击输入框右侧的图标，随机生成包含数字、小写和大写字母的 24 位 KEY。 |
|副 KEY |副 KEY，用于无缝更新主 KEY。<br><br>取值长度为 1\-100 个字符，可包含数字（0–9）、小写字母（a–z）和大写字母（A–Z）。<br><br>你也可以点击输入框右侧的图标，随机生成包含数字、小写和大写字母的 24 位 KEY。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">为防止在更换主 KEY 时出现在线服务中断，可以使用副 KEY 生成认证 URL，实现平滑过渡。在过渡期间，可以将认证 URL 替换为副 KEY 生成的版本。主 KEY 更换后，逐步将认证 URL 替换为新主 KEY 生成的认证 URL。</div><br> |
|签名参数 |签名参数的名称。默认值为`txSecret`。<br><br>取值长度为 1\-100 个字符，可包含：<br><br><br>* 数字（0\-9）<br><br>* 小写字母（a\-z）<br><br>* 大写字母（A\-Z）<br><br>* 下划线（_）<br><br>* 连字符（\-）<br><br>* 点号（.）<br><br>* 逗号（,）<br><br>* 感叹号（!）<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">该值必须包含至少一个字母。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">签名参数和时间戳参数不能使用相同的名称。</div><br> |
|时间戳参数 |时间戳参数的名称。默认值为`txTime`。<br><br>取值长度为 1\-100 个字符，可包含：<br><br><br>* 数字（0\-9）<br><br>* 小写字母（a\-z）<br><br>* 大写字母（A\-Z）<br><br>* 下划线（_）<br><br>* 连字符（\-）<br><br>* 点号（.）<br><br>* 逗号（,）<br><br>* 感叹号（!）<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">该值必须包含至少一个字母。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">签名参数和时间戳参数不能使用相同的名称。</div><br> |
|有效期 |签名的有效期。单位：秒。默认值为`600`。取值范围：[0, 2592000]。<br><br>该参数与鉴权 URL 中的`timestamp`参数配合使用，可用于计算实际签名失效时间。签名失效后，用户无法通过鉴权 URL 拉流。<br><br>签名失效时间 = `timestamp` + 有效期。例如，`timestamp` 的值为`68cd7af3`（2025\-09\-19 23:46:59），有效期为 600 秒，则签名失效时间为`68cd7d4b`（2025\-09\-19 23:56:59）。 |
|时间戳基数 |`timestamp`的时间格式。默认值为**Hexadecimal**。可选值：<br><br><br>* **Decimal**<br><br>* **Hexadecimal** |

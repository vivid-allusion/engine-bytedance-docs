---
title: "管理 SSL 证书"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-managing-certificates-zh-CN"
---

要为您的 MediaLive 域名实现通过 HTTPS 进行安全加密的流推送和拉取，可以使用证书托管功能。本主题提供分步说明，指导您如何将 SSL 证书上传至 MediaLive 控制台、有效管理证书，并为绑定到您的域名做好准备。

<span id="67b2ec91"></span>
## 限制

MediaLive 支持上传用于 Nginx 服务器类型的证书和私钥文件。

<span id="8c573f7b"></span>
## 添加 SSL 证书


1. 从您的证书提供商处下载 PEM 格式的 SSL 证书文件到您的计算机。

2. 登录 [BytePlus MediaLive 控制台](https://console.byteplus.com/live)。

3. 在左侧导航栏，选择 **设置** \> **证书**，进入证书列表页面。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8ba70f2ac8c4476688aa2ea51562caa5~tplv-goo7wpa0wc-image.image) </span>

4. 点击 **添加证书**，打开 **添加 HTTPS 证书**对话框，并按照提示添加证书。

   下表描述了参数：

   
   |**参数** |**接口行为** |
   |---|---|
   |证书名称 |自定义证书名称，不限制字符类型，最大长度为 40 个字符。 |
   |选择项目 |选择证书所属项目，配置项目后，具有项目权限的子账号可管理证书。 |
   |上传方式 |选择上传方式。<br><br><br>* 手动输入<br><br>* 文件上传 |
   |证书内容 |证书文件内容：<br><br><br>* 如果选择手动上传，请使用文本编辑器打开证书文件，并将内容复制到此字段。<br><br>* 如果选择文件上传，请选择本地证书文件。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">支持自动补全证书链。只需上传为域名签发的证书，证书链会自动补全。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">如选择上传证书链，请确保证书链包含服务器证书、中间证书和根证书。它们需按正确顺序排列（服务器证书在前，中间证书和根证书依次排列）。顺序错误会导致证书链无效。</div><br> |
   |私钥 |证书私钥文件内容：<br><br><br>* 选择手动上传时，请使用文本编辑器软件在本地打开证书私钥文件，并将证书私钥内容复制到此处。<br><br>* 选择文件上传时，请选择本地证书私钥文件进行上传。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">请确保证书私钥未设置密码保护。</div><br> |
   

5. 点击 **确认**保存证书。


<span id="82892b1b"></span>
## 管理 SSL 证书

在 **证书**页面，您可以对已添加的证书执行以下操作。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6939111c604049e19097063bce2601c5~tplv-goo7wpa0wc-image.image) </span>


|操作 |接口行为 |
|---|---|
|搜索指定证书 |可通过以下条件筛选证书：<br><br><br>* 证书状态：点击不同的标签页，可按状态查看证书。为确保域名的 HTTPS 加密不中断，必须及时更新已过期、即将过期或有变更的证书。<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/02b6f7ae51b7482a9b75de171b3b4b85~tplv-goo7wpa0wc-image.image) </span><br><br>* 证书名称：支持模糊、英文不区分大小写搜索。<br><br>* 链 ID：点击**链 ID**输入框，在弹出的对话框中输入所需的证书链 ID。一次最多可输入 50 个证书链 ID，每个 ID 单独占一行。英文不区分大小写。<br><br>* 可配置域名：可绑定到当前证书的域名。一次最多可输入 1 个域名。支持模糊搜索，英文区分大小写。<br><br>* 关联域名：当前已绑定证书的域名。点击**关联域名**输入框，在弹出的对话框中输入所需的关联域名。一次最多可输入 50 个域名，每个域名单独占一行。英文区分大小写。<br><br>* 关联域名状态：可在下拉列表中选择当前证书绑定域名的一个或多个状态。当域名状态为**在线**、**配置中**、**离线**或**缺少 ICP 备案**时，可为该域名更新证书或绑定其他证书。<br><br>* 项目搜索：在**查询项**下拉列表中选择证书项目。<br><br>* 证书过期时间：筛选在指定时间范围内过期的证书。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">可通过点击对应标签页获取某一状态的证书。其他条件需配置后，点击<strong>搜索</strong>，即可获取符合条件的证书。</div><br> |
|查看证书信息 |查看证书信息。<br><br>其中，<br><br><br>* 可点击证书的关联域名，跳转至该域名的 HTTPS 设置页面。<br><br>* 可按上传时间和过期时间对证书进行升序或降序排序。 |
|更新证书信息 |要更新证书信息，请点击其所在行的**更新**。更新后的证书仅对状态为**在线**、**配置中**、**离线**或**缺少 ICP 备案**的关联域名生效。 |
|删除证书 |若证书已不再使用，可点击证书右侧的**删除**。 |


<span id="a976fb30"></span>
## 后续操作

绑定 SSL 证书到域名并启用 HTTPS。有关如何启用 HTTPS 的更多信息，请参见 [HTTPS 配置](https://docs.byteplus.com/docs/byteplus-media-live/docs-https-zh-CN)。

<span id="53a4af28"></span>
## 常见问题

<span id="43d0f559"></span>
### 证书链顺序错误

**错误**：上传证书时出现 “证书链顺序错误，请检查证书并重新上传” 的错误。

**原因**：该问题可能是由于手动将证书组合成链导致。证书链由多个证书按一定顺序组成，链中的每个证书都由其后一个证书签发。如果链中的某个证书不是由下一个证书签发，则该链无效。

**解决方案**：MediaLive 证书管理支持自动补全证书链。您只需参考以下方法，获取仅为您的域名签发的证书进行上传，无需提交完整证书链。

假设您的原始证书链包含三个证书，其结构如下：

```Plain
-----BEGIN CERTIFICATE-----
Certificate A
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
Certificate B
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
Certificate C
-----END CERTIFICATE-----
```


您可以使用证书解析工具分别解析证书 A、证书 B 和证书 C，以查找为您的域名签发的证书。

假设您找到的证书是证书 A。那么，在上传证书时，只需输入以下内容即可成功上传证书：

```Plain
-----BEGIN CERTIFICATE-----
Certificate A
-----END CERTIFICATE-----
```

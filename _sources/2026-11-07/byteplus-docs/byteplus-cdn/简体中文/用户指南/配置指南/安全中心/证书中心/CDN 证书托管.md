---
title: "CDN 证书托管"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cdn-cert-hosting_zh-cn"
---

默认情况下，您通过 BytePlus CDN 上传的证书是托管在 BytePlus 证书中心的。除此之外，CDN 还提供了证书托管的能力，但需要您 [提交工单](https://console.byteplus.com/workorder/create) 来启用此能力。

CDN 除了能托管服务端证书以外，还能托管 CA 证书。如果您要启用 CDN 中依赖 CA 证书的特性（例如 [访问双向认证](https://docs.byteplus.com/docs/byteplus-cdn/mtls_zh-cn)），您需要先将相应的 CA 证书上传到 CDN 进行托管。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">主账号下最多能上传 500 本证书到 CDN 进行托管。</div>


在您启用 CDN 证书托管功能前，BytePlus CDN 控制台左导航栏的 **安全中心** 下只有 **证书中心** 菜单项；启用后，**安全中心** 下会新增独立的 **证书管理** 菜单项，该页面即为 CDN 证书托管页面。

**证书管理** 页面顶部提供以下两个操作入口：


* **配置证书**：将托管在 CDN 中的证书与一个或多个域名关联。具体操作步骤参见 [通过配置证书关联域名](https://docs.byteplus.com/docs/byteplus-cdn/cdn-cert-hosting_zh-cn#5e4d0956)。

* **上传证书托管**：将证书上传到 CDN 进行托管。具体操作步骤参见 [上传证书托管](https://docs.byteplus.com/docs/byteplus-cdn/cdn-cert-hosting_zh-cn#291be72b)。


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5bdc256e93614005a62b32e6f2290117~tplv-goo7wpa0wc-image.image) </span>

页面下方的证书列表展示了所有已托管在 CDN 中的证书，列表字段说明如下：


|**字段** |**说明** |
|---|---|
|证书 ID |表示该证书在 CDN 托管中的 ID，格式为 `cert_hosting-` 开头的字符串。 |
|证书名称 |表示证书的名称。 |
|证书状态 |表示证书的当前状态，可以是以下某个状态：<br><br><br>* **运行中**：证书有效。<br><br>* **即将过期**：离证书到期日不足一个月。<br><br>* **已过期**：证书已过期。<br><br><br>您可以点击列头的筛选图标，按 **运行中**、**即将过期**、**已过期** 进行筛选。 |
|证书来源 |对于 CDN 托管的证书，该字段值是 **CDN 服务托管**。 |
|证书类型 |表示证书的类型，可以是 **服务端证书** 或 **CA 证书**。 |
|可配置域名 |表示 CDN 中可以与该证书关联的域名。 |
|已关联域名 |表示 CDN 中已与该证书关联的域名。 |
|开始时间 |表示证书的签发时间。 |
|操作 |可对该证书进行的操作：<br><br><br>* **关联域名**：将该证书与一个或多个域名关联。具体操作步骤参见 [通过证书列表关联域名](https://docs.byteplus.com/docs/byteplus-cdn/cdn-cert-hosting_zh-cn#3ed6c205)。<br><br>* **删除**：删除该 CDN 托管证书。 |


<span id="291be72b"></span>
## 上传证书托管

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">无论您上传的是服务端证书还是 CA 证书，都建议证书文件包含完整的证书链。</div>



1. 在 BytePlus CDN 控制台的左导航栏，选择 **安全中心** \> **证书管理**。

2. 在 **证书管理** 页面，点击 **上传证书托管**。

3. 在 **上传证书托管** 页面，参考配置说明进行设置，然后点击 **上传**。


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1d825878feb440ab979ed47dcc886b23~tplv-goo7wpa0wc-image.image) </span>

<span id="7f201896"></span>
### 配置说明


|**配置** |**说明** |
|---|---|
|证书来源 |当前仅支持 **CDN 服务托管**。 |
|证书类型 |表示您要上传的证书类型。该配置有以下选项：<br><br><br>* **服务端证书**：用于域名的 HTTPS 访问。<br><br>* **CA 证书**：用于 CDN 中依赖 CA 证书的特性（例如 [访问双向认证](https://docs.byteplus.com/docs/byteplus-cdn/mtls_zh-cn)）。 |
|上传方式 |表示证书的上传方式。该配置有以下选项：<br><br><br>* **手动输入**：表示粘贴证书文件和私钥文件中的内容。<br><br>* **文件上传**：表示上传证书文件和私钥文件。 |
|证书文件 / CA 证书 |表示证书文件。证书文件必须包含完整的证书链，扩展名是 .crt 或者 .pem，内容以 `-----BEGIN CERTIFICATE-----` 开头。<br><br><br>* 当 **证书类型** 是 **服务端证书** 时，该字段名为 **证书文件**。<br><br>* 当 **证书类型** 是 **CA 证书** 时，该字段名为 **CA 证书**。 |
|证书私钥 |表示证书的私钥文件。私钥文件的扩展名是 .key 或者 .pem，内容以 `-----BEGIN XXX PRIVATE KEY-----` 开头。该字段仅在 **证书类型** 是 **服务端证书** 时显示。 |
|备注名称 |表示证书的备注。 |


<span id="add58a79"></span>
## 关联域名

将 CDN 托管的证书与域名关联后，该证书才能用于域名的相关安全配置。**证书管理** 页面提供了以下两种关联入口。

<span id="5e4d0956"></span>
### 通过配置证书关联域名

适用于一次性为多个域名批量关联同一本证书的场景。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/01c3f12d47ab44b69f2f300b1fb82590~tplv-goo7wpa0wc-image.image) </span>


1. 在 BytePlus CDN 控制台的左导航栏，选择 **安全中心** \> **证书管理**。

2. 在 **证书管理** 页面，点击 **配置证书**。

3. 在 **配置证书** 页面，按以下三个步骤完成配置：

   1. **选择证书**：

      * **证书来源**：固定为 **CDN 服务托管**。

      * **证书类型**：选择 **服务端证书** 或 **CA 证书**。

      * **配置模式**：选择 **单证书** 或 **双证书**。

      * **选择证书**：根据所选的 **配置模式**，操作有所不同。

         * **单证书**：在 **选择证书** 列表中，单选一本要关联的证书。如果列表中没有所需证书，请先返回 [上传证书托管](https://docs.byteplus.com/docs/byteplus-cdn/cdn-cert-hosting_zh-cn#291be72b) 完成上传。

         * **双证书**：从 **待选证书** 列表中点击对应证书行的 **添加到已选**，将证书添加到 **已选证书** 列表中。如果列表中没有所需证书，可点击 **上传其他证书** 直接上传。


设置完成后，点击 **下一步**。


2. **关联域名**：在 **关联域名** 步骤的左侧 **全部** 列表中勾选需要关联该证书的域名，被勾选的域名会出现在右侧 **已选** 列表中。选择完成后，点击 **下一步**。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">列表中只展示可与该证书关联的域名，已下线的域名不会展示。   </div>
   

3. **配置预检测**：平台会对所选域名的目标配置进行预检测，**检测结果** 列表会展示每个域名的 **变更确认** 状态（例如 **可变更无风险**）。对于不希望本次变更的域名，可点击该域名所在行的 **取消变更**。确认无误后，点击 **确认** 完成关联。


<span id="3ed6c205"></span>
### 通过证书列表关联域名

适用于在证书列表中对单本证书快速关联或调整域名的场景。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3d4e51f6d9774562a339d6e3ae6ffcfb~tplv-goo7wpa0wc-image.image) </span>


1. 在 BytePlus CDN 控制台的左导航栏，选择 **安全中心** \> **证书管理**。

2. 在 **证书管理** 页面的证书列表中，找到目标证书，并在该证书的 **操作** 列点击 **关联域名**。

3. 在 **关联域名** 页面，按以下两个步骤完成配置：

   1. **关联域名**：在左侧 **全部** 列表中勾选需要关联该证书的域名，被勾选的域名会出现在右侧 **已选** 列表中。选择完成后，点击 **下一步**。

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">列表中只展示可与该证书关联的域名，已下线的域名不会展示；列表中还会标注每个域名上当前已关联证书的状态（如 <strong>已过期</strong>），便于您筛选。      </div>
      

   2. **配置预检测**：平台会对所选域名的目标配置进行预检测，**检测结果** 列表会展示每个域名的 **变更确认** 状态。对于不希望本次变更的域名，可点击该域名所在行的 **取消变更**。确认无误后，点击 **确认** 完成关联。

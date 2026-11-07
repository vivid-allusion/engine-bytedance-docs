---
title: "SaaS Cloud-Hosted Version Usage Process"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/SaaS_Cloud-Hosted_Version_Usage_Process"
---

火山引擎智能数据洞察 DataWind 是一款支持千亿级别数据自助分析的一站式数据分析与协作平台，可打通从数据接入、数据整合、查询分析到全员协同共享的全流程，以数据门户、数字大屏、管理驾驶舱等可视化形态，助力业务用户实现智能洞察，让数据发挥价值。DataWind 支持云托管模式，该模式将数据存储与计算托管到云端客户自有 ByteHouse 云数仓版（CDW），为企业提供数据洞察和分析解决方案，提升数据查询、数据可视化效率。本文介绍了如何开通和配置 ByteHouse 云数仓版和 DataWind，帮助您快速上手使用。

<span id="529aeba9"></span>
# 配置流程概述


1. 在火山引擎购买并开通 **DataWind** **SaaS** **云托管版本**和 **ByteHouse** **云数仓版**服务。

2. 在火山引擎 **IAM** **访问控制**中创建 IAM 子用户，并授予 ByteHouse 云数仓版产品权限，用于后续连接配置。

3. 在 ByteHouse 中配置**计算组**、**角色**，用于在 DataWind 中配置 ByteHouse 云数仓版连接信息。

4. 根据 ByteHouse 中提供的连接信息，在 DataWind 中配置连接。

5. 配置完成后，即可正常使用 DataWind。


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a2df6391350341cb81eceee93db615c1~tplv-goo7wpa0wc-image.image) </span>

<span id="a8e0e7fa"></span>
# 准备工作


1. 访问[火山引擎官网](https://console.volcengine.com/auth/login)，登录或注册火山引擎账号。

2. 后续开通产品服务步骤需完成实名验证，如果您尚未实名验证，请先使用完成实名验证。


<span id="791ed5c7"></span>
# 操作步骤

<span id="34f8b734"></span>
## 步骤一：开通 DataWind 服务


1. 使用**火山引擎主账号**登录火山引擎，在 [DataWind 产品页](https://www.volcengine.com/product/datawind)单击**产品购买**，单击**智能数据洞察**·**云托管**，跳转至云托管版本购买页面。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/392e43e21709437582502e68326c5708~tplv-goo7wpa0wc-image.image) </span>

2. 在购买页面选择您需要的版本，按需选择增值服务，您可实时查看服务价格。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0c123e52f62e4db5a4ef216939a88f2e~tplv-goo7wpa0wc-image.image) </span>

3. 确认选购方案无误，阅读并同意服务协议/条款等内容后，单击**立即购买**。


<span id="f228e85d"></span>
## 步骤二：开通 ByteHouse 服务

使用**火山引擎主账号**登录火山引擎，在 [ByteHouse 产品页](https://www.volcengine.com/product/bytehouse)上购买并开通 ByteHouse 云数仓版服务，需确保 ByteHouse 与 DataWind 处于同一地域。开通 ByteHouse 操作详情请参考[开通 ByteHouse 云数仓版](https://www.volcengine.com/docs/6517/76325#%E5%BC%80%E9%80%9A-bytehouse-%E4%BA%91%E6%95%B0%E4%BB%93%E7%89%88)。

<span id="9b540a92"></span>
## 步骤三：创建火山引擎 IAM 子用户


1. 使用**火山引擎主账号**登录火山引擎 [IAM 访问控制](https://console.volcengine.com/iam)设置页面，在左侧导航栏，选择**用户管理** \> **用户**，单击**新建用户**按钮。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a9ba317116c4c54abd534560e049ee6~tplv-goo7wpa0wc-image.image) </span>

2. 选择创建子用户的方式。

   1. （推荐）通过用户名创建：通过主用户手机号码验证，快速创建子用户。

   2. 通过手机号或巨量引擎账号邀请：对方会收到邀请，可以自行创建子账号。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/19f672f36dbf4dc184f2b1f6503b40c4~tplv-goo7wpa0wc-image.image) </span>

3. 配置用户基本信息。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4346cef0bb3840349541befd896d3ae0~tplv-goo7wpa0wc-image.image) </span>

   * **用户信息**：填写子用户的用户名（必选）、手机号、邮箱、显示名称、备注、标签等信息。

   * **访问方式**：需勾选”**编程访问**“和”**控制台访问**“选项，并为用户分配密码。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">您可以根据自身安全策略要求，选择是否启用“下次登录时重置密码”与“登录时开启 MFA 二次身份认证”功能。   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">开启”下次登录时重置密码“功能后，在用户的下次登录时，会弹出修改密码页面，完成后才可进入 ByteHouse 控制台。   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">开启”MFA 二次身份认证“功能后，每次登录时需要通过 TOTP 校验器 APP（如 Google Authenticator 等 ），或者是支持 FIDO Passkey 的终端设备来实现身份验证。具体可参见<a href="https://www.volcengine.com/docs/6261/70811">启用和解绑 MFA 设备</a>。   </div>
   

4. 配置 ByteHouse 产品权限。在权限策略中，搜索并选择 **ByteHouseFullAccess** 权限策略。

   ByteHouseFullAccess 权限策略对应 **ByteHouse** **管理员权限**，映射到 ByteHouse 内部的 **SystemAdmin** 角色。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9a26d2ec532744c3859dec7dbc4f7241~tplv-goo7wpa0wc-image.image) </span>

5. 完成权限配置后，单击**下一步**，审阅授予的权限，确认无误后，单击**下一步**，完成子用户创建。

   创建完成后，复制或保存您创建的 IAM 子用户的登录地址、账号、密码，用于后续子用户登录 ByteHouse 操作和 DataWind 连接配置。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/770eb76988d941db9edfee962c62db12~tplv-goo7wpa0wc-image.image) </span>


<span id="24e58ad9"></span>
## 步骤四：ByteHouse 侧配置


1. 使用步骤三中创建的 **IAM** **子用户**登录 [ByteHouse 云数仓版控制台](https://console.volcengine.com/bytehouse/region:bytehouse+cn-beijing/database)。

2. 为子账号设置默认计算组。单击顶部**租户管理**，在**参数设置**页签下的**用户参数**模块，设置默认计算组。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/41965f5531ba403a8d58c02880a89cd1~tplv-goo7wpa0wc-image.image) </span>

3. （可选）创建计算组，并记录计算组名称，用于后续为 DataWind 配置连接信息，并为 DataWind 提供所需的查询和计算资源。

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">如果您想要直接使用步骤 2 中设置的默认计算组，可记录默认计算组名称，并跳过该步骤。   </div>
   

   1. 单击顶部**计算组**，单击  **+计算组**，您可按需选择计算组配置信息，详情请参考[创建/编辑计算组](https://www.volcengine.com/docs/6517/1257382)。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e5d3e384fdf44fbb9945cffce9c8a145~tplv-goo7wpa0wc-image.image) </span>

   2. 创建完成后，在计算组列表中，复制并记录计算组名称，用于后续在 DataWind 中配置 ByteHouse 授权信息。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8e80733cf9d54972a9cc2ed8df6c2a51~tplv-goo7wpa0wc-image.image) </span>

4. 单击顶部**权限管理**，单击左侧边栏的**用户**页签，在用户列表中搜索步骤三中创建的子用户，确认并记录以下信息，用于后续在 DataWind 中配置 ByteHouse 授权信息：

   1. 确认该用户的已授予的角色为 **SystemAdmin**，确认无误后，记录该角色名。

   2. 查看并复制用户 ID。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c4413aff68d440f9b28e15d01a94015e~tplv-goo7wpa0wc-image.image) </span>


<span id="c8466196"></span>
## 步骤五：DataWind 侧配置

使用步骤四中复制的 ByteHouse 云数仓版子账号 ID、角色、计算组信息，填写云托管环境的配置。填写完成后单击**提交配置**，即可开始使用。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/31bf905d7012494cb40b813176cd5ccb~tplv-goo7wpa0wc-image.image) </span>

**参数说明**


|参数项 |配置说明 |
|---|---|
|ByteHouse 托管主账号 ID |火山引擎主账号 ID。您可在**火山引擎控制台**上，单击右上角用户头像，查看并复制账号 ID。<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/83b4a7fcf1cb49a3a5fae9c4d0dc8603~tplv-goo7wpa0wc-image.image) </span> |
|ByteHouse 托管子账号 ID |填写步骤四中复制的 ByteHouse 子用户 ID。 |
|ByteHouse 托管角色 |填写步骤四中记录的 ByteHouse 子用户角色。 |
|ByteHouse 计算组名称 |在下拉列表中选择默认计算组名称或您在步骤四中创建的计算组名称。 |
|ByteHouse 托管角色配置 |请再次确认您已为 ByteHouse 托管子账号配置了默认计算组和角色，可单击 **ByteHouse** **默认参数设置按钮**，跳转至 ByteHouse 云数仓版控制台确认：<br><br><br>1. 通过**租户管理** \> **参数设置** \> **用户参数**路径，查看是否已配置默认计算组。<br><br>2. 通过**权限管理** \> **用户**路径，查看子用户角色是否为 SystemAdmin。<br><br><br>如果未配置上述信息，后续将无法正常使用 DataWind 云托管版本的功能。 |


<span id="fed8d6f0"></span>
## 步骤六：开始使用

完成以上所有配置之后，您可以正常按照 DataWind 的 SaaS 标准功能接入 ByteHouse CDW 数据，并开始正常使用数据洞察功能，具体操作请参见以下文档：


* 接入 ByteHouse CDW 数据源：[ByteHouse CDW](https://www.volcengine.com/docs/4726/152195)。

* 其他操作请参见 [DataWind 官方文档](https://www.volcengine.com/docs/4726)。


<span id="9598bcfc"></span>
# Trial of the cloud\-hosted version

For users of the trial DataWind SaaS version with a **Volcano Engine primary account**, go to the "System Management" \- "System Information" page and click "Trial Cloud\-Hosted Version".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0067ed38751e4592b5e223bc7cc98031~tplv-goo7wpa0wc-image.image) </span>

Click "OK" to enter the cloud\-hosted configuration page. For detailed configuration operations, see the instructions above [步骤五：DataWind 侧配置](https://docs.byteplus.com/docs/undefined/68bea0b486defa05443e88e4#66734728). After configuration, you can trial the SaaS cloud\-hosted version.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Only the trial version supports switching between SaaS and cloud\-hosted versions (the official version does not support this). After switching, the system does not migrate resources configured in the original trial version.</div>


* <div data-tips="true" data-tips-type="warning">After users switch to the cloud\-hosted trial version or SaaS trial version, the current trial version will inherit the remaining trial time from the previous trial version.</div>



To switch back to the DataWind SaaS trial version, click "Trial SaaS Version", then click "OK" to switch back to the SaaS trial version.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/54d3f52908354ed7bd1094fa092fb23a~tplv-goo7wpa0wc-image.image) </span>

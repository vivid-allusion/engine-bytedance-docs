---
title: "配置 hosts 文件测试加速域名"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-test-domain-name-with-hosts-cn"
---

在前面的步骤中，您已成功地在 BytePlus CDN 控制台中添加了域名。同时，CDN 已经为您的域名分配了一个 CNAME。在您配置 DNS 解析记录将您站点的域名指向该 CNAME 之前，建议您配置 hosts 文件测试域名的访问。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">需要留意的是，测试 CNAME 的过程会在 CDN 侧产生极少量的流量，这些流量是会被计费的。</div>


* <div data-tips="true" data-tips-type="tip">该文档是基于 <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-overview_1-cn">教程介绍</a> 中描述的场景。</div>



<span id="步骤一：获取-cname"></span>
# 步骤一：获取 CNAME


1. 登录 [BytePlus CDN 管理控制台](https://console.byteplus.com/cdn)。

2. 在左侧导航栏，点击 **域名接入**。

3. 在 **域名接入** 页面，找到您添加的域名 `www.example.com`。

4. 在 **CNAME** 列，点击 **复制** 按钮。

   您获取的 CNAME 应该是 `www.example.com.bplslb.com`。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_a7cf581a83bea9367fef6aeaad7d7a36.png) </span>


<span id="步骤二：获取该-cname-的-ip-地址"></span>
# 步骤二：获取该 CNAME 的 IP 地址

根据您客户端的操作系统，参考以下步骤获取 CNAME 的 IP 地址。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">以下截图中的那个 IP 地址仅用于演示目的，并不是真实的。</div>


<span id="macos-和-linux：使用-dig-命令获取该-ip-地址"></span>
## macOS 和 Linux：使用 dig 命令获取该 IP 地址


1. 在一个 Terminal 窗口中，运行命令 `dig www.example.com.bplslb.com`。

2. 在 **ANSWER SECTION** 下方，找到该 CNAME 的 IP 地址。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_004df10162659ecc7b86c105e5061295.png) </span>


<span id="windows：使用-ping-命令获取该-ip-地址"></span>
## Windows：使用 ping 命令获取该 IP 地址


1. 在一个 **命令提示符** 窗口中，运行命令 `ping www.example.com.bplslb.com`。

2. 在命令下方的信息中，找到该 CNAME 的 IP 地址。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_c1de146606226ae567cdd4f04d55fd64.png) </span>


<span id="第三步：验证该-ip-地址是否归属于-cdn"></span>
# 第三步：验证该 IP 地址是否归属于 CDN

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">在本文中，假设您获取的 IP 地址是 <code>203.0.113.5</code>。</div>



1. 打开 [诊断工具](https://console.byteplus.com/cdn/cdn-volc/diagnosis)。

2. 输入获取的 IP 地址，点击 **查询**。

3. 在查询结果中，查看 **是否归属于 CDN** 列显示的值。

   * 如果值是 **是**，表示该 IP 地址是一个 CDN 节点的，符合预期。

   * 如果值是 **否**，表示该 IP 地址不归属于 CDN。请 [提交工单](https://console.byteplus.com/workorder/create)。


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_f6f7c3357f98bc6f88b0bcba18f1231e.png) </span>

<span id="第四步：配置操作系统的-hosts-文件"></span>
# 第四步：配置操作系统的 hosts 文件

在 hosts 文件中，您需要添加一个条目，将您站点的域名指向该 IP 地址。

根据您客户端的操作系统，参考以下步骤配置 hosts 文件。

<span id="masos：修改-hosts-文件"></span>
## masOS：修改 hosts 文件


1. 在一个 Terminal 窗口中，运行命令 `sudo nano /etc/hosts`。

2. 在 hosts 文件文件末尾，输入 `203.0.113.5 www.example.com`。

3. 按 `CTRL` + `O` 保存文件，然后按 `CTRL` + `X` 退出编辑。

4. 为了使变更生效，运行命令 `sudo killall -HUP mDNSResponder`。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_580c68beca18fbf7b34c311d4fd06a1d.png) </span>


<span id="windows：修改-hosts-文件"></span>
## Windows：修改 hosts 文件


1. 使用 **Run as administrator** 选项打开 Notepad。

2. 按 `CTRL` + `O`，在 **File name** 处输入 `%Windir%\System32\drivers\etc\hosts`，然后点击 **Open**。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_a14fc1f526ec32b2efa5f3f5e7ee79df.png) </span>

3. 在 hosts 文件末尾，输入 `203.0.113.5 www.example.com`。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_5025e1778d51d53d116d95b6dc082c22.png) </span>

4. 按 `CTRL` + `SHIFT` + `S` 保存更改。

5. 为了使变更生效，打开一个 **命令提示符** 窗口，然后运行命令 `ipconfig /flushdns`。


<span id="步骤五：测试域名"></span>
# 步骤五：测试域名

测试前，请检查控制台中您添加的域名的状态是否是 **在线**。如果不是，请稍等几分钟后，再刷新页面检查。如果依然不是 **在线**，请 [提交工单](https://console.byteplus.com/workorder/create)。

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_dd0d8497fe6da72f2ce94b2cdf0b67a6.png) </span>


1. 使用浏览器访问您站点上的某个文件。假设该文件的地址是 `www.example.com/sample.png`。

2. 按 `F12` 打开 **Developer tools**。

3. 在 **Network** 标签页中的左侧文件列表中，找到 `sample.png`，然后点击该文件。

4. 在右侧的 **Headers** 标签页中，查看 **Remote Address** 是否为 `203.0.113.5`。

   * 如果是，表示测试成功。

   * 如果不是，表示测试不成功。请检查 hosts 文件是否配置正确。


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_abd3bbe1441a7551bf08cc605d246878.png) </span>

如果测试成功，请在 hosts 文件中删除您刚才添加的条目。然后在您域名的 DNS 解析服务商处，创建一条 CNAME 记录。在 CNAME 记录中，将您的站点域名指向 `www.example.com.bplslb.com`。

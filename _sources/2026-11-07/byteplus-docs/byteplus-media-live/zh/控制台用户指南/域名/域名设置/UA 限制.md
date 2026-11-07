---
title: "UA 限制"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-ua-blocklist-and-allowlist-zh-CN"
---

User\-Agent（UA）是一个 HTTP 请求头，包含客户端发起请求时的系统类型和浏览器版本等信息。你可以通过拉流请求中的 UA 请求头值，允许或阻止特定用户访问你的域名。

<span id="630434dd"></span>
## 操作流程


1. 登录 [BytePlus MediaLive 控制台](https://console.byteplus.com/live)。

2. 在左侧导航栏，点击 **域名**。

3. 找到你要配置的域名，在 **操作**列点击 **设置**。

4. 点击 **访问控制**标签页。

5. 在 **UA 限制**开关右侧点击 **编辑**。

6. 在弹出的 **编辑 UA blocklist 和 allowlist**对话框中，配置以下参数。

   
   |**配置** |**接口行为** |
   |---|---|
   |名单类型 |此配置的选项如下：<br><br><br>* **blocklist**：如果请求的 UA 请求头在 blocklist 中，则该请求会被拒绝，返回 403 状态码。<br><br>* **allowlist**：只有 UA 请求头在 allowlist 中的请求才能访问你的资源。其他请求将被拒绝，返回 403 状态码。 |
   |规则 |输入一个或多个 UA 请求头。所有条目的总长度不得超过 30,000 个字符。最多可输入 1,000 个 UA 请求头。<br><br><br>* UA 请求头区分大小写。<br><br>* 你可以使用通配符（\*）表示任意数量的字符。`*`只能出现在 UA 请求头的开头或结尾。你可以在 UA 请求头的开头和结尾都添加 `*`，例如 `*curl*`。<br><br>* UA 请求头不能为 `*`。<br><br>* UA 请求头不能包含 `**`。<br><br>* UA 请求头只能包含可打印的 ASCII 字符，不能包含 Delete（ASCII 码 127）。<br><br>* 每行输入一个 UA。<br><br>* UA 请求头不能仅由空格组成。 |
   |包含空 UA 请求头 |指定是否将规则应用于 UA 请求头为空或缺失的请求。例如，如果 **名单类型**设置为 **blocklist**，且 **包含空 UA 请求头**设置为 **包含**，则 UA 请求头为空或缺失的请求会被拒绝。 |
   

7. 点击 **确认**。

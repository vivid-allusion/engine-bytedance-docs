---
title: "Referer"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-referer-zh-CN"
---

您可以配置 Referer 黑名单或白名单，以控制对您的内容的访问并防止未经授权的访问。

HTTP 请求头中的 Referer 字段用于指示请求的来源。例如，如果您在页面 `https://www.example.com/test.html` 上点击指向 `https://www.byteplus.com` 的链接，则 HTTP 请求头将包含：

```Plain
Referer: https://www.example.com/test.html
```


空 Referer 表示该请求没有可识别的来源。

<span id="0978b46f"></span>
## 适用范围

拉流域名

<span id="8e696869"></span>
## 前提条件

已添加域名

<span id="882853d7"></span>
## 操作步骤


1. 登录 [BytePlus MediaLive 控制台](https://console.byteplus.com/live)。

2. 在左侧导航栏，点击 **域名**。

3. 找到您要查看的域名，在 **操作**列点击 **设置**。

4. 点击 **访问控制**标签页。

5. 在 **Referer**开关右侧点击 **编辑**。

6. 在弹出的 **编辑 Referer**对话框中，**Referer**会自动开启。配置以下参数。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1cf760bb74934ad396eb212ce2708631~tplv-goo7wpa0wc-image.image) </span>

   
   |**参数** |**接口行为** |
   |---|---|
   |Referer 类型 |选择 **黑名单**或**白名单**。<br><br><br>* **黑名单**：拦截来自指定域名的请求。<br><br>* **白名单**：仅允许来自指定域名的请求。 |
   |Referer \*\*\*\* 规则 |您可以添加完整域名或泛域名作为规则。目前最多可配置 100 条规则。配置示例如下。<br><br><br>* **如果您将规则配置为** `www.example.com`：<br><br>   * 该规则仅匹配完全相同的域名 `www.example.com`。<br><br>   * 不会匹配 `http(s):// www.example.com`、`www.example.com/` 或 `http(s):// www.example.com/path`。<br><br>* **如果您将规则配置为** `*. example.com`：<br><br>   * 将匹配 `http(s):// www.example.com`。<br><br>   * 不会匹配 `http(s):// www.example.com/`。<br><br>* **如果您将规则配置为** `*.example.*`：<br><br>   将匹配以下所有内容：`www.example.com`、`http(s):// www.example.com`、`www.example.com/` 和 `http(s):// www.example.com/path`。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">如需配置超过 100 条规则，请 <a href="https://console.byteplus.com/workorder/create">联系支持</a>。</div><br> |
   |空 Referer |勾选此项以允许 Referer 为空的请求。 |
   

7. 点击 **确认**。

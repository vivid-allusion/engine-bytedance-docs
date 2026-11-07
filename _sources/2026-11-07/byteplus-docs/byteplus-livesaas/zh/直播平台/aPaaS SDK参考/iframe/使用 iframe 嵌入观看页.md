---
title: "使用 iframe 嵌入观看页"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-docs-embedding-a-viewing-page-with-iframe-zh-CN"
---

要将 BytePlus Live 直播流集成到您自己的网站中，可以通过 iframe 嵌入观看页。此方法可以降低开发成本，并允许观众直接在您的页面上观看，有助于吸引新用户并留住现有用户。本指南提供了成功实现所需的步骤、代码示例和重要注意事项。

<span id="542f23c9"></span>
## 注意


* 请勿执行任何读取或写入 Cookie 的操作，因为部分浏览器会禁用第三方 Cookie。这意味着以下功能不受支持：发布发送时间为观众进入直播间时的问卷，以及要求观众在进入直播间前登录（即将观看限制设置为密码、手机号等）。如需使用这些功能，可以通过添加 CNAME 记录自定义内嵌页（即观看页）的域名，使您的页面与内嵌页使用相同的域名。此时，内嵌页的 Cookie 将作为第一方 Cookie 写入，从而避免第三方 Cookie 限制。如需添加 CNAME 记录，请联系 BytePlus Live 技术支持。

* 建议您将观看限制设置为**自定义**，并选择观众在登录您的账号系统后可直接进入直播间、无需二次登录的方案。更多信息，请参见[Solution B](https://docs.byteplus.com/docs/byteplus-livesaas/docs-applying-advanced-viewing-restrictions-zh-CN#29214805)。

* 请勿在 HTTPS 页面中嵌入 HTTP 页面，否则页面可能无法正常显示。

* 嵌入聊天互动菜单时，PC 端最小宽度为 320 px。


<span id="b1c0e113"></span>
## 嵌入方式


1. 将可嵌入的内嵌链接设置为`iframe` 标签的 src 属性。

   * 如需全页嵌入（例如在 PC 端嵌入整个观看页），可参考以下示例。

      ```Plain
      <iframe src="https://live.byteplus.com/1323/6****21?platform=pc"></iframe>
      ```
      

   * 如需嵌入特定模块（如播放器），可参考以下示例。

      ```Plain
      <iframe src="https://live.byteplus.com/1323/6****21?mode=player"></iframe>
      ```
      

   请将`https://live.byteplus.com/1323/6****21`替换为您的直播间观看页 URL。有关内嵌链接支持的参数，请参见[参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-parameter-zh-CN)。如需监听内嵌页事件，请参见[事件](https://docs.byteplus.com/docs/byteplus-livesaas/docs-embedding-a-viewing-page-with-iframe-zh-CN)。

2. 设置`iframe` 元素的属性。示例如下。

   ```Plain
   <iframe src="https://live.byteplus.com/1323/6****21?platform=pc" width="1000" height="600" allowfullscreen="true" autoplay="true" allow=“fullscreen; screen-wake-lock; autoplay; picture-in-picture; camera; microphone” frameborder="0" border="0"></iframe>
   ```
   

   * `width`：`iframe` 元素的宽度。当值为数字时，单位为 px。当值为百分比时，表示相对于父容器宽度的百分比。

   * `height`：`iframe` 元素的高度。当值为数字时，单位为 px。当值为百分比时，表示相对于父容器高度的百分比。

   * `allowfullscreen="true"`：允许内嵌页进入全屏模式。如内嵌页包含播放器，建议添加此属性。

   * `autoplay="true"`：允许媒体自动播放。

   * `allow`：内嵌页支持的功能。多个参数值请用分号（;）分隔。有效值：

      * `fullscreen`：允许内容进入全屏模式。适用于内嵌页包含播放器的场景。

      * `screen-wake-lock`：保持屏幕常亮。

      * `autoplay`：允许媒体自动播放。

      * `picture-in-picture`：画中画（PiP）模式。仅适用于 PC 端。

   * `frameborder`：`iframe` 元素是否有边框。有效值：

      * `0`：无边框。

      * `1`：有边框。

   * `border`：`iframe` 元素的边框宽度。单位为 px。

3. 将 `iframe` 标签插入到你的页面中。

---
title: "Web 观播 SDK 常见问题"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-faqs-about-web-viewer-sdk-zh-CN"
---

<span id="can-i-directly-override-the-element-style-in-modules"></span>
## 我可以直接覆盖 `modules` 中的元素样式吗？

可以。Web 观播 SDK 的 DOM 层级和 `class` 属性值不可更改。你可以在 `modules` 中按需覆盖元素样式。

<span id="does-the-web-viewer-sdk-support-preload-related-features-such-as-requiring-viewers-to-enter-correct-invitation-codes-or-submitting-questionnaires-before-entering-the-live-room"></span>
## Web 观播 SDK 是否支持预加载相关功能，例如要求观众输入正确的邀请码或在进入直播间前提交问卷？

不支持，对于 Web 观播 SDK，权限仅由用户 token 决定。

<span id="how-can-i-get-the-user-token"></span>
## 如何获取用户 token？


* 若 `mode` 的值为 `1`，可通过调用 [GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-CN) 或进入 **Producer** \> **Page embedding** \> **Web SDK embedding**，在 BytePlus Live 控制台的直播间页面获取用户 token。

* 若 `mode` 的值为 `2`，可通过调用 [GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-CN) 获取用户 token。


<span id="how-long-is-a-user-token-valid"></span>
## 用户 token 有效期多久？

用户 token 永不过期。

<span id="why-am-i-unable-to-play-previews-or-playbacks-locally"></span>
## 为什么我无法在本地播放预告或回放？

只有将你的域名加入 BytePlus Live allowlist 后，才能播放预告和回放。如果使用本地调试的域名 `localhost`，则无法播放预告或回放。

<span id="what-should-i-do-if-the-sdk-initialization-failed-and-the-apiservice-sdkinit-interface-reported-an-error-after-my-web-app-is-deployed"></span>
## Web 应用部署后，SDK 初始化失败且 `apiservice/sdkinit` 接口报错时该怎么办？

Web 观播 SDK 的 API 不支持跨域调用。请联系 BytePlus Live 技术支持，将你的域名加入 BytePlus Live allowlist。

<span id="what-should-i-do-if-the-aspect-ratios-of-menus-are-incorrect-on-mobile-devices-after-i-enter-the-live-room-or-when-i-switch-between-menus"></span>
## 进入直播间或切换菜单后，移动设备上的菜单视频长宽比显示异常时该怎么办？

菜单的高度和宽度继承自其父元素。这说明你提供的容器存在问题。请勿将容器的高度和宽度设置为动态值，如 `auto` 和 `unset`。

<span id="what-should-i-do-if-the-player-on-my-ipad-shows-a-black-screen"></span>
## iPad 上播放器出现黑屏时该怎么办？

播放器在 iPad 拉流时可能存在兼容性问题。在业务代码中，可使用 `const isMobile = /(ipad|iphone|ipod|windows phone|android)/i.test(navigator.userAgent)` 检查加载的 SDK 脚本是否与浏览器的用户代理（UA）匹配。对于 iPad，必须引入移动端资源，而非 PC 端资源。

---
title: "Web Viewer SDK FAQs"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-faqs-about-web-viewer-sdk"
---

<span id="aa2a89d8"></span>
## Can I directly override the element style in `modules`?

Yes. The DOM hierarchy and `class` attribute values of the Web Viewer SDK cannot be changed. In `modules`, you can override the element style as required.

<span id="0cf5bcc4"></span>
## Does the Web Viewer SDK support preload\-related features, such as requiring viewers to enter correct invitation codes or submitting questionnaires before entering the live room?

No, for the Web Viewer SDK, permissions are only related to the user token.

<span id="74f082f5"></span>
## How can I get the user token?


* If the value of `mode` is `1`, get the user token by calling [GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi) or navigating to the **Producer** \> **Page embedding** \> **Web SDK embedding** page of the live room on the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).

* If the value of `mode` is `2`, get the user token by calling [GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi).


<span id="e9f203f8"></span>
## How long is a user token valid?

No expiration exists for user tokens.

<span id="6a025b97"></span>
## Why am I unable to play previews or playbacks locally?

You can play previews and playbacks only after your domain name is added to the BytePlus Live allowlist. You cannot play previews or playbacks if `localhost`, the domain name for local debugging, is being used.

<span id="05511e4b"></span>
## What should I do if the SDK initialization failed and the `apiservice/sdkinit` interface reported an error after my Web app is deployed and available online?

The APIs of the Web Viewer SDK cannot be called across domains. Contact BytePlus Live technical support to add your domain name to the BytePlus Live allowlist.

<span id="45c57a46"></span>
## What should I do if the aspect ratios of menus are incorrect on mobile devices after I enter the live room or when I switch between menus?

The height and width of a menu are inherited from its parent element, meaning there must be an issue with your provided container. Do not set the height and width of the container to unfixed values, such as `auto` and `unset`.

<span id="c0c412bb"></span>
## What should I do if my iPad player goes black?

Certain compatibility issues exist on iPads for players to pull streams. In your business code, use `const isMobile = /(ipad|iphone|ipod|windows phone|android)/i.test(navigator.userAgent)` to check whether the loaded SDK script conforms with the user agent (UA) of your browser. For iPads, you must import mobile device, not PC, resources.

---
title: "Integrate the Webex Application"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Integrate_the_Webex_Application"
---

This article introduces how to integrate the Webex application.

<span id="e8a73b99"></span>
# Function overview

Webex integration can be completed by creating a custom application in the Webex application.

**Common application scenarios**


* Dashboard subscription

* Chart monitoring and alerting

* Dataset synchronization result notification


<span id="_2-前置配置说明"></span>
# Pre\-configuration instructions

Step 1: Register a bot from the [Webex Developer Platform](https://developer.webex.com/docs/bots), then provide the access token, configure it in System Management/Enterprise Domain Management \- Office Platform Integration, and record the bot username yourself.

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/1ace9d0071c8460ba17a700ae5e1e092) </span>

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/0271ca9c9d184bc2bcbbcbc6f068dd9d) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ca0f6d94cef84afd9758b7213f738b1e~tplv-goo7wpa0wc-image.image) </span>

Step 2: To send messages to individuals and groups, ensure the bot is in the same team (used for searching people and groups); you can add the bot to the team using the bot's username.

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/673da6892f214d78812f4a25b03e3328) </span>

Step 3: Sending messages to a group is equivalent to sending to a space, and the bot needs to be added to the space. There are general spaces (general) and smaller spaces.

Caution:

The bot used to send messages must correspond to the provided token. If you create a bot arbitrarily and add it to a group, it will not have the ability to send messages.

Step 4: On the user management page, bind the user's Webex account to the Intelligent Data Insight account.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/da6d3e55dc034519a4243533a0a5db75~tplv-goo7wpa0wc-image.image) </span>

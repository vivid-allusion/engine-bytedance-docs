---
title: "Using an iframe to embed the viewing page"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-embedding-a-viewing-page-with-iframe"
---

This topic describes how to embed the viewing page of a BytePlus Live live room into your own page by using an iframe. You can embed the viewing page anywhere on your page, effectively reducing development costs. At the same time, viewers can watch the live stream directly on your page, which not only attracts new users but also retains existing ones.

<span id="542f23c9"></span>
## Notes


* Do not perform any operations for reading from or writing to cookies, as some browsers disable third\-party cookies. This means the following features are not supported: publishing questionnaires whose send time is when viewers join the live room, and requiring viewers to log in to the live room before joining (namely setting the viewing restriction to password, phone number, and others). To use these features, you can customize the domain name of the embedded page, namely the viewing page, by adding a CNAME record, which allows your page and the embedded page to share the same domain name. The embedded page's cookies will then be written as first\-party cookies, avoiding third\-party cookie restrictions. To add a CNAME record, contact the technical support of BytePlus Live.

* We recommend that you set the viewing restriction to **Custom** and select the solution where viewers can join the live room directly without a second login after they log in to your account system. For more information, see [Solution B](https://docs.byteplus.com/docs/byteplus-livesaas/docs-applying-advanced-viewing-restrictions#29214805).

* Do not embed an HTTP page under an HTTPS domain name, as the page may not display correctly.

* When embedding the menu for chat interaction, the minimum width limit for PCs is 320 px.


<span id="b1c0e113"></span>
## Embedding method


1. Concatenate the embedded link in the `iframe` tag.

   * For full\-page embedding, such as embedding the entire viewing page on PCs, here is an example.

      ```Plain
      <iframe src="https://live.byteplus.com/1323/6****21?platform=pc"></iframe>
      ```
      

   * For embedding specific modules, such as the player, here is an example.

      ```Plain
      <iframe src="https://live.byteplus.com/1323/6****21?mode=player"></iframe>
      ```
      

   Replace `https://live.byteplus.com/1323/6****21` with the viewing page address of your live room. For supported parameters in the embedded link, see [Parameters](https://docs.byteplus.com/docs/byteplus-livesaas/iframe-parameters). For listening to events on the embedded page, see [Events](https://docs.byteplus.com/docs/byteplus-livesaas/iframe-events).

2. Set the attributes of the `iframe` element. Here is an example.

   ```Plain
   <iframe src="https://live.byteplus.com/1323/6****21?platform=pc" width="1000" height="600" allowfullscreen="true" autoplay="true" allow=“fullscreen; screen-wake-lock; autoplay; picture-in-picture; camera; microphone” frameborder="0" border="0"></iframe>
   ```
   

   * `width`: The width of the `iframe` element. When the value is a number, the unit is px. When the value is a percentage, it represents the percentage relative to the width of the parent container.

   * `height`: The height of the `iframe` element. When the value is a number, the unit is px. When the value is a percentage, it represents the percentage relative to the height of the parent container.

   * `allowfullscreen="true"`: Allows the embedded page to enter full screen mode. We recommend that you add this parameter when the embedded page contains a player to allow the player to enter full screen mode.

   * `autoplay="true"`: Automatically plays the video.

   * `allow`: The features supported by the embedded page. Separate multiple parameter values using semicolons (;). Valid values:

      * `fullscreen`: Enters full screen mode. Applicable to scenarios where the embedded page contains a player.

      * `screen-wake-lock`: Keeps the screen illuminated.

      * `autoplay`: Automatically plays the video.

      * `picture-in-picture`: Picture\-in\-picture (PiP) mode. Only applicable to PCs.

   * `frameborder`: Whether the `iframe` element has borders. Valid values:

      * `0`: Without borders.

      * `1`: With borders.

   * `border`: The border width of the `iframe` element. The unit is px.

3. Insert the `iframe` tag into your own page.

---
title: "Blocking URLs"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-blocking-urls"
---

You can enable the URL blocking feature to make the live room secure and free from malicious links or unwanted ads, enhancing the experience for both the host and viewers.

<span id="0c773710"></span>
## Prerequisite

A BytePlus account or an IAM user with Producer \> Edit permission. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/en/byteplus-livesaas/docs/managing-iam-users-and-roles).

<span id="1fa2b052"></span>
## Procedure


1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).

2. On the live stream list, click to open a live room.

3. On the left navigation pane, click **Producer** \> **URL filtering**.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/36cca073de054257a2e07d483176b1c4~tplv-goo7wpa0wc-image.image" width="1406px" />   </div>
   

4. On the **URL filtering** page, turn on the **URL blocking** switch. Then,

   * Comments containing URLs are only visible to viewers who send them.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">This feature applies to both the menu for chat interaction and that for Q&A.      </div>
      

   * Viewers and guests cannot enter nicknames containing URLs.

      By default, with the switch turned on, comments and nicknames containing `https://`, `http://`, `ftp://`, and `www.string.` are blocked. Here, `string` can contain letters, numbers, dots (.), and hyphens (\-).

5. (Optional) To allow comments and nicknames to contain specific URLs, you can add URLs to the allowlist. Then, URLs containing values in the allowlist are not blocked.

   To add URLs to the allowlist:

   1. Click **Add URLs to allowlist**.

      <div style="text-align: center">
      <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2adad3dfd4aa45c2adb2e965ede5dc01~tplv-goo7wpa0wc-image.image" width="1092px" />      </div>
      

   2. In the **Add URLs to allowlist** dialog box, add one or more URLs in the following ways and then click **OK**.

      * Directly enter URLs in the dialog box. When adding multiple URLs, separate them with commas (,) or by pressing the Enter key.

      * Click **Download template**, \*\*\*\* add URLs as instructed in the template, and click **Batch import from Excel** to upload the updated template.

         You can also click **Delete** in the **Actions** column to delete a URL from the allowlist.

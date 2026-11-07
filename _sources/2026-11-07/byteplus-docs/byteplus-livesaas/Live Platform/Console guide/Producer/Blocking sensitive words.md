---
title: "Blocking sensitive words"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-adding-sensitive-words"
---

You can add sensitive words to a live room to keep it free from such words.


* Comments containing sensitive words are only visible to viewers who send them.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">This feature applies to both the menu for chat interaction and that for Q&A.   </div>
   

* Viewers and guests cannot enter nicknames containing sensitive words.


<span id="7c495438"></span>
## Prerequisite

A BytePlus account or an IAM user with Producer \> Edit permission. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).

<span id="a26dda79"></span>
## Procedure


1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).

2. On the live room list, click to open a live room.

3. On the left navigation pane, click **Producer** \> **Sensitive words**.

4. Click **Add sensitive words**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e253c119d3934bedb74ace24797d8d3a~tplv-goo7wpa0wc-image.image) </span>

5. In the **Add sensitive words** dialog box, add one or more sensitive words in the following ways and then click **OK**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a24ca84215004639868d064e8c6dda1e~tplv-goo7wpa0wc-image.image) </span>

   * Directly enter sensitive words in the dialog box. When adding multiple sensitive words, separate them with commas (,) or by pressing the Enter key.

   * Click **Download template**, \*\*\*\* add sensitive words as instructed in the template, and click **Import** to upload the updated template.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">As the comma (,) is used to separate two sensitive words, a sensitive word cannot contain a comma.   </div>
   

6. (Optional) Turn on the **Fuzzy matching** switch, and then:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/33cb134161aa4d6ab41073d87268f590~tplv-goo7wpa0wc-image.image) </span>

   * Sensitive words are case\-insensitive. For example, if the sensitive word is **abc**, then comments and nicknames containing **Abc** are also blocked.

   * Spaces and the following special characters in comments and nicknames are ignored when matching sensitive words:

      `* # @ . , ? ! : ; “ ” ‘’ () — - … / ' _ + | & % $ ^ ~ < > = ～ [ ] \ ·` ¥ { } ！｜「 」（ ）〈 〉：【 】、；，。"《 》 ？`

      For example, if the sensitive word is **abc**, comments and nicknames containing \**a b@c* are also blocked.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If you want to add more special characters to the matching rule, contact your sales representative.      </div>
      

   * Sensitive words to be added cannot contain spaces and the special characters listed above. For example, if you enter \**a b@c* when adding a sensitive word, then the added sensitive word will be **abc**.

7. (Optional) Turn on the **Phone number blocking** switch and then:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/002d596b9a5e471796a2a22d25c7cc00~tplv-goo7wpa0wc-image.image) </span>

   * Comments containing phone numbers are only visible to viewers who send them.

   * Viewers and guests cannot enter nicknames containing phone numbers.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Currently, this feature is available to phone numbers in Singapore, Japan, Korea, Indonesia, Thailand, and China.   </div>
   

8. (Optional) Search for specific sensitive words by entering a value in the search box. Fuzzy search is supported.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ffd46ee2b71e48a7b4ece59224adafe2~tplv-goo7wpa0wc-image.image) </span>

9. (Optional) Click **Delete** in the **Actions** column to delete a sensitive word.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b5d00a0cd5df4ed1a018875a6ee86e5e~tplv-goo7wpa0wc-image.image) </span>

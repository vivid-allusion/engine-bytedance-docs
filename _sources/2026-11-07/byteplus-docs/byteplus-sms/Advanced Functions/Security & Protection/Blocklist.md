---
title: "Blocklist"
product: "BytePlus Messaging"
product_code: "byteplus-sms"
source: "https://docs.byteplus.com/en/docs/byteplus-sms/Blocklist"
---

The Blocklist module in BytePlus Messaging enables you to manage mobile numbers that should be restricted from receiving SMS messages. This helps control messaging reach, especially for refining marketing SMS targeting and avoiding unwanted communications. You can add mobile numbers to the blocklist, define applicable message groups, and manage restrictions based on your business needs.

<span id="9bfab613"></span>
## Prerequisite

BytePlus Messaging has been activated.

<span id="dbfeb28e"></span>
## Context

The blocklist gives you precise control over SMS delivery at the message group level. Each message group can have its own custom blocklist. After adding numbers to the blocklist, messages from the associated message group won’t be sent to those numbers. This helps you follow user preferences, meet compliance needs, and make your marketing campaigns more targeted by excluding specific contacts.

<span id="79cdce74"></span>
## Procedure


1. Go to [BytePlus Messaging Console](https://console.byteplus.com/sms).

2. In the left navigation pane, click **Security settings** \> **Blocklist**.

3. Use the dropdown menu at the top of the Blocklist page to choose the message group for which you want to configure the blocklist.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6ef62478bce04486808680e5e801fe25~tplv-goo7wpa0wc-image.image) </span>


4. Click the **Add Number** button. A pop\-up window will appear.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5d8192757ff746b585a81d8bc08224fc~tplv-goo7wpa0wc-image.image) </span>


5. In the **Mobile Number** field, enter the mobile numbers you want to block. You can add up to 10 numbers at a time, separated by commas.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bea5df28d77443c7a7bbe3420a58da3f~tplv-goo7wpa0wc-image.image) </span>


6. (Optional) In the **Description** field, add details about why these numbers are being blocked.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Blocklist is only available for marketing SMS.</div>



7. Click **Submit** to add the numbers to the blocklist. The numbers will now be restricted from receiving messages from the selected message group.

8. To remove numbers from the blocklist, select the relevant entries and click **Delete**.


<span id="de7e61b4"></span>
## Result

The added mobile numbers are now blocked from receiving marketing SMS messages from the configured message group. You can verify the blocklist entries on the Blocklist page, which will display details like the mobile numbers, associated message group, SMS type, and date of addition.

---
title: "Managing prizes in the prize library"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-managing-prizes-in-prize-library"
---

To streamline the setup of lucky draw events, you can create a central repository of reusable prizes in the prize library. This guide provides step\-by\-step instructions on how to add various types of prizes, such as physical, virtual, and vouchers, and then manage, edit, or delete them as needed.

<span id="8b9b1a32"></span>
## Prerequisite

A BytePlus account or an IAM user with **Prize library** \> **Edit** permission. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).

<span id="6e45be1c"></span>
## Note

An IAM user can only access the prizes they are permitted to access or edit.

<span id="2d2f17cc"></span>
## Procedure


1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).

2. In the top navigation bar, click **Media library**.

3. In the left navigation pane, select **Prize library**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c1cec96c5d6b496a983ee27f9c2a4204~tplv-goo7wpa0wc-image.image) </span>

4. On the **Prize library page**, \*\*\*\* click **Create prize**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f908158e22a9455d91d3f75676cd81f1~tplv-goo7wpa0wc-image.image) </span>

5. In the pop\-up **Create prize** dialog box, select a prize type and complete the following settings.

   
   |**Prize type** |**Description** |
   |---|---|
   |Physical |A physical prize is a tangible prize, such as mobile phones and collectible figurines. After the lucky draw, use the winner's information to contact them or to mail the prize. |
   |Virtual |Virtual prizes are non\-physical prizes, for example, in\-game virtual currency and equipment. After the lucky draw, contact the winner based on the winner's information. |
   |Custom Prizes |Prizes that an enterprise can distribute independently in the form of points. After the lucky draw, BytePlus Live will trigger a callback for the winning result. You can perform secondary development to distribute points to winning viewers based on the winning callback message, and send winning SMS or internal messages. |
   |Voucher |These are prizes, such as discount coupons and shopping vouchers, that viewers can claim themselves. After the lucky draw, winning viewers can directly claim their prizes through the prize collection link configured by the enterprise. |
   

   This document uses a physical prize as an example.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/80020e0b5992487a8289fc21a349ba45~tplv-goo7wpa0wc-image.image) </span>

   
   |**Configuration items** |**Description** |
   |---|---|
   |Prize name |Enter the name of the prize. Up to 20 characters can be entered. |
   |Prize images |Click **Upload** to upload an image of the prize to be displayed on the winning page. If images are not uploaded, the prize images will not be displayed on the winning page. Images in JPG, PNG, and JPEG formats are supported for upload. Maximum file size: 2 MB. Suggested image size: 160 × 160 px. |
   |Prize inventory |The number of prizes in inventory. The value range is [1,100000]. If the number is not specified, the inventory is considered unlimited.<br><br>If prizes remain after a lucky draw is completed, deleted, or closed, the remaining quantity is returned to the prize pool. |
   |Enter winner information |The personal information that winners must provide to claim their prize. This field becomes required when you select the corresponding checkbox. |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Changes made in the prize library are not automatically applied to existing lucky draws that use those prizes. To apply the changes, you must remove and re\-add the prize in each lucky draw.   </div>
   

6. (Optional) Edit, delete, search, and view prizes:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2b180c43070a4e2cbe86fe87c89621d0~tplv-goo7wpa0wc-image.image) </span>

   * Click **Edit** to modify prize information.

   * Click **Delete** to delete the specified prize.

   * Search for the specified prize by prize name. Fuzzy search is supported.

   * View prize details, such as type and inventory, in the list.

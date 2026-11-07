---
title: "Displaying the popularity of a live room"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/displaying-the-popularity-of-a-live-room"
---

You can display the popularity of a live room on the viewing page.

<span id="cd0585fc"></span>
## What your viewers see


<Tabs>
<Tab zoneid="eCze4mOluy" title="Viewers on PCs">
<TabTitle>Viewers on PCs</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1d170083fdff427d8576f918d7456cf9~tplv-goo7wpa0wc-image.image) </span>


</Tab>
<Tab zoneid="c7HOSuNLYy" title="Viewers on mobile devices">
<TabTitle>Viewers on mobile devices</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/182003a36ed6481b9d1eca92e8d506ac~tplv-goo7wpa0wc-image.image) </span>


</Tab>
</Tabs>


<span id="ba6fa37b"></span>
## Prerequisite

A BytePlus account or an IAM user with Live control \> Edit permission. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).

<span id="0c62728d"></span>
## Procedure


1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).

2. In the live room list, click to open a live room.

3. Click **Interaction popularity** \> **Popularity** under the player and then turn on the **Popularity display** switch.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5ffae7442c0f4ee5b8dc368fe50bb564~tplv-goo7wpa0wc-image.image) </span>

4. (Optional) Configure the initial popularity. Value range: [0,10000000].

   The initial popularity is the initial value displayed on the viewing page. To display a value higher than the actual popularity, you can use this feature. For example, if the initial popularity is set to 10, and then 5 viewers visit the viewing page, the popularity on the viewing page will be 15 (10+5).

5. (Optional) Configure the growth coefficient. Value range: [1,100].

   The growth coefficient determines the increment in the popularity value for every increase in real viewers of the live room. For example, if the growth coefficient is set to 10 and the number of real viewers increases by 2, the popularity on the viewing page will increase by 20 (2×10). If the growth coefficient is set to a range, the popularity on the viewing page will randomly increase by an integer value within that range for each additional real viewer.

6. (Optional) Configure the reduction coefficient. Value range: [1,100].

   The reduction coefficient determines the decrement in the popularity value for every decrease in real viewers of the live room. For example, if the reduction coefficient is set to 10 and the number of real viewers decreases by 2, the popularity on the viewing page will decrease by 20 (2×10). If the reduction coefficient is set to a range, the popularity on the viewing page will randomly decrease by an integer value within that range for each real viewer decrease.

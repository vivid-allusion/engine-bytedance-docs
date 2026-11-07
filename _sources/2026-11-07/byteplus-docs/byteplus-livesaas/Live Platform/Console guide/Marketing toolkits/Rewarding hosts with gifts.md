---
title: "Rewarding hosts with gifts"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-rewarding-hosts-with-gifts"
---

Viewers can use free gifts or redeem points for gifts to reward hosts when a live room is in any of the following statuses: **Live**, **Playback**, and **Over**.

<span id="9eb0668b"></span>
## Visual demonstrations

Viewers can send gifts and view gift effects and notifications on the viewing page, while you can view the gift effects and notifications on the **Live control** page of your live room.


<Tabs>
<Tab zoneid="dhXedLHkjO" title="Viewers on PCs">
<TabTitle>Viewers on PCs</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0719e07793634394a6240cd0df169b9c~tplv-goo7wpa0wc-image.image) </span>


</Tab>
<Tab zoneid="dWZC7xm7AQ" title="Viewers on mobile devices">
<TabTitle>Viewers on mobile devices</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0564ef20c9ac49829a1141a900e90594~tplv-goo7wpa0wc-image.image) </span>


</Tab>
<Tab zoneid="V9kRPV5B6n" title="BytePlus Live console">
<TabTitle>BytePlus Live console</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c8279ea79af145f999cf189c59db2f78~tplv-goo7wpa0wc-image.image) </span>


</Tab>
</Tabs>


<span id="aa8c440b"></span>
## Prerequisites


* A BytePlus account or an IAM user with Marketing toolkits \> Edit permission. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).

* The menu for chat interaction. For more information, see [Managing the chat area](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-the-chat-area).

* To allow viewers to redeem points for gifts, you need to integrate your points system with BytePlus Live by developing OpenAPIs for querying and updating points. For more information, see [Integrating your points system with BytePlus Live](https://docs.byteplus.com/docs/byteplus-livesaas/docs-rewarding-hosts-with-gifts#fdaa49e4).


<span id="afe3284d"></span>
## Context

Rewarding hosts can improve the marketing ability, interactivity, and live\-streaming effect. We recommend that you use the gift rewards feature in live streams, such as e\-commerce live streams, marketing live streams, and educational training sessions.

<span id="696e99e5"></span>
## Configuring the gift rewards feature


1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).

2. On the live room list, click to open a live room.

3. (Optional) To allow viewers to redeem points for gifts, click **Producer** \> **Viewing restrictions** on the left navigation pane and select **Custom** as the authentication type or comment restriction. For more information, see [Custom authentication login](https://docs.byteplus.com/docs/byteplus-livesaas/docs-applying-advanced-viewing-restrictions).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For Web Viewer SDK, Viewer SDK for iOS, Viewer SDK for Android, and Viewer SDK for Flutter, make sure the authentication mode is custom mode.   </div>
   

4. On the left navigation pane, click **Marketing toolkits** \> **Gift rewards**.

5. Turn on the **Gift rewards** switch.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e17d68aa306141fb92647ac3b3ce8634~tplv-goo7wpa0wc-image.image) </span>

6. Select the gift reward mode:

   * To allow viewers to use free gifts, select **Free** as the mode.

   * To allow viewers to redeem points for gifts, select **Points** as the mode.

7. （Optional）For **Points** mode, enter the URLs of the OpenAPIs used to query and update points in your own points system, such as `https://test.com/get` and `https://test.com/post`, messages to be displayed when the OpenAPI call fails and when the viewer does not have enough points, and the unit, such as gems and pearls.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/63cb62d498f244ccba503c70451f3eac~tplv-goo7wpa0wc-image.image) </span>

8. (Optional) By default, the system provides several kinds of gifts. You can edit the name, picture, and unit price of a gift, set whether to provide a gift in the live room and whether to make the gift effect more visible, and adjust the sequence that a gift is displayed on the viewing page by clicking and dragging the icon on the left of a gift.

9. (Optional) Create a custom gift.

   1. Click **Create gift**.

   2. In the **Create gift** dialog box, complete the following configurations and then click **OK**.

      
      |**Field** |**Description** |
      |---|---|
      |Gift name |Enter the gift name. Maximum character limit for each language is 50. |
      |Gift picture |Upload a picture no larger than 2 MB in JPG, PNG, or GIF format. |
      |Unit price |Configure the unit price of the gift if you select **Points** as the mode. |
      |Effect |Select the **Highlighted** checkbox to make the gift effect more visible. |
      

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/90b4c0e6bfeb4603b6fce86c36937cf2~tplv-goo7wpa0wc-image.image) </span>

10. (Optional) Turn on the **Gift leaderboard** switch to display the gift leaderboard in the live room. Enter the leaderboard name and the maximum number of viewers on the leaderboard.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">This feature is only available when viewers redeem points for gifts to reward hosts during a live stream.   </div>
   

11. Click **Save**.

12. (Optional) Enable gift notifications. Then, notifications indicating that someone has sent gifts can be seen both on the viewing page and the console.

   1. On the **Live control** page, click the **Manage notifications** icon under the menu for chat interaction.

   2. In the **Manage system notifications** dialog box that appears, turn on the **Gift** switch and click **OK**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4f6e04ce3df84450b5f7468d4269c3d5~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you log in to the console using an IAM user, make sure that the IAM user has the Live Control \> Edit permission.   </div>
   

13. (Optional) You can also view the gift data on the **Insights** \> **Gift details** page. For more information, see [Viewing data of a live room](https://docs.byteplus.com/docs/byteplus-livesaas/docs-data-statistics).


<span id="d35034f0"></span>
## Disabling gift effects and notifications

You can disable highlighted effects of gifts sent by others and notifications indicating that someone has sent gifts.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">To disable gift effects and notifications only on the console, a BytePlus account or an IAM user with the Live control \> View only or Edit permission is required. To disable gift notifications both on the console and viewing page, a BytePlus account or an IAM user with the Live control \> Edit permission is required. For more information on how to add IAM users, see <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles">Managing users, organizations, and roles</a>.</div>


* <div data-tips="true" data-tips-type="tip">After gift effects are disabled, viewers can still view the highlighted effects of gifts sent by themselves on the viewing page.</div>


* <div data-tips="true" data-tips-type="tip">After gift notifications are disabled on the viewing page, viewers cannot view gift notifications when other viewers or they themselves send gifts.</div>




|Feature |On mobile devices |On PCs |On BytePlus Live console |
|---|---|---|---|
|Disable gift effects |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/edffea79e4604e21aee5524f2fe2879f~tplv-goo7wpa0wc-image.image) </span><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This icon only appears when the live room is in the <strong>Live</strong> or <strong>Over</strong> status.</div><br> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/26978fe5c1b94614b7c916a9e58a4c04~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fafdc4fed9c24bf698cefc7bc08214a9~tplv-goo7wpa0wc-image.image) </span> |
|Disable gift notifications |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a6259ecbc5f44b8bed2fddcaa6a4631~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9054b023cd954476b7001221afeb2f76~tplv-goo7wpa0wc-image.image) </span> |* To disable gift notifications only on the console, viewers can view gift notifications on the viewing page when other viewers and they themselves send gifts.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a5a7799f7a674ab99f2bb607745f34ad~tplv-goo7wpa0wc-image.image) </span><br><br>* To disable gift notifications of other viewers both on the console and viewing page, viewers can still view gift notifications on the viewing page when they themselves send gifts.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2233f25ab2864a438a0074e41629c852~tplv-goo7wpa0wc-image.image) </span> |


<span id="fdaa49e4"></span>
## Integrating your points system with BytePlus Live

Before allowing viewers to redeem points for gifts to reward hosts, you must develop the following two OpenAPIs according to the specifications to integrate your points system with BytePlus Live.

If you have any questions about integration, contact your sales representative. If you do not have a sales representative, click [here](https://www.byteplus.com/en/contact) to fill in the form so that the BytePlus sales team can contact you later.

<span id="d1141f95"></span>
### Querying points

Description: BytePlus Live can call this OpenAPI to get the remaining points of a user from your own account system and display the points on the viewing page.

Method: GET

<span id="469a28b0"></span>
#### Request parameters

<span id="3884ac2c"></span>
##### **Query**


|Paramter Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|UserId |String |Yes |`8erwwdfthf6e****` |The user ID in your own account system. |
|UserName |String |Yes |`UserA` |The user name in your own account system. |
|Ts |Integer |Yes |`1650778541` |The system time when the OpenAPI is called in Unix timestamp format. Unit: seconds. |
|ActivityId |Integer |Yes |`172982551195****` |The activity ID of the live room. |
|Sign |String |Yes |`2625701639ccf0081d3862ab6815****` |The signature for verification.<br><br>To obtain the value of `Sign`, you must complete the following steps:<br><br><br>1. Order all the parameters and their values based on the parameter name in lexicographic order.<br><br>2. Concatenate the string in the format of `ParameterNameParameterValueParameterNameParameterValue`.<br><br>3. Add the value of `accountSecret` at the beginning and the end of the string. To obtain the value of `accountSecret`, contact your sales representative.<br><br>4. Encrypt the concatenated string in MD5 (32\-bit lowercase).<br><br><br>In this example, assume that the `accountSecret` value is `abc`. The concatenated string would then be `abcActivityId172982551195****Ts1650778541UserId8erwwdfthf6e****UserNameUserAabc`, with the `Sign` value as `2625701639ccf0081d3862ab6815****`. |


<span id="ab938545"></span>
#### Response parameters

<span id="f6b17ba6"></span>
##### **Body**


|Paramter Name |Data Type |Sample Value |Description |
|---|---|---|---|
|Code |Integer |`200` |The HTTP status code. |
|Status |Integer |`0` |The service status.<br><br><br>* `0`: Success.<br><br>* `1`: The user does not have enough points.<br><br>* `2`: Other errors. |
|Message |String |`-` |Returns a detailed error message if the value of `Status` is `2`. |
|Data |Integer |`123` |The remaining points of the user. |


<span id="986233ef"></span>
#### Samples

<span id="be7bd4e6"></span>
##### **Sample request**

```Plain
GET https://test.com/get?UserId=8erwwdfthf6e****&UserName=UserA&Ts=1650778541&ActivityId=172982551195****&Sign=2625701639ccf0081d3862ab6815****
```


<span id="ac01c937"></span>
##### **Sample response**

```JSON
{
        "Code": 200, 
        "Status": 0, 
        "Message": "", 
        "Data": 123 
    }
```


<span id="d8b30b1e"></span>
### Updating points

Description: BytePlus Live can call this OpenAPI to synchronize the points that a user has consumed for gift rewards from BytePlus Live to your own account system.

Method: POST

<span id="3f752430"></span>
#### Request parameters

<span id="a5dc2ed7"></span>
##### **Body**


|Paramter Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|UserId |String |Yes |`8erwwdfthf6e****` |The user ID in your own account system. |
|UserName |String |Yes |`UserA` |The user name in your own account system. |
|Ts |Integer |Yes |`1650778541` |The system time when the OpenAPI is called in Unix timestamp format. Unit: seconds. |
|GiftName |String |Yes |`Like` |The name of the gift for which the user redeems points. |
|GiftPrice |Integer |Yes |`1` |The price of the gift for which the user redeems points. |
|GiftCount |Integer |Yes |`100` |The number of gifts for which the user redeems points. |
|Amount |Integer |Yes |`100` |The total points that user redeems for gifts. |
|ActivityId |Integer |Yes |`172982551195****` |The activity ID of the live room. |
|Sign |String |Yes |`89827f98fadbd7f3183cb4008f80****` |The signature for verification.<br><br>To obtain the value of `Sign`, you must complete the following steps:<br><br><br>1. Order all the parameters and their values based on the parameter name in lexicographic order.<br><br>2. Concatenate the string in the format of `ParameterNameParameterValueParameterNameParameterValue`.<br><br>3. Add the value of `accountSecret` at the beginning and the end of the string. To obtain the value of `accountSecret`, contact your sales representative.<br><br>4. Encrypt the concatenated string in MD5 (32\-bit lowercase).<br><br><br>In this example, assume that the `accountSecret` value is `abc`. The concatenated string would then be `abcActivityId172982551195****Amount100GiftCount100GiftNameLikeGiftPrice1Ts1650778541UserId8erwwdfthf6e****UserNameUserAabc`, with the `Sign` value as `89827f98fadbd7f3183cb4008f80****`. |


<span id="c7e04da1"></span>
#### Response parameters

<span id="e6c485e7"></span>
##### **Body**


|Parameter Name |Data Type |Sample Value |Description |
|---|---|---|---|
|Code |Integer |`200` |The HTTP status code. |
|Status |Integer |`0` |The service status.<br><br><br>* `0`: Success.<br><br>* `1`: The user does not have enough points.<br><br>* `2`: Other errors. |
|Message |String |`-` |Returns a detailed error message if the value of `Status` is `2`. |
|Data |Integer |`123` |The remaining points of the user. |


<span id="5868ac81"></span>
#### **Samples**

<span id="0e247d47"></span>
##### **Sample request**

```JSON
POST https://test.com/post
            header Content-Type: application/json; charset=utf-8
            body {
                 "UserId": "8erwwdfthf6e****",
                 "UserName": "UserA",
                 "Ts": 1650778541,
                 "GiftName": "Like",
                 "GiftPrice": 1,
                 "GiftCount": 100,
                 "Amount": 100,
                 "ActivityId": "172982551195****",
                 "Sign": "89827f98fadbd7f3183cb4008f80****"
                 }
```


<span id="23b042de"></span>
##### **Sample response**

```JSON
{
       "Code": 200, 
       "Status": 0, 
       "Message": "", 
       "Data": 123 
   }
```

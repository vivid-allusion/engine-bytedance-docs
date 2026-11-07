---
title: "Telegram"
product: "Byteplus GMP"
product_code: "datagmp"
source: "https://docs.byteplus.com/en/docs/datagmp/telegram"
---

The Telegram Channel Reach feature allows users to automate private chat management and customer interaction through Telegram Bot. This function supports the sending of text messages, multiple options, files, and media, as well as the access and management of Bot Tokens, and the configuration of timed tasks and triggering tasks. Mainly suitable for overseas customer reach, automated customer interaction and marketing activities scenarios, it can improve reach efficiency, expand reach channels, and form reusable standardization capabilities. This article explains how to complete the access configuration and subsequent management of the Telegram channel.

<span id="e5f4a3d3"></span>
# prerequisite

Open the permission to create a new Telegram channel, please refer to the specific operation [权限设置](https://docs.byteplus.com/docs/datagmp/73332).

<span id="260862be"></span>
# Function Description

<span id="ef4e3ee3"></span>
## Add Bot Access

Get the token through BotFather and bind it to GMP, which supports associating existing robots or creating new robots.


1. Log in to the Growth Marketing Platform console, click **Marketing Configuration \> Channel Configuration** , click Telegram, and click **Add Bot Access** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e33f7eff8156401f8e74c50da0d1bd48~tplv-goo7wpa0wc-image.image) </span>

2. Fill in the parameters such as Telegram Token and channel name, then click **OK** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/edabc73d3a7244fea482dab3988c7b15~tplv-goo7wpa0wc-image.image) </span>

   
   |parameter |parameter description |
   |---|---|
   |channel name |Custom channel name |
   |Telegram Bot Token |You can get Telegram Bot Token in the following ways:<br><br><br>* Create a new Telegram bot:<br><br>   1. Send a message to BotFather on Telegram.<br><br>   2. Send the command `/newbot`and follow the instructions.<br><br>   3. After the creation is successful, you will receive a message with the token. Copy the Token and paste it into the text box.<br><br>* Connect to an existing Telegram Bot:<br><br>   1. Send a message to BotFather on Telegram.<br><br>   2. Send a command `/mybots`and select the robot you want to connect to.<br><br>   3. Select Token and paste it into the text box. |
   |Telegram Bot URL |Telegram Bot URL |
   |Send destination ID |Select the destination entity ID to send. The target entity ID is pulled from VeCDP, and the target entity ID can be referred to [ID graph construction ](https://www.volcengine.com/docs/7139/1222700).<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/882a2cd97587428aa5cfff5b46648f3b~tplv-goo7wpa0wc-image.image) </span> |
   |QPS cap |Number of interface calls per second, range 10\-30. |
   


<span id="6d599bcb"></span>
## Update configuration

The channel needs to be closed before updating the configuration. Support channel name, Telegram Bot Token and other information.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5c0315f0ce8343108436fbe3cb8725c3~tplv-goo7wpa0wc-image.image) </span>

<span id="4eb056d4"></span>
## **frequency control settings**

The transmission frequency control of this channel can be set. The touch using this channel will pass the channel frequency control. If multiple items are checked, all conditions must be met.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/db3aff4d29cb438fb11a531975c424ba~tplv-goo7wpa0wc-image.image) </span>

Currently supports sky\-level, week\-level, and month\-level frequency control.

If a Do Not Disturb policy is set, access using that channel will be implemented.

Touch task, process canvas, process canvas in the policy can also be a separate Do Not Disturb settings, such as set at the same time, then multiple Do Not Disturb conditions must be met.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6cb889989ea743c2bf897709606d5291~tplv-goo7wpa0wc-image.image) </span>

<span id="4c34d4e7"></span>
## **Delete channel**

Only closed channels can be deleted. Delete the channel, and subsequent tasks will not be able to create the channel. Please delete with caution.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1450240810354ed9aec065e4ec2223c3~tplv-goo7wpa0wc-image.image) </span>

<span id="f2b4ee12"></span>
# related operations

[Telegram Message Push Reach Task](https://docs.byteplus.com/docs/undefined/6948b8a1c50abf0502e493e6)

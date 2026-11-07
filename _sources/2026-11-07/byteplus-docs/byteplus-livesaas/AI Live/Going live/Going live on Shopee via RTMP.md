---
title: "Going live on Shopee via RTMP"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/going-live-on-shopee-via-rtmp"
---

You can push your BytePlus AI Live stream to Shopee via RTMP so viewers can watch your AI figure on Shopee. This guide explains how to configure Shopee as the streaming destination in AI Live, obtain the server URL and stream key from Shopee, and use the Live Connector browser extension to forward viewer comments. With comment syncing configured, your AI figure can generate and speak replies based on your knowledge base and prompts.

<span id="fdde2b5d"></span>
## Prerequisites


* You have set up an AI live room and are ready to go live. For more information, see [Starting an AI Live](https://docs.byteplus.com/docs/byteplus-livesaas/digital-human-livestream).

* You have permission to go live on Shopee and can obtain an RTMP server URL and stream key from the Shopee live dashboard.

* To have your AI figure reply to viewer comments, you have prepared and configured a knowledge base for replies. For more information, see [Preparing and uploading knowledge base files](https://docs.byteplus.com/docs/byteplus-livesaas/configuring-product-kb).

* To collect comments, you have installed Google Chrome or Microsoft Edge and contacted BytePlus technical support to obtain the **Live Connector** extension package.


<span id="621db0ae"></span>
## Procedure

<span id="d2716de0"></span>
### Step 1: Configure the Shopee RTMP streaming settings in AI Live

In AI Live, configure the RTMP streaming settings for Shopee in the **Live platform** dialog.


1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/) and open the AI live room you want to stream from.

2. In the top navigation bar, click **Live platform**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e6b082de70e24ddc8aa86c4726e151de~tplv-goo7wpa0wc-image.image) </span>

3. In the **Live platform** dialog, configure the following settings, and then click **Save**.

   
   |Configuration |Description |
   |---|---|
   |Live platform setting |Choose **Other** to configure Shopee as the streaming destination. |
   |Platform Name |Enter a name, such as `Shopee`, to help identify the streaming destination. |
   |URL Server |Enter the RTMP server URL for your current Shopee live stream. Create the live stream in the Shopee live dashboard to obtain its server URL and stream key.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/de402a754958448c8ad6747bdf7e44de~tplv-goo7wpa0wc-image.image) </span> |
   |Stream Key |Enter the Shopee stream key associated with the server URL above. |
   |Stream pushing |Enable this option to push your AI Live stream to Shopee. |
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6143bd00a92c4ada8b19ea234a4487f6~tplv-goo7wpa0wc-image.image) </span>


<span id="ff658d8a"></span>
### Step 2: Start the live stream in AI Live and Shopee


1. Start your AI Live. For more information, see [Starting an AI Live](https://docs.byteplus.com/docs/byteplus-livesaas/digital-human-livestream).

2. Open the Shopee live dashboard for the current live stream. After confirming that it is receiving video and audio from BytePlus, click **Go Live** in the upper\-right corner.

3. Confirm that the Shopee page displays **Live** and the elapsed streaming time.


<span id="67f662d9"></span>
### (Optional) Step 3: Forward Shopee viewer comments to your AI live room

Use the **Live Connector** browser extension to collect viewer comments from the Shopee live dashboard and send them to your specified BytePlus AI live room. Your AI figure can then generate and speak replies based on your knowledge base and prompts.

The Live Connector interface shown below is in Chinese. This guide retains the Chinese labels and provides English explanations to help you locate each control.

<span id="a8715f56"></span>
#### Step 1: Install Live Connector


1. Contact BytePlus technical support to obtain the Live Connector extension package, and extract it to a local folder.

2. Open Chrome or Edge. In the address bar, enter `chrome://extensions/` for Chrome or `edge://extensions/` for Edge to open the extensions management page.

3. Turn on **Developer mode**.

4. Click **Load unpacked** and select the extracted Live Connector extension folder.

5. Confirm that **Live Connector** appears in the extensions list and is enabled.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/322b352162ef416c802a15d7e0b090d2~tplv-goo7wpa0wc-image.image) </span>

6. Click the **Extensions** icon to the right of the browser address bar, and then click **Live Connector**. The extension opens in the browser's side panel. You can also pin the extension to the toolbar for easier access.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b0afeaaa89b5452fa3157d1d94dbf7d3~tplv-goo7wpa0wc-image.image) </span>


<span id="c2cae86b"></span>
#### Step 2: Connect your BytePlus account


1. In the extension's **登录 BytePlus** (Log in to BytePlus) step, click **去 BytePlus 登录** (Go to BytePlus to log in).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/47536cdfd0364931baf73e69dd38a398~tplv-goo7wpa0wc-image.image) </span>

2. Log in on the BytePlus page that opens. Use the account that owns the AI live room for this stream, and complete the login in the same browser and browser profile where you installed Live Connector.

3. Return to the extension and click **我已登录，连接账号** (I have logged in; connect account).

4. In the **选择直播间** (Select a live room) step, confirm that the extension displays the account that owns your AI live room and the status **BytePlus 已连接** (BytePlus connected). To switch accounts, click **更换账号** (Change account), and then log in and connect again.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/610f294649944ad889cbcb5a6e75d7a9~tplv-goo7wpa0wc-image.image) </span>


<span id="feb97d9b"></span>
#### Step 3: Identify the Shopee live stream and enter your BytePlus AI live room ID


1. In the browser where you installed Live Connector, log in to Shopee and open the dashboard for the live stream you started in Step 2 of the procedure.

2. Confirm that the Shopee live stream is running. The extension automatically detects the stream and displays its information under **采集来源** (Comment source), with the status **直播中** (Live).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1f639db64f1f487b929480ce87ace7fd~tplv-goo7wpa0wc-image.image) </span>

3. In the BytePlus Live console, open the AI live room that is pushing the stream to Shopee and copy its ID (`ActivityId`). Paste it into the extension's **上报目标** (Destination live room) field. Use the ID of the currently streaming BytePlus AI live room, not the Shopee live room ID.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/351bafca8b4c4c7187423c1edaeb4d6d~tplv-goo7wpa0wc-image.image) </span>

4. Confirm that the source and destination are correct, and then click **下一步** (Next) to proceed to the **开始同步** (Start syncing) step.


<span id="b649a8fd"></span>
#### Step 4: Start syncing comments and verify AI replies


1. On the **确认连接，开始同步** (Confirm connection and start syncing) page, check the Shopee comment source and BytePlus destination live room again, and then click **开始同步评论** (Start syncing comments).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1aed26aa899d4b5a926a4ab9d6ef8194~tplv-goo7wpa0wc-image.image) </span>

2. Confirm that the extension displays **连接完成** (Connection complete), the status **同步中** (Syncing), and a **停止同步** (Stop syncing) button. Keep the browser and Shopee live dashboard open, and stay logged in. **Closing the Shopee live dashboard stops comment collection.** 

3. Use a viewer account to post a new test comment in the current Shopee live stream. Ask a question that your knowledge base can answer, and then check the following:

   * The comment appears in the **Comments** section of the Shopee live dashboard.

   * The same comment appears under **最近评论** (Recent comments) in the extension, and the **已同步评论** (Synced comments) count increases.

   * The comment appears in the **Chats** list in your BytePlus AI live room.

4. Listen to the live stream as a viewer on Shopee and confirm that the AI figure speaks a relevant reply. A comment appearing in the extension does not confirm that the AI figure has generated or spoken a reply. Also check that BytePlus receives the comment and that the reply is audible in the live stream.


<span id="8e3c6ce0"></span>
## FAQs

<span id="5890df38"></span>
### Why is there no video on Shopee after I start AI Live?

In the **Live platform** dialog, check that **Stream pushing** is enabled and that **URL Server** and **Stream Key** match the values provided for the current stream in the Shopee live dashboard. Also confirm that you have completed the steps to go live on Shopee.

<span id="3d791ccd"></span>
### What should I do if the comment source shows 待识别 (Not yet detected) or 正在等待聊天连接… (Waiting for the chat connection)?

Confirm that you are logged in to Shopee in the same Chrome or Edge browser profile where you installed Live Connector, and that the dashboard for the current live stream is open. Follow the instructions for the status shown on the Shopee page:


* **The stream has not started:**  Confirm that Shopee is receiving the stream, and then click **Go Live**. The extension detects the page status automatically. Wait for the status to change to **直播中** (Live); you do not need to refresh the page manually.

* **The stream is live:**  Confirm that the page displays **Live** and the elapsed streaming time. Keep the dashboard open and check that the page has loaded correctly.

* **The stream has ended:**  If the page displays **Live Ended**, the stream has ended. After starting another stream, confirm the comment source and destination live room again, and start syncing comments.


<span id="bdc7fb75"></span>
### Why is my AI figure not replying to Shopee comments?

First, check the **Chats** list in your BytePlus AI live room to see whether the comments have arrived:


* **No comments have arrived:**  Confirm that new comments appear under **Comments** in the Shopee live dashboard. Then check that the extension shows **同步中** (Syncing), that the comments appear under **最近评论** (Recent comments), and that the **已同步评论** (Synced comments) count increases. Also check the connected BytePlus account and destination live room. The `ActivityId` must identify the currently streaming AI live room under that account. Keep the Shopee live dashboard open.

* **Comments have arrived:**  Check whether filtering rules have blocked the comments, and whether a knowledge base and comment reply settings are configured for the live room. For more information, see [Starting an AI Live](https://docs.byteplus.com/docs/byteplus-livesaas/digital-human-livestream).


<span id="next-steps"></span>
## Related operations

To configure how your AI figure replies to Shopee viewer comments, see [Configure comment reply strategies](https://docs.byteplus.com/en/docs/byteplus-livesaas/digital-human-livestream#143bb4f1) in *Starting an AI Live* for instructions on setting up knowledge bases, prompts, and comment filtering rules.

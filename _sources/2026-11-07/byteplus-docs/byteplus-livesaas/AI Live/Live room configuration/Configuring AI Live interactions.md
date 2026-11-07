---
title: "Configuring AI Live interactions"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/configuring-ai-live-interactions"
---

AI Live can automatically respond to audience comments and interaction events during a livestream. After **Live interaction** is configured, the AI host pauses the current script at the appropriate time, generates a reply based on your knowledge bases, prompts, and filter rules, and then resumes reading the script.

This guide explains how to configure comment replies, engage reply, and AI reply testing.

> **注意**

> Live interaction settings cannot be changed during a livestream. We recommend that you fully test and complete the related settings before going live.

## Prerequisites

* Before you start, prepare the knowledge bases used for replies. For details, see [Configuring knowledge bases](https://docs.byteplus.com/docs/byteplus-livesaas/configuring-product-kb).

* To go live on TikTok, make sure you have added the TikTok user id of the TikTok account you want to go live on:

   1. In the top navigation bar, enter your **TikTok user ID** to retrieve audience activities from the livestream.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/40fe23bba5e54a25ba69f4c6fa060a55~tplv-goo7wpa0wc-image.image)

      You can get the ID in your TikTok App as shown below.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/10ac18d800e74e5dbc8c28146e8b1580~tplv-goo7wpa0wc-image.image)

* To go live on Shopee, make sure you have added the Live Connector browser extension to forward viewer comments to BytePlus AI Live from Shopee live room. For details, see [Going live on Shopee via RTMP](https://docs.byteplus.com/docs/byteplus-livesaas/going-live-on-shopee-via-rtmp).

## Steps

1. Log in to the [BytePlus Live console](https://console.byteplus.com/).

2. In the top navigation bar, select **AI Live**.

3. On the **Live Room** page, click to open an existing live room or create a live room.

4. In the top navigation bar, click **Live interaction**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a503096289f4da690c236f6c926b6cf~tplv-goo7wpa0wc-image.image)

   The **Live interaction** window slides out. You can configure comment reply strategies and engage reply here.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/02aa9041d7a54864b563c1cd587f42be~tplv-goo7wpa0wc-image.image)

### Configure comment reply strategies

1. Under **Comment reply** tab, add a general knowledge base you created before. The product knowledge base is enabled only when you add a product script to the livestream and upload the corresponding files on the **Knowledge base** page. For details, see [Configuring knowledge bases](https://docs.byteplus.com/docs/byteplus-livesaas/configuring-product-kb).

2. (Optional) In the **Prompt Settings** box, customize the instructions that guide the AI's response style.

3. Adjust the **Dense Weight** to control the search preference. This value (0.2 to 1.0) balances keyword matching with semantic understanding. A higher value prioritizes the meaning of a question over exact words. The default is 0.5.

4. Under **Chat Settings**, configure rules to ignore irrelevant comments.

   |**Filter Rule** |**Description** |
   |---|---|
   |Pure emoji message blocking |Ignores comments that only contain emojis. (This supports BytePlus Live emojis, standard emojis, and TikTok emojis). |
   |Repeated screen refresh filtering |Filters duplicate spam messages that repeatedly refresh the screen. |
   |Chat sensitive words |Blocks comments containing words from your custom sensitive word list. For details, see [Blocking sensitive words](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-adding-sensitive-words). |
   |Word length filter |Sets the minimum and maximum word count for a comment to be eligible for a reply. Default is 0 to 50 words, which means comments longer than 50 words will be ignored. |
   |Comment Reply Strategy |* **Avatar Reply**: The Avatar reads and responds to comments aloud. This is the only strategy currently available.<br><br>* **Comment Section Reply**: Automatically posts replies in the chat. This option is not yet supported. |

### Configure engage reply strategies

Beyond replying to comments, the Avatar can proactively respond to audience activities. Under the **Engage reply** tab, turn on the response types you need and set how often they trigger. During the livestream, the host pauses the current script, delivers the response aloud, and then resumes the script.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/94c1109d7cdd4c9fbb55cc7aa2eaaac0~tplv-goo7wpa0wc-image.image)

|**Response type** |**Description** |
|---|---|
|**Join greetings** |After the viewer enters the room, generate a welcome and ask the host to read it aloud. You can set the probability that a viewer joining the room triggers a welcome. The default value is 30%. |
|**Engage thanks** |After the viewer likes, shares, or follows, generate a thank you and let the host read it aloud. You can set the probability that an interaction triggers a thank\-you message. The default value is 100%. |

### Test AI reply

Before going live, simulate viewer activities to preview how the Avatar responds. This lets you verify your comment reply and interactive response settings and refine them if needed.

1. On the script configuration page, click **AI reply test** in the top\-right corner of the **Explanation text** area.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b18a0c4eecc641f283a2f7dca1363a4e~tplv-goo7wpa0wc-image.image)

2. In the **AI response test** dialog, you act as the viewer: send a message to the AI reply robot and see how it replies.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/08d3051167ec45c5b066859058a499a8~tplv-goo7wpa0wc-image.image)

3. (Optional) In the **Viewer nickname** box, edit the name used in the test.

   * Trigger an activity or send a comment to test the corresponding reply:

   * **Join** / **Like** / **Follow** / **Gifting**: Click a button to simulate the viewer joining, liking, following, or sending a gift. The AI reply robot generates and shows the matching interactive response.

   * **Comment**: Enter a message in the text box and click **Send**. The AI reply robot replies based on your comment reply settings and knowledge base.

4. Review the replies in the conversation area to confirm they match your expectations. Adjust your interaction settings, prompts, or knowledge base as needed, and then test again.

## FAQs

### Q: Some viewer nicknames contain emojis or unreadable symbols. What should I do?

Add an instruction to the **Prompt** in comment reply settings so AI converts unreadable nicknames into readable text before responding. For example:

```Plain
If the username is emoji or unreadable symbol, transform those into readable before answering the question.
```

### Q: Viewer comments have entered the live room, but the AI host does not reply. What should I do?

Check the following items:

* Whether the comment was blocked by pure emoji, repeated spam, sensitive word, or word length filter rules.

* Whether a general knowledge base has been added to the live room, or whether the current product has an uploaded product knowledge base.

* If the comment comes from a third\-party platform, check whether the comment sync tool is still syncing and whether the comment has entered the **Chats** list of the BytePlus AI live room.

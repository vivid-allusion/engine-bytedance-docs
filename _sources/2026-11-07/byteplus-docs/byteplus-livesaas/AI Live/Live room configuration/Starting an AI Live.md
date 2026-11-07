---
title: "Starting an AI Live"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/digital-human-livestream"
---

This guide provides step\-by\-step instructions for using the BytePlus Live console to set up and launch an automated AI Live. You will learn how to create livestream scripts, configure intelligent replies for audience interaction, manage livestream settings, and start your broadcast. For an overview of the feature and the end\-to\-end workflow, see [AI Live overview](https://docs.byteplus.com/docs/byteplus-livesaas/digital-human-overview).

## Prerequisites

* **Subscribe to the AI Live service**: Refer to [Subscription billing method](https://docs.byteplus.com/docs/byteplus-livesaas/subscription-billing-method) and contact sales to subscribe to the AI Live service.

* **Train your Avatar**: Train your own avatar and voice so you can use them in the livestream. For details, see [Training avatar and voice](https://docs.byteplus.com/docs/byteplus-livesaas/training_digital_human_and_voice).

* **Prepare products and knowledge bases**: To allow the host to present merchandise and answer product questions, add your products to the **Product Library** and upload the corresponding knowledge base files first. For details, see [Managing product library](https://docs.byteplus.com/docs/byteplus-livesaas/managing-products-for-digital-human-livestreams) and [Configuring knowledge bases](https://docs.byteplus.com/docs/byteplus-livesaas/configuring-product-kb).

## Procedure

Follow these steps to set up and launch your AI Live.

### Step 1: Create an AI live room

1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).

2. Click **AI Live** in the top navigation bar.

3. On the **Live Room** page, click  **+New liveroom**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ef3aeee5a60a49349568177223f3a92d~tplv-goo7wpa0wc-image.image)

   The live room will automatically be tagged as **Digital Human Streaming** for easy identification.

4. In the **Create live room** dialog, set the room name, voice, avatar, and speaking speed, and then click **Create** to open the script configuration page.

   |**Configuration** |**Description** |
   |---|---|
   |**Live room name** |Enter a name for the live room. The name can be up to 150 characters long. |
   |**Language** |The system automatically detects the language of the voice. |
   |**Avatar** |Select an avatar for the live room. If your dialog shows no avatars available, refer to [Training avatar and voice](https://docs.byteplus.com/docs/byteplus-livesaas/training_digital_human_and_voice). |
   |**Avatar Voice** |* Select a voice from the available options. If your dialog shows no voices available, refer to [Training avatar and voice](https://docs.byteplus.com/docs/byteplus-livesaas/training_digital_human_and_voice).<br><br>* Adjust how fast the Avatar speaks. Set this before going live; speaking speed cannot be changed during the livestream. The range is [0.5,2]. |

### Step 2: Add livestream scripts

The Avatar reads from scripts to host the livestream. You can add two types of scripts, and mix multiple of each in a single livestream. For details, see [Generating livestream scripts](https://docs.byteplus.com/docs/byteplus-livesaas/generating-ai-live-scripts).

You can see the estimated speaking duration and character count, and click **Listen to the script** to hear how the selected voice reads the script before going live.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2fd5a3aef27847b58d9e7b88cb237a31~tplv-goo7wpa0wc-image.image)

You can add multiple product scripts and click the Drag icon to reorder them.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9ff21d518f5040d7b15809c86712c9b4~tplv-goo7wpa0wc-image.image)

Once you add a product script here, its matching product knowledge base will also be automatically enabled for replies. You can click **Live interaction** to view the settings.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d3ca9fb746dd44fb83c7e40ee0c3bd17~tplv-goo7wpa0wc-image.image)

### Step 3: Configure interaction settings

AI Live can automatically respond to audience comments and interaction events during a livestream. After **Live interaction** is configured, the AI host pauses the current script at the appropriate time, generates a reply based on your knowledge bases, prompts, and filter rules, and then resumes reading the script. For details, see [Configuring AI Live interactions](https://docs.byteplus.com/docs/byteplus-livesaas/configuring-ai-live-interactions).

### Step 4: Configure the stream destination

Set where the AI stream is pushed so it can be broadcast on TikTok, BytePlus Live, or another platform.

1. In the top navigation bar, click **Live platform**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e6b082de70e24ddc8aa86c4726e151de~tplv-goo7wpa0wc-image.image)

2. In the **Live platform** dialog, configure the following settings, and then click **Save**.

   |**Configuration** |**Description** |
   |---|---|
   |Live platform setting |Choose where to push the stream: **TikTok**, **BytePlus Live**, or **Other**. |
   |Streaming method |This option only appears when you choose **TikTok** as the Live platform.<br><br><br>* **RTMP**: Pulling streams using the RTMP protocol. See [Going live on TikTok via RTMP](https://docs.byteplus.com/docs/byteplus-livesaas/Synchronizing_a_live_stream_from_AI_Live_to_third-party_platforms).<br><br>* **Virtual Camera**. Go live via OBS. See [Going live on TikTok via OBS virtual camera](https://docs.byteplus.com/docs/byteplus-livesaas/Going_live_on_TikTok_via_Digital_Human_and_OBS). |
   |TikTok ID |The **TikTok user ID** used to retrieve audience activities from the livestream. This option only appears when you choose **TikTok** as the Live platform. Get the ID in your TikTok app as shown below.<br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/10ac18d800e74e5dbc8c28146e8b1580~tplv-goo7wpa0wc-image.image) |
   |URL Server |Enter the push URL (RTMP server address) of the target platform. For details, see [Get the server URL and stream key](https://docs.byteplus.com/docs/byteplus-livesaas/Synchronizing_a_live_stream_from_AI_Live_to_third-party_platforms#how-to-synchronize-a-live-stream-to-major-live-streaming-platforms). |
   |Stream Key |Enter the stream key of the target platform. For details, see [Get the server URL and stream key](https://docs.byteplus.com/docs/byteplus-livesaas/Synchronizing_a_live_stream_from_AI_Live_to_third-party_platforms#how-to-synchronize-a-live-stream-to-major-live-streaming-platforms). |
   |Stream pushing |Enable this option to push the Avatar stream to the selected platform. |

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9269d0affec041ab96bc5e24801eb065~tplv-goo7wpa0wc-image.image)

### (Optional) Step 5: Add Live watermark

Add a watermark, such as an "AI\-Generated" tag, that appears in the bottom\-right corner of the livestream.

1. In the top\-right toolbar, click the **More** ( **...** ) icon, and then select **Live Settings**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/36909d863cff43708758decab9fe46ef~tplv-goo7wpa0wc-image.image)

2. In the **Live Settings** dialog, turn on **Live watermark**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e99ea7d2eef42e1873b375b1eeef501~tplv-goo7wpa0wc-image.image)

3. Click **Upload Image** to upload your watermark logo, and then click **Save**. The image must meet the following requirements:

   * **Format**: JPG or PNG

   * **Maximum size**: 500 KB

   * **Maximum dimensions**: 540px (W) × 300px (H)

### Step 6: Go live and manage the stream

Before you start a livestream, BytePlus Live runs a **Start Live setting** setup flow that checks your content, loads the Avatar, and confirms the stream destination before broadcasting.

1. Click **Start Live**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/311ca298ee63456b814fbd870c404605~tplv-goo7wpa0wc-image.image)

   The **Start Live setting** setup flow opens at **Live room content check**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b069c5c5cf440fdb23ce9eb375db610~tplv-goo7wpa0wc-image.image)

2. Review the pre\-live content. If any check shows a warning, click **Modify content** to return and fix your scripts or knowledge bases, and then start again.

   |**Check item** |**Requirement** |
   |---|---|
   |Script check |It is recommended that the estimated broadcast time is **longer than 30 minutes**. If it is shorter, refer to [Generating livestream scripts](https://docs.byteplus.com/docs/byteplus-livesaas/generating-ai-live-scripts) to enrich the script. |
   |Repetition check |Long, fully repeated scripts are not allowed. |
   |Knowledge Base check |Add **at least one knowledge base** so the AI host can answer viewer questions correctly. |

3. Set the livestream duration, and then click **Next step**.

4. Under Live duration, select either **End LIVE when script is finished** or **Go LIVE for certain hours**, configure the required settings, and then click **Next step**.

   If you select **Go LIVE for certain hours**, you are recommended to enable the AI re\-write feature to avoid script repetition.

   > **说明**

   > You can set the livestream to run for up to 24 hours. When the set duration ends, the livestream automatically closes.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b70fd0fa53404d568a9b9738961799e1~tplv-goo7wpa0wc-image.image)

5. Wait for **Avatar resource loading** to finish, and then click **Next step**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ced49870982b4c9cb9d71ac0725561e0~tplv-goo7wpa0wc-image.image)

   > **说明**

   > Loading the avatar takes time (approx. 1 minute for an existing avatar, 10 minutes for a new one). Please wait patiently.

6. Confirm the stream destination you configured in Step 4, and then click **Save** to start broadcasting. Once live, the Avatar will begin reading the script.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/04e36f806a7f4656a1d805a2fd144985~tplv-goo7wpa0wc-image.image)

7. In the **Chats** list, you can filter comments by status: Blocked by rules, Unread, or Read.

8. Click **End Live** to stop the broadcast.

## FAQ

### **Q: Some viewer nicknames contain emojis and unreadable symbols. What should I do?**

Add an instruction to the **Prompt** in your AI reply settings so the AI converts unreadable nicknames into readable text before responding. For example, add the following to your prompt:

```Plain
If the username is emoji or unreadable symbol, transform those into readable before answering the question.
```

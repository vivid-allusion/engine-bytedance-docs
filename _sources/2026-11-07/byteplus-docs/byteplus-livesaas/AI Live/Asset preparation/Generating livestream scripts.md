---
title: "Generating livestream scripts"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/generating-ai-live-scripts"
---

Livestream scripts determine what the AI host says, how the host paces the livestream, and how the content connects products with audience interaction. You can use **AI script generation** to generate livestream scripts through an interactive prompt, and then apply the generated content to your live room. This guide explains how to generate scripts with AI, and review script quality before going live.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2935c7392c634a4f851c4dc8e5dd754a~tplv-goo7wpa0wc-image.image)

## Prerequisites

Before generating scripts, complete the following tasks:

1. If you want to add a product script, add products manually or from a product library. For details, see [Step 2: Add products manually or from a product library](https://docs.byteplus.com/docs/byteplus-livesaas/managing-products-for-digital-human-livestreams#c85b3d40).

2. Prepare and upload the required knowledge base files. For details, see [Configuring knowledge bases](https://docs.byteplus.com/docs/byteplus-livesaas/configuring-product-kb).

3. If you want to add a text script, go to **Live interaction** \> **Comment reply** and add the **General Knowledge base** that applies to the current live room. For details, see [Configuring AI Live interactions](https://docs.byteplus.com/docs/byteplus-livesaas/configuring-ai-live-interactions).

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cf6ef80b5e1d494eab139ca4936c4eee~tplv-goo7wpa0wc-image.image)

4. Decide how many scenes you need and how they should be arranged. To create multiple scenes, refer to [Decorating a live room](https://docs.byteplus.com/docs/byteplus-livesaas/decorating-a-live-room) to configure the visuals for each scene first, then generate a livestream script for each scene.

   > **说明**

   > A **scene** is a segment of a livestream with its own configured visuals and script, played in sequence as part of the live broadcast. You can customize each scene with different visual materials and a dedicated script to create a more dynamic livestream experience.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dc762a2ffb9b4577905d834e4bbb7acd~tplv-goo7wpa0wc-image.image)

## Steps

### Step 1: Add a script block

1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/digitalHuman/live-rooms).

2. Open the AI live room where you want to generate scripts.

3. On the script configuration page of the live room, click **Add**, and select **Text script** or **Product script**.

   * Select **Text script** for general livestream talk that is not bound to a specific product like brand information.

   * Select **Product script** and choose the product to present. The system generates product introduction content based on the product and its knowledge base. For details, see [Step 2: Add products manually or from a product library](https://docs.byteplus.com/docs/byteplus-livesaas/managing-products-for-digital-human-livestreams#c85b3d40) and [Configuring knowledge bases](https://docs.byteplus.com/docs/byteplus-livesaas/configuring-product-kb).

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4f82fdf0f0214cc5be5c07388ef1232a~tplv-goo7wpa0wc-image.image)

### Step 2: Start AI script generation

Before you go live, the system checks the cumulative estimated speaking duration of all scripts in the live room, including text scripts, product scripts, and scripts across different scenes. Make sure the cumulative estimated speaking duration is longer than 30 minutes.

1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/digitalHuman/live-rooms).

2. Open the AI live room where you want to generate scripts.

3. In the script editor, click **AI script generation** \> **new generation**. The script generation window opens and checks the knowledge bases that can be used for generation.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e0ad027a3a4c44b5b691836b6e26d111~tplv-goo7wpa0wc-image.image)

4. If the knowledge base check fails, follow the prompt to add the required knowledge base:

   * If a text script lacks a knowledge base, go back to **Live interaction** \> **Comment reply** for the live room and add a general knowledge base.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d18ba4fa1e204cc3b3ec46fbc2d73ea6~tplv-goo7wpa0wc-image.image)

      You can upload or add an existing knowledge base. For details, see [Configuring knowledge bases](https://docs.byteplus.com/docs/byteplus-livesaas/configuring-product-kb).

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dc7cba44481f452daf831c665f1fa19c~tplv-goo7wpa0wc-image.image)

   * If a product script lacks a knowledge base, go to **Knowledge base** \> **Product** and upload this product's knowledge base file.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3b4b96eee451431c8abd181eb4b062d1~tplv-goo7wpa0wc-image.image)

### Step 3: Enter generation requirements

1. In the generation window, modify the blue highlighted parts in the example prompt, and then send the updated prompt to AI.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8a32ffd22b0548f89d951c16dfe77636~tplv-goo7wpa0wc-image.image)

   > **说明**

   * > AI script generation processes the script in segments. The generation time varies based on the duration of the spoken script you request. We recommend testing with a 1\-hour to 3\-hour script first. Do not disconnect from the network or close the page during generation.

   * > The script input box has a character limit. If the generated script is too long and cannot be pasted into one input box, add a scene and paste the remaining script into the new scene.

   * > During the livestream, scripts are played from top to bottom and from left to right. The AI host reads all scene scripts for product 1 first, and then continues to the scripts for product 2, product 3, and later products in order.

2. When all segments are complete, click **Apply to script** to write the generated content into the current script. If you only want to use part of the generated content, copy the segment you need and adjust it manually.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9a253008a6a348df8aeb249c8fe96a1b~tplv-goo7wpa0wc-image.image)

### Step 4 (Recommended): Replace words with corrected pronunciations

If the script contains brand names, product names, polyphonic characters, foreign words, or words the AI host may mispronounce, use **phonetic replacement** to fix their pronunciation. Phonetic replacement replaces specified words with the pronunciation notation you enter, helping prevent pronunciation errors during livestream reading.

1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/digitalHuman/live-rooms).

2. Open the AI live room where you want to generate scripts.

3. In the script editor, click **AI script generation** \> **phonetic transcription replacement**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/296f341196d34f1289cbc6739ad09148~tplv-goo7wpa0wc-image.image)

   The **phonetic transcription replacement** window pops up.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c6bd81092c9d47aeab1e5d3248bc6e91~tplv-goo7wpa0wc-image.image)

4. In **Original**, enter the word in the script whose pronunciation needs correction.

5. In **Replace**, enter the pronunciation you want the AI host to use.

6. Click **full text replacement** to replace all matching words in the script with the specified pronunciation.

   For example, if you want the AI host to read `直播` as `zhi2 bo1`, fill in the fields as follows:

   |**Field** |**Example** |
   |---|---|
   |**Original** |直播 |
   |**Replace** |`(zhi2 bo1)` |

   You can enter pronunciations in the following ways:

   * For English words, use IPA notation. For example, mark different uses of `live` as `(lɪv)` or `(laɪv)`.

   * For Chinese polyphonic characters, use pinyin with tone numbers. For example, mark “和” in “和平” as `(he2)` and “歌” in “唱歌” as `(ge1)`.

   * For product names, brand names, or platform terms, use the pronunciation familiar to your target audience.

7. After replacing the full text, read through the script again to make sure the result still sounds natural and that words with the same spelling in other contexts were not replaced incorrectly.

## Review and adjust scripts

AI\-generated content must be manually reviewed before going live. Check the following items:

* **Facts are accurate**: Check product names, specifications, prices, offers, inventory, logistics, after\-sales policies, and other key information.

* **Language is consistent**: Each script should use one language, unless brand names, platform names, or product names must remain unchanged.

* **Expression is natural**: Remove stiff, repetitive, or manual\-like wording. Keep short sentences and natural transitions suitable for livestream speech.

* **Content is not repetitive**: Avoid exact or highly similar repeated sentences, paragraphs, and interaction prompts.

* **Pronunciation is correct**: Check brand names, product names, foreign words, and polyphonic characters. If the AI host may mispronounce a word, use phonetic replacement.

* **Content matches the knowledge base**: If the script mentions information that is not in the knowledge base, add it to the knowledge base or remove the statement.

> **注意**

> AI\-generated scripts may contain inaccurate or business\-inappropriate information. Always review them manually before use, especially prices, offers, specifications, and after\-sales policies.

##  **(Recommended) Enable AI rewrite**

We recommend enabling **AI Rewrite**. Once enabled, after your added script has been read, BytePlus Live will use AI to automatically continue writing based on your original script, enrich your livestream content, reduce content repetition in the live room, and save the newly generated script. The newly saved script will be marked with an AI tag in the script list.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b19b2677e2c04888b53cc33e6d3ddfd0~tplv-goo7wpa0wc-image.image)

On the script configuration page, click **AI re\-write** to enable the feature.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a98ea87f8b1a44c6b4fbe1b71569f9fe~tplv-goo7wpa0wc-image.image)

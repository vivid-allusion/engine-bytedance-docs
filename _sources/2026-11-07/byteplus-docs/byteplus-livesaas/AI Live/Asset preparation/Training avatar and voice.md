---
title: "Training avatar and voice"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/training_digital_human_and_voice"
---

To run unattended, automated livestreams for your e\-commerce store, you can use the avatar Livestreaming feature from BytePlus Live. You can upload video/audio to create your own figure and voice for the livestream. This guide explains how to train your own avatar and voice in the console, and then use them on the avatar livestreaming page.

## Prerequisites

* **Activate the service**: Refer to [Subscription billing method](https://docs.byteplus.com/docs/byteplus-livesaas/subscription-billing-method) and contact sales to subscribe AI Live service.

* **Prepare your figure assets**: Refer to the [Preparing avatar training assets](https://docs.byteplus.com/docs/byteplus-livesaas/preparing-audio-and-video-for-digital-human-livestreaming) to learn about the requirements for figure assets.

* Get a BytePlus account or an IAM user account with **Live control** \> **Edit** permission. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).

## Procedure

### Train avatar and voice

Follow these steps to train your own avatar and voice.

1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).

2. On BytePlus Live's menu bar, click **AI Live**.

3. On the left navigation pane, click **Model Training** \> **Avatar**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/645eb8f5d22647448ea663af2731ee93~tplv-goo7wpa0wc-image.image)

4. On the **Avatar** page, click **Train an avatar**.

   The **Train** **an avatar** panel slides out.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ecf9e6b18324476abe331a8d26453ea4~tplv-goo7wpa0wc-image.image)

5. Fill in the fields on the panel.

   |**Configuration item** |**Description** |
   |---|---|
   |Avatar name |Enter a name for your avatar. |
   |Avatar video footage |Upload the video used for cloning. Refer to [Preparing audio and video for Digital Human livestreaming](https://docs.byteplus.com/docs/byteplus-livesaas/preparing-audio-and-video-for-digital-human-livestreaming) for requirements and best practices. |
   |Green screen matting |Enable this option if your footage was shot against a green screen. Green\-screen avatars support background removal during live room decoration. |
   |Synchronous training sound |Toggle whether to train a voice together with the avatar. If enabled, you must configure the voice\-related fields below. |
   |Voice name |Enter a name for the voice (up to 50 characters).<br><br>**Note**: This name cannot be changed after training begins. |
   |Language |The system automatically detects the language of the voice. AI Live supports 41 languages: Chinese, Cantonese, English, Arabic, Russian, Spanish, French, Portuguese, German, Turkish, Dutch, Ukrainian, Vietnamese, Indonesian, Japanese, Italian, Korean, Thai, Polish, Romanian, Greek, Czech, Finnish, Hindi, Bulgarian, Dari, Danish, Hebrew, Malay, Persian, Slovak, Swedish, Croatian, Filipino, Hungarian, Norwegian, Slovenian, Catalan, Norwegian (Nynorsk), Tamil, and Afrikaans. |
   |Voice avatar |Upload an image to represent the voice. Recommended: **1:1** aspect ratio; **JPG/PNG**; size  **<= 2 MB**. |
   |Authorization agreement |Check and agree to the **avatar Creation Authorization Form** before you can start training. |

6. Click **Start training**. Training an avatar can take from 6 hours to 1 day. Please be patient.

### Preview your avatar and voice

* **Preview your figure**: To preview your trained figure and voice, start an avatar livestream. For details, see [Starting a Digital Human livestream](https://docs.byteplus.com/docs/byteplus-livesaas/digital-human-livestream).

* **Preview your voice**: Once the voice has been successfully trained, click its card to view the details and select **Listen** to preview the audio.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3443a5adef9c4153bfd0d8ad21528279~tplv-goo7wpa0wc-image.image)

### (Optional) Clone a voice from an audio separately

You can clone a voice separately on the **Voice Cloning** page. Currently, BytePlus Live supports Chinese, Cantonese, English, Arabic, Russian, Spanish, French, Portuguese, German, Turkish, Dutch, Ukrainian, Vietnamese, Indonesian, Japanese, Italian, Korean, Thai, Polish, Romanian, Greek, Czech, Finnish, Hindi, Bulgarian, Dari, Danish, Hebrew, Malay, Persian, Slovak, Swedish, Croatian, Filipino, Hungarian, Norwegian (Bokmål), Slovenian, Catalan, Norwegian (Nynorsk), Tamil, and Afrikaans. Follow the steps below to train your voice.

1. On the **Voice Cloning** page, click the  **+Clone a voice** button.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/522724f10afe455f9ab34d8521783be9~tplv-goo7wpa0wc-image.image)

   The **Clone a voice** panel slides out.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e4ca5b2616414e78a090590479beb6b2~tplv-goo7wpa0wc-image.image)

2. Fill in the required fields and upload the audio file. The table below explains each configuration item.

   |**Configuration item** |**Description** |
   |---|---|
   |Voice name |Enter a name for the voice (up to 50 characters). |
   |Language |The system automatically detects the language of the voice. AI Live supports 41 languages: Chinese, Cantonese, English, Arabic, Russian, Spanish, French, Portuguese, German, Turkish, Dutch, Ukrainian, Vietnamese, Indonesian, Japanese, Italian, Korean, Thai, Polish, Romanian, Greek, Czech, Finnish, Hindi, Bulgarian, Dari, Danish, Hebrew, Malay, Persian, Slovak, Swedish, Croatian, Filipino, Hungarian, Norwegian, Slovenian, Catalan, Norwegian (Nynorsk), Tamil, and Afrikaans. |
   |Voice avatar |Upload an image to represent the voice. Recommended: **1:1** aspect ratio; **JPG/PNG**; size  **<= 2 MB**. |
   |Audio files |Upload your audio (WAV or MP3). Refer to [Preparing audio and video for Digital Human livestreaming](https://docs.byteplus.com/docs/byteplus-livesaas/preparing-audio-and-video-for-digital-human-livestreaming) for requirements and best practices. |
   |Authorization agreement |Check and agree to the **avatar Creation Authorization Form** before you can start training. |

3. Click **Start training**. Cloning the voice usually takes several minutes. Please wait patiently.

## Next steps

1. Add products and knowledge base: Add products and a knowledge base in the console. For a complete guide, see [Managing product library](https://docs.byteplus.com/docs/byteplus-livesaas/managing-products-for-digital-human-livestreams) and [Configuring knowledge bases](https://docs.byteplus.com/docs/byteplus-livesaas/configuring-product-kb).

2. **Start a Livestream:**  Configure your live room and go live. For details, see [Starting an AI Live](https://docs.byteplus.com/docs/byteplus-livesaas/digital-human-livestream).

## FAQ

### Q: Who can see the assets I trained?

The trained assets belong to the logged\-in IAM user. Only the owner and the admin account can view it. For more information, see [Account data isolation for AI live](https://docs.byteplus.com/docs/byteplus-livesaas/account-data-isolation-for-ai-live).

---
title: "Decorating a live room"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/decorating-a-live-room"
---

Live room decoration lets you customize how an AI Live room looks on screen. You can add background images, foreground images, stickers, and cutaway videos, adjust each material's layer, position, and size, and enable green\-screen matting for avatars trained with green\-screen footage.

## Prerequisites

* You have activated AI Live. To activate the service, contact sales as described in [Subscription billing method](https://docs.byteplus.com/docs/byteplus-livesaas/subscription-billing-method).

* You have uploaded the required images or videos to the material library. For details, see [Managing live room visual materials](https://docs.byteplus.com/docs/byteplus-livesaas/manage-live-room-visual-materials).

* To add a background image behind the AI host, the host avatar must have been trained with green\-screen footage and have green\-screen matting enabled. For details, see [Training avatar and voice](https://docs.byteplus.com/docs/byteplus-livesaas/training_digital_human_and_voice).

## **Use case**

You can use one scene as the main livestream view and another as a product close\-up cutaway. For example, Scene 1 shows the AI host speaking in the live room, with overlay videos and images to enhance the presentation. Scene 2 plays a cutaway video, such as a close\-up of the product. The cutaway video's original audio is muted, while the AI host continues reading the script configured for Scene 2 as the video plays.

**Scene 1**

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fbe54ac0d5bc447c93524e1e2e1fe16e~tplv-goo7wpa0wc-image.image)

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/913e74fb26454172ace0d4fada522390~tplv-goo7wpa0wc-image.image)

**Scene 2**

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/57db58f2b2aa44e2a7bee6d61c2a6dc2~tplv-goo7wpa0wc-image.image)

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3d7abf2b9d64411aa988816e770d1412~tplv-goo7wpa0wc-image.image)

## Basic concepts

You can decorate each scene with images or video materials:

* **Cutaway Video**: Close\-up product clips inserted in the middle of the live stream, such as product showcases or transition scenes. Only the video plays — the original audio is muted. The clip plays once, then disappears and the AI host resumes broadcasting.

* **Overlay Video**: A video overlay superimposed on the live screen. The original audio is muted, and the clip loops within the scene.

* **Image**: Image assets used as overlays on the live screen, including backgrounds, foregrounds, campaign stickers, and price tags.

## Steps

Before decorating your live stream, decide how many scenes you need and how they should be arranged. Next, configure the materials for each scene, then return to **Live Scene** to review the script for each scene. During the live stream, the AI host will read each script and display the corresponding visuals in the configured scene order (e.g., Scene 1, Scene 2, and Scene 3).

The steps below show how to create two scenes and use one scene as the main livestream view and another scene as a product close\-up cutaway.

1. Log in to the [BytePlus Live console](https://console.byteplus.com/).

2. In the top navigation bar, select **AI Live**.

3. On the **Live Room** page, click to open an existing live room or create a live room.

4. On the AI live room page, click **Live room decoration**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2481d8482ddc48bca314506d245183bf~tplv-goo7wpa0wc-image.image)

5. Click the  **+**  icon in the scene area to create Scene 1 and Scene 2.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ce457b151b6c44e581750fc9118b342c~tplv-goo7wpa0wc-image.image)

6. Select **Scene 1**.

7. Add materials for the main livestream view. If there are no materials, click the + upload icon to add a new material. For steps, see [Managing live room visual materials](https://docs.byteplus.com/docs/byteplus-livesaas/manage-live-room-visual-materials).

   * To add a video overlay, select **Overlay Video**, and then click the target video.

   * To add an image, select **Image**, and then click the target image.

      The selected material is added directly and appears in the preview area.

8. Select **Scene 2**.

9. Add a cutaway video for the product close\-up:

   1. Select **Cutaway Video**.

   2. Click the target product close\-up video. The video is added to Scene 2.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/367f0b8a7f334cf1ba4063499313257e~tplv-goo7wpa0wc-image.image)

10. Adjust the layer order, position, size, and opacity of the materials in each scene as needed. For details, see [Adjust materials](https://docs.byteplus.com/docs/byteplus-livesaas/decorating-a-live-room#85a40001).

11. After adding materials, click **Live Scene**.

12. Select Scene 1, and then enter or generate the script for the main livestream view.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/92851edd64d64c29b1446aaee29d68be~tplv-goo7wpa0wc-image.image)

13. Select Scene 2, and then enter or generate the script for the product close\-up. The preview area displays the cutaway video. The video itself is muted, and the AI host reads the script configured for Scene 2.

14. Repeat the same process for additional scenes. The AI host reads the scripts and plays the configured videos in scene order.

### Adjust materials

After you select a material in the preview area, you can adjust it in the property area.

#### Layer order

Adjust the layer order of a material in either of two ways:

* In the **Layer** panel, drag a material thumbnail up or down to reorder it.

* In the **Layer order** section of the property panel, click the **Move up** or **Move down** icon to shift the selected material one layer at a time, or click the **Bring to front** or **Send to back** icon to move it to the top or bottom of the stack.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1d68636bcebe48c290fadf1ef47778ca~tplv-goo7wpa0wc-image.image)

#### Position and size

Adjust the position and size of a material in either of two ways:

* **On the preview canvas**: Drag the material to move it, or drag any of its four corners to resize it.

* **In the property panel**: Enter exact values under **Location** (X, Y) to reposition the material, or under **Size (%)**  (W, H) to resize it. Click the link icon between W and H to keep the aspect ratio unlocked.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c96f6a9a201942549fef4f2ed2212e18~tplv-goo7wpa0wc-image.image)

#### Opacity

Change the transparency of the material.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f81bb7b8dc2b4febaca993e0d5c776fc~tplv-goo7wpa0wc-image.image)

**Apply to all scenes**

In the property panel, click **App to all** to apply the currently selected material and its configuration to every live scene in the live room.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c842aa8a8e42418ea442182d089748aa~tplv-goo7wpa0wc-image.image)

#### Live stream effect preview

Click the eye icon above the preview area to overlay a sample live\-stream scene — including bullet chat, gift banners, and product cards — on top of your current decoration. This helps you check whether foreground elements, stickers, or product cards will be covered during the live stream. Click the icon again to turn the preview off.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/844a35ea5504466c9919ba820414f34a~tplv-goo7wpa0wc-image.image)

#### Safe area

Click the frame icon above the preview area to display or hide the safe zone. The area outside the frame is dimmed to indicate that it may be cropped or covered by system UI on some devices — keep key materials such as product cards, price stickers, and text inside the highlighted zone.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/109ca42856934febaa349e901c4eb0a3~tplv-goo7wpa0wc-image.image)

## Related documents

* [Managing live room visual materials](https://docs.byteplus.com/docs/byteplus-livesaas/manage-live-room-visual-materials)

* [Starting an AI Live](https://docs.byteplus.com/docs/byteplus-livesaas/digital-human-livestream)

* [Training avatar and voice](https://docs.byteplus.com/docs/byteplus-livesaas/training_digital_human_and_voice)

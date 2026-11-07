---
title: "Live streaming FAQs"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-faqs-about-live-streaming"
---

<span id="8039a848"></span>
## Live streaming from your web browser

<span id="7ce8a98e"></span>
### Why am I unable to share my screen on Mac?

For macOS 10.15 or later, complete the following steps to manually allow Google Chrome to record your screen.


1. Click the Apple icon \> **System Preferences** and then click **Security & Privacy**.

2. Click **Screen Recording** on the left.

3. Select the **Google Chrome** checkbox on the right.


<span id="3a18e309"></span>
### Why are my CPU and memory usage so high?


* Make sure that your computer is a Windows PC with at least 8 GB of memory, a Core i5 processor, a discrete graphics card, and 4 GB of video memory. Otherwise, your CPU and memory usage may be high since live streaming from a web browser consumes a certain amount of memory and CPU resources.

* Check if the **Use hardware acceleration when available** switch is turned on for your Google Chrome, which allows the browser to use GPU resources. Not activating it can drain your CPU.


<span id="9c940194"></span>
### My audio sometimes cuts out for viewers. Why does this happen?

This happens when you switch the sound collection device, for example from a Bluetooth headset to a computer microphone, during a live stream. To resolve the issue, refresh the live streaming page after you switch the device.

<span id="45b1e9c3"></span>
### How to use the OBS virtual camera?

[Open Broadcaster Software (OBS)](https://obsproject.com/), available for Windows, macOS, and Linux, is a free and open source software for video recording and live streaming. For more information, see the [OBS User Guide](https://obsproject.com/help).

You can select the [OBS virtual camera](https://obsproject.com/kb/virtual-camera-guide) as your camera when live streaming from your web browser. To do so, complete the following steps.

<span id="00c945b8"></span>
#### Step 1: Download and install OBS

Click [here](https://obsproject.com/download) to download and install OBS.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Make sure the version is 26.0 or later.</div>


* <div data-tips="true" data-tips-type="tip">Make sure your computer meets the corresponding system requirements for OBS. For more information, see <a href="https://obsproject.com/kb/system-requirements">System requirements</a>.</div>



<span id="e0b23598"></span>
#### Step 2: Configure the server URL and stream key


1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).

2. On the live room list, click to open a live room.

3. On the **Live control** page, click **Push stream** on the **Broadcast method** tab under the player.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/066ac95fff29473b806bf6e1bcca0d84~tplv-goo7wpa0wc-image.image) </span>

4. Copy the server URL and stream key.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Keep your server URL and stream key confidential. Anyone who has the server URL and stream key can push live content to your live room.   </div>
   

5. Open your OBS and click **File** \> **Settings** in the upper\-left corner.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/826f32e64d6340a28d0489136545d635~tplv-goo7wpa0wc-image.image) </span>

6. In the **Settings** dialog box, click **Stream** on the left navigation pane and select **Custom...**  from the **Service** drop\-down list.

7. Enter the server URL and stream key copied in step 4 into the **Server** and **Stream Key** fields.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6883c5c7b1024a238d7d1cc39d42ecb4~tplv-goo7wpa0wc-image.image) </span>

8. Click **OK**.


<span id="91dde1c2"></span>
#### Step 3: Add sources

Add the sources that you want viewers to watch during the live stream. In this example, add the display capture to start a live stream with real\-time screen capturing.


1. Click + in the **Sources** section at the bottom of OBS.

2. Select **Display Capture** from the drop\-down list.

3. Enter a name and click **OK** in the **Create/Select Source** dialog box that appears.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/21275bbaf230430dbdefdb1cd09e9360~tplv-goo7wpa0wc-image.image) </span>

4. (Optional) In the dialog box that appears, adjust the settings as needed, such as whether to capture your cursor.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f01284a7d1364c828f08b7ebed9024ac~tplv-goo7wpa0wc-image.image) </span>

5. Click **OK**.


<span id="1e594a77"></span>
#### Step 4: Synchronize OBS source to live room with OBS virtual camera


1. Click **Start Virtual Camera** in the lower\-right corner of OBS.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5d94897c1b974961a88089e0018c614c~tplv-goo7wpa0wc-image.image) </span>

2. Go to the live streaming page of your live room in a web browser.

3. In the **Test your device** dialog box that appears, select **OBS Virtual Camera** from the **Select camera** drop\-down list. Then, the OBS source is synchronized to the live room. However, the source audio cannot be synchronized.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/92e9f3d41f6a44819397396b7dafaac1~tplv-goo7wpa0wc-image.image) </span>

   If OBS virtual camera is not selected when you enter the live streaming page, you can also click the **Media settings** icon and change the camera to OBS virtual camera.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c12b507f55cd4326af5a4cb491bc9268~tplv-goo7wpa0wc-image.image) </span>

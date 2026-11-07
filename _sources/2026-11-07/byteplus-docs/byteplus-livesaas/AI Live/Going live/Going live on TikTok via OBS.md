---
title: "Going live on TikTok via OBS"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/Going_live_on_TikTok_via_Digital_Human_and_OBS"
---

To stream your BytePlus AI figure to TikTok, this guide provides the complete setup process using OBS Studio and TikTok Live Studio. You will learn how to configure all required software, route audio and video signals between applications, and troubleshoot common issues for a successful livestream.

<span id="202b2df4"></span>
## System Requirements

Before you begin, ensure your computer meets the system requirements and install the required software listed below.


* **RAM:**  Minimum 16 GB (stream may lag or crash with less)

* **GPU:**  GTX 1080 / RTX 2070 / RTX 3060 or higher

* **CPU:**  Intel i9, Intel i7\-9700K, or AMD Ryzen 5 3600X or higher


<span id="18fb01ff"></span>
## Prerequisites


* A BytePlus account or an IAM user with **Marketing toolkits** \> **Edit** permission. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).

* The permission to go live on TikTok. For more information, see [Who can use LIVE on TikTok](https://www.tiktok.com/support/faq_detail?id=7543604790438451768&category=web_account#2).

* You have downloaded the following software:



|**Software name** |**Download Link** |**Purpose** |
|---|---|---|
|Google Chrome |[Download Google Chrome](https://www.google.com/chrome/) |Required for the BytePlus AI figure platform. Only Chrome is supported. |
|OBS Studio |[Download OBS Studio](https://obsproject.com/download) (install with default options) |Video capture and streaming software. |
|VB\-Audio Virtual Cable |Contact Sales for download link |Virtual audio device to route audio from OBS to TikTok. |
|TikTok Live Studio |[Download TikTok Live Studio](https://www.tiktok.com/studio/download) |Official TikTok streaming assistant. |


<span id="a159f787"></span>
## Steps

<span id="448e55b2"></span>
### Step 1: Configure Google Chrome browser


1. Open **Google Chrome** on your computer.

2. Click on the address bar at the top of the browser window and paste the following URL exactly:


```Plain
chrome://settings/content/popups
```



3. Press **Enter** on your keyboard.

4. Enable "Sites can send pop\-ups and use redirects."

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/15fa2a981c43491d8ec1d9d8598f587c~tplv-goo7wpa0wc-image.image) </span>


<span id="f0f7c889"></span>
### Step 2: Configure VB\-Audio Virtual Cable


1. Contact Sales for the VB\-Audio Virtual Cable download link.

2. Extract the ZIP.

3. Inside the VB\-Cable folder, right\-click `VBCABLE_Setup_x64.exe` and choose "Run as administrator".

4. When the installer opens, click the **Install Driver** button. If a prior version exists, click "Remove Driver" first, then re\-install.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a683c1ad239b44a1afc7c75a21d3e316~tplv-goo7wpa0wc-image.image) </span>


<span id="4f131f1d"></span>
### **Step 3: Configure sound settings**


1. Open **Windows Settings** by pressing **Win + I**.

2. Go to **System** \> **Sound**.

3. Under **Input**, select **CABLE Output (VB\-Audio Virtual Cable)**  as the default input device.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2eb0ed44a0f94955a3a97258cef953f7~tplv-goo7wpa0wc-image.image) </span>

4. If needed, click **All sound devices** to view the full device list and confirm both virtual cable devices are available:

   * **CABLE Input** should appear under **Output devices**

   * **CABLE Output** should appear under **Input devices**

5. Disable any recording devices you do not plan to use, so the virtual cable is the active input path.


<span id="28c94099"></span>
### **Step 4:**  Start an AI Live

Refer to [Starting an AI Live](https://docs.byteplus.com/docs/byteplus-livesaas/digital-human-livestream) to complete the process for going live and ensure the stream starts successfully. A video preview appears on the screen when the stream is live.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/621856507af14628a00986a367b92c3c~tplv-goo7wpa0wc-image.image) </span>

<span id="8cdb2f65"></span>
### **Step 5: Get pull stream address**


1. In the top navigation bar, click the **Live platform** button.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e6b082de70e24ddc8aa86c4726e151de~tplv-goo7wpa0wc-image.image) </span>

2. In the **Live platform** dialog, select **TikTok** as the live platform and **Virtual camera** as the streaming method.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/56b641374be9477ead9cbde9d6097879~tplv-goo7wpa0wc-image.image) </span>

3. Get the ID in your TikTok App as shown below.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a0e3fc1adba4f5fb470be530312ebb4~tplv-goo7wpa0wc-image.image) </span>

4. Click the **Copy** button. The address starts with "rtmp://pull\-rtmp\-...".


<span id="3d5cd8e0"></span>
### **Step 6:**  Pull the stream into OBS via Media Source


1. Open OBS Studio.

2. In the **Sources** panel, click the  **+**  button and choose **Media**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0fb4b58c328b41ef95646c2bdf7ec532~tplv-goo7wpa0wc-image.image) </span>

3. On the **Create/Select Source** dialog, confirm the name and click **OK**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/61355af960bb4352b8d8c1203b86fa04~tplv-goo7wpa0wc-image.image) </span>

4. In the **Properties for 'Media'**  dialog, uncheck "Local File", paste the live stream URL from Step 5 into the Input field, set **Input Format** to flv, and then click **OK**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/237cf3914e2045d78e42bcd8328382fa~tplv-goo7wpa0wc-image.image) </span>


<span id="08bd8cd5"></span>
### Step 7: Route OBS audio into the virtual microphone


1. In OBS, click the gear icon in the bottom\-right corner of the Audio Mixer panel to open the audio properties dialog.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9a038fa968a4dbf94ce4f51553e58bc~tplv-goo7wpa0wc-image.image) </span>

2. For the **Media** Source row, set Audio Monitoring to "**Monitor and Output**". This routes the stream's audio into the VB\-Cable virtual microphone so that TikTok Live Studio can capture it.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b6107940fa304cc4ab9b5bb35ccc7bc0~tplv-goo7wpa0wc-image.image) </span>

3. Then enable the Virtual Camera in OBS by clicking **Start Virtual Camera** in the **Controls** panel.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5466bb9d7b1e41c68cf793061baf9f65~tplv-goo7wpa0wc-image.image) </span>


<span id="7b713c58"></span>
### Step 8: Add the camera in TikTok Live Studio and go live


1. Open TikTok LIVE Studio.

2. In the Sources panel, click **Add Source**.

3. In the **Add Source** dialog, select **Camera**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b4fa84fc27d94c5c9bcf4193f386c84b~tplv-goo7wpa0wc-image.image) </span>

4. In the **Camera** dropdown, select **OBS Virtual Camera**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/29f01a49481b41ffac345d2747025c46~tplv-goo7wpa0wc-image.image) </span>

5. Confirm the preview shows your OBS scene. If your image is inverted, click **Rotate** or **Flip** to adjust it.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/24e186f9e96d4c508e39180ca237b51a~tplv-goo7wpa0wc-image.image) </span>

6. Click the Audio mixer icon in the bottom toolbar and click  **+ Add**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c3a436b5a3274a1cb12acd9461a8e595~tplv-goo7wpa0wc-image.image) </span>

7. Select **CABLE Output (VB\-Audio Virtual Cable)**  and then click **Add**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c1cb4dc32038413f9fd90f9568e8158f~tplv-goo7wpa0wc-image.image) </span>

8. Mute other microphones.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0cbd2c8c73f14b2e82ddde59739a71e4~tplv-goo7wpa0wc-image.image) </span>

9. Verify that you can see the stream's video and that the microphone level meter is moving. When everything looks good, click **Start Live** in the bottom\-right corner.


<span id="8a791e48"></span>
## Troubleshooting

Audio problems are by far the most common issue with this setup. Below are the symptoms users report most often, and the exact fix for each.

<span id="7d8d33f8"></span>
### Echo on the stream (viewers hear your audio repeating)

**Likely causes:** 


* OBS Audio Monitoring is set to "Monitor and Output" on a source that is ALSO captured by your microphone (e.g., desktop speakers and a microphone).

* Both Desktop Audio AND the Media Source are being sent into the virtual cable, so TikTok captures the same sound twice.

* Windows "Listen to this device" is enabled on CABLE Output, looping audio back to your speakers.


**Fixes:** 


* In OBS → Advanced Audio Properties: ONLY the Media Source (the BytePlus pull stream) should be set to "Monitor and Output". Set every other source — Desktop Audio, Mic/Aux, browser sources, etc. — to "Monitor Off".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e520771d8754e33a649d5a3f3dcc976~tplv-goo7wpa0wc-image.image) </span>

* Mute Desktop Audio in the OBS mixer if you do not need to share PC sound.

* Open Windows Sound → Recording → CABLE Output → Properties → Listen tab, and UNCHECK "Listen to this device".

* Use headphones instead of speakers while testing — speaker output picked up by your physical mic is a frequent echo source.


<span id="46e3bc9e"></span>
### Double audio input (audio is duplicated)

**Likely causes:** 


* Both your physical microphone and the VB\-Cable virtual microphone are enabled as inputs in TikTok LIVE Studio.

* OBS is sending audio to BOTH the virtual cable and TikTok's direct capture (Desktop Audio Monitor) at the same time.

* Two Media Sources have been accidentally added in OBS, both pulling the same BytePlus stream.

* VB\-Cable was installed twice, creating CABLE\-A and CABLE\-B, and audio is being routed through both.


**Fixes:** 


* In TikTok LIVE Studio audio settings, set ONLY one Main Microphone — CABLE Output (VB\-Audio Virtual Cable). Disable any other mic in the dropdown.

* In Windows Sound → Recording, right\-click every input that is not CABLE Output and choose Disable. Keep only CABLE Output enabled.

* In OBS, check the Sources list and ensure there is exactly ONE Media Source for the BytePlus pull stream. Delete any duplicates.

* In OBS Audio Mixer, mute Mic/Aux unless you genuinely need to overlay your own voice on top of the digital host.

* Open Programs and Features in Windows; if you see VB\-Audio Virtual Cable listed twice, uninstall both, reboot, then re\-install once.


<span id="50fab813"></span>
### No audio reaches TikTok LIVE Studio


* Confirm OBS is actually playing the Media Source (you should see the green VU meter moving on that row).

* In OBS → Advanced Audio Properties, set the Media Source row to "Monitor and Output" (NOT just "Monitor Off" or "Monitor Only").

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e520771d8754e33a649d5a3f3dcc976~tplv-goo7wpa0wc-image.image) </span>

* In Windows Sound → Playback, make sure CABLE Input (VB\-Audio Virtual Cable) is ENABLED. If it is disabled, OBS cannot route audio to it.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2eb0ed44a0f94955a3a97258cef953f7~tplv-goo7wpa0wc-image.image) </span>

* In TikTok LIVE Studio, confirm the Main Microphone is CABLE Output and click **Test** to see the meter move.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0cbd2c8c73f14b2e82ddde59739a71e4~tplv-goo7wpa0wc-image.image) </span>

* Restart OBS after changing audio routing — some changes only apply after a relaunch.


<span id="4b88becc"></span>
### Crackling, robotic, or distorted audio


* In Windows Sound → Recording → CABLE Output → Properties → Advanced, set the sample rate to 48 000 Hz, 16\-bit (DVD quality).

* In Windows Sound → Playback → CABLE Input → Properties → Advanced, set the SAME sample rate (48 000 Hz, 16\-bit). The sample rate must match on both sides of the virtual cable.

* In OBS → Settings → Audio, set Sample Rate to 48 kHz and Channels to Stereo.

* If your CPU is under heavy load, lower the OBS output resolution or video bitrate to free up CPU resources for audio processing.


<span id="e46a54c3"></span>
### Stream lags, freezes, or drops


* Confirm RAM ≥ 16 GB and that no other heavy apps (games, browsers with many tabs, video editors) are running.

* In OBS → Settings → Output, lower video bitrate to 4 000–6 000 kbps and set encoder to NVENC (NVIDIA) or QuickSync (Intel) instead of x264.

* Use a wired Ethernet connection instead of Wi\-Fi.

* If the Media Source freezes, right\-click it in OBS → Restart, or simply remove and re\-add the source with the same flv URL.

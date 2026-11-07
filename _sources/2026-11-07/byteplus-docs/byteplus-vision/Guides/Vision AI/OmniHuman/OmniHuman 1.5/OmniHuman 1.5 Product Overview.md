---
title: "OmniHuman 1.5 Product Overview"
product: "Vision AI"
product_code: "byteplus-vision"
source: "https://docs.byteplus.com/en/docs/byteplus-vision/omnihuman1_5overview"
---

1. # Product Introduction <span id="7NJtpwjV"></span>

   ## Product Name    <span id="EX4pi143"></span>


OmniHuman 1.5


## Product Description <span id="l5S3NouF"></span>


OmniHuman 1.5 can generate a video based on a single image + audio uploaded by the user. It supports inputting images of any frame size (under 4096\*4096) that contain people or other subjects (pets, animations, etc.), and combines them with audio to generate high\-quality videos.

The emotions and movements of the characters have a strong correlation with the audio. It supports adjusting the picture, movements, and camera movements through prompts. At the same time, OmniHuman 1.5 has good support for images such as animations and pets, allowing the designation of speakers/subjects, and can be widely used in scenarios such as singing, and performances.

Compared with the previous generation model, OmniHuman 1.5 has significantly improved motion naturalness and structural stability, and is superior in the motion expressiveness of characters/subjects and picture quality. It can be widely used in creating content such as plot dialogues, multi\-person dialogues/duets, product interactions, and animation dramas. Compared with other general video models, the OmniHuman digital human model has significant advantages in the plot interpretation effect of characters/subjects.


## Product Advantages <span id="BY8WSdlK"></span>

* **Rhythmic Performance**: The flexibility of the model extends to the music field. The algorithm can create emotional digital singers using only a single image and a song. Driven by our inference module, movements are not limited to simple lip\-sync—they also include natural pauses and rhythmic variations, enabling flexible adaptation to various styles, from solo lyrical songs to lively concert performances.

* **Emotional Performance**: Using only a single image and a piece of audio, the model can bring digital actors "to life". By analyzing the emotional connotation of the audio (no text prompt required), it generates engaging, cinematic performances that cover a full range of dramatic expressions, from intense anger to sincere confessions.

* **Context Awareness**: By parsing the semantic context of the audio, our model goes beyond simple lip\-sync and repetitive movements. It enables characters to exhibit authentic emotional changes, and aligns their movements with their words and intentions—as if they have their own will.

* **Text\-Guided Multimodal Performance**: The carefully designed algorithm framework accepts text prompts and demonstrates excellent prompt\-following capabilities. This allows precise control over object generation, camera movements, and specific actions while maintaining perfect audio synchronization.

* **Single/Multi\-Person Scene Performance**: The model framework extends to complex multi\-person scenarios. It generates dynamic performances by routing separate audio tracks to the correct character in a single frame, supporting both the specification of a speaker and joint performances.

* **Support for Diverse Subjects**: The model exhibits excellent robustness and covers an incredibly wide range of subjects, including real animals, anthropomorphic characters, and stylized cartoons.


*Note: The model’s generation results have a certain degree of randomness, and not every generation effect may meet your expectations.* 


## Demo Showcases <span id="cGyrj0EX"></span>

1. **Continuous actions and movement control**


Describe the order of actions using words like 'first' and 'then' to achieve complex action choreography. Remember to include words like 'talking' and 'singing' for the characters in the prompt.


|**Input Image & Audio** |**Prompt** |Generated Videos |
|---|---|---|
|Image:<br><br><span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_4186eb9fd131c774f2733851d387cf61.PNG) </span>Audio:<br><br><Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_bbbec653ed512bac17224f76249321b3.MP3" name="Audio 1.MP3">Audio 1.MP3</Attachment><br> |The man walks forward first, then stops and puts his hands on his hips while **speaking**. Then, he turns around to look at the explosion behind him, showing his back. The clothes on his back have been blown to pieces.<br><br> |<video src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_d52390f4339275e757889c0b05a78a60.mp4" controls></video><br> |
|Image: <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_7776f9104109225849484aca24279910.PNG) </span>Audio:<br><br><Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_ee7974a0b8c6851248191ec772c3e15a.MP3" name="Audio 2.MP3">Audio 2.MP3</Attachment><br> |The camera follows. The man turns around, looks at the camera and walks forward, **singing** intoxicatedly. He first touches his collar with both hands, then spreads his hands and raises his head, looking completely absorbed. |<video src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_cfd951a6c4ac9dfc9d80eca63bb207a3.mp4" controls></video><br> |



2. **Speak first then make a gesture / Make a gesture first then speak**


Not only can the gestures during speaking be choreographed, but gestures can also be inserted before or after speaking.


|**Input Image & Audio** |**Prompt** |Gernerated Videos |
|---|---|---|
|Image:<br><br><span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_fe2929efc95a4d3b994379626c78107c.PNG) </span><br><br>Audio:<br><br><Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_4a51d8013b7dd812f0c710cc9299c815.MP3" name="Audio 3.MP3">Audio 3.MP3</Attachment><br> |The man quickly took out the cigarette from his mouth and then started speaking to the camera.<br><br> |<video src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_636c43f995a9fa5057e0f61dc1551589.mp4" controls></video><br> |
|Image:<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_2b09396f974e2b4ac49d15856e7004ec.png) </span>Audio:<br><br><Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_f1f7d06c1e328727b0a530f4c13e6316.m4a" name="Audio 4.m4a">Audio 4.m4a</Attachment><br> |The camera zoomed in. The woman spoke to the camera, and after finishing, she quickly turned around and ran backward. |<video src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_1ffdd3ff76ed4a76b376b920e3160380.mp4" controls></video><br> |



3. **Multi\-character Action Control**


The multi\-person scenario focuses on describing the **interaction modes** between characters.

>  **⚠️ ** Note: OmniHuman 1.5 does not support using a single audio clip to drive a conversation between different characters. In a multi\-character scenario, one audio clip can only be used to drive one character to speak or multiple characters to speak simultaneously. If you need to enable a conversation between different characters, please call the interface multiple times to generate videos and then stitch the videos together.

> 

> **For multi\-person singing and speaking (in a multi\-person scenario, specifying one person or multiple people simultaneously), the Subject Detection service is required.**  This service will detect all subjects (people, animals, etc.) in the image and return their respective mask_urls. If you want to specify one character to speak, pass the mask_url corresponding to that character. If you want to specify multiple characters (to speak simultaneously), pass a list of mask_urls.



|**Input Image & Audio** |**Prompt** |**Generated Videos** |
|---|---|---|
|Image:<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_929d7fea56c15644f3dedded0e8cd55f.png) </span>Audio:<br><br><Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_ef3e8c3fc5e9c58ba6d6972fcebe1243.MP3" name="Audio 5.MP3">Audio 5.MP3</Attachment><br> |Following the camera, the boy first quickened his pace forward to catch up with the girl and then started talking to her. The girl stopped, turned around with an impatient look, and stared at the boy. |<video src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_6ad5c23f6303717e3e8766335b45b222.mp4" controls></video><br> |
|Image:<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_7bdb0cc3c376825dad0faa3aacc4ed3b.png) </span>Audio:<br><br><Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_132452c45ba990abb2c93bc9449717e0.MP3" name="Audio 6.MP3">Audio 6.MP3</Attachment><br> |Following the camera, the man holding a torch on the left side of the screen first looked at the others while speaking and then looked back at the camera. |<video src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_fe7afacfc7df4032aee6bc0530163e28.mp4" controls></video><br> |



4. **Camera movement control**


Precisely control the movement mode and rhythm of the camera.


> * The techniques are consistent with those of the video generation model. You can precisely control the speed and end position of the camera movement by describing the camera state at the end of the movement. For example, 'The camera moves forward and focuses on xx.'

> * Using words like 'rapidly' can improve the responsiveness of camera movement.



|**Input Image & Audio** |**Prompt** |Generated Videos |
|---|---|---|
|Image:<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_2e992cf61383d6ff9eba4220c4161420.jpeg) </span>Audio:<br><br><Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_3d9148009003419fead32f89b7f8a986.MP3" name="Audio 7.MP3">Audio 7.MP3</Attachment><br><br><br> |**Pan the camera to the right in a circular motion and focus on the man's front face**. The man quickly takes off his glasses and speaks while facing straight ahead. |<video src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_6fa9fd7e2a9852aef1f30d282863ae8f.mp4" controls></video><br> |
|Image:<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_5e6d19ffce17602e23e711caeec3a142.jpeg) </span>Audio:<br><br><Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_2ddcd5eeb8ca18dd7b469e97203e132c.MP3" name="Audio 8.MP3">Audio 8.MP3</Attachment><br> |**Pan the camera to the right in a circular motion**. The character speaks while facing straight ahead. **Then quickly zoom in the camera and focus on the character's front face**. The character puts down the binoculars and speaks. |<video src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_8f3996c5b34e00d64a31c19299e37d2d.mp4" controls></video><br><br><br> |


When a character leaves the camera frame for a long time and then re\-enters, consistency changes are likely to occur. When designing camera movement prompts, try to avoid situations where the character repeatedly leaves the camera frame.


5. **Emotional level control & Micro\-expression control**


Describe delicate emotional changes in combination with audio content.


|**Input Image & Audio** |**Prompt** |Generated Videos |
|---|---|---|
|Image:<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_507b94ce8244644ed1c351c79405f64a.png) </span>Audio:<br><br><Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_47616059eed19f2394ddb1e73d18af7f.MP3" name="Audio 9.MP3">Audio 9.MP3</Attachment><br> |First, the man looked calm and spoke to the camera. Then, he suddenly became nervous and panicked, frowning tightly. |<video src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_2300b3ea6b874e290b233478f82d9fde.mp4" controls></video><br> |
|Image:<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_6d82fd090040eca3c882970083561822.png) </span>Audio:<br><br><Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_8cfc468f6489617f3c4ac668abba307c.MP3" name="Audio 10.MP3">Audio 10.MP3</Attachment><br><br><br> |First, the woman rolled her eyes disdainfully and spoke with a contemptuous look. Then, she used her index finger to support her chin with one hand. Finally, she played with the box on the table with a haughty attitude. The background remained still throughout. |<video src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_a1e74d71cada9b5de9991e8ec5d8bb35.mp4" controls></video><br> |



6. **Special effects / Creation out of nothing / Adding visual elements**


Elements not present in the reference image can be added using prompt words.


|**Input Image & Audio** |**Prompt** |Generated Videos |
|---|---|---|
|Image:<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_f3d3dda560f740ac6ac630dc27f68c66.png) </span>Audio:<br><br><Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_16aa7938676e842633dd4ef2b269866a.MP3" name="Audio 11.MP3">Audio 11.MP3</Attachment><br> |The father and son looked at the camera in shock, and the son spoke. Then the camera began to slowly zoom in. Distorted ripples appeared in the air. **The father and son were sucked into the depths of the picture like dust and vanished instantly.**  The camera froze, leaving only the remote control and the phone on the empty sofa. |<video src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_74778e9ea5ee081ba3eab2a0332efc73.mp4" controls></video><br> |
|Image:<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_59d819a1363142b962e0c4dd68be0946.jpeg) </span>Audio:<br><br><Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_b598370c918571cf2698dcf25339695e.MP3" name="Audio 12.MP3">Audio 12.MP3</Attachment><br> |The chick **put on sunglasses and held two guns in hand** and spoke evilly. |<video src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_61a4acfeb12a07860eb363ebaf1ccf6f.mp4" controls></video><br> |



7. **Camera focus control**


For scenes where there are different characters in the foreground and background respectively, the camera's focus shift can be controlled through prompt words to match the content's meaning.


|**Input Image & Audio** |**Prompt** |Generated Videos |
|---|---|---|
|Image:<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_9b000374f0b7effb381d4764426b0f2d.png) </span>Audio:<br><br><Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_20ed83cd0810bc44443c43bc9ba12294.MP3" name="Audio 13.MP3">Audio 13.MP3</Attachment><br> |The reporter is reporting to the camera. Meanwhile, the king behind suddenly collapses. **The camera focuses on** the collapsed king behind the reporter. The reporter turns around incredibly quickly and speaks while looking behind. |<video src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_c9f4d252505832bb61515b1564f4904d.mp4" controls></video><br> |
|Image:<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_7d29d504a90a3d9554c7dfa233339d52.png) </span>Audio:<br><br><Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_817fefe6af91e2dfdef1569756a8ec68.MP3" name="Audio 14.MP3">Audio 14.MP3</Attachment><br> |The woman turns around and speaks while looking at the soldier behind. Meanwhile, **the camera focuses on the soldier behind**. Then the woman turns back and continues speaking to the camera. |<video src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_2c9d65158d92ceaa05b38601b69f9460.mp4" controls></video><br> |



8. **Environmental interaction description**


Create a natural interactive relationship between the character and the environment, or describe the events taking place in the background scene.


|**Input Image & Audio** |**Prompt** |Generated Videos |
|---|---|---|
|Image:<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_acb84d04326453695183a54a07af5e05.png) </span>Audio:<br><br><Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_c6da8f6ca111dddf4e40ee2ad42d33e3.MP3" name="Audio 15.MP3">Audio 15.MP3</Attachment><br> |The orangutan stands still, raises its right arm to maintain a selfie pose, and talks while looking at the camera. **The volcanic lava behind it gradually turns blue.**  |<video src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_ad515cbed946416709b7bdd785f056a9.mp4" controls></video><br> |
|Image:<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_2c3247644704b1167d0465ddbbbd9f63.jpeg) </span>Audio:<br><br><Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_b854284dba5380a9b75cc0e90d6f24df.MP3" name="Audio 16.MP3">Audio 16.MP3</Attachment><br> |Holding the camera, the woman looks into the distance. In the distance behind her, **fireworks are going off, and the wind blows her hair and clothes.**  |<video src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_55d8ac5d8c400d43b35c1cf03d22220b.mp4" controls></video><br> |



2. # Input and Output Parameter Description <span id="Ogb4g2TG"></span>



|**Input** |**Specific Requirements & Description** |
|---|---|
|Image |* Format: Common formats such as JPG (JPEG), PNG, JFIF; **JPG is recommended as the preferred format**<br><br>* Size: Less than 5 MB, resolution less than 4096\*4096; the clearer the input image, the better the generation effect.<br><br>* Additional Recommendation: If a speaker needs to be specified, **subject detection** must be performed first; if not, subject detection can be skipped. |
|Audio |* Duration: The duration must be less than 60 seconds. If the audio exceeds 60 seconds, an error will be generated and the generation will fail; excessive duration may lead to degraded effect) |
|Prompt (Optional) |* Supported Languages: Only Chinese, English, Japanese, Korean, Spanish (Mexican), Indonesian<br><br>* Note: Optional, used for precise control of the scene, movements, camera movements, etc. |



|**Output** |**Description** |
|---|---|
|Video<br><br> |* Format: MP4<br><br>* Resolution: **720P/1080P (default)** <br><br>* **Generation Time**: The RTF value for 1080P video is 27, and RTF value for 720P video is 23. If there is service congestion, the generation time may increase. |



3. # Service Activation <span id="U38JJTbt"></span>

   ## Steps    <span id="20URjDHH"></span>

1. **Console Operation Guide:** 

   1. BytePlus users can access the [Vision AI] console via [https://console.byteplus.com/ai](https://console.byteplus.com/ai)


<div style="text-align: center">
<img src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_eea2506cd5d345d93e53a75a5c2e784c.png" width="1908px" /></div>



2. **Obtaining AK/SK:** 

   1. BytePlus users can navigate to the AK/SK acquisition process by clicking the [Get key] button under [Obtain Secret Key] at the top of the console.


<div style="text-align: center">
<img src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_5a565788de764417de8fd9426d5c24e8.png" width="1908px" /></div>



3. **Activate the Service:** 

   1. Click [Model Plaza], locate the Omnihuman 1.0/1.5 service, and click on Omnihuman 1.0/1.5 to enter the activation process.

   2. Click [Activate Service] to enable the service automatically.


<div style="text-align: center">
<img src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_e0b4fd7b4d2e9471d3ebbe272d321b99.png" width="1908px" /></div>


<div style="text-align: center">
<img src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_5606e683926f4ed62d96a6daa4b4df05.png" width="1907px" /></div>


<div style="text-align: center">
<img src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_fc160c0ba248b3f54b5902fcb0444371.png" width="1902px" /></div>



4. **Deactivating the Service:** 

   1. Click [Overview] to access the console homepage and view all currently activated services.

   2. Find [Omnihuman 1.0] [Omnihuman 1.5], click [Close Service] under the Actions column, and confirm to deactivate the service.<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_f98f9a637da7b0c6490cad932ca2e213.png) </span>

5. **Accessing API Documentation:** 

   1. Method 1: Go to [Model Plaza], find the corresponding service, and click [Documentation] to view the documentation.

   2. Method 2: Go to [Overview], find the activated service, and click [Documentation] to view the documentation.



&nbsp;

## Pricing <span id="Gy4QoBcG"></span>


This service is billed based on the duration of the generated video.


* **Unit Price**:  0.12 USD per second

* **Concurrency Limit**: 1

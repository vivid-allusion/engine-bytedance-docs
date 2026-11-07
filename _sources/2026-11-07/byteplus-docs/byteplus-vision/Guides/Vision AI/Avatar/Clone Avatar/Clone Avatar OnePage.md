---
title: "Clone Avatar OnePage"
product: "Vision AI"
product_code: "byteplus-vision"
source: "https://docs.byteplus.com/en/docs/byteplus-vision/clone-avatar-onepage"
---

<span id="4my0F0dx"></span>
### One\-sentence description:

Empower users to clone personalized avatars with just a few steps.

<span id="0VgKtLUA"></span>
### Clone Avatar solution:

The Clone Avatar feature enables users to generate a lifelike avatar by uploading a 3\-minute training video. Through a rapid 3\-6 hour fine\-tuning process, the system creates a customized avatar character that can be driven by audio input to produce lip\-synced videos with natural mouth movements and facial expressions.

<span id="YQmsQ2Yy"></span>
# Product Introduction

Based on clone avatar technology, a single\-person video input is used to create an avatar character. By pairing the avatar with audio, an avatar speaking video with a duration of no more than 12 minutes can be produced in a single session.


1. ## Effect Demo <span id="JKQeEQP7"></span>



|<video src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_d97fbb74732d36f4d230b14760ae388a.mp4" controls></video><br><br><br> |<video src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_24974204c48ecbc243b22c74cb341695.mp4" controls></video><br><br><br> |<video src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_cf049c0aecfe7e89ef9d22075ce9dca3.mp4" controls></video><br><br><br> |<video src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_c6038a2579938e876d823e669b5dae50.mp4" controls></video><br><br><br> |
|---|---|---|---|



&nbsp;

2. ## Capability Introduction <span id="BsJZhgr7"></span>


**From the whole\-link automation level**, it has a complete process of material and processing \-\> task training \-\> inference creation. Users can upload training videos according to the instructions, and a avatar image will be returned without any additional human involvement.


* Material and processing: Convert the training data input by the user into target format and perform various verifications (such as ray, face, etc.) at the server level.

* Task Training: Execute the task of avatar image training, obtain avatar image resources, and support the management (addition, deletion, modification, and query) of image resources;

* Reasoning Creation: Supports loading generated avatar images and creating avatar videos based on audio input.

* Through optimizing the video preprocessing workflow, pre\-training the Audio2BS model, pre\-training the GAN model, and adjusting the GAN size, it is currently possible to complete the customization work for a 5\-minute video within 3\-6 hours.

* For various input behaviors that users may generate, complete the verification of limit cases, and improve the error code return mechanism according to the experimental results


**Algorithm solution:** 

The process consists of the following sequential steps:


1. Video Preprocessing

2. Audio\-Video Processing (including detecting the synchronization rate and extracting valid audio)

3. Video Processing (involving extracting video frames, face detection, keypoint detection, 3D parameter calculation, and texture modeling)

4. Train Audio2BS Model (extracting audio features and training the model)

5. GAN Model Training

6. Package Model


Each step builds on the output of the previous one, with specific sub\-tasks (e.g., synchronization rate detection in audio\-video processing, 3D parameter calculation in video processing) to refine the data for subsequent model training.


3. ## Explanation of avatar Replication Effect <span id="IIYBdQdE"></span>

* Voice Replication: Using Doubao's large speech model, it replicates voices in seconds, restoring timbre characteristics, speech style, accent, and acoustic environment. 

* Expression replication: Based on the training videos uploaded by users, replicate the facial expressions of the avatar, which will be randomly rotated during avatar video making.

* Motion Replication: Based on the training videos uploaded by users, replicate the gestures and body movements of the avatar, which will be randomly played in rotation during video making. 


<span id="XquNIs42"></span>
# How to start

Click Experience center to enter the Visual AI Console and activate the service

<span id="YVYWTTn4"></span>
# Usage Instructions


1. Upload a video to generate a Video Cloud ID

2. Free trial status: Concurrency Limit is 1

3. Official status: Concurrency Limit is 1, no charges will be incurred for now

4. Create a clone avatar character

   * Free Trial Status: In the free trial status, you cannot create new avatar avatars (you can use the test avatar provided by the official **250623\-zhibo\-linyunzhi**) 

   * Official status: Concurrency Limit is 1. For each resource package purchased, one clone avatar can be created.

5. Generate Avatar Video

* Official status: Concurrency Limit is 1, billed by video generation duration at 0.015 USD per second

3. Usage Recommendations & Billing Instructions

   * Billing will only occur when the call is successful (the generated avatar and video are returned normally). 

   * Each call to the interface outputs one video/one avatar.


 **(1) Generate clone avatar \- number of pre\-orders**


|**API** |**Billing Method **  |**Number of Calls (times)**  |**Price **  |
|---|---|---|---|
|Create a clone clone avatar character |Resource Package |1 |**300 USD** |


 **(2) Generate avatar video \- Charged based on the duration of the generated video result**


|**API** |**Billing Method **  |**Price (USD/second)**  |
|---|---|---|
|Generate clone avatar video |Charges are based on the duration of the video generation result |**0.015** |


<span id="sW7ZEumX"></span>
# Clone Avatar shooting guide


1. ## **Deliverables** <span id="8B8zPm91"></span>


<span id="zfMxblgP"></span>
### Format Requirements


|**Type** |**A 3\-5 minute video** |
|---|---|
|Video File Format |.mp4 |
|Video Resolution |Upload videos no lower than 720p; 1080P is recommended, 4K is optimal |
|Video Frame Rate |Over 25fps |
|Video Bitrate |Over 20Mbps and ≤50Mbps |
|Video File Size |≤1GB |


<span id="Y9ANtMkQ"></span>
### Recommended Examples


|**Video Quality** |**100 Points** |**80 Points** |**60 Points** |**60 Points** |**40 Points** |
|---|---|---|---|---|---|
|Video Sample |&nbsp;<br><br><video src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_ca812e0b9aa9746441b221780b422881.mp4" controls></video><br> |&nbsp;<br><br><video src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_c2663c3e80fd75e7ccb63f9d80adab43.mp4" controls></video><br> |&nbsp;<br><br><video src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_416d189e28193b7d1ed27d07fc3b8564.mov" controls></video><br><br><br> |&nbsp;<br><br><video src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_390e80a4908d5007a6b4fa633f0d8387.mp4" controls></video><br> | |
|Video Evaluation |* Stable lighting and clean background<br><br>* High video clarity<br><br>* Rich expressiveness: eyes, body language, and facial expressions are rich and coherent |* Stable lighting and clean background<br><br>* High video clarity<br><br>* Moderate expressiveness: lack of facial changes and rich body language |* Stable lighting and slightly backlit background<br><br>* High video clarity<br><br>* Moderate expressiveness: only one action and one eye movement |* Poor lighting and backlit whiteboard<br><br>* Rich expressiveness but eyes not looking at the camera |* Poor lighting and pale face<br><br>* Poor expressiveness: eyes not looking at the camera and unnatural body language |



2. ## Shooting Guide <span id="UJD1ok8Y"></span>


<span id="6YiK8l07"></span>
### Pre\-shooting Recommendations

<span id="1zT0iG0t"></span>
#### **Venue Preparation**


|**Recommended Practices** |**Negative Examples** |
|---|---|
|✅ Choose a fixed background and position |❌ Do not walk while speaking |
|✅ Choose a green screen, solid color, or clean background |❌ Avoid dark and cluttered backgrounds |
|✅ Walking avatar:<br><br><br>1. Consistent facial lighting throughout the video;<br><br>2. Steady camera movement |❌ Do not shake the frame too quickly |


<span id="8BdQ00Fz"></span>
#### **Lighting Requirements**


|**Recommended Practices** |**Negative Examples** |
|---|---|
|✅ Uniform and flicker\-free lighting; no changes in lighting during recording |❌ Do not shoot in dark or backlit environments |
|✅ Shoot with front lighting to ensure no excessive shadows on the face |❌ Avoid top lighting or backlighting |
|<div style="text-align: center"><br><img src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_f0f683f9f5a2d09900a1daf79c4443db.png" width="2304px" /><img src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_77c3c04bb8959d94486aa728b0d3355d.png" /></div><br><br><br>&nbsp;<br><br><span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_a1fc117c498b0c3821818923378278a0.png) </span> |<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_2775d244ef03da50683f5b060b3bfc37.png) </span><span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_3710c429ba749bb462095f3bbfbbb130.png) </span><br><br><span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_e9e8ab49da0a0a9721a5fdf540c7b81b.png) </span><span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_e6b59068a97dbb3c725d701a6ab7c704.png) </span> |


**Shooting Script**

You can prepare your own script; the official script below is recommended ⬇️


|**Chinese Corpus** |**English Corpus** |
|---|---|
|<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_a18c650f4d19e4f6cfb18e8e54507c2f.txt" name="Chinese voice-over script.txt">Chinese voice-over script.txt</Attachment><br> |<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_cb975e4620703c593e07855137d07b27.txt" name="English voice-over script.txt">English voice-over script.txt</Attachment><br> |


<span id="57Aqk5vi"></span>
### During\-shooting Recommendations

<span id="SZ6pqYFG"></span>
#### **Shooting Process Overview**

**First, remain silent with your mouth closed for 10 seconds, then speak the script continuously for 3\-5 minutes**


1. Silence for 10 seconds: The recording environment must remain quiet within 10 seconds, and no human voice should be heard

2. Speak the script continuously for 3\-5 minutes

3. Mistakes or pauses are allowed; skip naturally if an error occurs

4. Pause with your mouth closed for 1\-2 seconds after each sentence; do not deliberately purse or lick your lips


<span id="dUupcXRS"></span>
#### Shooting Requirements


| |**Requirements** |**Examples** |
|---|---|---|
|Image requirements<br><br> |1. Hair is neatly groomed and does not cover the face or neck<br><br>2. Sitting and standing postures are allowed (both full body and half body are acceptable) <br><br>3. Don't wear clothes of the same color as the background |<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_f67bbbd4248f25d7a1ad2dec82196711.png) </span><br><br><span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_4fb83d3e292b49e29db4ed5bf4a6505e.jpeg) </span> |
|Picture Requirements<br><br> |1. Try to keep the characters in the middle of the picture and not out of the picture |<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_aafad94d20a16566ce472018641ac288.png) </span> |
|Expressiveness Requirements |1. The head should be as level as possible, without significant rotation, and the acceptable range is within 30 degrees up, down, left, and right. <br><br>2. Keep your eyes level and looking straight ahead while recording, and don't tuck in your chin too much or be overly constrained  |<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_c23aebd953a2404ab43cc43efaa7c873.png) </span><br><br> |
||1. Do not make hand movements around the face and neck<br><br>2. Try to avoid directional movements, such as numbers<br><br>3. [⭐ Best to have] Rich expressions, rich movements, strong expressiveness, rich emotions |<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_536b29eb2e157adf68c54c30142cf365.png) </span><span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_85d8a3329c6a94b29c7d9b161c04390f.png) </span> |

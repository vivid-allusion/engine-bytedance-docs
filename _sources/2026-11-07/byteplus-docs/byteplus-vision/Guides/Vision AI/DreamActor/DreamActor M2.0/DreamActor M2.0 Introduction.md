---
title: "DreamActor M2.0 Introduction"
product: "Vision AI"
product_code: "byteplus-vision"
source: "https://docs.byteplus.com/en/docs/byteplus-vision/dreamactor-m2-0-introduction"
---

1. # **What is DreamActor M2.0** <span id="PCmX14Lf"></span>


DreamActor M2.0 is the motion control feature driven by the large model. By inputting a single image and a template video, it can drive the character in the image to replicate the **motion, facial expressions, and lip movements** from the template video, while preserving the subject and background features of the input image consistently. 

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true"><strong>DreamActor M2.0 Features</strong></div>



* <div data-tips="true" data-tips-type="warning"><strong>Input (mandatory):</strong></div>


   * <div data-tips="true" data-tips-type="warning">1 image (including 1 or multiple, human or non\-human characters)</div>


   * <div data-tips="true" data-tips-type="warning">1 template video</div>


* <div data-tips="true" data-tips-type="warning"><strong>Output:</strong></div>


   * <div data-tips="true" data-tips-type="warning">720P video with character(s) from the image and motions from the template video</div>


* <div data-tips="true" data-tips-type="warning"><strong>Exclusive Features of DreamActor M2.0 (not found in other vendors):</strong></div>


   * <div data-tips="true" data-tips-type="warning">Multi\-character driving</div>


   * <div data-tips="true" data-tips-type="warning">Non\-human character driving</div>


   * <div data-tips="true" data-tips-type="warning">SOTA pose replication and character & background preservation</div>


2. # **Features & Demos** <span id="ye2SPNBv"></span>

   1. ## General Showcase <span id="ye2SPNBv"></span>

   * **Break through the limitation of vertical screen format, and videos of various formats and proportions can be highly restored.** 

   <video src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_edf188423eec7b0a85a7cf9902f2c4e8.mov" controls></video>
   

   * **Support more styled characters**

   <video src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_5e5e209911595f7feb5639c62aea7fdc.mov" controls></video>
   

   * **Has the ability to re\-show camera movements**

      * Template video:

      <video src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_1245a943232e4a7801f3e4dfba953ba5.mp4" controls></video>
      

      * Input image:

      <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_3c9a3a3a30ad420105024b6d6d882fee.jpeg) </span>

      * Output video:

      <video src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_9c9db66dc4e9b9da069707181eacfad2.mp4" controls></video>
      

   2. ## Multi\-character Driving <span id="YnfDrjXS"></span>

   <video src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_4ab4efca98144654b4fcb7fc4cc20ff3.mp4" controls></video>
   

   3. ## Non\-human Character Driving <span id="Se4PapUe"></span>

   <video src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_f6832b5cc49444c266650451517a6a8c.mp4" controls></video>
   

   4. ## SOTA Image Elements Preservation <span id="JI2sFSXM"></span>

   <video src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_957b690c41dd6db926635d4ec732e52b.mp4" controls></video>
   

   5. ## Good Image Frame & Original Pose Preservation <span id="UwqC58Kc"></span>

   <video src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_697c28cf846c65092942e3ca54479e23.mp4" controls></video>
   



&nbsp;

3. # **Best Practices** <span id="PjJjoDOY"></span>

1. **The template video is suggested to be HD or UHD: ** To generate fine\-grained movements such as finger motions, we recommend using input videos with clear, distinct finger articulation as much as possible. For videos requiring the reproduction of subtle facial expressions, high\-quality clear input also helps increase the model's accuracy in precise reproduction.

2. **Character & camera movement shall not be too fast: ** Rapid camera movement or fast motion of the character in the template video may result in blurring. Excessive camera movement or frequent scene transitions may also affect the final output quality.

3. **The character proportions and frame dimensions of the input image are consistent with those of the video: ** The closer the body exposure ratio and pose of the character in the driving video are to those in the image, the more stable the rendering outcome will be. In addition, for scenarios requiring limb or hand motion driving, having the character’s limbs and hands fully visible in the reference image helps achieve better results.

4. **Clear character in the image and template video: ** The character in the template video must be clear with no obvious motion blur; the faces in both the image and template video should be clear and fully framed.

5. **Less occlusions: ** Keep the character facing forward as much as possible. Instability or mesh penetration may easily occur when body parts occlude each other (e.g., hands behind the back, crossed legs). Characters should ideally not hold objects, and there should be no occlusions on the face or front torso.

4. # **Input & Output Requirements** <span id="mxtIXr0i"></span>



| |<div style="text-align: center"><br><strong>Type</strong></div><br> |**Parameter** |
|---|---|---|
|<div style="text-align: center"><br><strong>Input</strong></div><br><br><br><div style="text-align: center"><br></div><br> |<div style="text-align: center"><br><strong>Image + Video</strong></div><br> |1. **Template video:** <br><br>   1. Duration: should not exceed ** 30 seconds**<br><br>   2. Format: mp4, mov, & webm<br><br>   3. Resolution: 200\*200 \- 2K (2048\*1440)<br><br>2. **Image: ** <br><br>   1. Size: less than 4.7MB<br><br>   2. Format: jpeg, jpg & png<br><br>   3. Resolution: 480\*480 \- 1920\*1080 (anything larger will be proportionally reduced)<br><br>3. It supports both facial expressions and body movement driving, and can handle full\-body, half\-body, or portrait driving:<br><br>* Driving source: Video (supports real people, animation, pets).<br><br>* Driving range: Full face + body.<br><br>* Image supports driving for real people, animation, pets, etc.; overly abstract subjects may fail to generate. |
|<div style="text-align: center"><br><strong>Output</strong></div><br> |<div style="text-align: center"><br><strong>Video</strong></div><br> |1. The output video will be the image video after driving. The aspect ratio of the output video will aim to closely match the input image, but may not be identical.<br><br>2. The RTF (Real\-Time Factor) is about 18, meaning generating a 10\-second video will take approximately 180 seconds. Processing time may increase during peak service times.<br><br>3. The output video format is mp4, with a resolution of 720P and 25fps. |



5. # **Service Activation and Pricing** <span id="dwRiGCAo"></span>


<span id="pvGS3cxY"></span>
## Service Activation

You can go to Vision AI console to activate the service and collect ak/sk. https://console.byteplus.com/ai/overview

<span id="ooZ8nwyr"></span>
## Pricing

0.05 USD/second with 1 concurrency

---
title: "Smart Editor Prompt Guide"
product: "BytePlus Kickart"
product_code: "kickart"
source: "https://docs.byteplus.com/en/docs/kickart/Smart_editor_users_guide"
---

&nbsp;

<span id=""></span>
# 1. Creation Pipeline Overview

Follow this workflow: prepare source images → generate video clips → refine and assemble the final video.


1. **Prepare source images** (AI\-generated, uploaded from your device, or imported from your space): use them to establish consistent product and character references for video generation.

2. **Generate video clips**: write a prompt to animate the image and generate one 5–15\-second clip at a time.

3. **Refine the final cut**: if a result is unsatisfactory, regenerate it with a revised image or prompt. Use Erase Subtitles to correct subtitle issues, then use Compose Video to combine and export multiple clips.



|**Step** |**Where to start** |
|---|---|
|**1. Prepare source images** |Generate or upload product, character, and environment images to use as video references.<br><br><span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260915115440-862615270703.png) </span> |
|**2. Generate video clips** |Open the Video Clip tab at the bottom of the editor. Enter a prompt, then use @ to attach reference images.<br><br><span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260915115631-1166935729740.png) </span> |
|**3. Append a clip** |Right\-click an existing clip and select Add clip.<br><br><span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260915115701-632838744046.png) </span> |
|**4. Refine** |Right\-click a clip and select Erase subtitles, Add subtitles, or Delete clip.<br><br><span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260915115733-617311026908.png) </span> |
|**5. Compose and export** |Select Compose Video in the top\-right corner.<br><br><span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260915115808-1089102232564.png) </span><br><br> |


&nbsp;

<span id=""></span>
# 2. Preparing Source Images

Text\-to\-video alone provides limited control over product appearance and character likeness. Generate a high\-quality reference image first, then animate it to improve product consistency and preserve character identity throughout the video.

<span id=""></span>
## 2.1 Source image requirements


|**Principle** |**Description** |
|---|---|
|**Make the product the primary subject** |<div style="text-align: center"><br>The product should occupy at least 50% of the image so it remains prominent against the background.</div><br><br><br><div style="text-align: center"><br><img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260915115153-1227424245720.jpeg" width="213px" /></div><br> |
|**Provide an additional headshot for each person** |When a real person appears in the video, provide a separately cropped facial close\-up as an independent reference in addition to the full\-body or waist\-up image. This helps prevent identity drift.<br><br><div style="text-align: center"><br><img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260915115321-668563241993.png" width="259px" /></div><br> |
|**Keep the background clean** |Use a solid\-color background or a simple environment. Busy backgrounds can reduce subject consistency in the generated video.<br><br><div style="text-align: center"><br><img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260915115155-529806035328.png" width="171px" /></div><br> |


<span id=""></span>
## 2.2 Writing image prompts

**Image generation formula =**  Image quality + Subject features + Scene/background + Composition and shot type + Style and mood + Lighting and tone + Intended use


|**Scenario** |**Prompt** |**Example** |
|---|---|---|
|**Beauty product image**<br><br>Use this image to establish the visual style of a brand commercial. | **[Image quality]**  high\-quality commercial photography,  **[Subject features]**  a serum bottle centered in the frame and covered with fine water droplets,  **[Scene/background]**  placed on a countertop with a few rose petals nearby against a light\-pink gradient background,  **[Composition and shot type]**  product close\-up, 9:16 vertical,  **[Style and mood]**  minimalist and premium,  **[Lighting and tone]**  soft studio side lighting,  **[Intended use]**  first\-frame reference for a beauty brand commercial. |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260915115256-632241770596.png) </span> |
|**Apparel model image**<br><br>Use this image as a character reference for narrative product\-promotion videos. | **[Image quality]**  4K commercial photography,  **[Subject features]**  a young Asian woman with long straight hair and light makeup, wearing an oversized beige blazer over a white T\-shirt, smiling confidently,  **[Scene/background]**  standing at the entrance of a coffee shop on a city street corner,  **[Composition and shot type]**  full\-body shot, 9:16 vertical,  **[Style and mood]**  natural street\-photography aesthetic,  **[Lighting and tone]**  natural side lighting for a clean, airy look,  **[Intended use]**  character reference for an outfit\-focused narrative product\-promotion video. |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260915115238-335664061148.png) </span> |
|**Presenter image**<br><br>Use this image as a character reference for presenter\-led product videos. | **[Image quality]**  4K commercial photography,  **[Subject features]**  a fair\-skinned 25\-year\-old Chinese woman wearing a facial\-cleansing headband and holding a white facial cleanser,  **[Scene/background]**  standing in a natural\-looking bathroom, preparing to wash her face,  **[Composition and shot type]**  waist\-up shot, 9:16 vertical,  **[Style and mood]**  clean, fresh, and approachable,  **[Lighting and tone]**  soft natural light and an overall bright look,  **[Intended use]**  character reference for a presenter\-led product video.<br><br> |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260915115243-58499278122.png) </span> |


<span id=""></span>
## 2.3 Image editing prompts

**Image editing formula =**  Edit action + Target + Desired result


|**Scenario** |**Prompt** |**Example** |
|---|---|---|
|**Change the image background**<br><br>Convert a street photograph into an indoor studio image. | **[Edit action]**  replace  **[Target]**  the background with  **[Desired result]**  a light\-pink gradient background; keep the serum bottle unchanged, place it on a reflective, glossy countertop, scatter a few rose petals around it, and add soft overhead studio lighting for a premium commercial\-photography aesthetic.<br><br> |Before <br><br><span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260915115245-1411272949218.png) </span><br><br>👉 After<br><br><span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260915115302-1480617926608.png) </span><br><br> |


<span id=""></span>
# 3. Video Prompts

<span id=""></span>
## 3.1 Seedance 2.5 series


|**Mode** |**Suitable for** |**Not suitable for** |
|---|---|---|
|**Universal reference** |Creating a video from multiple assets while linking the character, product, and environment to separate references. |Making a single adjustment to an existing source clip. |
|**Video editing** |Preserving the source clip while replacing a specific object or its audio. |Changing camera movement, pacing, duration, or aspect ratio. |
|**Video extension** |Adding footage before or after the source clip. |Starting a new storyline or changing the environment or subject. |



1. ### General approach <span id=""></span>


**Prompt formula =**  [Asset description] + [One\-sentence summary] + [Specific scenes] + [Global notes]


* **Asset description**: define the purpose of each asset in upload order. Omit this section when no assets are provided.

   * Sentence pattern: Use @Asset N as the reference for <subject\>—specifically, <attributes\>; do not carry over <excluded content\>.

* **One\-sentence summary**: subject + location + event + genre/style + distinctive camera movement.

* **Specific scenes**: describe the visuals, camera movement, actions, dialogue, and sound effects for each time segment. Limit each five\-second segment to one primary action.

* **Global notes**: place this section at the end. Specify the number of subjects, logo orientation, camera position, and lighting, and list any elements that must not appear in the video.


To reproduce the sample outputs, keep any prompt that includes spoken Chinese in Chinese. Translating the prompt or dialogue may change the generated video.

**Full example: presenter\-led beauty product video**

Assets: front\-facing, waist\-up presenter image ×1, lipstick product image ×1, 15\-second presenter voice reference audio.

```JSON
[Asset description]
@Image1 is used for the female presenter's face, hairstyle, and makeup, do not use the image background or clothing.
@Image2 is used for this lipstick's tube color, metallic logo, and bullet shade, do not use the original white background.
@Audio1 is used for the female presenter's voice.

[One-sentence summary]
The female presenter demonstrates and recommends this lipstick at a warmly lit vanity; beauty product-promotion video; fixed camera; close-up.

[Specific scenes]
0-2s: she holds the lipstick tube toward the camera with her left hand and twists up the lipstick with her right hand, {这个色号黄皮也压得住}.
2-4s: she lowers her gaze and applies one layer to her lips; the camera pushes in to a lip close-up; <the faint sound of the lipstick gliding across her lips>.
4-5s: she looks into the camera, presses her lips together, and smiles.

[Global notes]
No subtitles. Do not generate background music.
```


&nbsp;


&nbsp;

2. ### Breakdown by function <span id=""></span>


<span id=""></span>
##### Universal reference

Universal reference supports multimodal inputs. Images, videos, and audio can all serve as reference assets. Use it for scenarios such as:


* Matching a character to a specific face.

* Matching a presenter to a specific recorded voice.

* Creating a ready\-to\-publish presenter\-led video from a single product image.

* Reusing the camera movement and pacing of a reference video with a different product.


**Suitable for**


* Assigning the subject, action, and voice to separate assets.

* Combining character, product, and environment references across assets.

* Replicating the camera movement and pacing of a reference video.


**Not suitable for**


* Combining too many subjects in a single image.

* Relying on the model to infer the purpose of each asset.

* Using assets with significantly different visual styles.


&nbsp;

**Universal reference formula**

**<ins>Asset description:</ins>** 

@Image1 is used for <the person\>'s <face and hairstyle\>, do not use <the image background and clothing\>.

@Image2 is used for <the product\>'s <shape, material, and logo\>, do not use <the original background\>.

@Audio1 is used for <the person\>'s voice.

**<ins>One\-sentence summary:</ins>** 

<The person\> <does what\> in <the scene\>, <genre/style\>, <camera position and shot type\>.

**<ins>Specific scenes:</ins>** 

0\-2s: <visuals and action\>, {Chinese dialogue, no more than 15 characters}.

2\-5s: <visuals and action\>, <sound effect\>.

**<ins>Global notes:</ins>** 

No subtitles.

&nbsp;

**Video examples**


|**Use case** |**Input assets** |**Input prompt** |**Output result** |
|---|---|---|---|
|Creating a presenter\-led product video from character and product images.<br><br> |Multi\-angle character reference ×1 (front and side)<br><br>Product image ×1 (held outdoors with the flip\-top lid open)<br><br>Product opening detail image ×1 (stainless\-steel liner visible)<br><br>15\-second presenter voice reference audio (remove the @Audio1 line if unavailable)<br><br><span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260915115302-412012600956.png) </span><br><br><span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260915115215-1510589605803.jpeg) </span><span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260915115207-1254010552316.jpeg) </span><br><br> |@Image1 is used for the female presenter's face, hairstyle, and skin tone; the front and side views are multi\-angle references of the same person; do not use the image background or the white top.<br><br>@Image2 is used for the insulated cup's body color, texture, side handle design, and flip\-top lid design; do not use the folding table, chairs, or floor in the image.<br><br>@Image3 is used as the reference for the metallic reflections on the cup's inner rim and stainless\-steel liner; do not use the background.<br><br>@Audio1 is used for the female presenter's voice.<br><br>At an outdoor campsite, the female presenter stands beside a folding table, holds the gray\-blue insulated cup, and presents the product directly to the camera; live\-action style; natural daylight; fixed camera; waist\-up shot.<br><br>0\-2s: she raises the cup of water to chest height, faces the camera, and smiles, {露营一整天就靠这一杯}.<br><br>2\-4s: referencing @Image2, she opens the flip\-top lid with one hand; steam rises from the cup opening as the camera slowly pushes in, <the soft click of the flip\-top lid opening\>, {早上装的水现在还烫}.<br><br>4\-5s: she unscrews the lid and tilts the cup slightly toward the camera to show the liner and water, referencing @Image3, while the camera tilts down slightly.<br><br>Show only one person and one insulated cup throughout; the cup's body color and handle design match @Image2 exactly; keep the outdoor camping environment; no subtitles. |<video src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260915120027-1573877203586.mp4" controls></video><br><br><br> |
|Creating a brand\-commercial\-quality ad from a single product image. |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260915115206-752213298814.png) </span> |@Image1 is used for the perfume bottle's shape, translucent blue glass texture, black cap, and the blue flower label on the front; do not use the original background.<br><br>A translucent blue glass perfume bottle is displayed on a dark stone countertop in a premium brand commercial; slow lateral tracking shot; hard rim lighting.<br><br>0\-2s: the camera tracks left to right along the countertop; a beam of hard light strikes the blue bottle, casting a blue highlight on the countertop.<br><br>2\-4s: the camera slowly rises to a high\-angle view of the black cap; a wisp of mist drifts from the bottle mouth.<br><br>4\-5s: the camera lowers and holds on the front label; the image fades to black.<br><br>A single low string note plays in the background. The video contains only one perfume bottle, with no person or hands; the bottle color and label pattern match @Image1 exactly; no subtitles.<br><br> |<video src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260915120058-1278149572627.mp4" controls></video><br><br><br> |


<span id=""></span>
##### Video editing

Video editing preserves the source clip's camera movement and pacing while replacing a single element in the frame. Use it for scenarios such as:


* Replacing the model in a proven clip to create a new version.

* Replacing the background to adapt a clip for a different audience.

* Replacing the product in an existing clip after a new SKU launches.

* Removing auto\-generated subtitles and background music, then adding a new voice\-over.


**Suitable for**


* Swapping the person, background, or product.

* Removing subtitle overlays or background music while preserving the voice.

* Correcting continuity errors.


**Not suitable for**


* Changing camera movement or pacing.

* Changing duration or aspect ratio.

* Substantially changing the frame layout or composition.


&nbsp;

**Video editing formula**

**<ins>Asset description:</ins>** 

@Video1 is the master clip; preserve its camera movement, pacing, duration, and composition.

@Image1 is used for <the new object\>'s <appearance/material\>, do not use <the image background\>.

**<ins>One\-sentence summary:</ins>** 

Replace <the original object\> in the frame with <the new object\>; everything else in the frame stays unchanged.

**<ins>Specific scenes:</ins>** 

<The new object\> inherits <the original object\>'s on\-screen timing, position, motion path, occlusion, and exit time.

**<ins>Global notes:</ins>** 

Do not change the camera movement, duration, or framing; do not add or remove other elements.

&nbsp;

Unlike the general formula, do not divide [Specific scenes] into time\-coded segments. The master clip determines the pacing, so describe only how the new object follows the original object's timeline.

&nbsp;

**Video examples**


|**Use case** |**Input assets** |**Input prompt** |**Output result** |
|---|---|---|---|
|Replacing the person in an existing clip with a more suitable model. |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260915115312-1683918069878.png) </span><br><br>&nbsp;<br><br><video src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260915120149-386854816166.mp4" controls></video><br><br><br> |@Video1: preserve its camera movement, pacing, duration, and composition.<br><br>@Image1 is used for the new model's face, hairstyle, and clothing; do not use the image background.<br><br>Replace the original female model in the frame with the female model in @Image1; everything else in the frame stays unchanged.<br><br>The new model inherits the original model's on\-screen timing, standing position, hand\-motion path, occlusion with the product, and exit time; lip movements remain synchronized with the original speech.<br><br>Do not change the camera movement, duration, or framing; do not add or remove any other element.<br><br> |<video src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260915120207-1040189201579.mp4" controls></video><br><br><br> |
|Replacing the background of an existing clip to show a different use environment. |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260915115318-1664882643279.png) </span><br><br> |@Video1 is the master clip; preserve its camera movement, pacing, duration, and composition.<br><br>Replace the background with a bus interior; keep the person and product unchanged.<br><br>Match the person's lighting to the new background.<br><br>Do not change the duration or frame; do not add people or products.<br><br> |<video src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260915120228-537428056390.mp4" controls></video><br><br><br> |


<span id=""></span>
##### Video extension

Video extension adds footage before or after an existing clip while maintaining continuity. Use it for scenarios such as:


* Adding a closing action, such as setting the product down, when the clip ends abruptly.

* Adding an opening shot in which the person enters the frame before speaking.

* Extending a five\-second clip to meet an eight\-second ad placement requirement.


**Suitable for**


* Adding a 3–5\-second closing action.

* Adding a lead\-in shot at the beginning.

* Continuing the same action from the final frame.


**Not suitable for**


* Starting a new storyline in the extended segment.

* Changing the scene or the subject.

* Substantially changing the visual language.


&nbsp;

**Video extension formula**

**<ins>Asset description:</ins>** 

@Video1 is the original clip to extend. Use it as the reference for the subject, clothing, product, environment, lighting, visual style, and pacing in the extended segment.

If an image is also uploaded, add one line: @Image1 is used for <the new prop\>'s <shape and material\>, do not use <the image background\>.

**<ins>One\-sentence summary:</ins>** 

Continue <N\> seconds after @Video1 (to add before it instead, write: add <N\> seconds before @Video1). Match the first frame of the extended segment exactly to the final frame of the original clip: <subject pose + prop position + camera framing + lighting + sound state\>.

**<ins>Specific scenes:</ins>** 

Describe what happens next: <one action per 3–5 seconds\>.

**<ins>Global notes:</ins>** 

Within the extended segment, keep <subject appearance/clothing/product/scene/shot type\> unchanged; do not introduce new people or objects.

Unlike the general formula, [Asset description] specifies only what the original clip provides. State the extension length and transition details in [One\-sentence summary].

**Video examples**


|**Use case** |**Input assets** |**Input prompt** |**Output result** |
|---|---|---|---|
|Extending a clip to add presenter dialogue.<br><br> |<video src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260915120248-645800841805.mp4" controls></video><br><br><br> |@Video1 is the original clip to be extended; the extended segment's person, clothing, product, scene, and lighting are all based on it.<br><br>Use the final frame of @Video1 as the first frame of the extended segment, then continue for 3 seconds: she holds the cup body upright, screws the lid back on, looks up at the camera, and smiles, {露营带它一个就够}.<br><br>Within the extended segment, keep the person's face, white top, the insulated cup's gray\-blue body and side handle design, the camping background, and the waist\-up shot unchanged; use the same speaker's voice as in the original clip; do not introduce new people or objects; no subtitles.<br><br>End the video by holding on her as she smiles at the camera, with the insulated cup upright on the table and facing the camera. |<video src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260915120300-669746867886.mp4" controls></video><br><br><br> |


&nbsp;

&nbsp;

&nbsp;

<span id=""></span>
## 3.2 Seedance 2.0 series (mini/fast/pro)


1. ### General formula <span id=""></span>


**Video generation formula =**  Reference subject + Video type/goal + Camera movement + Subject action + Environment + Dialogue/audio + Consistency constraints

Emphasize different details for each video type:


* **Brand commercial**: provide more detail about camera movement, visual style, and mood.

* **Narrative**: cite multiple reference images and identify the reference for each subject.

* **Presenter\-led video**: keep spoken lines in Chinese, preferably within 15 Chinese characters, and describe the vocal tone.



&nbsp;

2. ### By video type <span id=""></span>


<span id=""></span>
##### Brand commercial videos

Brand commercial videos emphasize cinematic camera movement and high visual quality. They typically rely on visuals and background music rather than spoken dialogue. Describe the camera movement and environment in detail.


|**Scenario** |**Prompt (with formula labels)**  |**Example** |
|---|---|---|
|**Beauty serum**<br><br>Product texture detail | **[Reference subject]**  the rose\-gold serum bottle in reference image 1,  **[Video type]**  generate a brand commercial.  **[Camera movement]**  the camera slowly orbits from a front view to a 45\-degree angle, then pushes in to a close\-up of the bottle mouth.  **[Subject action]**  water droplets slide down the bottle, and a drop of serum stretches into a thin strand from the pump.  **[Environment]**  a dark gradient background with a faint glowing water reflection at the bottom.  **[Dialogue/audio]**  background music: an ethereal electronic soundscape.  **[Consistency constraints]**  keep the bottle's appearance, material, and proportions strictly consistent; do not add unrelated elements; do not generate subtitles or watermarks. |<video src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260915120327-1744766731329.mp4" controls></video><br><br><br> |
|**Consumer electronics: headphones**<br><br>Futuristic floating display | **[Reference subject]**  the white wireless headphones in reference image 1,  **[Video type]**  generate a brand commercial.  **[Camera movement]**  the camera slowly pushes in from the side to a close\-up of the ear\-cup interior, then pulls back to a wide shot.  **[Subject action]**  the headphones slowly complete one full rotation to show the metal hinge detail, as a blue futuristic glow travels along the edges.  **[Environment]**  a dark\-gray gradient background.  **[Dialogue/audio]**  background music: low\-frequency electronic beat.  **[Consistency constraints]**  keep the headphones' appearance and material strictly consistent; do not add unrelated elements; do not generate subtitles or watermarks. |<video src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260915120334-466582960441.mp4" controls></video><br> |


&nbsp;

<span id=""></span>
##### Narrative videos

Narrative videos feature interactions among characters, products, and environments. They typically use multiple reference images. Cite both the face and product references, and identify each subject explicitly every time.

**Key rules for multi\-subject reference:** 


* Character reference: crop the face into a separate close\-up reference image and cite it first.

* Product reference: use a separate product image rather than combining it with the character image.

* Identify each subject by its full reference every time, for example "the woman in image 1" and "the serum in image 2".

* End the prompt with: Do not duplicate any character in the video.



|**Scenario** |**Input images** |**Prompt** |**Example** |
|---|---|---|---|
|**Wuxia inn confrontation**<br><br>Two\-character confrontation |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260915115250-1462119011980.png) </span><br><br><span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260915115324-1623903387595.png) </span><br><br><span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260915115225-1017922422849.png) </span> |> Storyboard 1 is shown below. Use the same structure for the remaining storyboards.<br><br><br> **[Reference subject]**  the young woman in reference image 1 and the young man in image 2,  **[Video type]**  generate a short period drama.  **[Camera movement]**  the camera remains fixed in a wide shot.  **[Subject action]**  the young man in image 2 slams the table with his right hand and draws his sword, with an angry expression, loudly demanding the antidote from the young woman in image 1, who sits calmly nearby.  **[Environment]**  the lobby of a traditional wuxia\-style inn with a timber interior, a long staircase, red silk banners, and calligraphy signage; warm lighting.  **[Dialogue/audio]**  spoken dialogue in the young man's voice (line: 交出解药！).  **[Consistency constraints]**  keep the facial features and outfits of the young woman in image 1 and the young man in image 2 consistent; do not generate subtitles or watermarks.<br><br> |<video src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260915120408-1712032324218.mp4" controls></video><br><br><br> |


&nbsp;

<span id=""></span>
##### Presenter\-led product videos

Presenter\-led product videos require precise control of the spoken script. Line length, vocal tone, and timing directly affect the result. Use a mostly fixed medium shot with subtle camera movement, emphasizing facial expressions and product presentation.

**Guidelines for effective dialogue:** 


* For the most reliable results, keep each Chinese line within 15 characters and never exceed 30 Chinese characters.

* Avoid mixing Chinese and English, rare words, and technical jargon.

* Describe the vocal tone, for example: "Use a gentle, warm young woman's voice."

* Have the presenter handle or display the product while speaking instead of keeping both hands still.



|**Scenario** |**Input images** |**Prompt (with formula labels)**  |**Example** |
|---|---|---|---|
|**Beauty sunscreen**<br><br>Product texture demonstration |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260915115243-969051592138.png) </span><br><br><span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260915115318-942721193783.png) </span> | **[Reference subject]**  the young woman in reference image 1 and the sunscreen in image 2.  **[Video type]**  Generate a presenter\-led product video.  **[Camera movement]**  Keep a stable medium shot from the waist up.  **[Subject action]**  The woman in image 1 raises the sunscreen from image 2 in her right hand, then squeezes a small amount onto the back of her left hand to demonstrate its lightweight texture.  **[Environment]**  Bright floor\-to\-ceiling windows with sunlight streaming in.  **[Dialogue/audio]**  She smiles at the camera and speaks in a confident, upbeat tone (line: 这支防晒超轻薄完全不搓泥).  **[Consistency constraints]**  Keep the facial features of the person in image 1 and the product appearance in image 2 consistent. Do not add unrelated elements, subtitles, or watermarks.<br><br> |<video src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260915120445-1297586095108.mp4" controls></video><br><br><br> |
|**Snack recommendation**<br><br>Taste\-test reaction<br><br> |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260915115220-1013432298378.png) </span><br><br><span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260915115242-87237156183.png) </span> | **[Reference subject]**  the young woman in reference image 1 and the bag of mixed nuts in image 2.  **[Video type]**  Generate a presenter\-led product video.  **[Camera movement]**  Keep a stable medium shot from the waist up.  **[Subject action]**  The woman in image 1 opens the bag from image 2, pours some nuts into her palm to show them, then eats one and looks satisfied.  **[Environment]**  A warm\-toned living room beside a sofa.  **[Dialogue/audio]**  She smiles and speaks in a relaxed, cheerful tone (line: 一口一个停不下来真的太香了).  **[Consistency constraints]**  Keep the facial features of the person in image 1 and the packaging appearance in image 2 consistent. Do not add unrelated elements, subtitles, or watermarks.<br><br> |<video src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260915120454-1196394523036.mp4" controls></video><br><br><br> |

---
title: "Ad Variations Prompt Guide"
product: "BytePlus Kickart"
product_code: "kickart"
source: "https://docs.byteplus.com/en/docs/kickart/AdVariations"
---

This guide answers three questions: 


* which model to pick — what's improved in Seedance 2.5 vs. 2.0; 

* how well your category performs; 

* how to feed inputs for the best results.



---



<span id="KEO2WvQc"></span>
## 1. Model Selection: Use Seedance 2.5

For structural imitation, **Seedance 2.5** is the default recommendation. Under matched tests (same batch of hit reference videos + same batch of product images), 2.5 delivers clearly perceivable gains over 2.0.

<span id="02qouwUR"></span>
### 1.1 Where 2.5 Beats 2.0


|**Improvement** |**What users will notice** |
|---|---|
|Cleaner, sharper visuals |Higher\-definition output, fewer blurry surfaces and color artifacts, higher usable rate |
|More accurate product restoration |Product shape, logo, and packaging text closer to the real item — fewer "wrong\-item" cases |
|More stable text and captions |Noticeably fewer double subtitles and garbled text, closer to final\-quality output |



---



<span id="IJsft6Pb"></span>
## 2. Category Tips

General rule: categories with **tidy packaging and intuitive selling points** restore better; **complex structures, special materials, or text\-dense packaging** are harder.


|**Category** |**Tips & cautions** |
|---|---|
|Apparel & Bags |On\-model and single\-item restoration is stable; upload a clean single\-item shot and a clear on\-model shot separately |
|Food & Beverage |Overall solid, but dense packaging text can break — keep on\-screen text minimal |
|Health Supplements |Specialized terms (ingredient names, tablet types) are often mispronounced; keep product names spelled consistently |
|Beauty & Personal Care |Product consistency and motion are the weak spots; add multi\-angle shots and texture close\-ups |
|Home & Daily Use |Product consistency is on the lower side; provide multi\-angle and in\-use shots |
|3C & Electronics |Complex structures, metallic/transparent materials — the hardest category; preserve body details carefully |



---



<span id="JPN7Vsjd"></span>
## 3. Best Input Setup: How to Feed Images

Results depend heavily on input quality. Based on matched A/B tests, inputs split into three types with clear preferences.

**Headline rule**: prefer **white\-background shots** for stability; use **real\-shot photos / reference videos** when you want authentic texture; **avoid** marketing images loaded with special effects and text. All inputs must be clear, multi\-angle, 720P or higher, and free of dense small text.

<span id="9PDm9s1c"></span>
### 3.1 Human Reference Images


* Use frontal, unobstructed shots with the full face visible

* Use a clean background; avoid multiple people in one frame

* To convey a full outfit, add a clear half\-body or full\-body shot

* Human reference images are only used as replacement material — no need to number them in the prompt

* If a specific real person is featured, besides the full\-/half\-body shot, crop a separate face close\-up as an independent reference to prevent identity drift


<div style="text-align: center">
<img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20261012064007-571873152051.png" width="2560px" /></div>


<span id="8CLVgeab"></span>
### 3.2 Product Reference Images

**Recommended: white\-background shots**


* Prefer white or clean backgrounds

* Provide multiple angles: front, side, back

* Keep shape, color, logo, and packaging text clear

* Only one SKU per product reference set

* For handheld or wearable items, include shots that convey realistic scale



|<div style="text-align: center"><br><strong>Multi\-angle references (front/side/back/detail) help restore shape and spatial features</strong></div><br> |||||
|---|---|---|---|---|
|<div style="text-align: center"><br><img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20261012064005-758235357567.png" width="959px" /></div><br><br><br><div style="text-align: center"><br></div><br> |<div style="text-align: center"><br><img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20261012064007-949801877255.png" width="3000px" /></div><br> |<div style="text-align: center"><br><img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20261012064006-1790377040811.png" width="959px" /></div><br> |<div style="text-align: center"><br><img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20261012064006-574567267094.png" width="3000px" /></div><br> |<div style="text-align: center"><br><img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20261012064006-1542538916804.png" width="2048px" /></div><br> |


**Also recommended: real\-shot photos / reference videos**


* Reference videos capture more authentic appearance and in\-use states, with a slight edge in product consistency

* Prefer single\-scene, single\-person (or no\-person), continuously shot videos within 1 minute



|<div style="text-align: center"><br><strong>Real\-shot photos must have a clear main subject with distinguishable details</strong></div><br> ||
|---|---|
|<div style="text-align: center"><br><img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20261012064006-154918115127.png" width="853px" /></div><br><br><br> |<div style="text-align: center"><br><img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20261012064005-1482611241849.png" width="800px" /></div><br> |


**Not recommended:** 


* Marketing images with heavy decorative text, effects, or spec callouts — the model will "learn" those overlays into the output, causing broken text, double subtitles, and distorted graphics

* Remove size charts, feature callouts, and marketing copy; keep only the primary brand logo and product name



| ** Example** ||
|---|---|
|<div style="text-align: center"><br><img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20261012064007-1610280955744.png" width="1024px" />text appears blurry</div><br><br><br> |<div style="text-align: center"><br><img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20261012064007-56640614259.png" width="1024px" />small text is garbled and unreadable</div><br> |


<span id="pGnkH7Iy"></span>
### 3.3 Scene Reference Images

Example prompt: *Replace the office in the video with a bright home living room.* 


* Use a single, complete scene with no people blocking the view

* Keep the shooting angle close to the original video

* Leave enough room in the main subject area

* Match the lighting direction and brightness of the original

* Keep spatial structure clear to support later composition and product placement


<div style="text-align: center">
<img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20261012064007-450757665535.png" width="367px" /></div>



---



<span id="YTBv1rnJ"></span>
## 4. Strong Interaction: Driving Variations with User Prompts

Structural imitation lets you go beyond 1:1 replication: with a single User Prompt, you can change key elements of the video to produce differentiated, "one\-shot\-per\-user" variations, avoiding duplication tags and improving first\-publish odds.

**One\-line idea**: Replication = keep the original; variation = replication + a User Prompt that rewrites key elements. The more specific the rewrite, the more differentiated — and the less likely to collide with other creators.

<span id="Q2R5AzJB"></span>
### Three High\-Frequency Interaction Types

The three most useful User Prompt types are **Role swap**, **Location swap**, and **Voice\-over constraint**. Follow the pattern  **"target object + specific requirements"**  — the more specific, the better.


|<div style="text-align: center"><br><strong>Type</strong></div><br> |<div style="text-align: center"><br><strong>What it does</strong></div><br> |<div style="text-align: center"><br><strong>How to write it</strong></div><br> |<div style="text-align: center"><br><strong>Example</strong></div><br> |
|---|---|---|---|
|Role swap |Changes the on\-camera person's gender, age, or persona for differentiation |Specify the role to change and the target persona (gender / age / identity). Richer personas (identity + region + emotion + context) give stronger differentiation. For multi\-person videos (max 3 recommended), you can target a single role individually. |"Replace the host with a man around 30, home\-chef persona." / "Change the on\-camera person to a professional fashion buyer running her own studio in Guangzhou." |
|Location swap |Changes the setting — venue, decor, lighting/time, indoor/outdoor |First classify the original scene type (home / office / social), then adjust decor, props, lighting/time, indoor\-outdoor, camera or model movement. More changes mean richer variation and clearer differentiation. |"Change the scene to a bright home living room, add plants and a shelf in the background." / "Switch to a storefront reception with the brand name on the backdrop, warm lighting." |
|Voice\-over constraint |Constrains opening lines, price/promo info, or the entire script |Use a User Prompt to lock the opening hook, swap price/promo details, or fully rewrite the script. Techniques like "paraphrase" or "my own story" help differentiate copy while keeping the hit's hook. |"The voice\-over must start with 'I haven't bought new clothes in three years.'" / "Change the price to the group\-buy price of 99 yuan." / "Change the promo to buy\-7\-get\-1\-free." |

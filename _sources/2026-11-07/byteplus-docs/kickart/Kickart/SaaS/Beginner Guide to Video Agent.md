---
title: "Beginner Guide to Video Agent"
product: "BytePlus Kickart"
product_code: "kickart"
source: "https://docs.byteplus.com/en/docs/kickart/GettingStartedGuide"
---

<span id="zBnd9yCy"></span>
# Feature Overview

Quick overview of core features:


1. Material understanding: AI "understands products," deeply analyzes captured product information or the materials you upload, automatically extracts structured selling points, identifies the main body of the product, evaluates image quality and provides optimization suggestions, and supports manual supplementary adjustments.

2. Storyboard: Generates shot\-by\-shot scripts and product/character/scene reference images; supports image replacement and dialogue modification.

3. Video generation: Automatically synthesizes the final video. After generation, the feature supports preview, download, and direct publishing. The exported video can also be imported into the smart editor for fine\-tuned secondary editing.


<span id="XK710Hj3"></span>
# A Practical guide for materials


1. How to upload product media assets

   1. Best input 

      1. Solid colors and clean base maps; no redundant fonts.

      2. Images show the product from different angles and forms (for example, the reference sample covers side, front, and bottom views).

      3. The picture is clear and above 720P.



<columns>
<columnsItem zoneid="PENXAihoMs">

<div style="text-align: center">
<img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260612105400-291967234463.png" width="959px" /></div>


</columnsItem>
<columnsItem zoneid="dwi6LNVLRC">

<div style="text-align: center">
<img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260612105412-522147216653.png" width="3000px" /></div>


</columnsItem>
<columnsItem zoneid="XYaEbBOtx3">

<div style="text-align: center">
<img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260612105419-437402808513.png" width="959px" /></div>


</columnsItem>
<columnsItem zoneid="UQClXsN2qq">

<div style="text-align: center">
<img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260612105428-630870204266.png" width="3000px" /></div>




</columnsItem>
<columnsItem zoneid="eJCetnBzTS">

<div style="text-align: center">
</div>


<div style="text-align: center">
<img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260612105447-28557841685.png" width="2048px" /></div>


</columnsItem>
</columns>



   2. Not recommended input

         Lacking product information

         1. Typical scenario 1: Gift\-boxed products require promotional shooting; their packaging is exquisite and suitable for gifting, plus the inner contents of the gift box.



<columns>
<columnsItem zoneid="qpmDBVrjqL">

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260612105529-118349593681.png) </span>❌When there are few input images, there are only boxed product images, and the model cannot clearly understand the internal product style, making it easy to "make random decisions".

</columnsItem>
<columnsItem zoneid="nhbBbUpynv">

<div style="text-align: center">
<img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260612105828-1219719018980.png" width="312px" /></div>


✅Product outer packaging, product interior, and food cross\-section information are all provided.

</columnsItem>
</columns>



         2. Typical Scenario 2: The complete picture of the product is missing



<columns>
<columnsItem zoneid="UepyUX5V23">

<div style="text-align: center">
<img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260612110212-858514739111.png" width="170px" /></div>


<div style="text-align: center">
❌Can’t see the effect of the product on the body.</div>


</columnsItem>
<columnsItem zoneid="y1UqIf9HGo">

<div style="text-align: center">
<img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260612105937-1673830570975.png" width="182px" /></div>


<div style="text-align: center">
✅The whole picture of the product is clear; the background is clean, and there are no redundant fonts.</div>


</columnsItem>
<columnsItem zoneid="mV5SEXX4Ay">

<div style="text-align: center">
<img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260612105944-196969491966.png" width="140px" /></div>


<div style="text-align: center">
❌Can’t see the shape of the bottle mouth.</div>


</columnsItem>
<columnsItem zoneid="A9X18Zxsj3">

<div style="text-align: center">
<img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260612105948-1652986657229.png" width="212px" /></div>


<div style="text-align: center">
✅Includes details: bottle mouth shape, product texture.</div>


</columnsItem>
</columns>



Poor picture quality



<columns>
<columnsItem zoneid="lAsPP7O7Hh">

<div style="text-align: center">
<img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260612110542-92941004008.jpeg" width="268px" /></div>


<div style="text-align: center">
❌Too much text</div>


</columnsItem>
<columnsItem zoneid="A1lgTA5XLe">

<div style="text-align: center">
<img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260612110547-892270166931.png" width="200px" /></div>


<div style="text-align: center">
❌Too vague</div>


</columnsItem>
<columnsItem zoneid="JjWQYot4Jw">

<div style="text-align: center">
<img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260612110550-1704486901469.png" width="294px" /></div>


<div style="text-align: center">
❌There are too many product SKUs, and the main body is unclear.</div>


</columnsItem>
</columns>



2. Product information 



|<div style="text-align: center"><br><strong>field type</strong></div><br> |<div style="text-align: center"><br><strong>Case description</strong></div><br> |
|---|---|
|<div style="text-align: center"><br>Product name</div><br> |What will be affected: AI uses it to understand product categories and positioning, and then determine the content direction of the video.<br><br>❌ "SKU\-20240301\-A" / "The product in the link"<br><br>> Meaningless numbers or vague references; AI cannot understand what the product is.<br><br><br>✅ "Volcano White Breathable Mesh Sneakers" / "Hyaluronic Acid Moisturizing Cream 50ml"<br><br>> They cover category information and core features, so the AI can quickly locate product attributes. |
|<div style="text-align: center"><br>Target audience</div><br> |What will be affected: "pain point groups" and scene selection shown in the video.<br><br>❌ "All ages" / "18\-60 years old"<br><br>> If the scope is too large, it means nothing is said, and AI cannot focus on pain points.<br><br><br>✅ "Commuting women aged 25\-35, focusing on comfort and style"/ "College students, limited budget but pursuing quality"<br><br>> Clarify age, identity and core needs to facilitate the storyboard to present the pain point scenarios of the corresponding group of people. |
|<div style="text-align: center"><br>Product descriptions</div><br> |What will be affected: The quantity affects the presentation rhythm of the video; the description method affects the presentation method.<br><br>For example, the selling point of slippers is "non\-slip", the video may show scenes of bathroom use.<br><br>❌ "Very useful" / "Good value for money"<br><br>> Too abstract for AI to translate into concrete pictures.<br><br><br>✅"A mesh running shoe suitable for summer, weighing only 180g, breathable and not stuffy, suitable for daily commuting and light exercise"<br><br>> Contains usage scenarios, specific parameters and somatosensory descriptions, based on which AI can design and display actions and environments. |
|<div style="text-align: center"><br>Product selling point</div><br> |What will be affected: The quantity affects the presentation rhythm of the video; the description method affects the presentation method.<br><br>For example, the selling point of slippers is "non\-slip", so the video may show scenes of bathroom use.<br><br>&nbsp;<br><br>❌How to describe it: "Easy to wear, good\-looking, and easy to match."<br><br>> Three words are too broad, and the video can only be shown in a general way.<br><br><br>Enter 8 selling points at once<br><br>> Too many to fit into a 15\-second video. It is recommended to focus on the selling points according to the length of the video.<br><br><br>✅"The sole is 2cm thicker and made of PVA material with high support, so you won’t feel tired after standing for a long time."<br><br>> The functional characteristics are concrete and quantified, and there are scenes to display and body sensations.<br><br><br>"One shoe for two wears: wear the heel on the street and stand on the heel when commuting."<br><br>> This is a scenario description, so the video will show two ways of wearing.<br><br><br>It is recommended that the 15\-second video focus on 2\-3 selling points, and the 30\-second video can be expanded to 4\-5. |


&nbsp;

<span id="Zwi9zrUg"></span>
# A Practical Guide to Storylines


1. Output description



|**Output items** |**Illustrate** |**What will be affected** |
|---|---|---|
|Title |Summary of the core creativity of the storyline |The overall tone and direction of the video |
|Storyline<br><br> |Description by timeline<br><br> |Video narrative rhythm and content arrangement |
|Visual style<br><br> |Such as "Japanese fresh,"<br><br>"textured blockbuster,"<br><br>"situational drama" |The texture and atmosphere of the final film |
|Duration<br><br> |15s/30s/60s |Creation point consumption and platform adaptation |



2. How can I talk to the Agent?



|**what do I want to do** | **✅ This works well** | **❌ The effect is poor** |**Why** |
|---|---|---|---|
|**Give a direction** |"Make a video recommending good products for mothers, 15 seconds, highlighting the safety of milk powder without additives." |"Make a video for me."<br><br> |The more specific it is (target audience, type, duration and selling point), the more accurate the storyline generated by AI will be; if it is too vague, it can only be output in a general way. |
|**Specify video type** |"I need a plot type that attracts readers to continue reading through plot reversal and clear storyline: the heroine discovers the product, tries it, and gets surprise feedback." |"Let’s do something different." |With a clear type and concise plot framework, the AI can achieve differentiated content under the same orientation; merely saying "different" provides no clear direction.<br><br> |
|**Adjust duration** |"Shorten it to less than 15 seconds, the pace should be fast, and it is suitable for short video information streams." |"Shorter." |With specific duration and delivery scenarios, AI can match the rhythm and habits of the corresponding platform. |
|**Adjust style** |"The style has been changed to Japanese and fresh, with clean images and warm tones." |"Better looking" / "More advanced." |Describe specific visual keywords (tone, atmosphere or reference style) before AI can be implemented. |
|**Modify content **  |"The rhythm of the second paragraph is too slow. It is shortened to less than 3 seconds and directly shows the close\-up of the product." |"Not good, change it to another one." |Point out what's wrong and what you want to change to, and AI will make precise adjustments; merely saying "Change" leads to random repeated revisions. |
|**Highlight specific selling points** |"Focus on the waterproof function, preferably with water splashing or raining scenes to demonstrate." |"Show more features." |Selling points and scene\-based demonstration method are given together, and AI can directly convert them into images; mentioning "function" in a general way makes it unclear what needs to be demonstrated. |
|**Change some ideas** |"These are too routine. If you want to create more twists/suspense, create pain points first and then reveal the product." |"Change." (available but not very effective) |Give "the specific direction for new ideas you expect", and the quality of the replacement will be higher; pure replacement is a random refresh. |


<span id="J64MHkZv"></span>
# A Practical Guide to Storyboard


1. Output description



|**Output items** |**Illustrate** |**Operable** |
|---|---|---|
|Shot list |Duration of each shot and picture description (Prompt) |Regenerate through dialogue |
|Product picture |Used for product display in storyboards |Can be manually replaced / AI regenerated |
|Figures |Character images appearing in storyboards |Can be manually replaced / AI regenerated |
|Scene picture<br><br> |Background environment in storyboard |Can be manually replaced / AI regenerated<br><br> |



2. How can I talk to the Agent?


Once the storyboard is generated, you can have the AI readjust in the following ways. Each modification will recalculate the creation points and deduct them after confirmation.

**Core principle: ** Tell AI ** "what needs to be modified, the revised content, and whether to retain unchanged sections." ** The more complete the three elements are, the more quickly the regenerated results will be in place.


|**Modification type** |**Illustrate** | **✅This works well** | **❌ The effect is poor** |
|---|---|---|---|
|**Give comments / modifications to the script** |Provide a text script or specific modification points, and AI will regenerate storyboards and pictures accordingly.<br><br> |"Remake it according to this structure: the beginning 3s — the scene of girls suffering from foot pain while commuting / the middle 7s — walking easily after putting on our shoes / the end 5s — product close\-up and slogan 'Say goodbye to foot pain'" |"Remake a new version" (no direction, AI can only generate randomly). |
|**Upload reference video replica** |Upload a reference video; AI will deconstruct its structure and combine it with your product information to generate a new storyboard.<br><br> |"Refer to the suspenseful opening of the first 5 seconds of this video and the fast\-cut rhythm in the middle, the product is changed to my sneakers, and the promotional information at the end is changed to our activities". |Only upload videos without talking (AI doesn’t know which elements to refer to, whether to copy them in full or to learn from parts). |
|**Upload pictures and modification comments** |Upload a new reference picture and specify how AI should use it; the AI will incorporate the picture and modification comments into regeneration. |"I uploaded a picture of an outdoor runway and used it to replace the entire scene background, leaving the characters and product shots unchanged". |Upload an image and write "use this" (don't specify where to use it /what to replace /whether other parts should be changed). |
|**Change creative direction (return to storyline)**  |Not satisfied with the current direction of the story line and want to see more creative directions and choose again. |"This story line is not going in the right direction. Let's go back to the story line and give me a few plot twists".<br><br> |"No need to change it" (don't say what direction you want to change it to).<br><br> |
|**Supplementary product information**<br><br> |Provide new product materials or selling points, and the system will update the product information and synchronize it to the storyboard. |"One more selling point: This shoe has passed the SGS antibacterial test. Help me add it to the product information, and it will be automatically included in the subsequent generation". |"Add a selling point" (no selling point). |

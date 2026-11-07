---
title: "3D director desk"
product: "Dramagic"
product_code: "Dramagic"
source: "https://docs.byteplus.com/en/docs/Dramagic/3Ddirectordesk"
---

Welcome to the Dramagic '3D Director's Desk' feature! 

**What is the 3D Director's Desk?** 

The 3D Director's Desk is a tool for **AI short drama production**. It provides a lightweight virtual set, helping users complete character positioning, scene composition, camera design, and action rehearsal before generating video, and outputs frames or white model videos as references for AI video generation. 

Breaking down the challenge of “how to shoot” into three tasks: 


* Space and scheduling layer: where the characters stand, relative relationships ➡️ **What to shoot?** 

* Shot scale layer: proportion of the subject in the frame ➡️ **How big is the frame?** 

* Camera movement and perspective layer: how the camera moves, camera angle ➡️ **From which angle to shoot?**  **How does the camera move?** 


**Why use the 3D Director's Desk?** 

Relying solely on text prompts often makes it difficult to accurately control character positioning, camera angles, and movement relationships. 


* Character location, orientation, and spatial relationships are hard to accurately describe with text. 

* The shot scale, camera position, and composition in generated videos are difficult to control consistently. 

* Multi\-character actions and camera movements lack intuitive rehearsal. 

* Repeated video generation leads to wasted time and computing power.


&nbsp;

<span id="v9KXL5pU"></span>
#  1. Feature Introduction 


1. **At which stage should the Director's Desk be used?** 


After uploading the script and automatically parsing the shot prompts, during the stage of generating video from the shot, you can enter the Director's Desk to output static images or dynamic video references to help improve the accuracy of video generation. 


2. **Feature screenshot:** 



|  |Screenshot example  |
|---|---|
|Feature entry <br><br>  |The 3D Director's Desk is accessed from each shot; the 3D Director's Desk embeds the prompt for that shot. <br><br><span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/e1f3919ede924d9a9c09a0b192bab743) </span><br><br>  |
|Interface overview  |<div style="text-align: center"><br> </div><br><br><br><span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/1d80ed714bdd4327920faf269e2a6d79) </span><br><br>  |


<span id="mHmuwOvt"></span>
# 2. Core Module Introduction 


* **Main modules:** 


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/cc4a8963b7284eaab6e0d4bf71aed411) </span>

 
&nbsp;

* **Module introduction:** 



|  |Region  |Location  |Main purpose  |
|---|---|---|---|
|1  |Top toolbar  |Top of the page  |Framing ratio, take screenshot, record video, open asset list  |
|2  |Element panel  |Left side of the page  |Search and select 3D scenes, roles, and director cameras  |
|3  |3D workspace  |Center of the page  |View scenes, select, place, and adjust 3D objects  |
|4  |View navigation  |Upper right of the workspace  |Identify X/Y/Z directions, switch or reset observation perspective  |
|5  |Quick toolbar  |Bottom of the workspace  |* Object operation: move, rotate, zoom <br><br>* Add elements: add role/camera/props and 720P scene images <br><br>* Edit: undo, redo <br><br>* Panel control: open scene editing, open animation editing <br><br><br><span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/af153038e7924b23a49dd3f55589cbdf) </span><br><br>  |
|6  |Camera preview  |Upper right of the page  |View the final composition in the director camera in real time  |
|7  |Property panel  |Right side of the page  |Adjust parameters such as zoom, translation, rotation, and background for scenes or objects  |
|8  |Timeline  |Bottom of the page (after enabling)  |Play preview, locate time, add keyframes, generate or edit movement trajectory  |

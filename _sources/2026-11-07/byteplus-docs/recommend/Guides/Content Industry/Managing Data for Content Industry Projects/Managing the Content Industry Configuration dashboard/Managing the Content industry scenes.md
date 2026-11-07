---
title: "Managing the Content industry scenes"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/docs-managing-the-content-industry-scenes"
---

A **scene** is defined as the location with which the user interacts. This includes the home page, promotion page, details page, search page, and many others. BytePlus Recommend builds the recommendation models based on the data collected from these scenes. Through the data sent, our team uses a combination of `scene` and `UserEvent.event_type` to analyze the flow of the user's impression.

Clients can use some of the following scene name examples as references:


* Home page recommendations—Homepage

* Content Details—Content Detail Page


You can edit scenes by selecting scenes that are included in your data and collaboration scenes where your recommendation will be placed. You can also create custom scenes by adding new scene names.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">There are no differences in the scene configuration process between the Trial and Live mode.</div>


<span id="9a3b919d"></span>
# Types of scenes

There are two types of scenes within the BytePlus Recommend Console: **Scenes** and **Collaboration Scenes**.


|**Scene Types** |**Description** |
|---|---|
|Scenes |Scenes are defined as the location with which the user interacts. Scene data includes user events like clicks, impression, or purchase. |
|Collaboration scenes |Collaboration scenes are defined as the location where you want the recommendations to be shown to the users. This is necessary during the model creation process. |


<span id="7642f137"></span>
# Adding custom scenes

You can add custom scenes to the scene list if required.

**To add a custom scene:** 


1. Sign in to [BytePlus Recommend](https://console.byteplus.com/recommend/home).

2. Click on the project you want to modify.

3. Under the Scene section, click the edit icon.

   The Edit scene screen appears.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/18365ed848594ae4b97d24671ec0470a~tplv-goo7wpa0wc-image.image) </span>

4. Click **Create custom scene**.

   A new scene row appears.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fb83be1330d145269e4ed1175c672f9d~tplv-goo7wpa0wc-image.image) </span>

5. Modify the details as required.

6. Click **Save scene**.

7. (Optional) To delete the custom scene, click the delete icon.

   The custom scenes are added.


<span id="0b33078d"></span>
# Selecting the scenes

You can select the scenes to be included in your scenes list.

**Selecting the scenes fields:** 


1. Sign in to [BytePlus Recommend](https://console.byteplus.com/recommend/home).

2. Click on the project you want to modify.

3. In the Scene section, click the edit icon.

   The Edit scene screen appears.

4. Check the box next to the scenes listed in your imported data.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/29f04536a1f54e1ea74fd4e6bbf018ac~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Checking the top box allows you to select all the scene fields listed.   </div>
   

5. Toggle the Collaboration scenes button if applicable.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">At least one collaboration scene has to be selected.   </div>
   

6. Click **Save scene**.

   The updated scene list is saved.


<span id="e7647b7d"></span>
# Default scene list

The BytePlus Recommend console provides you with a default scene list. You can manage the scene list as required.

The scene list consists of:


* Homepage.

* Content Detail Page.
